---
title: 식 컨텍스트 및 쿼리 평가 (XQuery) | Microsoft Docs
description: XQuery 식의 정적 및 동적 컨텍스트에서 정보를 분석 하 고 평가 하는 데 사용 하는 방법에 대해 알아봅니다.
ms.custom: ''
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: sql
ms.reviewer: ''
ms.technology: xml
ms.topic: language-reference
dev_langs:
- XML
helpviewer_keywords:
- expression context [XQuery]
- XQuery, expression context
- XQuery, query evaluation
- static context
- dynamic context [XQuery]
ms.assetid: 5059f858-086a-40d4-811e-81fedaa18b06
author: rothja
ms.author: jroth
ms.openlocfilehash: a870cdbd9a90fefe29088892f278446479665de7
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85753636"
---
# <a name="expression-context-and-query-evaluation-xquery"></a>식 컨텍스트 및 쿼리 평가(XQuery)
[!INCLUDE [SQL Server Azure SQL Database ](../includes/applies-to-version/sqlserver.md)]

  식의 컨텍스트는 식을 분석 및 평가하는 데 사용되는 정보입니다. XQuery는 다음과 같은 두 개의 단계로 평가됩니다.  
  
-   **정적 컨텍스트** -쿼리 컴파일 단계입니다. 사용 가능한 정보에 따라 일부 경우에 이러한 쿼리 정적 분석 중에 오류가 발생할 수 있습니다.  
  
-   **동적 컨텍스트** -쿼리 실행 단계입니다. 쿼리 컴파일 중의 오류와 같은 정적 오류가 쿼리에 없는 경우에도 실행 중에 쿼리가 오류를 반환할 수 있습니다.  
  
## <a name="static-context"></a>정적 컨텍스트  
 정적 컨텍스트 초기화는 식에 대한 정적 분석을 위해 모든 정보를 함께 입력하는 프로세스를 의미합니다. 정적 컨텍스트 초기화의 일부로 다음과 같은 작업이 완료됩니다.  
  
-   **경계 공백** 정책이 스트립으로 설정 되어 있습니다. 따라서 경계 공백은 쿼리의 **모든 요소** 및 **특성** 생성자에 의해 유지 되지 않습니다. 예를 들면 다음과 같습니다.  
  
    ```  
    declare @x xml  
    set @x=''  
    select @x.query('<a>  {"Hello"}  </a>,  
  
        <b> {"Hello2"}  </b>')  
    ```  
  
     XQuery 식을 구문 분석하는 동안 경계 공백이 삭제되기 때문에 이 쿼리는 다음 결과를 반환합니다.  
  
    ```  
    <a>Hello</a><b>Hello2</b>  
    ```  
  
-   접두사 및 네임스페이스 바인딩은 다음에 대해 초기화됩니다.  
  
    -   미리 정의된 네임스페이스 집합  
  
    -   WITH XMLNAMESPACES를 사용하여 정의된 모든 네임스페이스. 자세한 내용은 [WITH XMLNAMESPACES를 사용 하 여 쿼리에 네임 스페이스 추가](../relational-databases/xml/add-namespaces-to-queries-with-with-xmlnamespaces.md)를 참조 하세요.  
  
    -   쿼리 프롤로그에 정의된 모든 네임스페이스. 프롤로그에 있는 네임스페이스 선언은 WITH XMLNAMESPACES에 있는 네임스페이스 선언을 무효화할 수 있습니다. 예를 들어 다음 쿼리에서 XMLNAMESPACES는 네임 스페이스 ()에 바인딩하는 접두사 (pd)를 선언 `https://someURI` 합니다. 하지만 WHERE 절에서 쿼리 프롤로그가 이 바인딩을 무효화합니다.  
  
        ```  
        WITH XMLNAMESPACES ('https://someURI' AS pd)  
        SELECT ProductModelID, CatalogDescription.query('  
            <Product   
                ProductModelID= "{ sql:column("ProductModelID") }"   
                />  
        ') AS Result  
        FROM Production.ProductModel  
        WHERE CatalogDescription.exist('  
            declare namespace  pd="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription";  
             /pd:ProductDescription[(pd:Specifications)]'  
            ) = 1  
        ```  
  
     이러한 모든 네임스페이스 바인딩은 정적 컨텍스트 초기화 중에 확인됩니다.  
  
-   형식화 된 **xml** 열 또는 변수를 쿼리하면 열 또는 변수와 연결 된 xml 스키마 컬렉션의 구성 요소를 정적 컨텍스트로 가져옵니다. 자세한 내용은 [형식화 된 Xml과 형식화 되지 않은 Xml 비교](../relational-databases/xml/compare-typed-xml-to-untyped-xml.md)를 참조 하세요.  
  
-   가져온 스키마에 있는 모든 원자 유형에 대해 정적 컨텍스트에서 캐스트 함수를 사용할 수도 있습니다. 다음 예에서 확인할 수 있습니다. 이 예에서는 형식화 된 **xml** 변수에 대해 쿼리가 지정 됩니다. 이 변수와 연결된 XML 스키마 컬렉션은 원자 유형인 myType을 정의합니다. 이 형식에 해당 하는 캐스팅 함수인 **myType ()** 은 정적 분석 중에 사용할 수 있습니다. 쿼리 식(`ns:myType(0)`)은 myType의 값을 반환합니다.  
  
    ```  
    -- DROP XML SCHEMA COLLECTION SC  
    -- go  
    CREATE XML SCHEMA COLLECTION SC AS '<schema xmlns="http://www.w3.org/2001/XMLSchema"   
    targetNamespace="myNS" xmlns:ns="myNS"  
    xmlns:s="https://schemas.microsoft.com/sqlserver/2004/sqltypes">  
          <import namespace="https://schemas.microsoft.com/sqlserver/2004/sqltypes"/>  
          <simpleType name="myType">  
                <restriction base="int">  
                 <enumeration value="0" />  
                  <enumeration value="1"/>  
                </restriction>  
          </simpleType>  
          <element name="root" type="ns:myType"/>  
    </schema>'  
    go  
  
    DECLARE @var XML(SC)  
    SET @var = '<root xmlns="myNS">0</root>'  
    -- specify myType() casting function in the query  
    SELECT @var.query('declare namespace ns="myNS"; ns:myType(0)')  
    ```  
  
     다음 예에서는 **int** 기본 제공 XML 유형에 대 한 캐스팅 함수를 식에 지정 합니다.  
  
    ```  
    declare @x xml  
    set @x = ''  
    select @x.query('xs:int(5)')  
    go  
    ```  
  
 정적 컨텍스트가 초기화된 다음 쿼리 식이 분석(컴파일)됩니다. 정적 분석에는 다음이 포함됩니다.  
  
1.  쿼리 구문 분석  
  
2.  식에 지정된 함수 및 유형 이름 확인  
  
3.  쿼리에 대한 정적 형식 지정. 이 작업은 쿼리가 안전한 유형인지 확인합니다. 예를 들어 다음 쿼리는 **+** 연산자에 숫자 기본 형식 인수가 필요 하기 때문에 정적 오류를 반환 합니다.  
  
    ```  
    declare @x xml  
    set @x=''  
    SELECT @x.query('"x" + 4')  
    ```  
  
     다음 예제에서 **value ()** 연산자에는 단일 항목이 필요 합니다. XML 스키마에 지정 된 대로 여러 요소가 있을 수 있습니다 \<Elem> . 식에 대한 정적 분석은 식의 안정성 여부와 정적 오류의 반환 여부를 확인합니다. 오류를 확인하려면 단일 항목(`data(/x:Elem)[1]`)을 명시적으로 지정하도록 식을 다시 작성해야 합니다.  
  
    ```  
    DROP XML SCHEMA COLLECTION SC  
    go  
    CREATE XML SCHEMA COLLECTION SC AS '<schema xmlns="http://www.w3.org/2001/XMLSchema"   
    targetNamespace="myNS" xmlns:ns="myNS"  
    xmlns:s="https://schemas.microsoft.com/sqlserver/2004/sqltypes">  
          <import namespace="https://schemas.microsoft.com/sqlserver/2004/sqltypes"/>  
          <element name="Elem" type="string"/>  
    </schema>'  
    go  
  
    declare @x xml (SC)  
    set @x='<Elem xmlns="myNS">test</Elem><Elem xmlns="myNS">test2</Elem>'  
    SELECT @x.value('declare namespace x="myNS"; data(/x:Elem)[1]','varchar(20)')  
    ```  
  
     자세한 내용은 [XQuery 및 정적 형식](../xquery/xquery-and-static-typing.md)지정을 참조 하세요.  
  
### <a name="implementation-restrictions"></a>구현 시 제한 사항  
 다음은 정적 컨텍스트와 관련된 제한 사항입니다.  
  
-   XPath 호환성 모드는 지원되지 않습니다.  
  
-   XML 생성의 경우 스트립 생성 모드만 지원됩니다. 이 값은 기본 설정입니다. 따라서 생성 된 요소 노드의 형식은 **xdt: 형식화** 되지 않은 형식이 고 특성은 **xdt: untypedAtomic** type입니다.  
  
-   정렬된 정렬 모드만 지원됩니다.  
  
-   스트립 XML 공백 정책만 지원됩니다.  
  
-   기본 URI 기능은 지원되지 않습니다.  
  
-   **fn: doc ()** 는 지원 되지 않습니다.  
  
-   **fn: collection ()** 은 지원 되지 않습니다.  
  
-   XQuery 정적 플래거는 제공되지 않습니다.  
  
-   **Xml** 데이터 형식과 연결 된 데이터 정렬이 사용 됩니다. 이 데이터 정렬은 항상 유니코드 코드 포인트 데이터 정렬로 설정됩니다.  
  
## <a name="dynamic-context"></a>동적 컨텍스트  
 동적 컨텍스트는 식을 실행할 때 제공되어야 하는 정보를 의미합니다. 정적 컨텍스트 외에도 다음 정보가 동적 컨텍스트의 일부로 초기화됩니다.  
  
-   컨텍스트 항목, 컨텍스트 위치 및 컨텍스트 크기와 같은 식의 중요 항목은 다음에 표시된 것과 같이 초기화됩니다. 이러한 값은 모두 [nodes () 메서드에](../t-sql/xml/nodes-method-xml-data-type.md)의해 재정의 될 수 있습니다.  
  
    -   **Xml** 데이터 형식은 처리 중인 노드인 컨텍스트 항목을 문서 노드로 설정 합니다.  
  
    -   처리 중인 노드에 상대적인 컨텍스트 항목의 위치인 컨텍스트 위치는 처음에 1로 설정됩니다.  
  
    -   처리 중인 시퀀스에 있는 항목 개수인 컨텍스트 크기는 항상 하나의 문서 노드만 있기 때문에 처음에 1로 설정됩니다.  
  
### <a name="implementation-restrictions"></a>구현 시 제한 사항  
 다음은 동적 컨텍스트와 관련된 제한 사항입니다.  
  
-   **현재 날짜 및 시간** 컨텍스트 함수 **fn: current-date**, **fn: current time**및 **fn: current-dateTime**은 지원 되지 않습니다.  
  
-   **암시적 표준 시간대** 는 UTC + 0으로 고정 되며 변경할 수 없습니다.  
  
-   **Fn: doc ()** 함수는 지원 되지 않습니다. 모든 쿼리는 **xml** 유형의 열 또는 변수에 대해 실행 됩니다.  
  
-   **Fn: collection ()** 함수는 지원 되지 않습니다.  
  
## <a name="see-also"></a>참고 항목  
 [XQuery 기본 사항](../xquery/xquery-basics.md)   
 [형식화된 XML과 형식화되지 않은 XML 비교](../relational-databases/xml/compare-typed-xml-to-untyped-xml.md)   
 [XML 스키마 컬렉션&#40;SQL Server&#41;](../relational-databases/xml/xml-schema-collections-sql-server.md)  
  
  
