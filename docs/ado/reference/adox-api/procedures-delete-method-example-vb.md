---
description: Procedures Delete 메서드 예제(VB)
title: 프로시저 Delete 메서드 예제 (VB) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
dev_langs:
- VB
helpviewer_keywords:
- Delete method [ADOX], Visual Basic example
ms.assetid: 94f1ac93-e778-4a40-a85e-94bce5316ac7
author: rothja
ms.author: jroth
ms.openlocfilehash: 16fe01770c486287ff2a188a9c682ffc1e230452
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/27/2020
ms.locfileid: "88983524"
---
# <a name="procedures-delete-method-example-vb"></a>Procedures Delete 메서드 예제(VB)
다음 코드에서는 프로시저 컬렉션의 [delete](./delete-method-adox-collections.md) 메서드를 사용 하 [여 프로시저를](./procedures-collection-adox.md) 삭제 하는 방법을 보여 줍니다.  
  
```  
' BeginDeleteProcedureVB  
Sub Main()  
    On Error GoTo DeleteProcedureError  
  
    Dim cat As New ADOX.Catalog  
  
    ' Open the catalog.  
    cat.ActiveConnection = _  
        "Provider='Microsoft.Jet.OLEDB.4.0';" & _  
        "Data Source='Northwind.mdb';"  
  
    ' Delete the procedure.  
    cat.Procedures.Delete "CustomerById"  
  
    'Clean up.  
    Set cat.ActiveConnection = Nothing  
    Set cat = Nothing  
    Exit Sub  
  
DeleteProcedureError:  
    Set cat = Nothing  
  
    If Err <> 0 Then  
        MsgBox Err.Source & "-->" & Err.Description, , "Error"  
    End If  
End Sub  
' EndDeleteProcedureVB  
```  
  
## <a name="see-also"></a>참고 항목  
 [ActiveConnection 속성 (ADOX)](./activeconnection-property-adox.md)   
 [Catalog 개체 (ADOX)](./catalog-object-adox.md)   
 [Delete 메서드 (ADOX Collections)](./delete-method-adox-collections.md)   
 [Procedure 개체 (ADOX)](./procedure-object-adox.md)   
 [Procedures 컬렉션(ADOX)](./procedures-collection-adox.md)