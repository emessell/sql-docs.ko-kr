---
title: Xml 데이터 형식에 대 한 XQuery 연산자 | Microsoft Docs
description: Xml 데이터 형식에 대해 사용할 수 있는 XQuery 연산자에 대해 알아봅니다.
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: sql
ms.reviewer: ''
ms.technology: xml
ms.topic: language-reference
dev_langs:
- XML
helpviewer_keywords:
- XQuery, operators
- operators [XQuery]
- xml data type [SQL Server], XQuery
ms.assetid: 39ca3d2e-e928-4333-872b-75c4ccde8e79
author: rothja
ms.author: jroth
ms.openlocfilehash: d3fc0fece7f57957f38344a557c88fbedb908090
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85730953"
---
# <a name="xquery-operators-against-the-xml-data-type"></a>xml 데이터 형식에 대한 XQuery 연산자
[!INCLUDE [SQL Server Azure SQL Database ](../includes/applies-to-version/sqlserver.md)]

  XQuery에는 다음 연산자가 지원됩니다.  
  
-   수치 연산자(+, -, *, div, mod)  
  
-   값 비교 연산자(eq, ne, lt, gt, le, ge)  
  
-   일반 비교 연산자 (=,! =, \<, > , \<=, > =)  
  
 이러한 연산자에 대 한 자세한 내용은 [XQuery &#40;비교 식](../xquery/comparison-expressions-xquery.md) 을 참조 하세요&#41;  
  
## <a name="examples"></a>예제  
  
### <a name="a-using-general-operators"></a>A. 일반 연산자 사용  
 다음 쿼리는 시퀀스에 적용되고 시퀀스를 비교하는 일반 연산자를 사용하는 방법을 보여 줍니다. 이 쿼리는 **Contact** 테이블의 **additional및 info** 열에서 각 고객에 대 한 일련의 전화 번호를 검색 합니다. 그런 다음 이 번호를 두 개의 전호 번호("111-111-1111", "222-2222")와 비교합니다.  
  
 이 쿼리에서는 비교 연산자를 사용 합니다 **=** . 연산자의 우변에 있는 시퀀스의 각 노드 **=** 는 왼쪽에 있는 시퀀스의 각 노드와 비교 됩니다. 노드가 일치 하면 노드 비교는 **TRUE**입니다. 그런 다음 int로 변환되고 1과 비교되어 쿼리가 고객 ID를 반환합니다.  
  
```sql
WITH XMLNAMESPACES (  
'https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ContactInfo' AS ACI,  
'https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ContactTypes' AS ACT)  
SELECT ContactID   
FROM   Person.Contact  
WHERE  AdditionalContactInfo.value('  
      //ACI:AdditionalContactInfo//ACT:telephoneNumber/ACT:number =   
          ("111-111-1111", "222-2222")',  
      'bit')= cast(1 as bit)  
```  
  
 이전 쿼리의 작동 방식을 확인 하는 또 다른 방법이 있습니다. **Additional및 info** 열에서 검색 된 각 전화번호 전화 번호 값을 두 개의 전화 번호 집합과 비교 합니다. 값이 집합에 있는 경우 각 해당 고객이 결과에 반환됩니다.  
  
### <a name="b-using-a-numeric-operator"></a>B. 숫자 연산자 사용  
 이 쿼리의 + 연산자는 단일 항목에 적용되기 때문에 값 연산자입니다. 예를 들어 쿼리에 의해 반환되는 로트 크기에 값 1이 추가됩니다.  
  
```sql
SELECT ProductModelID, Instructions.query('  
     declare namespace   
 AWMI="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions";  
     for $i in (/AWMI:root/AWMI:Location)[1]  
     return   
       <Location LocationID="{ ($i/@LocationID) }"  
                   LotSize  = "{  number($i/@LotSize) }"  
                   LotSize2 = "{ number($i/@LotSize) + 1 }"  
                   LotSize3 = "{ number($i/@LotSize) + 2 }" >  
  
       </Location>  
') as Result  
FROM Production.ProductModel  
where ProductModelID=7  
```  
  
### <a name="c-using-a-value-operator"></a>C. 값 연산자 사용  
 다음 쿼리는 `Picture` 그림 크기가 "small" 인 제품 모델에 대 한 <> 요소를 검색 합니다.  
  
```sql
SELECT CatalogDescription.query('  
     declare namespace PD="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription";  
     for $P in /PD:ProductDescription/PD:Picture[PD:Size eq "small"]  
     return  
           $P  
    ') as Result  
FROM Production.ProductModel  
where ProductModelID=19  
```  
  
 **Eq** 연산자에 대 한 피연산자는 모두 atomic 값 이므로 값 연산자가 쿼리에 사용 됩니다. 일반 비교 연산자 ()를 사용 하 여 동일한 쿼리를 작성할 수 있습니다 **=** .  
  
## <a name="see-also"></a>참고 항목  
 [Xml 데이터 형식에 대 한 XQuery 함수](../xquery/xquery-functions-against-the-xml-data-type.md)   
 [XML 데이터 &#40;SQL Server&#41;](../relational-databases/xml/xml-data-sql-server.md)   
 [XQuery 언어 참조&#40;SQL Server&#41;](../xquery/xquery-language-reference-sql-server.md)  
  
  
