---
title: 모바일 보고서에 데이터 표 추가 | Reporting Services | Microsoft Docs
description: SQL Server 모바일 보고서 게시자의 표에 데이터를 표시할 수 있습니다. 간단한 데이터 표, 표시기 데이터 표 또는 차트 데이터 표를 선택합니다.
ms.date: 03/01/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: mobile-reports
ms.topic: conceptual
ms.assetid: fe98a970-90d3-44d1-9189-9141c237f141
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: e346ff2f6d5b4951e7ce0e3af81914b15b34ac15
ms.sourcegitcommit: ea0bf89617e11afe85ad85309e0ec731ed265583
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/28/2020
ms.locfileid: "92907321"
---
# <a name="add-data-grids-to-mobile-reports--reporting-services"></a>모바일 보고서에 데이터 표 추가 | Reporting Services
경우에 따라 가장 적합한 시각화는 데이터 자체입니다. *에 데이터를 표시하기 위해 다음 세 가지* 데이터 표 [!INCLUDE[SS_MobileReptPub_Long](../../includes/ss-mobilereptpub-long.md)]또는 테이블에 대해 알아봅니다.
* 단순 데이터 표
* 표시기 데이터 표
* 차트 데이터 표

## <a name="simple-data-grid"></a>단순 데이터 표
가장 기본적인 단순 데이터 표는 사용자 지정 서식 및 머리글을 사용하여 데이터의 여러 열을 표시할 수 있습니다. 

![모바일 보고서 단순 데이터 표의 스크린샷](../../reporting-services/mobile-reports/media/mobile-report-simple-data-grid.png)

디자인 화면에 데이터 표를 추가한 후에 실제 데이터에 연결할 수 있습니다.

1. **레이아웃** 탭에서 디자인 눈금으로 단순 데이터 표를 끌어서 원하는 크기로 만듭니다.

2. [Excel 또는 공유 데이터 세트의 데이터](../../reporting-services/mobile-reports/data-for-reporting-services-mobile-reports.md)를 가져옵니다.

3. **데이터** 탭을 선택하고 **데이터 속성** 창의 **그리드 뷰에 대한 데이터** 아래에서 데이터 테이블을 선택합니다.

4. **열** 창에서 원하는 열을 선택합니다. 순서를 다시 매기고 이름을 바꾸고 해당 형식 및 집계를 설정합니다. 

 
##  <a name="indicator-data-grid"></a>표시기 데이터 표
표시기 데이터 표에 계기 열을 추가할 수 있습니다.

![모바일 보고서 표시기 데이터 표의 스크린샷](../../reporting-services/mobile-reports/media/mobile-report-indicator-data-grid.png)

1. **레이아웃** 탭에서 디자인 눈금으로 표시기 데이터 표를 끌어서 원하는 크기로 만듭니다.

2. **열** 창의 **데이터** 탭에서 **계기 열 추가** 를 선택합니다. 

3. **옵션** 을 선택한 다음 **계기 유형** 을 선택합니다. 

4. **모바일 보고서에 직접 추가하는 계기** 에서와 같이 **값** 및 **비교** 필드와 [값 방향](../../reporting-services/mobile-reports/add-gauges-to-mobile-reports-reporting-services.md)을 설정합니다.

데이터 표는 해당 데이터 표 행에 맞는 데이터만 계기에 자동으로 제공합니다.  

## <a name="chart-data-grid"></a>차트 데이터 표
차트 데이터 표에 계기 열 또는 차트 열을 추가할 수 있습니다. 

![모바일 보고서 차트 데이터 표의 스크린샷](../../reporting-services/mobile-reports/media/mobile-report-chart-data-grid.png)

데이터 표에 차트 열을 추가하는 경우 각 행의 차트에 대한 데이터를 제공하는 별도 데이터 테이블을 추가해야 합니다. 이 두 번째 데이터 테이블은 연관된 차트 데이터에 각 행을 연결하기 위해 기본 데이터 테이블과 필드를 공유해야 합니다. 

1. **레이아웃** 탭에서 디자인 눈금으로 차트 데이터 표를 끌어서 원하는 크기로 만듭니다.

2. **열** 창의 **데이터** 탭에서 **차트 열 추가** 를 선택합니다. 

3. 기본 데이터 테이블과 필드를 공유하는 두 번째 데이터 테이블을 추가하려면 아직 수행하지 않은 경우 [Excel 또는 공유 데이터 세트의 데이터](../../reporting-services/mobile-reports/data-for-reporting-services-mobile-reports.md)를 가져옵니다.

4. **데이터 속성** 아래 **그리드 뷰에 대한 데이터** 에서 기본 데이터 테이블을 선택한 다음 **차트 시각화에 대한 참조 데이터** 에서 두 번째 테이블을 선택합니다.

5. **옵션** 을 선택한 다음 **차트 종류** 를 선택합니다.
 
6. **차트 데이터 필드** , **원본 조회** 및 **대상 조회** 를 선택합니다. 
   이 세 가지 속성으로 datagrid가 열에서 각 차트에 데이터를 제공하는 방법이 결정됩니다.
   
   *   **원본 조회** 는 **그리드 뷰에 대한 데이터** 에 있는 데이터 테이블의 필드로 설정됩니다. 이 필드는 각 행에 대해 포함된 차트에 데이터를 제공하는 차트 참조 데이터 테이블에 적용된 행 기준 필터 역할을 합니다. 
   * **대상 조회** 는 **차트 시각화에 대한 참조 데이터** 에 있는 데이터 테이블의 필드입니다. 각 행에 있는 차트의 데이터는 이 두 개 필드에 조인됩니다.   
   * **차트 데이터 필드** 를 통해 각 행에서 차트의 y축 값 또는 계열로 사용할 **차트 시각화를 위한 참조 데이터** 데이터 테이블의 메트릭이 결정됩니다.  

## <a name="see-also"></a>참고 항목 
* [Reporting Services 모바일 보고서의 지도](../../reporting-services/mobile-reports/maps-in-reporting-services-mobile-reports.md)
* [Reporting Services 모바일 보고서의 탐색기](../../reporting-services/mobile-reports/add-navigators-to-reporting-services-mobile-reports.md)
* [Reporting Services 모바일 보고서의 시각화](../../reporting-services/mobile-reports/add-visualizations-to-reporting-services-mobile-reports.md)
* [Reporting Services 모바일 보고서의 계기](../../reporting-services/mobile-reports/add-gauges-to-mobile-reports-reporting-services.md)  
 
  
