---
title: Reporting Services에서 KPI 사용 | Microsoft Docs
description: SQL Server Reporting Services에서 KPI를 사용하여 상태 및 성능을 쉽게 측정할 수 있는 방법을 알아봅니다.
author: maggiesMSFT
ms.author: maggies
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: reporting-services
ms.topic: conceptual
ms.date: 07/02/2017
ms.openlocfilehash: e661fee4e9b5afe5f78cae444ff8d6574a536bb9
ms.sourcegitcommit: 80701484b8f404316d934ad2a85fd773e26ca30c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/03/2020
ms.locfileid: "93243782"
---
# <a name="working-with-kpis-in-reporting-services"></a>Reporting Services에서 KPI 사용

[!INCLUDE[ssrs-appliesto](../includes/ssrs-appliesto.md)] [!INCLUDE[ssrs-appliesto-2016-and-later](../includes/ssrs-appliesto-2016-and-later.md)] [!INCLUDE[ssrs-appliesto-pbirsi](../includes/ssrs-appliesto-pbirs.md)]

*KPI(핵심 성과 지표)* 는 목표에 대한 진척 정도를 알려 주는 시각적 단서입니다.  핵심 성과 지표는 팀, 관리자 및 비즈니스에서 측정 가능한 목표에 대한 진척 정도를 빠르게 평가하는 데 있어 중요합니다.
  
SQL Server Reporting Services에서 KPI를 사용하여 다음 질문에 대한 답변을 쉽게 시각화할 수 있습니다.  
  
- 내 앞 또는 뒤에 있는 것은 무엇인가?  
  
- 나는 얼마나 앞 또는 뒤에 있는가?  
  
- 내가 완료한 최소 금액은 얼마나 되는가?  

> [!NOTE]
> KPI는 SSRS 포털의 Enterprise(개발자) 버전에서만 액세스할 수 있습니다.

## <a name="creating-a-dataset"></a>데이터 세트 만들기

KPI는 공유된 데이터 세트에서 데이터의 첫 행만 사용합니다. 사용하려는 데이터가 첫 행에 있는지 확인합니다. 공유 데이터 세트를 만들기 위해 보고서 작성기 또는 SQL Server Data Tools를 사용할 수 있습니다.  
  
> **참고** : 데이터 세트는 KPI와 같은 폴더에 있을 필요가 없습니다.  
  
## <a name="placement-of-kpis"></a>KPI의 배치  
  
KPI는 보고서 서버의 모든 폴더에서 만들 수 있습니다.  KPI를 만들기 전에 저장할 적합한 위치에 대해 생각해 봐야 할 것입니다. 사용자가 볼 수 있는 폴더에 배치하는 동시에 KPI 주변의 다른 보고서 및 KPI와 관련될 수 있습니다.  
## <a name="adding-a-kpi"></a>KPI 추가
  
KPI의 위치를 확인한 후 해당 폴더로 이동하고 상단 메뉴에서 **New(새로 만들기)**  > **KPI** 를 선택합니다.  
  
![KPI 옵션이 호출된 새로 만들기 드롭다운 목록을 보여 주는 스크린샷](../reporting-services/media/rscreatekpi1.png)  
  
**New KPI(새 KPI)** 화면이 나타납니다.  
  
![새 KPI 화면을 보여 주는 스크린샷](../reporting-services/media/rscreatekpi2.png)  
  
정적 값을 할당 하거나 공유 데이터 세트에서 데이터를 사용할 수 있습니다. 새 KPI를 만들 때 임의 수동 데이터 집합으로 채워집니다.  
  
| 필드 | 설명 |
|-----------------|--------------------------------------------------------------------------------------------------------------------------------------------------|
| 값 형식 | 표시되는 값의 형식을 변경하는 데 사용합니다. |
| 값 | KPI에 대해 표시할 값입니다. |
| 목표 | 숫자 값에 대한 비교로 사용되며 백분율 차로 표시됩니다. |
| 상태 | KPI 타일 색을 결정하는 데 사용되는 숫자 값입니다. 유효한 값은 1(녹색), 0(주황색) 및 -1(빨강)입니다. |
| 추세 집합 | 차트 시각화에 사용되는 쉼표로 구분되는 숫자 값입니다. 또한, 추세를 나타내는 값으로 데이터 세트의 열에 설정할 수도 있습니다. |
| 관련 콘텐츠 | 드릴스루 링크를 설정하는 기능입니다. 이 링크는 포털에 게시된 모바일 보고서 또는 사용자 지정 URL일 수 있습니다. |
  
> **경고** : 설계 시간에 **상태** 필드에 대한 단어 값을 사용할 수 있지만, 데이터 세트를 새로 고침하는 경우 숫자 값을 사용해야 합니다. 숫자 대신 단어 값으로 데이터 세트를 새로 고침할 경우 서버에서 KPI가 손상될 수 있습니다.  
>
> **참고** : **값** , **목표** 및 **상태** 필드는 데이터 세트 결과의 첫 행에서만 값을 선택할 수 있습니다. 하지만, **집합 추세** 필드는 추세를 반영하는 열을 선택할 수 있습니다.  
  
새 공유 데이터 세트를 사용하려면, 다음을 수행해야 합니다.
  
1. 필드 드롭다운 상자를 **수동으로 설정** , 또는 **설정 안 함** 에서 **데이터 세트 필드** 로 변경합니다.  
  
    ![데이터 세트 필드로 설정된 값 옵션 및 설정되지 않음으로 설정된 데이터 세트 선택 필드를 보여 주는 스크린샷](../reporting-services/media/rscreatekpi3.png)  
  
2. 데이터 상자에서 **줄임표(...)** 를 선택합니다. 그러면 **데이터 세트 선택** 화면이 나타납니다.  
  
    ![Finance_KPI 옵션이 선택된 데이터 세트 선택 섹션의 스크린샷](../reporting-services/media/rscreatekpi4.png)  
  
3. 표시하려는 데이터가 있는 데이터 세트를 선택합니다.  
  
4. 사용하려는 필드를 선택합니다. **확인** 을 선택합니다.  
  
    ![Sum_Amount 옵션이 선택된 Finance_KPI에서 필드 선택 섹션을 보여 주는 스크린샷](../reporting-services/media/rscreatekpi5.png)  
  
5. **값 형식** 을 값 형식에 맞게 변경합니다. 이 예제에서는 값은 통화입니다.  
  
    ![통화로 설정된 값 형식 옵션을 보여 주는 KPI 미리 보기의 스크린샷](../reporting-services/media/rscreatekpi6.png)  
  
6. **적용** 을 선택합니다.  
  
    ![데이터 세트에 두 개의 항목이 있음을 보여 주는 KPI의 스크린샷](../reporting-services/media/rscreatekpi7.png)

## <a name="configuring-related-content"></a>관련 콘텐츠 구성

**모바일 보고서** 를 선택하면 대화 상자에서 대상을 선택할 수 있습니다.

   ![모바일 보고서로 설정된 관련 콘텐츠 옵션 및 설정되지 않음으로 설정된 모바일 보고서 선택 옵션을 보여 주는 스크린샷](media/rscreatekpi-related-content-mobile-report.png)

이제 포털에서 KPI를 클릭하면 모바일 보고서의 썸네일이 관련 콘텐츠 드롭다운 아래에 표시됩니다. 이 썸네일을 클릭하면 보고서로 곧장 이동하게 됩니다.

사용자는 또한 사용자 지정 URL을 지정할 수도 있습니다. 이 작업은 웹 사이트, SharePoint 사이트, SSRS 보고서 URL(하드 코드된 매개 변수를 함께 전달할 수 있음) 등 어떤 것이든 될 수 있습니다.

![사용자 지정 URL로 설정된 관련 콘텐츠 옵션 및 http://로 설정된 URL 입력 옵션을 보여 주는 스크린샷](media/rscreatekpi-related-content-custom-url.png)

이제 KPI를 클릭하면 관련 콘텐츠 아래에 URL이 표시됩니다.

모바일 보고서 하나 또는 사용자 지정 URL 하나만 추가할 수 있습니다.
  
## <a name="removing-a-kpi"></a>KPI 제거  
  
KPI를 제거하려면 다음을 수행해야 합니다.
  
1. 제거하려는 KPI의 **줄임표(...)** 를 선택합니다. **관리** 를 선택합니다.  
  
    ![호출된 관리 옵션 및 선택된 KPI의 줄임표 옵션 스크린샷](../reporting-services/media/rsremovekpi1.png)  
  
2. **삭제** 를 선택합니다. 확인 대화 상자에서 **삭제** 를 다시 선택합니다.  
  
    ![삭제 옵션의 스크린샷](../reporting-services/media/rsremovekpi2.png)  
  
## <a name="refreshing-a-kpi"></a>KPI 새로 고침  
  
KPI를 새로 고치려면 공유 데이터 세트에 대한 캐싱을 구성해야 합니다. 캐시 새로 고침 계획에 관련된 자세한 내용은 [공유 데이터 세트 사용](../reporting-services/work-with-shared-datasets-web-portal.md)을 참조하세요.  
  
## <a name="next-steps"></a>다음 단계
  
[웹 포털](../reporting-services/web-portal-ssrs-native-mode.md)  
[공유 데이터 세트 작업](../reporting-services/work-with-shared-datasets-web-portal.md)

추가 질문이 있으신가요? [Reporting Services 포럼에서 질문하기](https://go.microsoft.com/fwlink/?LinkId=620231)
