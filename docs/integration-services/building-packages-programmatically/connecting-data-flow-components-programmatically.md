---
description: 프로그래밍 방식으로 데이터 흐름 구성 요소 연결
title: 프로그래밍 방식으로 데이터 흐름 구성 요소 연결 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: reference
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- data flow task [Integration Services], components
- paths [Integration Services], components
- components [Integration Services], data flow
- data flow [Integration Services], components
ms.assetid: 404ecab7-7698-447b-93d6-dd256beb11ff
author: chugugrace
ms.author: chugu
ms.openlocfilehash: f6e577a267121a4e0ed42743b38ab5b5b27f4ebb
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88457820"
---
# <a name="connecting-data-flow-components-programmatically"></a>프로그래밍 방식으로 데이터 흐름 구성 요소 연결

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]


  데이터 흐름 태스크에 구성 요소를 추가한 후 해당 구성 요소를 연결하여 원본에서 변환을 거쳐 대상으로 이동하는 데이터 흐름을 나타내는 실행 트리를 만들 수 있습니다. 데이터 흐름의 구성 요소를 연결하려면 <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSPath100> 개체를 사용합니다.  
  
## <a name="creating-a-path"></a>경로 만들기  
 <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.MainPipe> 인터페이스에 있는 <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.MainPipeClass.PathCollection%2A> 속성의 새 메서드를 호출하여 새 경로를 만들고 이 경로를 데이터 흐름 태스크의 경로 컬렉션에 추가할 수 있습니다. 이 메서드는 연결이 끊어진 새 <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSPath100> 개체를 반환합니다. 그러면 이 개체를 사용하여 두 구성 요소를 연결할 수 있습니다.  
  
 경로를 연결하고 연결된 경로에 참여하는 구성 요소에 해당 구성 요소가 연결되었음을 알리려면 <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSPath100.AttachPathAndPropagateNotifications%2A> 메서드를 호출합니다. 이 메서드는 업스트림 구성 요소의 <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSOutput100>과 다운스트림 구성 요소의 <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSInput100>을 매개 변수로 받아들입니다. 기본적으로 구성 요소의 <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.ProvideComponentProperties%2A> 메서드를 호출하면 입력이 있는 구성 요소에 대한 단일 입력과 출력이 있는 구성 요소에 대한 단일 출력이 만들어집니다. 다음 예에서는 원본의 이 기본 출력과 대상의 입력을 사용합니다.  
  
## <a name="next-step"></a>다음 단계  
 두 구성 요소 간의 경로를 설정한 다음에는 다운스트림 구성 요소의 입력 열을 매핑해야 합니다. 이 단계에 대한 자세한 내용은 다음에 나오는 [프로그래밍 방식으로 입력 열 선택](../../integration-services/building-packages-programmatically/selecting-input-columns-programmatically.md) 항목에서 설명합니다.  
  
## <a name="sample"></a>샘플  
 다음 코드 예제에서는 두 구성 요소 간의 경로를 설정하는 방법을 보여 줍니다.  
  
```csharp  
using System;  
using Microsoft.SqlServer.Dts.Runtime;  
using Microsoft.SqlServer.Dts.Pipeline;  
using Microsoft.SqlServer.Dts.Pipeline.Wrapper;  
  
namespace Microsoft.SqlServer.Dts.Samples  
{  
  class Program  
  {  
    static void Main(string[] args)  
    {  
      Package package = new Package();  
      Executable e = package.Executables.Add("STOCK:PipelineTask");  
      TaskHost thMainPipe = e as TaskHost;  
      MainPipe dataFlowTask = thMainPipe.InnerObject as MainPipe;  
  
      // Create the source component.    
      IDTSComponentMetaData100 source =  
        dataFlowTask.ComponentMetaDataCollection.New();  
      source.ComponentClassID = "DTSAdapter.OleDbSource";  
      CManagedComponentWrapper srcDesignTime = source.Instantiate();  
      srcDesignTime.ProvideComponentProperties();  
  
      // Create the destination component.  
      IDTSComponentMetaData100 destination =  
        dataFlowTask.ComponentMetaDataCollection.New();  
      destination.ComponentClassID = "DTSAdapter.OleDbDestination";  
      CManagedComponentWrapper destDesignTime = destination.Instantiate();  
      destDesignTime.ProvideComponentProperties();  
  
      // Create the path.  
      IDTSPath100 path = dataFlowTask.PathCollection.New();  
      path.AttachPathAndPropagateNotifications(source.OutputCollection[0],  
        destination.InputCollection[0]);  
    }  
  }  
```  
  
 }  
  
```vb  
Imports Microsoft.SqlServer.Dts.Runtime  
Imports Microsoft.SqlServer.Dts.Pipeline  
Imports Microsoft.SqlServer.Dts.Pipeline.Wrapper  
  
Module Module1  
  
  Sub Main()  
  
    Dim package As Microsoft.SqlServer.Dts.Runtime.Package = _  
      New Microsoft.SqlServer.Dts.Runtime.Package()  
    Dim e As Executable = package.Executables.Add("STOCK:PipelineTask")  
    Dim thMainPipe As Microsoft.SqlServer.Dts.Runtime.TaskHost = _  
      CType(e, Microsoft.SqlServer.Dts.Runtime.TaskHost)  
    Dim dataFlowTask As MainPipe = CType(thMainPipe.InnerObject, MainPipe)  
  
    ' Create the source component.    
    Dim source As IDTSComponentMetaData100 = _  
      dataFlowTask.ComponentMetaDataCollection.New()  
    source.ComponentClassID = "DTSAdapter.OleDbSource"  
    Dim srcDesignTime As CManagedComponentWrapper = source.Instantiate()  
    srcDesignTime.ProvideComponentProperties()  
  
    ' Create the destination component.  
    Dim destination As IDTSComponentMetaData100 = _  
      dataFlowTask.ComponentMetaDataCollection.New()  
    destination.ComponentClassID = "DTSAdapter.OleDbDestination"  
    Dim destDesignTime As CManagedComponentWrapper = destination.Instantiate()  
    destDesignTime.ProvideComponentProperties()  
  
    ' Create the path.  
    Dim path As IDTSPath100 = dataFlowTask.PathCollection.New()  
    path.AttachPathAndPropagateNotifications(source.OutputCollection(0), _  
      destination.InputCollection(0))  
  
  End Sub  
  
End Module  
```  
  
## <a name="see-also"></a>참고 항목  
 [프로그래밍 방식으로 입력 열 선택](../../integration-services/building-packages-programmatically/selecting-input-columns-programmatically.md)  
  
  
