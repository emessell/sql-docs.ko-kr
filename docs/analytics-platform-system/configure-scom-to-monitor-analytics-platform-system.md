---
title: AP를 모니터링 하도록 System Center Operations Manager 구성
description: 분석 플랫폼 시스템용 SCOM (System Center Operations Manager) 관리 팩을 구성 하려면 다음 단계를 수행 합니다. 관리 팩은 SCOM에서 분석 플랫폼 시스템을 모니터링 하는 데 필요 합니다.
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.custom: seo-dt-2019
ms.openlocfilehash: 2840ba401c0b7f3df5b0b27726cbdaa05390f952
ms.sourcegitcommit: 442fbe1655d629ecef273b02fae1beb2455a762e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/03/2020
ms.locfileid: "93235270"
---
# <a name="configure-system-center-operations-manager-scom-to-monitor-analytics-platform-system"></a>분석 플랫폼 시스템을 모니터링 하는 System Center Operations Manager (SCOM) 구성
분석 플랫폼 시스템용 SCOM (System Center Operations Manager) 관리 팩을 구성 하려면 다음 단계를 수행 합니다. 관리 팩은 SCOM에서 분석 플랫폼 시스템을 모니터링 하는 데 필요 합니다.  
  
## <a name="before-you-begin"></a><a name="BeforeBegin"></a>시작하기 전 주의 사항  
**필수 구성 요소**  
  
System Center Operations Manager 2007 r 2를 설치 하 고 실행 해야 합니다.  
  
관리 팩을 설치 하 고 구성 해야 합니다. [&#40;분석 플랫폼 시스템&#41;Scom 관리 팩 설치](install-the-scom-management-packs.md) 를 참조 하 고 [PDW &#40;분석 플랫폼 시스템&#41;용 scom 관리 팩을 가져옵니다 ](import-the-scom-management-pack-for-pdw.md).  
  
## <a name="configure-run-as-profile-in-system-center"></a><a name="ConfigureRunAsProfile"></a>System Center에서 Run-As 프로필 구성  
System Center를 구성 하려면 다음 단계를 수행 해야 합니다.  
  
-   **APS 감시자** 도메인 사용자에 대 한 실행 계정을 만들어 **Microsoft aps 감시자 계정** 에 매핑합니다.  
  
-   **Monitoring_user** APS 사용자에 대 한 실행 계정을 만들어 **Microsoft aps 작업 계정** 에 매핑합니다.  
  
작업을 수행 하는 방법에 대 한 자세한 지침은 다음과 같습니다.  
  
1.  **Aps 감시자** 도메인 사용자에 대 한 **Windows** 계정 유형을 사용 하 여 **aps 감시자** 실행 계정을 만듭니다.  
  
    1.  **관리** 창으로 이동 하 여 **실행 구성** 계정을 마우스 오른쪽 단추로 클릭 하  ->  **Accounts** 고 **실행 계정 만들기** ...를 선택 합니다.  
  
        ![실행 계정 만들기 옵션을 보여 주는 스크린샷](./media/configure-scom-to-monitor-analytics-platform-system/ConfigureScomCreateRunAsAccount.png "ConfigureScomCreateRunAsAccount")  
  
    2.  **실행 계정 만들기 마법사** 대화 상자가 열립니다. **소개** 페이지에서 **다음** 을 클릭합니다.  
  
    3.  **일반 속성** 페이지의 **실행 계정 유형** 에서 **Windows** 를 선택 하 고 "ap 감시자"를 **표시 이름** 으로 지정 합니다.  
  
        ![실행 계정 만들기 마법사의 일반 속성 페이지를 보여 주는 스크린샷](./media/configure-scom-to-monitor-analytics-platform-system/CreateRunAsAccountWizardGeneralProperties.png "CreateRunAsAccountWizardGeneralProperties")  
  
    4.  **자격 증명** 페이지에서 ![실행 계정 만들기 마법사의 자격 증명 페이지를 보여 주는 스크린샷](./media/configure-scom-to-monitor-analytics-platform-system/CreateRunAsAccountWizardCredentials.png "CreateRunAsAccountWizardCredentials")  
  
    5.  **배포 보안** 페이지에서 **보안 수준 낮음** 을 선택 하 고 **만들기** 단추를 클릭 하 여 완료 합니다.  
  
        ![실행 계정 만들기 마법사의 배포 보안 페이지를 보여 주는 스크린샷](./media/configure-scom-to-monitor-analytics-platform-system/CreateRunAsAccountWizardDistributionSecurity.png "CreateRunAsAccountWizardDistributionSecurity")  
  
        1.  **보다 안전한** 옵션을 사용 하려는 경우 자격 증명을 배포할 컴퓨터를 수동으로 지정 해야 합니다. 이렇게 하려면 실행 계정을 만든 후 마우스 오른쪽 단추로 클릭 하 고 **속성** 을 선택 합니다.  
  
        2.  **배포** 탭으로 이동 하 여 원하는 컴퓨터를 **추가** 합니다.  
  
            ![실행 계정 속성 대화 상자를 보여 주는 스크린샷](./media/configure-scom-to-monitor-analytics-platform-system/RunAsAccountProperties.png "RunAsAccountProperties")  
  
2.  **Ap 감시자** 실행 계정을 사용 하도록 **Microsoft ap 감시자 계정** 프로필을 설정 합니다.  
  
    1.  **관리**  ->  **실행을 구성**  ->  **프로필로** 이동 합니다.  
  
        ![프로필 옵션을 보여 주는 스크린샷](./media/configure-scom-to-monitor-analytics-platform-system/AdministrationRunAsConfigurationProfiles.png "AdministrationRunAsConfigurationProfiles")  
  
    2.  목록에서 **MICROSOFT APS 감시자 계정을** 마우스 오른쪽 단추로 클릭 하 고 **속성** 을 선택 합니다.  
  
        ![속성 옵션을 보여 주는 스크린샷](./media/configure-scom-to-monitor-analytics-platform-system/MicrosoftApsWatcherAccountProperties.png "MicrosoftApsWatcherAccountProperties")  
  
    3.  **실행 프로필 마법사** 대화 상자가 열립니다. **다음** 을 클릭 하 여 **소개** 페이지를 건너뜁니다.  
  
    4.  **일반 속성** 페이지에서 **다음** 을 클릭합니다.  
  
    5.  **실행 계정** 페이지에서 **추가 ...** 단추를 클릭 하 고 이전에 만든 **ap 감시자** 실행 계정을 선택 합니다.  
  
        ![실행 계정 추가 대화 상자를 보여 주는 스크린샷](./media/configure-scom-to-monitor-analytics-platform-system/RunAsProfileWizardAdd.png "RunAsProfileWizardAdd")  
  
    6.  **저장** 을 클릭 하 여 프로필 할당을 완료 합니다.  
  
3.  APS 어플라이언스 검색이 완료 될 때까지 기다립니다.  
  
    1.  **모니터링** 창으로 이동 하 여 **SQL Server 어플라이언스**  ->  **Microsoft Analytics Platform System**  ->  **어플라이언스** 상태 보기를 엽니다.  
  
        ![어플라이언스 옵션을 보여 주는 스크린샷](./media/configure-scom-to-monitor-analytics-platform-system/SqlServerApplianceMicrosoftApsAppliances.png "SqlServerApplianceMicrosoftApsAppliances")  
  
    2.  목록에 기기가 나타날 때까지 기다립니다. 어플라이언스의 이름은 레지스트리에 지정 된 것과 같아야 합니다. 검색이 완료 되 면 나열 된 모든 어플라이언스는 표시 되지만 모니터링 되지 않습니다. 모니터링을 사용 하도록 설정 하려면 다음 단계를 수행 합니다.  
  
    > [!NOTE]  
    > 초기 어플라이언스 검색을 완료할 때까지 대기 하는 동안 다음 단계를 병렬로 완료할 수 있습니다.  
  
4.  상태 데이터 검색을 위해 AP를 쿼리하려면 또 다른 새 실행 계정을 만듭니다.  
  
    1.  1 단계에 설명 된 대로 새 실행 계정 만들기를 시작 합니다.  
  
    2.  **일반 속성** 페이지에서 **기본 인증** 계정 유형을 선택 합니다.  
  
        ![실행 계정 유형 드롭다운에서 선택 된 기본 인증을 사용 하 여 실행 계정 만들기 마법사의 일반 속성 페이지를 보여 주는 스크린샷](./media/configure-scom-to-monitor-analytics-platform-system/CreateRunAsAccountWizardGeneralProperties2.png "CreateRunAsAccountWizardGeneralProperties2")  
  
    3.  **자격 증명** 페이지에서 유효한 자격 증명을 제공 하 여 APS 상태 dmv에 액세스 합니다.  
  
        ![유효한 자격 증명을 사용 하 여 실행 계정 만들기 마법사의 자격 증명 페이지를 보여 주는 스크린샷는 AP 성능 상태 Dmv에 액세스 합니다.](./media/configure-scom-to-monitor-analytics-platform-system/CreateRunAsAccountWizardCredentials2.png "CreateRunAsAccountWizardCredentials2")  
  
5.  APS 인스턴스에 대해 새로 만든 실행 계정을 사용 하도록 **MICROSOFT Aps 작업 계정** 프로필을 구성 합니다.  
  
    1.  2 단계에 설명 된 대로 **MICROSOFT APS 작업 계정** 속성으로 이동 합니다.  
  
    2.  **실행 계정** 페이지에서 **추가 ...** 를 클릭 하 고 
    3.  새로 만든 실행 계정을 선택 합니다.  
  
        ![실행 계정 드롭다운 목록에서 AP 작업을 선택 하 여 실행 계정 추가 대화 상자를 보여 주는 스크린샷](./media/configure-scom-to-monitor-analytics-platform-system/RunAsProfileWizardAdd2.png "RunAsProfileWizardAdd2")  
  
## <a name="next-step"></a>다음 단계  
이제 관리 팩을 구성 했으므로 어플라이언스 모니터링을 시작할 준비가 되었습니다. 자세한 내용은 [System Center Operations Manager &#40;Analytics Platform System&#41;을 사용 하 여 어플라이언스 모니터링 ](monitor-the-appliance-by-using-system-center-operations-manager.md)을 참조 하세요.  
  
<!-- MISSING LINKS ## See Also  
[Common Metadata Query Examples &#40;SQL Server PDW&#41;](../sqlpdw/common-metadata-query-examples-sql-server-pdw.md)  -->  
  
