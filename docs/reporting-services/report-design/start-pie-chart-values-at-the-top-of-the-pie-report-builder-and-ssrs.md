---
title: 원형 차트 값을 원형의 위쪽에서 시작(보고서 작성기) | Microsoft Docs
description: 원형 차트의 값을 기본값인 차트 위쪽으로부터 90가 아니라 차트 맨 위에서 시작하는 방법을 알아봅니다.
ms.date: 03/01/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-design
ms.topic: conceptual
ms.assetid: d0e6fb59-ca4e-4d70-97cb-0ad183da21d3
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: b1158cf4a88bb491b8ed1cb492eec1c3021cb6f9
ms.sourcegitcommit: ea0bf89617e11afe85ad85309e0ec731ed265583
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/28/2020
ms.locfileid: "92907061"
---
# <a name="start-pie-chart-values-at-the-top-of-the-pie-report-builder-and-ssrs"></a>원형 차트를 원형의 위쪽에서 시작(보고서 작성기 및 SSRS)
[!INCLUDE[ssRSnoversion_md](../../includes/ssrsnoversion-md.md)] 페이지를 매긴 보고서의 원형 차트에서는 기본적으로 데이터 세트의 첫 번째 값이 원형의 위쪽으로부터 90도에서 시작합니다. 

![데이터 세트가 90도에서 시작하는 보고서 작성기 원형 차트의 스크린샷](../../reporting-services/media/report-builder-pie-chart-start-at-90.png)

*차트 값이 90도에서 시작합니다.*

대신 첫 번째 값을 맨 위에서 시작해야 할 수도 있습니다. 

![데이터 세트가 상단에서 시작하는 보고서 작성기 원형 차트의 스크린샷](../../reporting-services/media/report-builder-pie-chart-start-at-top.png)

*차트 값이 차트의 맨 위에서 시작합니다.*
  
## <a name="to-start-the-pie-chart-at-the-top-of-the-pie"></a>원형 차트가 원형의 위쪽에서 시작되게 하려면  
  
1.  원형 자체를 클릭합니다.  
  
2.  **속성** 창이 열려 있지 않으면 **보기** 탭에서 **속성** 을 클릭합니다.  
  
3.  **속성** 창의 **사용자 정의 특성** 에서 **PieStartAngle** 을 **0** 에서 **270** 으로 변경합니다.  
  
4.  **실행** 을 클릭하여 보고서를 미리 봅니다.  
  
 이제 첫 번째 값이 원형 차트의 위쪽에서 시작됩니다.  
  
## <a name="see-also"></a>참고 항목  
 [차트 서식 지정&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/formatting-a-chart-report-builder-and-ssrs.md)   
 [원형 차트 &#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/pie-charts-report-builder-and-ssrs.md)  
  
  
