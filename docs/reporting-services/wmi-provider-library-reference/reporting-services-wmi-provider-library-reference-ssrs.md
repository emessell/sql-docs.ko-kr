---
description: Reporting Services WMI 공급자 라이브러리 참조(SSRS)
title: Reporting Services WMI 공급자 라이브러리 참조 | Microsoft Docs
ms.date: 03/14/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: wmi-provider-library-reference
ms.topic: conceptual
apiname:
- Reporting Services WMI Provider Library
apilocation:
- reportingservices.mof
helpviewer_keywords:
- WMI provider [Reporting Services], library
ms.assetid: 17ba711d-7eff-4423-9168-63dc425a3428
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 88c12fdc3748b89ad3daba6fcdf5fcd22cdabaf9
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "92255589"
---
# <a name="reporting-services-wmi-provider-library-reference-ssrs"></a>Reporting Services WMI 공급자 라이브러리 참조(SSRS)
  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] WMI(Windows Management Instrumentation) 공급자는 보고서 서버 및 보고서 관리자의 설정을 수정하는 스크립트 및 코드를 쓸 수 있도록 WMI 작업을 지원합니다.  
  
 예를 들어, 보고서 서버에서 보고서 서버 데이터베이스에 연결할 때 통합 보안 사용 여부를 변경하려면 MSReportServer_ConfigurationSetting 클래스의 인스턴스를 만들고 보고서 서버 인스턴스의 DatabaseIntegratedSecurity 속성을 사용합니다. 다음 표에 표시된 클래스는 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 구성 요소를 나타냅니다. 클래스는 [!INCLUDE[ssRSWMInmspc](../../includes/ssrswminmspc-md.md)] 또는 [!INCLUDE[ssRSWMInmspcA](../../includes/ssrswminmspca-md.md)] 네임스페이스에 정의됩니다. 각 클래스는 읽기 및 쓰기 작업을 지원합니다. 만들기 작업은 지원되지 않습니다.  
  
## <a name="classes"></a>클래스  
 [MSReportServer_Instance 클래스](../../reporting-services/wmi-provider-library-reference/msreportserver-instance-class.md)  
 클라이언트에서 설치된 보고서 서버에 연결하는 데 필요한 기본 정보를 제공합니다.  
  
 [MSReportServer_ConfigurationSetting 클래스](../../reporting-services/wmi-provider-library-reference/msreportserver-configurationsetting-class.md)  
 보고서 서버 인스턴스의 설치 및 런타임 매개 변수를 나타냅니다. 이러한 매개 변수는 보고서 서버의 구성 파일에 저장됩니다.  
  
 WMI 작업에 대한 자세한 내용은 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] SDK에 포함된 WMI SDK 설명서를 참조하세요.  
  
## <a name="see-also"></a>참고 항목  
 [Reporting Services WMI 공급자 액세스](../../reporting-services/tools/access-the-reporting-services-wmi-provider.md)   
 [기술 참조&#40;SSRS&#41;](../../reporting-services/technical-reference-ssrs.md)  
  
  
