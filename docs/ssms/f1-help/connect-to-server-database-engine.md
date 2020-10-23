---
description: 서버에 연결(데이터베이스 엔진)
title: 서버에 연결(데이터베이스 엔진)
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: ssms
ms.topic: conceptual
f1_keywords:
- sql13.swb.connectoserverunknownservertype.f1
- sql13.swb.connection.login.sqlce.f1
- sql13.swb.connecttoce.f1
- SQL13.SWB.CONNECTION.LOGIN.SQLSERVER.F1
- sql13.swb.connection.login.sqlserver.f1
- sql13.swb.manageSS2k.f1
- connect-to-server-database-engine
ms.assetid: ee9017b4-8a19-4360-9003-9e6484082d41
author: markingmyname
ms.author: maghan
ms.reviewer: ''
ms.custom: seo-lt-2019
ms.date: 04/07/2020
ms.openlocfilehash: 83ff5d5ffae698c49655ef65e8e5d5171eae31ac
ms.sourcegitcommit: bd3a135f061e4a49183bbebc7add41ab11872bae
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/21/2020
ms.locfileid: "92300703"
---
# <a name="connect-to-server-database-engine"></a>서버에 연결(데이터베이스 엔진)

[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]
[!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion_md.md)]에 연결할 때 이 대화 상자를 사용하여 옵션을 확인하거나 지정할 수 있습니다. 대부분의 경우 **서버 이름** 상자에서 데이터베이스 서버의 컴퓨터 이름을 입력한 다음 **연결**을 클릭하여 연결할 수 있습니다. 명명된 인스턴스에 연결하는 경우 컴퓨터 이름, 백슬래시, 인스턴스 이름의 순서로 사용합니다. `mycomputer\myinstance`)을 입력합니다. [!INCLUDE[ssExpress](../../includes/ssexpress_md.md)]에 연결하는 경우 컴퓨터 이름과 그 뒤에 **\sqlexpress**를 사용합니다.
  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에 연결하는 데 다양한 요인이 영향을 줄 수 있습니다. 도움말을 보려면 다음 리소스를 참조하세요.

- [자습서 1단원: 데이터베이스 엔진에 연결](../../relational-databases/lesson-1-connecting-to-the-database-engine.md)  

- [SQL Server 데이터베이스 엔진에 대한 연결 문제 해결](../../database-engine/configure-windows/troubleshoot-connecting-to-the-sql-server-database-engine.md)  

- [Solving Connectivity errors to SQL Server](https://support.microsoft.com/help/4009936/solving-connectivity-errors-to-sql-server)(SQL Server에 대한 연결 오류 해결)   
  
## <a name="options"></a>옵션

**서버 유형**  
개체 탐색기에서 서버를 등록하는 경우 연결할 서버 유형을 [!INCLUDE[ssDE](../../includes/ssde_md.md)], [!INCLUDE[ssASnoversion](../../includes/ssasnoversion_md.md)], [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)], [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]중에서 선택합니다. 대화 상자의 나머지 부분에는 선택한 서버 유형에 적용되는 옵션만 표시됩니다. 등록된 서버에서 서버를 등록하는 경우 **서버 유형** 상자는 읽기 전용이며 등록된 서버 구성 요소에 표시된 서버 유형과 일치합니다. 다른 유형의 서버를 등록하려면 새 서버를 등록하기 전에 등록된 서버 도구 모음에서 [!INCLUDE[ssDE](../../includes/ssde_md.md)], [!INCLUDE[ssASnoversion](../../includes/ssasnoversion_md.md)], [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)], [!INCLUDE[ssEW](../../includes/ssew-md.md)]또는 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 중에서 선택합니다.  
  
**서버 이름**  
연결할 서버 인스턴스를 선택합니다. 마지막으로 연결한 서버 인스턴스가 기본적으로 표시됩니다.  
  
> [!NOTE]  
> [!INCLUDE[ssExpress](../../includes/ssexpress_md.md)]의 활성 사용자 인스턴스에 연결하려면 `np:\\.\pipe\3C3DF6B1-2262-47\tsql\query`와 같이 파이프 이름을 지정하는 명명된 파이프 프로토콜을 사용하여 연결합니다. 자세한 내용은 [!INCLUDE[ssExpress](../../includes/ssexpress_md.md)] 설명서를 참조하세요.  

> [!NOTE]  
> 일반적으로 연결은 "MRU(가장 최근에 사용됨)" 기록에서 보관됩니다. MRU에서 항목을 제거하려면 **서버 이름** 콤보 상자를 클릭하고, 제거할 서버 이름을 선택한 다음, **DEL** 키를 누르면 됩니다.  

**인증**  
SSMS의 현재 버전은 [!INCLUDE[ssDE](../../includes/ssde_md.md)]의 인스턴스에 연결할 때 다섯 가지 인증 모드를 제공합니다. 인증 대화 상자가 다음 목록과 일치하지 않으면 [SSMS(SQL Server Management Studio) 다운로드](../download-sql-server-management-studio-ssms.md)에서 최신 버전의 SSMS를 다운로드합니다.  

> **Windows 인증**  
> [!INCLUDE[msCoName](../../includes/msconame_md.md)] Windows 인증 모드에서는 사용자가 Windows 사용자 계정을 통해 연결할 수 있습니다.  
> 
> **SQL Server 인증**  
> 사용자가 지정한 로그인 이름과 암호를 사용하여 트러스트되지 않은 연결로부터 연결하면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 로그인 계정이 설정되고 지정한 암호가 전에 기록한 암호와 일치하는지를 확인하여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 가 자체적으로 인증을 수행합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에 로그인 계정이 설정되어 있지 않으면 인증이 실패하고 오류 메시지가 나타납니다. 가능하면 Windows 인증 또는 Active Directory - 암호 인증을 사용합니다.  
> 
> **Azure Active Directory - MFA가 지원되는 유니버설**  
> Active Directory - MFA를 통한 유니버설은 Azure MFA(Multi-Factor Authentication)를 지원하는 대화형 워크플로입니다. Azure MFA를 사용하면 간단한 로그인 프로세스에 대한 사용자 요구를 충족하는 동시에 데이터 및 애플리케이션에 대한 액세스를 보호할 수 있습니다. MFA는 전화 통화, 문자 메시지, PIN을 사용하는 스마트 카드, 모바일 앱 알림 등 다양하고 간단한 인증 옵션을 통해 강력한 인증을 제공하여 사용자가 원하는 방법을 선택할 수 있게 합니다. 사용자 계정이 MFA에 맞게 구성된 경우 대화형 인증 워크플로에는 팝업 대화 상자, 스마트 카드 사용 등을 통한 추가 사용자 작업이 필요합니다. 사용자 계정이 MFA에 맞게 구성된 경우 사용자가 연결하려면 Azure 유니버설 인증을 선택해야 합니다. 사용자 계정에 MFA가 필요하지 않은 경우에도 사용자는 다른 두 가지 Azure Active Directory 인증 옵션을 사용할 수 있습니다. 자세한 내용은 [SQL Database 및 Azure Synapse Analytics를 사용한 Azure AD MFA에 대한 SSMS 지원](/azure/azure-sql/database/authentication-mfa-ssms-overview)을 참조하세요. 필요한 경우 **옵션**을 클릭하고 **연결 속성** 탭을 선택한 다음 **AD 도메인 이름 또는 테넌트 ID** 상자를 입력하여 로그인을 인증하는 도메인을 변경할 수 있습니다.  
> 
> **Azure Active Directory - 암호**  
> Azure Active Directory 인증은 Azure AD(Azure Active Directory)에서 ID를 사용하여 [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]에 연결하는 메커니즘입니다.  Azure로 페더레이션되지 않은 도메인에서 자격 증명을 사용하여 Windows에 로그인하는 경우 또는 초기 도메인이나 클라이언트 도메인에 따라 Azure AD를 사용하는 Azure AD 인증을 사용하는 경우 [!INCLUDE[ssSDS](../../includes/sssds-md.md)]에 연결하는 데 이 방법을 사용합니다. 자세한 내용은 [Azure Active Directory 인증을 사용하여 SQL Database에 연결](/azure/azure-sql/database/authentication-aad-overview)을 참조하세요.  
> 
> **Active Directory - 통합**  
> Azure Active Directory 인증은 Azure AD(Azure Active Directory)에서 ID를 사용하여 [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]에 연결하는 메커니즘입니다. 페더레이션된 도메인에서 Azure Active Directory 자격 증명을 사용하여 Windows에 로그인하는 경우 [!INCLUDE[ssSDS](../../includes/sssds-md.md)]에 연결하는 데 이 방법을 사용합니다. 자세한 내용은 [Azure Active Directory 인증을 사용하여 SQL Database에 연결](/azure/azure-sql/database/authentication-aad-overview)을 참조하세요.  
  
**사용자 이름**  
연결에 사용할 Windows 사용자 이름입니다. 이 옵션은 **Azure Active Directory - 암호** 인증을 사용하여 연결하도록 선택한 경우에만 사용할 수 있습니다. **Windows 인증** 또는 **Azure Active Directory - 통합** 인증을 선택한 경우에는 읽기 전용이 됩니다.  
  
**로그인**  
연결 시 사용할 로그인을 입력합니다. 이 옵션은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인증 또는 Active Directory 암호 인증을 사용하여 연결하도록 선택한 경우에만 사용할 수 있습니다.  
  
> [!NOTE]  
> 일반적으로 연결은 "MRU(가장 최근에 사용됨)" 기록에서 보관됩니다. MRU에서 항목을 제거하려면 **서버 이름** 콤보 상자를 클릭하고, 제거할 서버 이름을 선택한 다음, **DEL** 키를 누르면 됩니다. SSMS 18.5에서 도입되었습니다.

**암호**  
로그인 암호를 입력합니다. 이 옵션은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인증 또는 Active Directory - 암호 인증을 사용하여 연결하도록 선택한 경우에만 편집할 수 있습니다.  

**연결**  
서버에 연결하려면 클릭합니다.

**옵션**  
**연결 속성** 및 **추가 연결 매개 변수** 탭을 표시하려면 클릭합니다.