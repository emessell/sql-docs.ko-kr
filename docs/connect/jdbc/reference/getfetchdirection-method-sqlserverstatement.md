---
description: getFetchDirection 메서드(SQLServerStatement)
title: getFetchDirection 메서드(SQLServerStatement) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerStatement.getFetchDirection
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: ceb4ae68-decc-46d3-83f1-0bbd23aaf58c
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: b2c42f7296f9bb4ac9cffd68f0d13d5ba7ca920c
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88436045"
---
# <a name="getfetchdirection-method-sqlserverstatement"></a>getFetchDirection 메서드(SQLServerStatement)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  이 [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md) 개체에서 생성된 결과 집합에 기본값으로 사용되는 데이터베이스 테이블에서의 행 인출 방향을 검색합니다.  
  
> [!NOTE]  
>  [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)]에서는 현재 이 메서드가 구현되지 않습니다. 따라서 항상 FETCH_UNKNOWN이 반환됩니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
public final int getFetchDirection()  
```  
  
## <a name="return-value"></a>Return Value  
 [setFetchDirection](../../../connect/jdbc/reference/setfetchdirection-method-sqlserverstatement.md) 메서드로 지정된 인출 방향을 나타내는 **int**입니다.  
  
## <a name="exceptions"></a>예외  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>설명  
 이 getFetchDirection 메서드는 java.sql.Statement 인터페이스의 getFetchDirection 메서드에 의해 지정됩니다.  
  
## <a name="see-also"></a>참고 항목  
 [SQLServerStatement 멤버](../../../connect/jdbc/reference/sqlserverstatement-members.md)   
 [SQLServerStatement 클래스](../../../connect/jdbc/reference/sqlserverstatement-class.md)  
  
  
