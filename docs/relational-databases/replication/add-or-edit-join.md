---
description: 조인 추가 또는 편집
title: 조인 추가 또는 편집 | Microsoft 문서
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
f1_keywords:
- sql13.rep.newpubwizard.addeditjoin.f1
- sql13.sql13.swb.agdashboard.arp4joinstate.issues.f1
ms.assetid: 3b546560-720f-48b8-9d63-cf159290e9d4
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 549970e81b86a8331c2d41afc3b01fab3eb7160b
ms.sourcegitcommit: bd3a135f061e4a49183bbebc7add41ab11872bae
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/21/2020
ms.locfileid: "92300735"
---
# <a name="add-or-edit-join"></a>조인 추가 또는 편집
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  **조인 추가** 및 **조인 편집** 대화 상자를 사용하여 병합 게시에 대한 조인 필터를 추가 및 편집할 수 있습니다.  
  
> [!NOTE]  
>  기존 게시에서 필터를 편집하려면 해당 게시에 대한 새 스냅샷이 필요합니다. 게시에 구독이 있으면 해당 구독을 다시 초기화해야 합니다. 속성 변경에 대한 자세한 내용은 [게시 및 아티클 속성 변경](../../relational-databases/replication/publish/change-publication-and-article-properties.md)을 참조하세요.  
  
 조인 필터를 사용하여 게시의 관련 테이블이 필터링되는 방식에 따라 테이블을 필터링할 수 있습니다. 일반적으로 부모 테이블은 매개 변수가 있는 행 필터를 사용하여 필터링됩니다. 그리고 나서 테이블 간 조인을 정의하는 방식과 매우 유사하게 하나 이상의 조인 필터가 정의됩니다. 조인 필터는 행 필터를 확장하므로 관련 테이블의 데이터는 조인 필터 절과 일치할 경우에만 복제됩니다.  
  
 일반적으로 조인 필터는 조인 필터가 적용되는 테이블에 대해 정의된 기본 키/외래 키 관계를 따르지만 기본 키/외래 키 관계를 엄격하게 따르지는 않습니다. 조인 필터는 두 아티클 테이블의 관련 데이터를 비교하는 논리를 기반으로 할 수 있습니다.  
  
> [!IMPORTANT]  
>  조인 필터는 테이블을 무제한 포함할 수 있지만 테이블 수가 많은 필터는 병합 처리 중 성능에 영향을 줄 수 있습니다. 5개 이상의 테이블을 가진 조인 필터를 생성하는 경우 다른 해결책을 고려하는 것이 좋습니다. 크기가 작거나, 변경될 가능성이 없거나, 기본적으로 조회 테이블에 해당하는 테이블은 필터링하지 마십시오. 구독자 간에 분할해야 하는 테이블 사이에서만 조인 필터를 사용합니다.  
  
## <a name="options"></a>옵션  
 이 대화 상자는 3단계로 이루어진 프로세스를 통해 두 테이블 간에 조인 필터를 만듭니다. 조인 필터를 두 개 이상 만들려면 대화 상자를 두 번 이상 완료해야 합니다.  
  
1.  **필터링된 테이블을 확인하고 조인된 테이블을 선택하십시오.**  
  
    -   새 조인을 추가하는 경우 **필터링된 테이블** 입력란의 테이블이 올바른지 확인합니다. 올바르지 않으면 **취소** 를 클릭하고 **테이블 행 필터** 페이지에서 올바른 테이블을 선택한 다음 **조인 추가** 를 클릭하여 이 대화 상자로 돌아옵니다. 그런 다음 **조인된 테이블** 드롭다운 목록 상자에서 테이블을 선택합니다.  
  
    -   기존 조인을 편집하는 경우에는 테이블 이름이 이미 지정되어 있으며 이를 변경할 수 없습니다. 조인과 관련된 테이블을 변경하려면 **테이블 행 필터** 페이지에서 기존 조인 필터를 삭제하고 다른 테이블 간에 새 조인을 만들어야 합니다.  
  
2.  **조인 문을 작성하십시오.**  
  
    -   새 조인을 추가하는 경우 **작성기를 사용하여 문 작성** 또는 **조인 문 직접 작성** 을 선택합니다. 수동으로 조인 작성을 시작하면 작성기를 사용할 수 없습니다.  
  
         작성기 사용을 선택하면 표의 열( **결합** , **필터링된 테이블 열** , **연산자** 및 **조인된 테이블 열** )을 사용하여 조인 문을 작성합니다. 그리드의 각 열에는 드롭다운 목록 상자가 있어 두 개의 열과 연산자( **=** , **<>** , **<=** , **\<**, **>=** , **>** , **like** )를 선택할 수 있습니다. 결과는 **미리 보기** 텍스트 영역에 표시됩니다. 조인이 둘 이상의 열 쌍을 포함하면 **결합** 열에서 결합( **AND** 또는 **OR** )을 선택한 다음 두 개의 추가 열과 다른 연산자를 입력합니다.  
  
         수동으로 문 작성을 선택하면 **조인 문** 텍스트 영역에 조인 문을 작성합니다. **필터링된 테이블 열** 목록 상자 및 **조인된 테이블 열** 목록 상자를 사용하여 열을 **조인 문** 텍스트 영역에 끌어다 놓습니다.  
  
    -   기존 조인을 편집하는 경우 수동으로 편집해야 합니다.  
  
3.  **조인 옵션을 지정하십시오.**  

    -   필터링된 테이블에서 조인하는 열이 고유하면 **고유 키** 를 선택합니다. 열이 고유하면 병합 프로세스에 특별한 성능 최적화 기능을 사용할 수 있습니다.  
  
        > [!CAUTION]  
        >  이 옵션을 선택하면 조인 필터에서의 자식 테이블과 부모 테이블 간의 관계가 일대일 또는 일대다가 됩니다. 자식 테이블에 있는 조인 열이 고유해야 하는 경우에만 이 옵션을 선택합니다. 이 옵션이 잘못 설정되면 데이터가 일치하지 않을 수 있습니다.  
  
    -   [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 이상 버전에만 해당됩니다. 기본적으로 병합 복제는 동기화 과정에서 행별로 변경 내용을 처리합니다. 관련 변경 내용을 하나의 단위로 처리하려면 **논리적 레코드** 를 선택합니다. 논리적 레코드를 사용하기 위한 아티클 및 게시 요구 사항이 충족되는 경우에만 이 옵션을 사용할 수 있습니다. 자세한 내용은 [논리적 레코드를 사용하여 관련된 행의 변경 내용 그룹화](../../relational-databases/replication/merge/group-changes-to-related-rows-with-logical-records.md)의 "논리적 레코드 사용 시 고려 사항" 섹션을 참조하세요.  
  
 필터를 추가 또는 편집한 후에는 **확인** 을 클릭하여 변경 내용을 저장하고 대화 상자를 닫습니다. 지정한 필터가 구문 분석되고 SELECT 절의 테이블에 대해 실행됩니다. 필터 문에 구문 오류나 기타 문제가 있으면 알림 메시지가 표시되며 이를 보고 필터 문을 편집할 수 있습니다.  
  
## <a name="see-also"></a>참고 항목  
 [Create a Publication](../../relational-databases/replication/publish/create-a-publication.md)   
 [게시 속성 보기 및 수정](../../relational-databases/replication/publish/view-and-modify-publication-properties.md)   
 [게시된 데이터 필터링](../../relational-databases/replication/publish/filter-published-data.md)   
 [Join Filters](../../relational-databases/replication/merge/join-filters.md)   
 [매개 변수가 있는 행 필터](../../relational-databases/replication/merge/parameterized-filters-parameterized-row-filters.md)   
 [데이터 및 데이터베이스 개체 게시](../../relational-databases/replication/publish/publish-data-and-database-objects.md)  
  
  
