---
description: 영향을 받는 개체 선택 및 구성(SybaseToSQL)
title: 영향을 받는 개체 선택 및 구성 (SybaseToSQL) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- Tester Component,Affected Objects
ms.assetid: a219df74-543a-4aec-aeeb-79f90ac3e2ee
author: nahk-ivanov
ms.author: alexiva
ms.openlocfilehash: 793430d548053b8d4c1cbf8dd07dd4e7d691c6d3
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88468745"
---
# <a name="selecting-and-configuring-affected-objects-sybasetosql"></a>영향을 받는 개체 선택 및 구성(SybaseToSQL)
이 페이지에서 테이블 및 외래 키를 선택할 수 있으며, SSMA가 이전 단계에서 선택한 개체의 실행 결과를 확인할 때 이러한 변경 내용을 비교 해야 합니다. 또한 확인 매개 변수를 사용자 지정할 수 있습니다.  
  
## <a name="selection-of-affected-objects"></a>영향을 받는 개체 선택  
창 왼쪽에 있는 Sybase 개체 트리에서 테이블 및 외래 키를 확인 하 고,의 변경 내용이 동일 하 게 비교 되어야 합니다.  
  
SSMA 테스터가 이러한 개체를 확인할 수 없는 경우 개체 트리 아래에 **선택한 일부 개체에 오류가** 있습니다. 라는 링크가 표시 됩니다. 이 링크를 클릭 하 여 이러한 개체를 비교할 수 없는 이유를 확인 하 고 잘못 된 개체 선택을 지울 수 있습니다.  
  
## <a name="table"></a>테이블  
테이블 탭에는 선택한 테이블의 표 뷰가 포함 되어 있습니다. 표는 선택한 테이블에 대 한 다음 정보를 포함 합니다.  
  
-   열 이름  
  
-   데이터 형식  
  
-   전체 자릿수  
  
-   확장  
  
-   규칙  
  
-   기본값  
  
-   ID  
  
-   Nullable  
  
## <a name="sql"></a>Sql  
SQL 탭에는 선택한 테이블의 "테이블 만들기" SQL이 포함 됩니다.  
  
## <a name="data"></a>데이터  
데이터 탭 선택한 테이블에 있는 데이터를 표시 합니다.  
  
## <a name="properties"></a>속성  
속성 탭 선택한 테이블의 속성을 표시 합니다. 속성 탭에는 다음과 같은 필드가 있습니다.  
  
-   만들었거나 마지막으로 수정한 날짜  
  
-   개체 이름  
  
## <a name="table-comparison-settings"></a>테이블 비교 설정  
**테이블 비교** 페이지에서 테이블에 대 한 비교 규칙을 설정 합니다. 다음과 같이 설정할 수 있습니다.  
  
### <a name="comparison-mode"></a>비교 모드  
비교를 수행할 테이블 콘텐츠를 정의 합니다.  
  
-   **변경 내용만**선택 하는 경우 테이블 행의 전체 비교가 수행 됩니다.  
  
-   **전체**를 선택 하면 변경 된 행에 대해서만 비교가 수행 됩니다.  
  
## <a name="column-comparison-settings"></a>열 비교 설정  
**열 비교** 페이지의 테이블 열에 대 한 비교 규칙을 설정 합니다. 다음과 같이 설정할 수 있습니다.  
  
### <a name="use-during-test-comparisons"></a>테스트 비교 중 사용  
이 열이 테스트 결과 확인에 참여할지 여부를 결정 합니다.  
  
-   **True**를 선택 하면 SQL Server의 열 내용으로 Sybase에서 테스트를 실행 한 후 ssma가이 열의 내용을 비교 합니다.
  
-   **False**를 선택 하면 열이 결과 확인에서 제외 됩니다.  
  
### <a name="use-custom-scale"></a>사용자 지정 배율 사용  
숫자 데이터 형식의 열에 대해서는 비교를 위해 사용자 지정 눈금을 설정할 수 있습니다.  
  
-   **True**를 선택 하는 경우 비교 하기 전에 **비교 배율** 값에 따라 숫자 값이 반올림 됩니다.  
  
-   **False**를 선택 하면 숫자 비교가 정확 하 게 됩니다.  
  
### <a name="comparing-scale"></a>배율 비교  
  
-   **사용자 지정 배율 사용** 옵션을 **True**로 설정한 경우에만 사용할 수 있습니다. 숫자 비교의 전체 자릿수입니다.  
  
### <a name="date-time-comparing"></a>비교 날짜 시간  
날짜/시간 값을 비교 하는 방법을 정의 합니다.  
  
-   **전체 날짜 비교**를 선택 하면 두 플랫폼의 값에 대 한 전체 비교가 수행 됩니다.  
  
-   **날짜만 비교**를 선택 하는 경우 시간 부분은 무시 됩니다.  
  
-   **시간만 비교**를 선택 하는 경우 날짜 부분은 무시 됩니다.  
  
-   **밀리초 무시**를 선택 하면 결과가 최대 초까지 비교 됩니다.  
  
-   **날짜 및 밀리초 무시**를 선택 하면 결과는 시간 부분에 의해서만 비교 되 고 초의 소수 부분은 무시 됩니다.  
  
### <a name="ignore-strings-case"></a>문자열 대/소문자 무시  
비교의 대/소문자 구분 여부를 제어 합니다.  
  
-   **True**를 선택 하면 비교 시 대/소문자를 구분 하지 않습니다.  
  
-   **False**를 선택 하는 경우 비교 시 대/소문자를 고려 합니다.  
  
## <a name="comparing-sql"></a>SQL 비교  
**SQL 비교** 페이지에서 Ssma 테스터에 의해 생성 된 SELECT 문을 볼 수 있습니다. 테스터는 행 단위로 이러한 문의 결과 집합을 비교 합니다. Sybase 결과 집합의 다음 행은에서 생성 된 결과 집합의 다음 행과 같아야 합니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
이러한 SELECT 문을 편집 하 여 사용자 지정 확인을 제공할 수 있습니다. Sybase 및 문에서 변경 내용을 저장 하려면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 원본 및 대상 SQL에서 **적용** 단추를 사용 합니다.  
  
## <a name="next-step"></a>다음 단계  
[호출 순서 사용자 지정 &#40;SybaseToSQL&#41;](../../ssma/sybase/customizing-calls-order-sybasetosql.md)  
  
## <a name="see-also"></a>참고 항목  
[테스트 사례 실행 &#40;SybaseToSQL&#41;](../../ssma/sybase/running-test-cases-sybasetosql.md)  
[마이그레이션된 데이터베이스 개체 테스트 &#40;SybaseToSQL&#41;](../../ssma/sybase/testing-migrated-database-objects-sybasetosql.md)  
  
