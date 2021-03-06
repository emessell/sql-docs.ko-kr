---
title: SQL Server 보안
description: SQL Server 보안 기능에 대해 간략하게 설명하고 SQL Server를 대상으로 하는 안전한 ADO.NET 애플리케이션을 만드는 시나리오를 제공합니다.
ms.date: 09/26/2019
ms.assetid: 9053724d-a1fb-4f0f-b9dc-7f6dd893e8ff
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
author: David-Engel
ms.author: v-daenge
ms.reviewer: v-kaywon
ms.openlocfilehash: ea2f8a65cb8ca16efd625309f73d7dccc3e27505
ms.sourcegitcommit: fe5c45a492e19a320a1a36b037704bf132dffd51
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80911669"
---
# <a name="sql-server-security"></a>SQL Server 보안

[!INCLUDE[Driver_ADONET_Download](../../../includes/driver_adonet_download.md)]

SQL Server에는 보안 데이터베이스 애플리케이션을 만들 수 있도록 지원하는 많은 기능이 있습니다.  
  
데이터 절도나 손상같이 일반적으로 발생하는 보안 문제는 사용 중인 SQL Server 버전에 관계없이 항상 고려해야 할 사항입니다. 데이터 무결성도 보안 문제로 간주해야 합니다. 데이터가 보호되지 않는 경우 임시 데이터 조작이 허용되고 잘못된 값을 사용하여 데이터가 실수로 또는 악의적으로 수정되거나 완전히 삭제되면 데이터가 가치가 없게 될 수 있습니다. 또한 기밀 정보의 올바른 저장과 같이 반드시 준수해야 하는 법적 요구 사항이 있습니다. 일부 개인 정보 저장은 특정 관할지에 적용되는 법에 따라 전적으로 규정됩니다.  
  
Windows가 버전마다 다른 것처럼 SQL Server도 버전마다 보안 기능이 다르며 최신 버전이 이전 버전보다 향상된 보안 기능을 가지고 있습니다. 보안 기능만으로는 안전한 데이터베이스 애플리케이션을 보장할 수 없다는 것을 이해하는 것이 중요합니다. 각 데이터베이스 애플리케이션은 요구 사항, 실행 환경, 배포 모델, 물리적 위치 및 사용자 집단에서 고유합니다. 범위가 로컬인 일부 애플리케이션의 경우 최소한의 보안만 필요한 반면 다른 로컬 애플리케이션이나 인터넷을 통해 배포된 애플리케이션은 엄격한 보안 조치와 지속적인 모니터링 및 평가가 필요할 수 있습니다.  
  
SQL Server 데이터베이스 애플리케이션의 보안 요구 사항은 디자인 타임부터 고려해야 하며 뒤늦게 생각해서는 안 됩니다. 개발 주기 초기에 위협을 평가하면 취약성이 발견될 때마다 잠재적 피해를 완화할 수 있습니다.  
  
애플리케이션의 초기 디자인이 건전하더라도 시스템이 발전함에 따라 새로운 위협이 발생할 수 있습니다. 데이터베이스에 대해 여러 방어선을 만들어 보안 위반으로 인한 피해를 최소화할 수 있습니다. 첫 번째 방어선은 절대적으로 필요한 권한 이상의 권한을 부여하지 않고 공격 노출 영역을 줄이는 것입니다.  
  
이 단원의 항목에서는 개발자와 관련이 있는 SQL Server의 보안 기능에 대해 간략히 설명하며, 이러한 항목에 대해 자세히 다루고 있는 SQL Server 온라인 설명서와 기타 리소스의 관련 항목으로 연결되는 링크를 제공합니다.  
  
## <a name="in-this-section"></a>섹션 내용  
[SQL Server에서 인증](authentication-sql-server.md)  
SQL Server의 로그인 및 인증에 대해 설명하고 추가 리소스에 대한 링크를 제공합니다. 
  
[SQL Server의 애플리케이션 보안 시나리오](application-security-scenarios-sql-server.md)  
ADO.NET 및 SQL Server 애플리케이션에 대한 다양한 애플리케이션 보안 시나리오를 설명하는 항목을 제공합니다.  
  
[SQL Server Express 보안](sql-server-express-security.md)  
SQL Server Express의 보안 고려 사항에 대해 설명합니다.  
  
## <a name="related-sections"></a>관련 단원  
[SQL Server 데이터베이스 엔진 및 Azure SQL Database 보안 센터](../../../relational-databases/security/security-center-for-sql-server-database-engine-and-azure-sql-database.md)  
SQL Server 및 Azure SQL Database의 보안 고려 사항에 대해 설명합니다.

[SQL Server 설치에 대한 보안 고려 사항](../../../sql-server/install/security-considerations-for-a-sql-server-installation.md)  
SQL Server를 설치하기 전에 고려해야 하는 보안 문제에 대해 설명합니다.

## <a name="next-steps"></a>다음 단계
- [SQL Server 및 ADO.NET](index.md)
