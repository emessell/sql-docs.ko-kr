---
description: setClob 메서드(int, java.io.Reader)
title: setClob 메서드(int, java.io.Reader) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 2b3727da-0480-4cea-b8b1-abda90699b84
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 93c869b07771ef3223901948cb5ce6ccb13d59ee
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88432165"
---
# <a name="setclob-method-int-javaioreader"></a>setClob 메서드(int, java.io.Reader)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  지정된 매개 변수를 지정된 Reader 개체로 설정합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
public final void setClob(int parameterIndex,  
                          java.io.Reader reader)  
```  
  
#### <a name="parameters"></a>매개 변수  
 *parameterIndex*  
  
 매개 변수 인덱스를 나타내는 **int**입니다.  
  
 *reader*  
  
 Reader 개체입니다.  
  
## <a name="exceptions"></a>예외  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>설명  
 이 setClob 메서드는 java.sql.PreparedStatement 인터페이스의 setClob 메서드에 의해 지정됩니다.  
  
## <a name="see-also"></a>참고 항목  
 [setClob 메서드&#40;SQLServerPreparedStatement&#41;](../../../connect/jdbc/reference/setclob-method-sqlserverpreparedstatement.md)   
 [SQLServerPreparedStatement 멤버](../../../connect/jdbc/reference/sqlserverpreparedstatement-members.md)  
  
  
