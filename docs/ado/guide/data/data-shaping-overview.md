---
description: 데이터 셰이핑 개요
title: 데이터 셰이핑 개요 | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- data shaping [ADO], overview
ms.assetid: 4cb5fd29-4e56-46ac-ae48-a6771c321c0c
author: rothja
ms.author: jroth
ms.openlocfilehash: 45538bd81be1e4a64c41479ab6c4fb2165b26b78
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/27/2020
ms.locfileid: "88991434"
---
# <a name="data-shaping-overview"></a>데이터 셰이핑 개요
*데이터 셰이핑* 은 쿼리에서 둘 이상의 논리적 엔터티 간에 계층적 관계를 작성 하는 것을 의미 합니다. 계층 구조는 한 레코드 [집합](../../reference/ado-api/recordset-object-ado.md)의 레코드와 다른 레코드 **집합**의 하나 이상의 레코드 (챕터 라고도 함) 간의 부모-자식 관계에서 볼 수 있습니다. 부모-자식 관계에서 부모 **레코드 집합** 은 자식 **레코드 집합**을 포함 합니다. 이러한 계층적 관계의 예는 고객과 주문입니다. 데이터베이스의 모든 고객에 대해 0 개 이상의 주문이 있을 수 있습니다. 계층 관계는 재귀적 일 수 있습니다. 즉, 하위 레코드에서 손자 레코드를 중첩할 수 있습니다. 원칙적으로 계층적 레코드는 모든 깊이에 중첩 될 수 있습니다. 실제로 ADO는 재귀를 최대 512 개의 **레코드 집합**으로 제한 합니다.  
  
 일반적으로 셰이프 **레코드 집합** 의 열에는 Microsoft® SQL Server, 다른 **레코드 집합**에 대 한 참조, **레코드 집합**의 단일 행에 대 한 계산에서 파생 된 값 또는 전체 **레코드 집합**의 열에 대해 작업에서 파생 된 값과 같은 데이터 공급자의 데이터가 포함 될 수 있습니다. 열은 새로 만들고 비워 둘 수도 있습니다.  
  
 다른 **레코드 집합**에 대 한 참조를 포함 하는 열의 값을 검색 하면 ADO에서 참조로 표시 되는 실제 **레코드 집합** 을 자동으로 반환 합니다. **레코드 집합** 에 대 한 참조는 실제로 *장*이라는 자식의 하위 집합에 대 한 참조입니다. 단일 부모는 둘 이상의 자식 **레코드 집합**을 참조할 수 있습니다.  
  
 데이터 셰이핑을 위한 ADO 지원을 통해 데이터 원본을 쿼리하고 (부모) 레코드가 (자식) 레코드 **집합**을 나타내는 **레코드 집합** 을 반환할 수 있습니다. 고객 주문 시나리오에서는 데이터 셰이핑을 사용 하 여 고객 정보 뿐만 아니라 각 고객이 단일 쿼리로 배치 된 주문도 검색할 수 있습니다. 결과 **레코드 집합** 을 모양이 지정 된 레코드 **집합**이라고 합니다.  
  
 또한 ADO의 데이터 셰이핑을 사용 하면 **new** 키워드를 사용 하 여 부모 및 자식 **레코드 집합**의 필드를 설명 함으로써 기본 데이터 원본 없이 새 **레코드 집합** 개체를 만들 수 있습니다. 그러면 새 **레코드 집합** 개체를 데이터로 채우고 영구적으로 저장할 수 있습니다. 또한 개발자는 자식 필드에서 다양 한 계산 또는 집계 (예: **SUM**, **AVG**, **MAX**)를 수행할 수 있습니다. 또한 데이터 셰이핑은 자식의 레코드를 그룹화 하 고 자식에 있는 각 그룹의 부모에 하나의 행을 배치 하 여 자식 **레코드 집합** 에서 부모 **레코드 집합** 을 만들 수 있습니다.  
  
 일반 SQL을 사용 하면 **JOIN** 구문을 사용 하 여 데이터를 검색할 수 있지만, 지정 된 부모-자식 관계에 대해 반환 되는 각 레코드에서 중복 부모 데이터가 반복 되므로이는 비효율적 이며 어려울 수 있습니다. 데이터 셰이핑은 부모 레코드 **집합** 의 단일 부모 레코드를 자식 **레코드 집합**의 여러 자식 레코드와 연결 하 여 **조인의**중복성을 피할 수 있습니다. 대부분의 사람들은 단일 **레코드 집합 조인** 모델 보다 자연스럽 고 작업 하기 쉬운 부모-자식 **레코드 집합** 프로그래밍 모델을 찾습니다.