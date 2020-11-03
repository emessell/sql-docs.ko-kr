---
description: 옵션(디자이너 - 테이블 및 데이터베이스 디자이너 페이지)
title: 옵션(디자이너 - 테이블 및 데이터베이스 디자이너 페이지)
ms.custom: seo-lt-2019
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
f1_keywords:
- VS.ToolsOptionsPages.Designers.Table_Designer
ms.assetid: b43f4b97-17b9-4004-a824-f77b9e145741
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 36e62c2d30e4678c8b41223003db35b13e8d15ac
ms.sourcegitcommit: 22e97435c8b692f7612c4a6d3fe9e9baeaecbb94
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/27/2020
ms.locfileid: "92679245"
---
# <a name="options-designers---table-and-database-designers-page"></a>옵션(디자이너 - 테이블 및 데이터베이스 디자이너 페이지)
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]
이 페이지를 사용하여 디자이너의 기본 동작을 결정할 수 있습니다. 이 설정에 액세스하려면 **도구** 메뉴에서 **옵션** 을 클릭하고 **디자이너** 폴더를 확장한 다음 **테이블 디자이너** 를 클릭합니다.  
  
## <a name="ui-element-list"></a>UI 요소 목록  
**테이블 디자이너 업데이트에 대한 연결 문자열 제한 시간 값 재정의**  
테이블 디자이너의 동작에 대해 새 제한 시간 값을 설정하도록 허용합니다. 이 옵션은 테이블 디자이너가 수정하는 데 시간이 많이 걸리는 대형 테이블에 대한 작업을 수행하는 경우에 유용합니다.  
  
**트랜잭션 제한 시간**  
테이블 디자이너에 대한 제한 시간 값을 설정합니다.  
  
**변경 스크립트 자동 생성**  
테이블 디자이너에서 정의된 변경 내용을 구현하는 스크립트를 자동으로 만듭니다.  
  
**Null 기본 키 경고**  
기본 키로 선택한 필드에 Null 값이 포함될 수 있는 경우에 경고 대화 상자를 표시합니다.  
  
**차이점 발견 경고**  
이 확인란을 선택하면 변경 내용을 저장할 때 현재 변경 내용과 다른 사용자의 변경 내용 간 충돌 사항이 모두 메시지 상자에 나열됩니다.  
  
**영향을 받는 테이블 경고**  
동작 대상 테이블을 표시하고 사용자의 확인을 받는 경고 대화 상자를 표시합니다.  
  
**테이블을 다시 만들어야 하는 변경 내용 저장 사용 안 함**  
테이블을 다시 만들어야 하는 변경 내용을 사용자가 저장할 수 없게 만듭니다. 다음 동작을 수행하려면 테이블을 다시 만들어야 할 수 있습니다.  
  
-   테이블의 중간에 새 열 추가  
  
-   열 삭제  
  
-   열의 Null 허용 여부 변경  
  
-   열의 순서 변경  
  
-   열의 데이터 형식 변경  
  
**기본 테이블 뷰**  
다음과 같이 디자이너에서 테이블을 표시하는 방법을 선택합니다.  
  
-   **Standard**  
  
    테이블 머리글, 모든 열 이름, 데이터 형식 및 Null 허용 설정을 표시합니다.  
  
-   **열 이름**  
  
    열 이름을 표시합니다.  
  
-   **Key**  
  
    테이블 머리글과 기본 키 열을 표시합니다.  
  
-   **테이블 이름만**  
  
    이름이 있는 테이블 머리글만 표시합니다.  
  
-   **Custom**  
  
    표시할 열을 선택할 수 있습니다.  
  
**새 다이어그램에서 [테이블 추가] 대화 상자 시작**  
디자이너가 열리면 자동으로 **테이블 추가** 대화 상자가 열립니다.  
  
