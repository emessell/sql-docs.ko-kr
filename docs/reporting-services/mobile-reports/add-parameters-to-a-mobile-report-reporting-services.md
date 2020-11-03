---
title: 모바일 보고서에 매개 변수 추가 | Reporting Services | Microsoft Docs
description: Reporting Services 모바일 보고서는 매개 변수를 포함할 수 있으므로 보고서 독자가 보고서를 필터링할 수 있습니다. 해당 보고서는 드릴스루의 대상으로 사용할 수도 있습니다.
ms.date: 07/30/2018
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: mobile-reports
ms.topic: conceptual
ms.assetid: 113cb057-deec-40eb-abc8-f35d3900eaa6
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 36bf305d4685f18e1c6df9129716ae9de84d4f84
ms.sourcegitcommit: ea0bf89617e11afe85ad85309e0ec731ed265583
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/28/2020
ms.locfileid: "92907291"
---
# <a name="add-parameters-to-a-mobile-report--reporting-services"></a>모바일 보고서에 매개 변수 추가 | Reporting Services
작성자와 보고서를 읽는 사람이 보고서를 필터링할 수 있도록 매개 변수가 있는 [!INCLUDE[ssRSnoversion_md](../../includes/ssrsnoversion-md.md)] 모바일 보고서를 작성할 수 있습니다. 매개 변수가 있는 보고서는 [원본 보고서에서 드릴스루](../../reporting-services/mobile-reports/add-drillthrough-from-a-mobile-report-to-other-mobile-reports-or-urls.md)의 대상이 될 수도 있습니다. 

매개 변수가 있는 모바일 보고서를 만들려면 적어도 하나의 매개 변수가 있는 공유 데이터 세트로 시작합니다. [공유 데이터 세트에 매개 변수 만들기](../../reporting-services/report-data/create-a-shared-dataset-or-embedded-dataset-report-builder-and-ssrs.md)를 참조하세요. 모바일 보고서는 기본 매개 변수에 대해 null 값을 지원하지 않으므로, 매개 변수에 null이 아닌 기본값이 있는지 확인하세요.

모바일 보고서에 매개 변수를 추가한 후 URL을 만들어 [쿼리 문자열 매개 변수가 있는 보고서를 열 수 있습니다.](../../reporting-services/mobile-reports/open-a-mobile-report-with-specific-query-string-parameters-reporting-services.md) 

1. [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion.md)] 웹 포털의 위쪽 표시줄에서 **새로 만들기** > **모바일 보고서** 를 선택합니다.  
  
   ![PBI_SSMRP_NewMenu](../../reporting-services/mobile-reports/media/pbi-ssmrp-newmenu.png)  
     
2. **왼쪽 위에서** 데이터 [!INCLUDE[SS_MobileReptPub_Long](../../includes/ss-mobilereptpub-long.md)]탭을 선택합니다.   
  
3. 오른쪽 위에서 **데이터 추가** 를 선택합니다.  
  
4. **보고서 서버** 를 선택한 다음 서버를 선택합니다.  
  
5. 서버의 공유 데이터 세트로 이동하고 다음 매개 변수가 있는 데이터 세트를 선택합니다.  
  
   표에 데이터 세트의 데이터가 표시됩니다. 괄호 **{ }** 안에 녹색 원은 매개 변수가 있는 데이터 세트를 표시합니다.  
     
   ![SSMRP_PforParam](../../reporting-services/mobile-reports/media/ssmrp-pforparam.png)  
  
6. 탭에서 코그를 선택한 다음, **매개 변수 {}** 를 선택합니다.  
  
   ![SSMRP_ParamWheel](../../reporting-services/mobile-reports/media/ssmrp-paramwheel.png)  
  
7. 매개 변수에 값을 전달할 보고서 요소를 선택합니다.  
  
   ![SSMRP_SetParam](../../reporting-services/mobile-reports/media/ssmrp-setparam.png)  
     
8. **미리 보기** 를 선택하면 보고서가 표시되는 모양을 확인할 수 있습니다. 이 보고서에서 선택 목록은 범주 매개 변수를 사용합니다.

   ![선택 목록 1이 설명선으로 표시된 보고서 미리 보기의 스크린샷](../../reporting-services/mobile-reports/media/sql-server-mobile-report-publisher-selection-list-view-no-selection.png) 
   
9. 선택 목록에서 값을 선택하면 보고서는 해당 값으로 필터링됩니다(이 경우 보조 프로그램).

   ![선택 목록 1이 설명선으로 표시되고 액세서리 옵션이 선택된 보고서 미리 보기의 스크린샷](../../reporting-services/mobile-reports/media/sql-server-mobile-report-publisher-selection-list-category-selected.png)   
  
### <a name="see-also"></a>참고 항목  
-  [특정 쿼리 문자열 매개 변수가 있는 모바일 보고서 열기](../../reporting-services/mobile-reports/open-a-mobile-report-with-specific-query-string-parameters-reporting-services.md)
-  [모바일 보고서에서 다른 모바일 보고서나 URL로 드릴스루 추가](../../reporting-services/mobile-reports/add-drillthrough-from-a-mobile-report-to-other-mobile-reports-or-urls.md)
-  [공유 데이터 세트 또는 포함된 데이터 세트 만들기](../../reporting-services/report-data/create-a-shared-dataset-or-embedded-dataset-report-builder-and-ssrs.md)
- [SQL Server 모바일 보고서 게시자를 사용하여 모바일 보고서 만들기 및 게시](../../reporting-services/mobile-reports/create-mobile-reports-with-sql-server-mobile-report-publisher.md)  
  
  

