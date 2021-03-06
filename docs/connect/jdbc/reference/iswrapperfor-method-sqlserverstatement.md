---
description: isWrapperFor 메서드(SQLServerStatement)
title: isWrapperFor 메서드(SQLServerStatement) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 53f3291f-d43a-476b-a656-d86168dacf6c
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: a4eaf93ee14ced763099ae6080775df5eac2d750
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88433305"
---
# <a name="iswrapperfor-method-sqlserverstatement"></a>isWrapperFor 메서드(SQLServerStatement)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  이 문 개체가 지정된 인터페이스에 대한 래퍼인지 여부를 나타냅니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
public boolean isWrapperFor(Class iface)  
```  
  
#### <a name="parameters"></a>매개 변수  
 *iface*  
  
 인터페이스를 정의하는 **클래스**입니다.  
  
## <a name="return-value"></a>반환 값  
 이 개체가 인터페이스를 구현하거나 인터페이스를 구현하는 개체를 래핑하면 **true**이고, 그렇지 않으면 **false**입니다.  
  
## <a name="exceptions"></a>예외  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>설명  
 [isWrapperFor](../../../connect/jdbc/reference/iswrapperfor-method-sqlserverstatement.md) 메서드와 [unwrap](../../../connect/jdbc/reference/unwrap-method-sqlserverstatement.md) 메서드는 JDBC 4.0에서 도입된 java.sql.Wrapper 인터페이스에 의해 정의됩니다.  
  
 이 메서드가 true를 반환하는 경우 동일한 인수로 [unwrap](../../../connect/jdbc/reference/unwrap-method-sqlserverstatement.md)을 호출하는 데 성공합니다.  
  
 예제 코드는 [대규모 데이터 업데이트 샘플](../../../connect/jdbc/updating-large-data-sample.md)을 참조하세요.  
  
 자세한 내용은 [래퍼 및 인터페이스](../../../connect/jdbc/wrappers-and-interfaces.md)를 참조하세요.  
  
## <a name="see-also"></a>참고 항목  
 [unwrap 메서드&#40;SQLServerStatement&#41;](../../../connect/jdbc/reference/unwrap-method-sqlserverstatement.md)   
 [SQLServerStatement 멤버](../../../connect/jdbc/reference/sqlserverstatement-members.md)   
 [SQLServerStatement 클래스](../../../connect/jdbc/reference/sqlserverstatement-class.md)  
  
  
