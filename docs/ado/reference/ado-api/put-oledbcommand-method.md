---
description: put_OLEDBCommand 메서드
title: put_OLEDBCommand 메서드 | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- put_OLEDBCommand method [ADO]
ms.assetid: ca6a5804-bf5c-4afc-99db-22904bc0b33d
author: rothja
ms.author: jroth
ms.openlocfilehash: 5239a1b1924cb767d0425b2a6c686fc15607a08a
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/27/2020
ms.locfileid: "88989944"
---
# <a name="put_oledbcommand-method"></a>put_OLEDBCommand 메서드
이 메서드는 작업을 수행 하지 않으며 항상 S_OK을 반환 합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
HRESULT put_OLEDBCommand(  
      IUnknown *pOLEDBCommand  
);  
```  
  
#### <a name="parameters"></a>매개 변수  
 *pOLEDBCommand*  
 진행 OLE DB Command 개체에 대 한 포인터입니다.  
  
## <a name="applies-to"></a>적용 대상  
 [IADOCommandConstruction](/previous-versions/windows/desktop/aa965677(v=vs.85))