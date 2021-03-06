---
description: NamedParameters 속성(ADO)
title: NamedParameters 속성 (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- _Command::NamedParameters
helpviewer_keywords:
- NamedParameters property [ADO]
ms.assetid: 42409387-026c-435f-a9b1-bf4167095875
author: rothja
ms.author: jroth
ms.openlocfilehash: 18552a7d15a5dbe36a05c7391d0fd7e2ab3a6d94
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/27/2020
ms.locfileid: "88990494"
---
# <a name="namedparameters-property-ado"></a>NamedParameters 속성(ADO)
매개 변수 이름을 공급자에 게 전달할지 여부를 나타냅니다.  
  
## <a name="remarks"></a>설명  
 이 속성이 true 이면 ADO는 [명령 개체](./command-object-ado.md)의 **매개 변수** 컬렉션에 있는 각 매개 변수의 **Name** 속성 값을 전달 합니다. 공급자는 매개 변수 이름을 사용 하 여 **CommandText** 또는 **commandstream** 속성의 매개 변수를 일치 시킵니다. 이 속성이 false (기본값) 이면 매개 변수 이름이 무시 되 고 공급자가 매개 변수 순서를 사용 하 여 값을 **CommandText** 또는 **commandstream** 속성의 매개 변수와 일치 시킵니다.  
  
## <a name="applies-to"></a>적용 대상  
 [명령 개체(ADO)](./command-object-ado.md)  
  
## <a name="see-also"></a>참고 항목  
 [CommandText 속성 (ADO)](./commandtext-property-ado.md)   
 [CommandStream 속성 (ADO)](./commandstream-property-ado.md)   
 [Parameters 컬렉션(ADO)](./parameters-collection-ado.md)