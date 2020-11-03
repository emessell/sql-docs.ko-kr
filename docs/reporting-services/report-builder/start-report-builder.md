---
title: 보고서 작성기 시작 | Microsoft Docs
description: 보고서 작성기는 독립 실행형 보고서 제작 환경입니다. 보고서 작성기를 처음 시작하면 Microsoft 다운로드 센터에서 다운로드하라는 메시지가 표시됩니다.
ms.date: 01/03/2020
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-builder
ms.topic: conceptual
helpviewer_keywords:
- Report Builder, launching
- launching Report Builder
- SharePoint integration [Reporting Services], starting Report Builder
- starting Report Builder
ms.assetid: 8c8c7d2e-b315-418d-bf65-90e7685e4259
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 00a954a23cf9b17a58c3272a03222019400ae891
ms.sourcegitcommit: ea0bf89617e11afe85ad85309e0ec731ed265583
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/28/2020
ms.locfileid: "92907041"
---
# <a name="start-report-builder"></a>보고서 작성기 시작

[!INCLUDE[ssRBnoversion](../../includes/ssrbnoversion.md)]는 독립 실행형 보고서 제작 환경입니다. 보고서 작성기를 사용하면 페이지를 매긴 보고서를 만들어 기본 또는 SharePoint 통합 모드에서 설치된 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 에 게시할 수 있습니다.  

> [!NOTE]
> SQL Server 2016 이후부터 SharePoint와의 Reporting Services 통합을 사용할 수 없습니다.
  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 웹 포털 또는 SharePoint 통합 모드의 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]에서 처음으로 [!INCLUDE[ssRBnoversion](../../includes/ssrbnoversion.md)]를 시작하면 Microsoft 다운로드 센터에서 다운로드하라는 메시지가 표시됩니다. 
 
![보고서 작성기를 여는 중 메시지의 스크린샷](../../reporting-services/report-builder/media/report-builder-get-report-builder.png) 
 
 개발자나 관리자는 [Microsoft 다운로드 센터에서 컴퓨터에 보고서 작성기를 설치](https://go.microsoft.com/fwlink/?LinkID=219138)할 수도 있습니다. 자세한 내용은 [보고서 작성기 설치](../../reporting-services/install-windows/install-report-builder.md) 의 "Systems Manager Server를 사용하여 보고서 작성기 설치"를 참조하세요.
 
 [!INCLUDE[ssRBnoversion](../../includes/ssrbnoversion.md)]는 SQL Server Reporting Services를 설치할 때 함께 설치되지 않으므로 별도로 다운로드하여 설치해야 합니다.  
  
 웹 포털 또는 SharePoint 사이트에서 [!INCLUDE[ssRBnoversion](../../includes/ssrbnoversion.md)] 를 시작할 때 이전 [!INCLUDE[ssRBnoversion](../../includes/ssrbnoversion.md)] 버전이 열리면 관리자에게 문의하세요. 그러면 관리자가 웹 포털이나 SharePoint 사이트의 버전을 업데이트할 수 있습니다.  
  
## <a name="to-start-ssrbnoversion-from-the-ssrsnoversion-web-portal"></a>[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 웹 포털에서 [!INCLUDE[ssRBnoversion](../../includes/ssrbnoversion.md)]를 시작하려면  
  
1.  웹 브라우저의 주소 표시줄에 보고서 서버의 URL을 입력합니다. 기본적으로 URL은 https://\<*servername*>/reports입니다.  
  
2.  웹 포털의 위쪽 막대에서 **새로 만들기** > **페이지를 매긴 보고서** 를 선택합니다.  
  
     ![PBI_SSMRP_NewMenu](../../reporting-services/mobile-reports/media/pbi-ssmrp-newmenu.png "PBI_SSMRP_NewMenu")  
  
     처음에는 [보고서 작성기를 설치](../../reporting-services/install-windows/install-report-builder.md)하라는 메시지가 표시됩니다. 
  
     그런 다음, [!INCLUDE[ssRBnoversion](../../includes/ssrbnoversion.md)]가 열리고 페이지를 매긴 보고서를 만들거나 보고서 서버에서 보고서를 열 수 있습니다.  
  
## <a name="to-start-ssrbnoversion-in-sharepoint-integrated-mode"></a>SharePoint 통합 모드에서 [!INCLUDE[ssRBnoversion](../../includes/ssrbnoversion.md)]를 시작하려면  
  
1.  원하는 라이브러리가 있는 SharePoint 사이트로 이동합니다.  
  
2.  라이브러리를 엽니다.  
  
3.  **문서** 를 클릭합니다.  
  
4.  **새 문서** 메뉴에서 **보고서 작성기 보고서** 를 클릭합니다.  
  
     처음으로 SQL Server [!INCLUDE[ssRBnoversion](../../includes/ssrbnoversion.md)] 마법사가 시작됩니다. 자세한 내용은 [Install Report Builder](../../reporting-services/install-windows/install-report-builder.md) 를 참조하십시오.  
  
     [!INCLUDE[ssRBnoversion](../../includes/ssrbnoversion.md)]가 열리고 페이지를 매긴 보고서를 만들거나 보고서 서버에서 보고서를 열 수 있습니다.  
  
     **참고** **새 문서** 메뉴에 **보고서 작성기 보고서** , **보고서 작성기 모델** 및 **보고서 데이터 원본** 옵션이 나열되지 않는 경우 해당 콘텐츠 형식을 SharePoint 라이브러리에 추가해야 합니다. 자세한 내용은 [SharePoint 라이브러리에 Reporting Services 콘텐츠 형식 추가](../../reporting-services/report-server-sharepoint/add-reporting-services-content-types-to-a-sharepoint-library.md)를 참조하세요.  

## <a name="next-steps"></a>다음 단계

[SQL Server의 보고서 작성기](../../reporting-services/report-builder/report-builder-in-sql-server-2016.md)   
[보고서 작성기에 대한 기본 옵션 설정](../../reporting-services/report-builder/set-default-options-for-report-builder.md)  

추가 질문이 있으신가요? [Reporting Services 포럼에서 질문하기](https://go.microsoft.com/fwlink/?LinkId=620231)
