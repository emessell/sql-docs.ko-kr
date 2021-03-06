---
description: 사용자의 사용 권한 테스트(Master Data Services)
title: 사용자&#39;s 사용 권한 테스트
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: mds
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
ms.assetid: 83a03b85-ea7f-4b4a-b19b-f7eca534ffae
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: 90299ab429b38e3c851b51273742c5fef28fec40
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88471909"
---
# <a name="test-a-user39s-permissions-master-data-services"></a>사용자의 사용 권한 테스트(Master Data Services)

[!INCLUDE [SQL Server - Windows only ASDBMI  ](../includes/applies-to-version/sql-windows-only-asdbmi.md)]

  [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]에서 테스트 사용자를 만들고 사용 권한을 테스트하기 위해 웹 애플리케이션에 로그인할 수 있습니다. 사용자가 [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] URL에 액세스하려고 시도할 때 사용자의 자격 증명이 인증됩니다. Internet Explorer의 보안 설정에 따라 인증이 자동으로 진행되는지, 아니면 사용자 이름 및 암호를 입력해야 하는지 여부가 결정됩니다. 이 설정을 변경하려면 다음 단계를 수행하십시오.  
  
### <a name="to-test-a-users-security"></a>사용자의 보안을 테스트하려면  
  
1.  Internet Explorer 7 이상에서 **도구**, **인터넷 옵션**을 차례로 클릭한 다음 **보안** 탭을 클릭합니다.  
  
2.  **로컬 인트라넷** 을 클릭한 다음 **사용자 지정 수준** 단추를 클릭합니다.  
  
3.  **사용자 인증** 섹션에서 **사용자 이름 및 암호 확인**을 선택합니다.  
  
4.  다음에 브라우저 창을 열면 사용자 이름과 암호를 입력하라는 메시지가 표시됩니다.  
  
## <a name="see-also"></a>참고 항목  
 [보안&#40;Master Data Services&#41;](../master-data-services/security-master-data-services.md)  
  
  
