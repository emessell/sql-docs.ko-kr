---
description: 웹 서버 정보
title: 웹 서버 정보 | Microsoft 문서
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
f1_keywords:
- sql13.rep.newsubwizard.webserverinformation.f1
ms.assetid: 86d72275-45c7-459f-98cf-f5a366ed279c
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 7ba110489a2ec2623018563257953d764ef371c2
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88325958"
---
# <a name="web-server-information"></a>웹 서버 정보
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  병합 복제에 대해 웹 동기화 옵션을 사용하려면 웹 서버 정보가 필요합니다. 웹 동기화를 구성하는 방법은 [웹 동기화 구성](../../relational-databases/replication/configure-web-synchronization.md)을 참조하세요.  
  
## <a name="options"></a>옵션  
 **웹 서버 주소**  
 **게시 속성** 대화 상자의 **FTP 스냅샷 및 인터넷** 페이지에서 웹 서버 주소를 지정한 경우 이 주소가 입력란에 기본값으로 표시됩니다. 해당 기본값을 사용하거나 이 구독을 동기화하는 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 인터넷 정보 서비스(IIS) 서버에 대해 정규화된 웹 서버 주소를 입력하십시오.  
  
 **각 구독자를 웹 서버에 연결하는 방법을 선택하십시오.**  
 웹 서버에 연결할 때 사용할 인증 유형을 지정합니다. IIS 서버에 연결할 때는 이전에 SSL(Secure Sockets Layer)로 알려진 TLS(전송 계층 보안)와 함께 기본 인증을 사용하는 것이 좋습니다. 기본 인증을 선택하는 경우 구독자에서 IIS 서버로 연결할 때 사용할 로그인 및 암호를 입력합니다.  
  
## <a name="see-also"></a>참고 항목  
 [Create a Pull Subscription](../../relational-databases/replication/create-a-pull-subscription.md)   
 [끌어오기 구독 속성 보기 및 수정](../../relational-databases/replication/view-and-modify-pull-subscription-properties.md)   
 [Non-SQL Server Subscribers](../../relational-databases/replication/non-sql/non-sql-server-subscribers.md)   
 [Subscribe to Publications](../../relational-databases/replication/subscribe-to-publications.md)   
 [병합 복제에 대한 웹 동기화](../../relational-databases/replication/web-synchronization-for-merge-replication.md)  
  
  
