---
description: updateNCharacterStream 메서드(int, java.io.Reader, long)
title: updateNCharacterStream 메서드(int, java.io.Reader, long) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: aeec0a56-038e-45b1-98c8-b1046ebd25db
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 17e2d51566ce037813184d8cd22cf84bcff8fc99
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88478383"
---
# <a name="updatencharacterstream-method-int-javaioreader-long"></a>updateNCharacterStream 메서드(int, java.io.Reader, long)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  지정된 열을 지정된 바이트 수를 포함하는 문자 스트림 값으로 업데이트합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
public void updateNCharacterStream(int columnIndex,  
                                    java.io.Reader x,  
                                    long length)  
```  
  
#### <a name="parameters"></a>매개 변수  
 *columnIndex*  
  
 열 인덱스를 나타내는 **int**입니다.  
  
 *x*  
  
 Reader 개체입니다.  
  
 *length*  
  
 스트림의 길이입니다.  
  
## <a name="exceptions"></a>예외  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>설명  
 이 updateNCharacterStream 메서드는 java.sql.ResultSet 인터페이스의 updateNCharacterStream 메서드에 의해 지정됩니다.  
  
 이 메서드는 Reader 개체의 유니코드 문자를 선택된 **nchar**, **nvarchar(max)** , **ntext** 및 **xml** 열에 전달합니다. 다른 데이터 형식 열에 이 메서드를 사용하면 예외가 발생합니다.  
  
 스트림의 길이가 *length* 매개 변수에 지정된 길이와 다르면 행이 업데이트되거나 삽입될 때 JDBC 드라이버에서 예외가 발생합니다.  
  
 스트림의 길이를 알 수 없으면 *length* 매개 변수는 드라이버에서 스트림의 길이에 상관없이 스트림을 허용해야 함을 나타내는 -1로 설정될 수 있습니다. sqljdbc4.jar을 사용하면 애플리케이션에서 길이를 알 수 없는 스트림에서 열을 업데이트하려고 할 때 JDBC 4.0 메서드 [updateNCharacterStream 메서드&#40;int, java.io.Reader&#41;](../../../connect/jdbc/reference/updatencharacterstream-method-int-java-io-reader.md)를 사용하는 것이 좋습니다.  
  
## <a name="see-also"></a>참고 항목  
 [updateNCharacterStream 메서드&#40;SQLServerResultSet&#41;](../../../connect/jdbc/reference/updatencharacterstream-method-sqlserverresultset.md)   
 [SQLServerResultSet 멤버](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [SQLServerResultSet 클래스](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
