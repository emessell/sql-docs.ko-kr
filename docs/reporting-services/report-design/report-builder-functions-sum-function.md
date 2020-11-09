---
title: Sum 함수(보고서 작성기) | Microsoft Docs
description: 보고서 작성기의 Sum 함수는 식으로 지정된 Null이 아닌 모든 숫자 값의 합을 반환합니다.
ms.date: 03/07/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-design
ms.topic: conceptual
ms.assetid: 2b45a024-398d-43b8-9948-b8b23fb674c9
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: fe8a7c4948b811a97c2f6973a04227543a496991
ms.sourcegitcommit: b3a711a673baebb2ff10d7142b209982b46973ae
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/05/2020
ms.locfileid: "93364425"
---
# <a name="report-builder-functions---sum-function"></a>보고서 작성기 함수 - Sum 함수
  식으로 지정되어 정해진 범위에서 계산되는 Null이 아닌 모든 숫자 값의 합계를 반환합니다.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="syntax"></a>구문  
  
```  
  
Sum(expression, scope, recursive)  
```  
  
#### <a name="parameters"></a>매개 변수  
 *expression*  
 ( **Integer** 또는 **Float** ) 집계를 수행할 식입니다.  
  
 *범위*  
 ( **문자열** ) 선택 사항입니다. 집계 함수를 적용할 보고서 항목을 포함하는 데이터 세트, 그룹 또는 데이터 영역의 이름입니다. *scope* 를 지정하지 않은 경우 현재 범위가 사용됩니다.  
  
 *재귀*  
 ( **열거 형식** ) 선택 사항입니다. **Simple** (기본값) 또는 **RdlRecursive** 입니다. 집계를 재귀적으로 수행할지 여부를 지정합니다.  
  
## <a name="return-type"></a>반환 형식  
 10진수 식에는 **Decimal** 을, 그 외 다른 식에는 **Double** 을 반환합니다.  
  
## <a name="remarks"></a>설명  
 식에 지정한 데이터 집합은 동일한 데이터 형식으로 구성되어야 합니다. 여러 숫자 데이터 형식이 포함된 데이터를 동일한 데이터 형식으로 변환하려면 **CInt** , **CDbl** 또는 **CDec** 같은 변환 함수를 사용하세요. 자세한 내용은 [형식 변환 함수](https://go.microsoft.com/fwlink/?LinkId=96142)를 참조하세요.  
  
 *scope* 의 값은 문자열 상수여야 하고 식일 수 없습니다. 외부 집계나 다른 집계를 지정하지 않는 집계의 경우 *scope* 는 현재 범위나 포함하는 범위를 참조해야 합니다. 집계의 집계의 경우 중첩 집계는 자식 범위를 지정할 수 있습니다.  
  
 *Expression* 에는 다음 예외와 조건이 있는 중첩 집계 함수에 대한 호출이 포함될 수 있습니다.  
  
-   중첩 집계의 *Scope* 는 외부 집계의 범위와 동일하거나 외부 집계의 범위에 포함되어야 합니다. 식에 있는 모든 고유 범위의 경우 한 범위는 다른 모든 범위에 대한 자식 관계에 있어야 합니다.  
  
-   중첩 집계의 *Scope* 는 데이터 세트의 이름일 수 없습니다.  
  
-   *Expression* 에는 **First** , **Last** , **Previous** 또는 **RunningValue** 함수가 포함되지 않아야 합니다.  
  
-   *Expression* 에는 *recursive* 를 지정하는 중첩 집계가 포함되지 않아야 합니다.  
  
 자세한 내용은 [집계 함수 참조&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/report-builder-functions-aggregate-functions-reference.md) 및 [합계, 집계 및 기본 제공 컬렉션의 식 범위&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/expression-scope-for-totals-aggregates-and-built-in-collections.md)를 참조하세요.  
  
 재귀 집계에 대한 자세한 내용은 [재귀 계층 구조 그룹 만들기&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/creating-recursive-hierarchy-groups-report-builder-and-ssrs.md)를 참조하세요.  
  
## <a name="examples"></a>예제  

### <a name="a-sum-of-line-item-totals"></a>A. 줄 항목 합계의 총계 
 다음의 두 코드 예제에서는 `Order` 그룹 또는 데이터 영역에서 줄 항목 합계의 총계를 제공합니다.  
  
```  
=Sum(Fields!LineTotal.Value, "Order")  
' or   
=Sum(CDbl(Fields!LineTotal.Value), "Order")  
```  
  
### <a name="b-maximum-value-from-all-nested-regions"></a>B. 모든 중첩된 영역의 최댓값 
 중첩 행 그룹 Category 및 Subcategory와 중첩 열 그룹 Year 및 Quarter가 있는 행렬 데이터 영역의 가장 안쪽 행 및 열 그룹에 속하는 셀에서 다음 식은 모든 하위 범주에 대한 모든 분기의 최대값으로 계산됩니다.  
  
```  
=Max(Sum(Fields!Sales.Value))  
```  
  
## <a name="see-also"></a>참고 항목  
 [보고서에 사용되는 식&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/expression-uses-in-reports-report-builder-and-ssrs.md)   
 [식 예&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/expression-examples-report-builder-and-ssrs.md)   
 [식의 데이터 형식&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/data-types-in-expressions-report-builder-and-ssrs.md)   
 [합계, 집계 및 기본 제공 컬렉션의 식 범위&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/expression-scope-for-totals-aggregates-and-built-in-collections.md)  
  
  
