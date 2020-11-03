---
description: Power BI 보고서 서버 통합(구성 관리자)
title: Power BI 보고서 서버 통합(구성 관리자) | Microsoft Docs
author: maggiesMSFT
ms.author: maggies
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.topic: conceptual
ms.date: 09/17/2017
ms.openlocfilehash: 47964ebf5702542452227589e1426948825cc216
ms.sourcegitcommit: 22e97435c8b692f7612c4a6d3fe9e9baeaecbb94
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/27/2020
ms.locfileid: "92678876"
---
# <a name="power-bi-report-server-integration-configuration-manager"></a>Power BI 보고서 서버 통합(구성 관리자)

[!INCLUDE[ssrs-appliesto](../../includes/ssrs-appliesto.md)] [!INCLUDE[ssrs-appliesto-2016-and-later](../../includes/ssrs-appliesto-2016-and-later.md)] [!INCLUDE[ssrs-appliesto-pbirsi](../../includes/ssrs-appliesto-pbirs.md)]

**구성 관리자의** Power BI 통합 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 페이지는 보고서 서버 사용자가 지원되는 보고서 항목을 [!INCLUDE[sspowerbi](../../includes/sspowerbi-md.md)] 대시보드에 고정할 수 있도록 보고서 서버를 원하는 Azure AD(Active Directory) 관리되는 테넌트에 등록하는 데 사용됩니다. 고정할 수 있는 지원되는 항목의 목록은 [Power BI 대시보드에 Reporting Services 항목 고정](../../reporting-services/pin-reporting-services-items-to-power-bi-dashboards.md)을 참조하세요.

## <a name="requirements-for-power-bi-integration"></a><a name="bkmk_requirements"></a> Power BI 통합에 대한 요구 사항

[!INCLUDE[sspowerbi](../../includes/sspowerbi-md.md)] 서비스로 이동할 수 있는 활성 인터넷 연결 외에 [!INCLUDE[sspowerbi](../../includes/sspowerbi-md.md)]통합을 완료하기 위한 다음 요구 사항이 있습니다.

- **Azure Active Directory:** 조직에서 Azure 서비스 및 웹 애플리케이션에 대한 디렉터리 및 ID 관리를 제공하는 Azure Active Directory를 사용해야 합니다. 자세한 내용은 [Azure Active Directory란?](/azure/active-directory/fundamentals/active-directory-whatis)을 참조하세요.

- **관리되는 테넌트:** 보고서 항목을 고정할 [!INCLUDE[sspowerbi](../../includes/sspowerbi-md.md)] 대시보드는 Azure AD 관리되는 테넌트에 속해야 합니다.  관리되는 테넌트는 Microsoft 365 및 Microsoft Intune과 같은 Azure 서비스를 처음으로 구독할 때 자동으로 만들어집니다.   바이럴 테넌트는 현재 지원되지 않습니다.  자세한 내용은 [Azure AD 디렉터리란?](/previous-versions/azure/azure-services/jj573650(v=azure.100)#BKMK_WhatIsAnAzureADTenant)에서 "Azure AD 테넌트란" 및 "Azure AD 디렉터리를 가져오는 방법" 섹션을 참조하세요.

- [!INCLUDE[sspowerbi](../../includes/sspowerbi-md.md)] 통합을 수행하는 사용자는 Azure AD 테넌트의 멤버이고, [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 시스템 관리자이며, ReportServer 카탈로그 데이터베이스의 시스템 관리자여야 합니다.

- [!INCLUDE[sspowerbi](../../includes/sspowerbi-md.md)] 통합을 수행하는 사용자는 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 를 설치하는 데 사용되는 계정 또는 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]서비스를 실행 중인 계정으로 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 구성 관리자를 시작해야 합니다.

- 고정하려는 보고서는 저장된 자격 증명을 사용해야 합니다. 이는 [!INCLUDE[sspowerbi](../../includes/sspowerbi-md.md)] 통합 자체의 요구 사항이 아니라 고정된 항목에 대한 새로 고침 프로세스의 요구 사항입니다.  보고서 항목 고정 작업은 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 구독을 만들어 [!INCLUDE[sspowerbi](../../includes/sspowerbi-md.md)]에서 타일의 새로 고침 일정을 관리합니다. [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 구독에는 저장된 자격 증명이 필요합니다. 보고서에서 저장된 자격 증명을 사용하지 않는 경우 사용자는 보고서 항목을 고정할 수 있지만 연결된 구독에서 [!INCLUDE[sspowerbi](../../includes/sspowerbi-md.md)]에 데이터를 새로 고치려고 경우 **내 구독** 페이지에 다음과 유사한 오류 메시지가 표시됩니다.

    PowerBI 배달 오류: 대시보드: IT 지출 분석 샘플, visual: Chart2, 오류: 현재 작업을 완료할 수 없습니다. 사용자 데이터 원본 자격 증명이 요구 사항을 준수하지 않아 이 보고서 또는 공유 데이터 세트를 실행할 수 없습니다. 뿐만 아니라 사용자 데이터 원본 자격 증명도 실행할 수 없습니다.

자격 증명을 저장하는 방법은 [Reporting Services 데이터 원본에 자격 증명 저장](../../reporting-services/report-data/store-credentials-in-a-reporting-services-data-source.md)에서 "보고서별 데이터 원본에 대한 저장된 자격 증명 구성" 섹션을 참조하세요.

관리자는  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 로그 파일에서 자세한 내용을 검토할 수 있습니다.  다음과 유사한 메시지가 표시됩니다. [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 로그 파일을 검토하고 모니터링하는 유용한 방법은 파일에서 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 파워 쿼리를 사용하는 것입니다.  자세한 내용 및 간단한 비디오는 [Report Server Service Trace Log](../../reporting-services/report-server/report-server-service-trace-log.md)를 참조하세요.

- subscription!WindowsService_1!1458!09/24/2015-00:09:27:: e ERROR: PowerBI 배달 오류: 대시보드: IT 지출 분석 샘플, visual: Chart2, 오류: 현재 작업을 완료할 수 없습니다. 사용자 데이터 원본 자격 증명이 요구 사항을 준수하지 않아 이 보고서 또는 공유 데이터 세트를 실행할 수 없습니다. 사용자 데이터 원본 자격 증명이 보고서 서버 데이터베이스에 저장되어 있지 않거나, 사용자 데이터 원본이 자격 증명을 요구하지 않도록 구성되어 있지만 무인 실행 계정이 지정되어 있지 않습니다.

- notification!WindowsService_1!1458!09/24/2015-00:09:27:: e ERROR: Error occurred processing subscription fcdb8581-d763-4b3b-ba3e-8572360df4f9: PowerBI 배달 오류: 대시보드: IT 지출 분석 샘플, visual: Chart2, 오류: 현재 작업을 완료할 수 없습니다. 사용자 데이터 원본 자격 증명이 요구 사항을 준수하지 않아 이 보고서 또는 공유 데이터 집합을 실행할 수 없습니다. 사용자 데이터 원본 자격 증명이 보고서 서버 데이터베이스에 저장되어 있지 않거나, 사용자 데이터 원본이 자격 증명을 요구하지 않도록 구성되어 있지만 무인 실행 계정이 지정되어 있지 않습니다.

## <a name="to-integrate-and-register-the-report-server"></a><a name="bkmk_steps2integrate"></a> 보고서 서버를 통합하고 등록하려면

[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 구성 관리자에서 다음 단계를 완료합니다. 자세한 내용은 [보고서 서버 구성 관리자](../../reporting-services/install-windows/reporting-services-configuration-manager-native-mode.md)를 참조하세요.

1. [!INCLUDE[sspowerbi](../../includes/sspowerbi-md.md)] 통합 페이지를 선택합니다.

2. **Power BI에 등록** 을 선택합니다.

    >[!Note]
    > 포트 443이 차단되지 않았는지 확인합니다.

3. [!INCLUDE[msCoName](../../includes/msconame-md.md)] 로그인 대화 상자에서 [!INCLUDE[sspowerbi](../../includes/sspowerbi-md.md)]에 로그인하는 데 사용할 자격 증명을 입력합니다.

4. 등록이 완료되면 **Power BI 등록 정보** 섹션에 Azure 테넌트 ID와 리디렉션 URL이 기록됩니다.  URL은 [!INCLUDE[sspowerbi](../../includes/sspowerbi-md.md)] 대시보드에서 등록된 보고서와 다시 통신할 수 있는 통신 프로세스 및 로그인의 일부로 사용됩니다.

5. 향후 참조를 위해 저장할 수 있도록 **결과** 창에서 **복사** 단추를 선택하여 Windows 클립보드에 등록 정보를 복사합니다.

## <a name="unregister-with-power-bi"></a><a name="bkmk_unregister"></a> Power BI 등록 취소

**등록 취소:** Azure Active Directory에서 보고서 서버의 등록을 취소하면 다음과 같은 상황이 발생합니다.

- **내 설정** 링크가 웹 포털 메뉴 모음에 더 이상 표시되지 않습니다.

- 이미 고정된 보고서 항목은 대시보드에 계속 고정되지만 대시보드의 타일은 더 이상 업데이트되지 않습니다.

- 타일을 업데이트하는 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 구독은 보고서 서버에 계속 존재하지만 구성된 일정에 따라 실행될 때 다음과 유사한 오류 메시지를 표시합니다.

    **이 구독에 대한 배달 확장 프로그램을 로드할 수 없습니다.**

구성 관리자의 **Power BI** 페이지에서 **Power BI 등록 취소** 단추를 선택합니다.

##  <a name="update-registration"></a><a name="bkmk_updateregistration"></a> 등록 업데이트

보고서 서버의 구성이 변경된 경우 **등록 업데이트** 를 사용합니다. 예를 들어 사용자가 [!INCLUDE[ssRSWebPortal](../../includes/ssrswebportal.md)]로 이동하는 데 사용하는 URL을 추가하거나 제거하려는 경우가 여기에 해당합니다.

- [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 구성 관리자에서 **웹 포털 URL** 을 선택합니다.

     **고급** 을 선택합니다.

- **추가** 를 선택하여 [!INCLUDE[ssRSWebPortal](../../includes/ssrswebportal.md)] 에 대한 새 HTTP ID를 추가한 다음 **확인** 을 선택합니다.

     서버 구성이 변경되었음을 나타내도록 [!INCLUDE[sspowerbi](../../includes/sspowerbi-md.md)] 아이콘이 변경됩니다.  ![ssrs_powebi_icon_warning](../../reporting-services/install-windows/media/ssrs-powebi-icon-warning.png "ssrs_powebi_icon_warning")

- **Power BI 통합** 페이지에서 **등록 업데이트** 를 선택합니다.

     Azure AD에 로그인하라는 메시지가 표시됩니다. 페이지가 새로 고쳐지고 **리디렉션 URL** 에 새 URL이 나열됩니다.

##  <a name="summary-of-the-power-bi-integration-and-pin-process"></a><a name="bkmk_integration_process"></a> Power BI 통합 및 고정 프로세스 요약

이 섹션에서는 보고서 서버를 [!INCLUDE[sspowerbi](../../includes/sspowerbi-md.md)] 와 통합하고 보고서 항목을 대시보드에 고정할 때의 관련 기술 및 기본 단계를 요약합니다.

 **통합:**

1. 구성 관리자에서 **Power BI에 등록** 단추를 선택하면 Azure Active Directory에 로그인하라는 메시지가 나타납니다.

2. [!INCLUDE[sspowerbi](../../includes/sspowerbi-md.md)] 클라이언트 앱이 관리되는 테넌트에 등록됩니다.

3. Azure Active Directory 내에서 관리되는 테넌트는 Power BI 클라이언트 앱을 만들 위치입니다.

4. 등록에는 사용자가 보고서 서버에서 로그인할 때 사용되는 리디렉션 URL이 포함됩니다.  앱 ID 및 URL은 ReportServer 데이터베이스에 저장됩니다. 리디렉션 URL은 호출이 보고서 서버에 반환될 수 있도록 Azure에 인증 호출 시 사용됩니다. 예를 들어, 사용자가 로그인하거나 대시보드에 항목을 고정하는 경우가 여기에 해당합니다.

5. 앱 ID와 URL이 구성 관리자에 표시됩니다.

 ![ssrs_pbiflow_integration](../../reporting-services/install-windows/media/ssrs-pbiflow-integration.png "ssrs_pbiflow_integration")

 **사용자가 대시보드에 보고서 항목을 고정하는 경우**

1. 사용자가 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)][!INCLUDE[ssRSWebPortal](../../includes/ssrswebportal.md)]에서 보고서를 미리 보고 [!INCLUDE[ssRSWebPortal](../../includes/ssrswebportal.md)]에서 보고서 항목을 고정하려고 처음 클릭합니다.

2. 이렇게 하면 Azure AD 로그인 페이지로 리디렉션됩니다. [!INCLUDE[ssRSWebPortal](../../includes/ssrswebportal.md)] **내 설정** 페이지에서 로그인할 수도 있습니다. 사용자가 Azure 관리되는 테넌트에 로그인하면 사용자의 Azure 계정과 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 권한 간에 관계가 설정됩니다.  자세한 내용은 [Power BI 통합을 위한 내 설정&#40;웹 포털&#41;](../my-settings-for-power-bi-integration-web-portal.md)과 통합해야 합니다.

3. 사용자 보안 토큰이 보고서 서버에 반환됩니다.

4. 사용자 보안 토큰은 ReportServer 데이터베이스에 저장됩니다.

5. 사용자가 액세스할 수 있는 그룹 및 대시보드 목록이 [!INCLUDE[sspowerbi](../../includes/sspowerbi-md.md)] 서비스에서 검색됩니다.  사용자는 대상 그룹 및 대시보드를 선택하고 [!INCLUDE[sspowerbi](../../includes/sspowerbi-md.md)] 타일에서 데이터를 새로 고칠 빈도를 구성합니다.

6. 보고서 항목이 대시보드에 고정됩니다.

7. 대시보드 타일에서 보고서 항목의 예약된 새로 고침을 관리하기 위해 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 구독이 만들어집니다. 이 구독에서는 사용자가 로그인할 때 생성된 보안 토큰을 사용합니다.

     토큰은 **90일** 동안 유효합니다. 이후에는 사용자가 다시 로그인하여 새 사용자 토큰을 만들어야 합니다. 토큰이 만료된 경우 고정된 타일은 대시보드에 계속 표시되지만 데이터가 더 이상 새로 고쳐지지 않습니다.  새 사용자 토큰이 만들어질 때까지 고정된 항목에 사용된 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 구독에서 오류가 발생합니다. [Power BI 통합을 위한 내 설정&#40;웹 포털&#41;](../my-settings-for-power-bi-integration-web-portal.md)을 참조하세요. 이동하세요.

사용자가 두 번째로 항목을 고정하는 경우에는 1~4단계를 건너뛰고 대신 앱 ID와 URL이 ReportServer 데이터베이스에서 검색되며 5단계로 진행됩니다.

![사용자가 대시보드에 보고서 항목을 고정할 때 발생하는 프로세스를 보여 주는 다이어그램](../../reporting-services/install-windows/media/ssrs-pin-to-powerbi-flow.png)

 **대시보드 타일을 새로 고치기 위해 구독이 실행되는 경우**

1. [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 구독이 실행되면 보고서가 렌더링됩니다.

2. 사용자 토큰은 ReportServer 데이터베이스에서 검색됩니다.

3. 보고서 항목 상태 및 데이터가 토큰과 함께 [!INCLUDE[sspowerbi](../../includes/sspowerbi-md.md)]서비스로 전송됩니다.

4. 유효성 검사를 위해 Azure AD로 토큰이 전송됩니다. 토큰이 유효한 경우 보고서 항목 데이터가 대시보드 타일로 전송되고 타일의 날짜 속성이 업데이트됩니다.

5. 토큰이 유효하지 않은 경우 오류가 반환되고 보고서 서버에 기록됩니다.  상태 또는 기타 정보가 대시보드에 전송되지 않습니다.

![대시보드 타일을 새로 고치기 위해 구독이 실행될 때 발생하는 프로세스를 보여 주는 다이어그램](../../reporting-services/install-windows/media/ssrs-subscription-to-powerbi-flow.png)

   <iframe width="560" height="315" src="https://www.youtube.com/embed/QhPQObqmMPc" frameborder="0" allowfullscreen></iframe>

## <a name="considerations-and-limitations"></a>고려 사항 및 제한 사항

* 바이럴 및 정부 테넌트는 지원되지 않습니다.

## <a name="next-steps"></a>다음 단계

[Power BI 통합을 위한 내 설정&#40;웹 포털&#41;](../my-settings-for-power-bi-integration-web-portal.md)  
[Power BI 대시보드에 Reporting Services 항목 고정](../../reporting-services/pin-reporting-services-items-to-power-bi-dashboards.md)
[Power BI의 대시보드](https://powerbi.microsoft.com/documentation/powerbi-service-dashboards/)  

추가 질문이 있으신가요? [Reporting Services 포럼에서 질문하기](https://go.microsoft.com/fwlink/?LinkId=620231)