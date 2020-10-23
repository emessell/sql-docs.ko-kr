---
description: 서비스 SID를 사용하여 SQL Server의 서비스에 사용 권한 부여
title: 서비스 SID를 사용하여 서비스에 사용 권한 부여
ms.custom: seo-dt-2019
author: randomnote1
ms.author: dareist
ms.date: 05/02/2019
ms.topic: conceptual
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.openlocfilehash: ab9af4d073cbec00736bab6a24817502d353ffd8
ms.sourcegitcommit: 2b6760408de3b99193edeccce4b92a2f9ed5bcc6
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/19/2020
ms.locfileid: "92175927"
---
# <a name="using-service-sids-to-grant-permissions-to-services-in-sql-server"></a>서비스 SID를 사용하여 SQL Server의 서비스에 사용 권한 부여

SQL Server는 [서비스별 SID(보안 식별자)](https://support.microsoft.com/help/2620201/sql-server-uses-a-service-sid-to-provide-service-isolation)(서비스 보안 주체라고도 함)를 사용하여 사용 권한을 특정 서비스에 직접 부여할 수 있습니다. 이 메서드는 SQL Server에서 엔진 및 에이전트 서비스(각각 NT SERVICE\MSSQL$<InstanceName> 및 NT SERVICE\SQLAGENT$<InstanceName>)에 사용 권한을 부여하기 위해 사용됩니다. 이 메서드를 사용하면 해당 서비스는 서비스가 실행 중일 때만 데이터베이스 엔진에 액세스할 수 있습니다.

다른 서비스에 사용 권한을 부여할 때도 이와 동일한 메서드를 사용할 수 있습니다. 서비스 SID를 사용하면 서비스 계정 관리 및 유지의 오버헤드가 제거되고 시스템 리소스에 부여된 사용 권한을 보다 강력하고 세밀하게 제어할 수 있습니다.

서비스 SID를 사용할 수 있는 서비스의 예는 다음과 같습니다.

- System Center Operations Manager 상태 서비스(NT SERVICE\HealthService)
- WSFC(Windows Server 장애 조치(Failover) 클러스터링) 서비스(NT SERVICE\ClusSvc)

일부 서비스에는 기본적으로 서비스 SID가 없습니다. 서비스 SID는 [SC.exe](/windows/desktop/services/configuring-a-service-using-sc)를 사용하여 만들어야 합니다. [이 메서드](https://kevinholman.com/2016/08/25/sql-mp-run-as-accounts-no-longer-required/)는 Microsoft System Center Operations Manager 관리자가 SQL 서버 내의 HealthService에 사용 권한을 부여하기 위해 채택했습니다.

서비스 SID가 만들어지고 확인되면 SQL Server 내에서 사용 권한을 부여받아야 합니다. 권한 부여는 [SSMS(SQL Server Management Studio)](../../ssms/download-sql-server-management-studio-ssms.md) 또는 쿼리를 사용하여 Windows 로그인을 생성하여 수행할 수 있습니다. 로그인이 생성되면 다른 로그인처럼 권한이 부여되고 역할에 추가되며 데이터베이스에 매핑될 수 있습니다.

> [!TIP]
> `Login failed for user 'NT AUTHORITY\SYSTEM'` 오류가 수신되면 원하는 서비스에 대한 서비스 SID가 있는지, SQL Server에 서비스 SID 로그인이 생성되었는지, SQL Server의 서비스 SID에 적절한 사용 권한이 부여되었는지 확인합니다.

## <a name="security"></a>보안

### <a name="eliminate-service-accounts"></a>서비스 계정 제거

일반적으로 서비스 계정을 사용하면 서비스가 SQL Server에 로그인할 수 있습니다. 서비스 계정은 서비스 계정 암호를 유지 관리하고 정기적으로 업데이트해야 하기 때문에 관리 복잡성을 가중시킵니다. 또한 서비스 계정 자격 증명은 인스턴스에서 작업을 수행할 때 해당 작업을 마스크하려는 개인이 사용할 수 있습니다.

### <a name="granular-permissions-to-system-accounts"></a>시스템 계정에 대한 세부적인 사용 권한

시스템 계정은 지금까지 [LocalSystem](/windows/win32/services/localsystem-account)([en-us의 NT AUTHORITY\SYSTEM](../../database-engine/configure-windows/configure-windows-service-accounts-and-permissions.md#Localized_service_names)) 또는 [NetworkService](/windows/desktop/Services/networkservice-account)([en-us의 NT AUTHORITY\NETWORK SERVICE](../../database-engine/configure-windows/configure-windows-service-accounts-and-permissions.md#Localized_service_names)) 계정에 대한 로그인을 생성하고 해당 로그인 권한을 부여하여 사용 권한을 부여 받았습니다. 이 메서드는 시스템 계정으로 실행 중인 SQL에 모든 프로세스 또는 서비스 사용 권한을 부여합니다.

서비스 SID를 사용하면 특정 서비스에 사용 권한을 부여할 수 있습니다. 이 서비스는 실행 중일 때 권한이 부여된 리소스에만 액세스할 수 있습니다. 예를 들어 `HealthService`가 `LocalSystem`으로 실행 중이고 `View Server State`가 부여된 경우 `LocalSystem` 계정은 `HealthService`의 컨텍스트에서 실행 중일 때 `View Server State`에 대한 권한만 가집니다. 다른 프로세스가 SQL의 서버 상태에 `LocalSystem`으로 액세스하려고 하면 액세스가 거부됩니다.

## <a name="examples"></a>예제

### <a name="a-create-a-service-sid"></a>A. 서비스 SID 만들기

다음 PowerShell 명령은 System Center Operations Manager 상태 서비스에서 서비스 SID를 만듭니다.

```PowerShell
sc.exe --% sidtype "HealthService" unrestricted
```

> [!IMPORTANT]
> `--%`는 나머지 명령 구문 분석을 중지하도록 PowerShell에 지시합니다. 이는 레거시 명령 및 애플리케이션을 사용할 때 유용합니다.

### <a name="b-query-a-service-sid"></a>B. 서비스 SID 쿼리

서비스 SID를 확인하거나 서비스 SID가 있는지 확인하려면 PowerShell에서 다음 명령을 실행합니다.

```PowerShell
sc.exe --% qsidtype "HealthService"
```

> [!IMPORTANT]
> `--%`는 나머지 명령 구문 분석을 중지하도록 PowerShell에 지시합니다. 이는 레거시 명령 및 애플리케이션을 사용할 때 유용합니다.

### <a name="c-add-a-newly-created-service-sid-as-a-login"></a>C. 새로 만든 서비스 SID를 로그인으로 추가

다음 예제에서는 T-SQL을 사용하여 System Center Operations Manager 상태 서비스에 대한 로그인을 만듭니다.

```SQL
CREATE LOGIN [NT SERVICE\HealthService] FROM WINDOWS
GO
```

### <a name="d-add-an-existing-service-sid-as-a-login"></a>D. 기존 서비스 SID를 로그인으로 추가

다음 예제에서는 T-SQL을 사용하여 클러스터 서비스에 대한 로그인을 만듭니다. 클러스터 서비스에 대한 사용 권한을 직접 부여하면 SYSTEM 계정에 과도한 사용 권한을 부여할 필요가 없습니다.

```SQL
CREATE LOGIN [NT SERVICE\ClusSvc] FROM WINDOWS
GO
```

### <a name="e-grant-permissions-to-a-service-sid"></a>E. 서비스 SID에 사용 권한 부여

가용성 그룹을 관리하는 데 필요한 권한을 클러스터 서비스에 부여합니다.

```SQL
GRANT ALTER ANY AVAILABILITY GROUP TO [NT SERVICE\ClusSvc]
GO

GRANT CONNECT SQL TO [NT SERVICE\ClusSvc]
GO

GRANT VIEW SERVER STATE TO [NT SERVICE\ClusSvc]
GO
```

  > [!NOTE]
  > 서비스 SID 로그인을 제거하거나 sysadmin 서버 역할에서 제거하면 SQL Server 데이터베이스 엔진에 연결되는 SQL Server의 다양한 구성 요소에 문제가 발생할 수 있습니다. 몇 가지 문제는 다음과 같습니다.
  > - SQL Server 에이전트가 시작할 수 없거나 SQL Server 서비스에 연결할 수 없습니다.
  > - SQL Server 설치 프로그램에서 다음 Microsoft 기술 자료 문서에 설명된 문제가 발생합니다. https://support.microsoft.com/help/955813/you-may-be-unable-to-restart-the-sql-server-agent-service-after-you-re
  >
  > SQL Server의 기본 인스턴스인 경우 다음 Transact-SQL 명령을 사용하여 서비스 SID를 추가하여 이 문제를 해결할 수 있습니다.
  >
  > ```sql
  > CREATE LOGIN [NT SERVICE\MSSQLSERVER] FROM WINDOWS WITH DEFAULT_DATABASE=[master], DEFAULT_LANGUAGE=[us_english]
  > 
  > ALTER ROLE sysadmin ADD MEMBER [NT SERVICE\MSSQLSERVER]
  > 
  > CREATE LOGIN [NT SERVICE\SQLSERVERAGENT] FROM WINDOWS WITH DEFAULT_DATABASE=[master], DEFAULT_LANGUAGE=[us_english]
  > 
  > ALTER ROLE sysadmin ADD MEMBER [NT SERVICE\SQLSERVERAGENT]
  > ```
  > SQL Server의 명명된 인스턴스를 사용하려면 다음 Transact-SQL 명령을 사용하세요.
  > ```sql
  > CREATE LOGIN [NT SERVICE\MSSQL$SQL2019] FROM WINDOWS WITH DEFAULT_DATABASE=[master], DEFAULT_LANGUAGE=[us_english]
  > 
  > ALTER ROLE sysadmin ADD MEMBER [NT SERVICE\MSSQL$SQL2019]
  > 
  > CREATE LOGIN [NT SERVICE\SQLAgent$SQL2019] FROM WINDOWS WITH DEFAULT_DATABASE=[master], DEFAULT_LANGUAGE=[us_english]
  > 
  > ALTER ROLE sysadmin ADD MEMBER [NT SERVICE\SQLAgent$SQL2019]
  > 
  > ```
  > 이 예제에서 `SQL2019`는 SQL Server의 인스턴스 이름입니다.

## <a name="next-steps"></a>다음 단계

서비스 sid 구조에 대한 자세한 내용은 [SERVICE_SID_INFO 구조](/windows/win32/api/winsvc/ns-winsvc-service_sid_info)를 참조하세요.

[로그인을 만들](../../t-sql/statements/create-login-transact-sql.md) 때 사용할 수 있는 추가 옵션에 대해 읽어보세요.

서비스 SID와 함께 역할 기반 보안을 사용하려면 SQL Server에서 [역할 만들기](../../t-sql/statements/create-role-transact-sql.md)에 대해 읽어보세요.

SQL Server의 서비스 SID에 [권한을 부여](../../t-sql/statements/grant-transact-sql.md)하는 다양한 방법을 읽어보세요.
