---
title: LookupSet 함수(보고서 작성기) | Microsoft Docs
description: 이름 또는 값 쌍이 있는 데이터 세트에서 지정된 이름과 일치하는 값 집합을 반환하는 LookupSet 함수에 대해 알아봅니다.
ms.date: 03/07/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-design
ms.topic: conceptual
ms.assetid: 7685acfd-1c8d-420c-993c-903236fbe1ff
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 22d4a311d38d32fad4910960007223edbe2f9b70
ms.sourcegitcommit: b3a711a673baebb2ff10d7142b209982b46973ae
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/05/2020
ms.locfileid: "93364465"
---
# <a name="report-builder-functions---lookupset-function"></a>보고서 작성기 함수 - LookupSet 함수
  이름/값 쌍을 포함하는 데이터 세트에서 지정된 이름과 일치하는 값 집합을 반환합니다.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="syntax"></a>구문  
  
```  
  
LookupSet(source_expression, destination_expression, result_expression, dataset)  
```  
  
#### <a name="parameters"></a>매개 변수  
 *source_expression*  
 ( **Variant** ) 현재 범위에서 평가되고, 조회할 키 또는 이름을 지정하는 식입니다. 예들 들어 `=Fields!ID.Value`입니다.  
  
 *destination_expression*  
 ( **Variant** ) 데이터 세트의 각 행에 대해 평가되고, 일치시킬 키 또는 이름을 지정하는 식입니다. 예들 들어 `=Fields!CustomerID.Value`입니다.  
  
 *result_expression*  
 ( **Variant** ) *source_expression* = *destination_expression* 인 데이터 세트의 행에 대해 평가되고, 검색할 값을 지정하는 식입니다. 예들 들어 `=Fields!PhoneNumber.Value`입니다.  
  
 *데이터 세트*  
 보고서의 데이터 세트 이름을 지정하는 상수입니다. 예를 들면 "ContactInformation"입니다.  
  
## <a name="return"></a>반환 값  
 **VariantArray** 를 반환하거나, 일치하는 항목이 없으면 **Nothing** 을 반환합니다.  
  
## <a name="remarks"></a>설명  
 **LookupSet** 을 사용하여 일 대 다 관계의 이름/값 쌍에 대한 지정된 데이터 세트에서 값 집합을 검색할 수 있습니다. 예를 들어 테이블에 있는 고객 식별자의 경우 **LookupSet** 을 사용하여 데이터 영역에 바인딩되지 않은 데이터 세트에서 해당 고객에 대해 연결된 전화 번호를 모두 검색할 수 있습니다.  
  
 **LookupSet** 은 다음을 수행합니다.  
  
-   현재 범위에서 원본 식을 평가합니다.  
  
-   지정된 데이터 세트의 데이터 정렬을 기반으로 필터가 적용된 후 지정된 데이터 세트의 각 행에 대해 대상 식을 평가합니다.  
  
-   원본 식과 대상 식의 일치 항목을 찾을 때마다 데이터 세트의 해당 행에 대해 결과 식을 평가합니다.  
  
-   결과 식 값의 집합을 반환합니다.  
  
 일 대 일 관계의 이름/값 쌍을 포함하는 데이터 세트에서 지정된 이름에 대한 단일 값을 검색하려면 [Lookup 함수&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/report-builder-functions-lookup-function.md)을 사용합니다. 값 집합에 대한 **Lookup** 을 호출하려면 [Multilookup 함수&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/report-builder-functions-multilookup-function.md)를 사용합니다.  
  
 다음 제한 사항이 적용됩니다.  
  
-   **LookupSet** 은 모든 필터 식이 적용된 후 평가됩니다.  
  
-   조회 수준이 하나만 지원됩니다. 원본, 대상 또는 결과 식에는 조회 함수에 대한 참조가 포함될 수 없습니다.  
  
-   원본 식과 대상 식의 데이터 형식이 같아야 합니다.  
  
-   원본, 대상 및 결과 식에는 보고서 또는 그룹 변수에 대한 참조가 포함될 수 없습니다.  
  
-   **LookupSet** 은 다음 보고서 항목에 대한 식으로 사용할 수 없습니다.  
  
    -   데이터 원본에 대한 동적 연결 문자열  
  
    -   데이터 세트의 계산된 필드.  
  
    -   데이터 세트의 쿼리 매개 변수.  
  
    -   데이터 세트의 필터.  
  
    -   보고서 매개 변수  
  
    -   Report.Language 속성입니다.  
  
 자세한 내용은 [집계 함수 참조&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/report-builder-functions-aggregate-functions-reference.md) 및 [합계, 집계 및 기본 제공 컬렉션의 식 범위&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/expression-scope-for-totals-aggregates-and-built-in-collections.md)를 참조하세요.  
  
## <a name="examples"></a>예

 다음 예제에서는 영업 지역 식별자 TerritoryGroupID를 포함하는 데이터 세트에 테이블이 바인딩되어 있다고 가정합니다. "Stores"라는 별도의 데이터 세트에는 지역의 모든 매장 목록과 지역 식별자 ID 및 매장 이름 StoreName이 포함되어 있습니다.  
  
### <a name="a-use-lookupset"></a>A. LookupSet 사용  
 다음 식에서 **LookupSet** 는 TerritoryGroupID 값을 "Stores" 데이터 세트에 있는 각 행의 ID와 비교합니다. 일치 항목을 찾을 때마다 해당 행에 대한 StoreName 필드의 값이 결과 집합에 추가됩니다.  
  
```  
=LookupSet(Fields!TerritoryGroupID.Value, Fields!ID.Value, Fields!StoreName.Value, "Stores")  
```  
  
### <a name="b-use-join-to-create-a-result-list"></a>B. Join을 사용하여 결과 목록 만들기 
 **LookupSet** 은 개체 컬렉션을 반환하므로 결과 식을 입력란에 직접 표시할 수 없습니다. 컬렉션에 있는 각 개체의 값을 문자열로 연결할 수 있습니다.  
  
 [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)] 함수 **Join** 을 사용하여 개체 집합에서 구분된 문자열을 만들 수 있습니다. 개체를 한 줄로 결합하려면 쉼표를 구분 기호로 사용합니다. 일부 렌더러에서는 [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)] 줄 바꿈(`vbCrLF`)을 구분 기호로 사용하여 각 값을 새 줄에 나열할 수 있습니다.  
  
 입력란의 Value 속성으로 사용된 다음 식은 **Join** 을 사용하여 목록을 만듭니다.  
  
```  
=Join(LookupSet(Fields!TerritoryGroupID.Value, Fields!ID.Value, Fields!StoreName.Value, "Stores"),",")  
```  
  
### <a name="c-add-code-to-generate-html"></a>C. HTML을 생성하는 코드 추가
 몇 번만 렌더링되는 입력란의 경우 입력란에 값을 표시하는 HTML을 생성하기 위해 사용자 지정 코드를 추가하도록 선택할 수도 있습니다. 입력란에 HTML을 표시하려면 추가 처리 작업이 필요하므로 수천 번 렌더링되는 입력란의 경우에는 이러한 선택이 적합하지 않습니다.  
  
 다음 [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)] 함수를 보고서 정의의 Code 블록에 복사합니다. **MakeList** 는 *result_expression* 에서 반환되는 개체 배열을 사용하고 HTML 태그를 사용하여 정렬되지 않은 목록을 만듭니다. **Length** 는 개체 배열의 항목 수를 반환합니다.  
  
```  
Function MakeList(ByVal items As Object()) As String  
   If items Is Nothing Then  
      Return Nothing  
   End If  
  
   Dim builder As System.Text.StringBuilder =   
      New System.Text.StringBuilder()  
   builder.Append("<ul>")  
  
   For Each item As Object In items  
      builder.Append("<li>")  
      builder.Append(item)  
   Next  
   builder.Append("</ul>")  
  
   Return builder.ToString()  
End Function  
  
Function Length(ByVal items as Object()) as Integer  
   If items is Nothing Then  
      Return 0  
   End If  
   Return items.Length  
End Function  
```  
  
### <a name="d-call-the-function"></a>D. 함수 호출
 HTML을 생성하려면 함수를 호출해야 합니다. 다음 식을 입력란의 Value 속성에 붙여넣고 텍스트의 태그 형식을 HTML로 설정합니다. 자세한 내용은 [보고서에 HTML 추가&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/add-html-into-a-report-report-builder-and-ssrs.md)를 참조하세요.  
  
```  
=Code.MakeList(LookupSet(Fields!TerritoryGroupID.Value, Fields!ID.Value, Fields!StoreName.Value, "Stores"))  
```  
  
## <a name="see-also"></a>참고 항목  
 [보고서에 사용되는 식&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/expression-uses-in-reports-report-builder-and-ssrs.md)   
 [식 예&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/expression-examples-report-builder-and-ssrs.md)   
 [식의 데이터 형식&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/data-types-in-expressions-report-builder-and-ssrs.md)   
 [합계, 집계 및 기본 제공 컬렉션의 식 범위&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/expression-scope-for-totals-aggregates-and-built-in-collections.md)  
  
  
