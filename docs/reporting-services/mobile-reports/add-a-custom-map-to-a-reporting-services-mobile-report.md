---
title: Reporting Services 모바일 보고서의 사용자 지정 지도 추가 | Microsoft Docs
description: Reporting Services 모바일 보고서에 사용자 지정 지도를 추가할 수 있습니다. 이 문서에서는 데이터를 로드하고 사용자 지정 지도에 연결하는 방법을 설명합니다.
ms.date: 01/31/2020
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: mobile-reports
ms.topic: conceptual
ms.assetid: fd259b95-bb58-4eb1-a436-6aa12fc6f5f2
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: a1c15d5b5155d68f94a1672ca55654485c6b1835
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/29/2020
ms.locfileid: "79448341"
---
# <a name="add-a-custom-map-to-a-reporting-services-mobile-report"></a>Reporting Services 모바일 보고서의 사용자 지정 지도 추가
사용자 지정 지도에는 다음과 같은 두 개의 파일이 필요합니다.  
* 셰이프 기하 도형용 .SHP 파일  
* 메타데이터용 .DBF 파일  
  
[Reporting Services 모바일 보고서의 사용자 지정 맵](../../reporting-services/mobile-reports/custom-maps-in-reporting-services-mobile-reports.md)에 대해 자세히 알아봅니다.  
  
두 파일은 같은 폴더에 저장합니다. canada.shp 및 canada.dbf와 같이 두 파일의 이름이 같아야 합니다. 메타데이터(DBF 파일)의 첫 번째 열은 지도에 데이터를 입력할 때 사용할 해당 셰이프의 이름(키)의 키 값과 대응시키는 데 사용됩니다.
  
## <a name="load-a-custom-map"></a>사용자 지정 지도 로드  
  
1. **레이아웃** 탭에서 맵 유형을 **그라데이션 열 지도**, **범위 중지 열 지도**또는 **거품형 지도** 중에서 선택하고 디자인 화면으로 끌어서 원하는 크기로 만듭니다.  
  
   ![SSMRP_MapsGallery](../../reporting-services/mobile-reports/media/ssmrp-mapsgallery.png)  
  
2. **레이아웃** 뷰 > **시각적 속성** 패널 > **지도**에서 **파일의 사용자 지정 지도**를 선택합니다.   
  
   ![SSMRP_SelectCustomMap](../../reporting-services/mobile-reports/media/ssmrp-selectcustommap.png)  
  
3. **열기** 대화 상자에서 SHP 및 DBF 파일의 위치를 찾은 다음 두 파일을 모두 선택합니다.   
  
   ![SSMRP_SelectDBFandSHP](../../reporting-services/mobile-reports/media/ssmrp-selectdbfandshp.png)  
  
## <a name="connect-data-to-a-custom-map"></a>사용자 지정 지도에 데이터 연결  
보고서에 사용자 지정 지도를 처음 추가할 때 [!INCLUDE[SS_MobileReptPub_Short](../../includes/ss-mobilereptpub-short.md)] 에서는 시뮬레이트된 지리 데이터를 지도에 입력합니다.  
  
![SSMRP_MapsData](../../reporting-services/mobile-reports/media/ssmrp-mapsdata.png)  
  
사용자 지정 지도에서 실제 데이터를 표시하는 것은 기본 제공 지도에서 데이터를 표시하는 것과 같습니다. [Reporting Services 모바일 보고서의 지도](../../reporting-services/mobile-reports/maps-in-reporting-services-mobile-reports.md) 에 나와 있는 단계에 따라 데이터를 표시합니다.  
  
### <a name="see-also"></a>참고 항목  
- [Custom maps in Reporting Services mobile reports](../../reporting-services/mobile-reports/custom-maps-in-reporting-services-mobile-reports.md)  
- [Reporting Services 모바일 보고서의 지도](../../reporting-services/mobile-reports/maps-in-reporting-services-mobile-reports.md)  
- [SQL Server 모바일 보고서 게시자를 사용하여 모바일 보고서 만들기 및 게시](../../reporting-services/mobile-reports/create-mobile-reports-with-sql-server-mobile-report-publisher.md)   
  
  
  
  
