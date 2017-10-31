---
title: "最佳做法：中介 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 2d41b337-8132-4ac2-bea2-6e9ae2f00f8d
caps.latest.revision: 2
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 2
---
# 最佳做法：中介
当调用中介机构，以确保中介服务端通道已正确关闭时必须小心，正确处理故障。  
  
 请考虑下列情形。客户端调用中介机构，然后中介机构调用一个后端服务。后端服务定义没有故障合同，因此任何故障引发从该服务将被视为一个泛型故障。后端服务引发<xref:System.ApplicationException>和 WCF 正确中止服务端信道。<xref:System.ApplicationException>然后曲面作为  <xref:System.ServiceModel.FaultException>，则会引发向中介人。中介机构重新引发 <xref:System.ApplicationException>.WCF 将此解释为从中介泛型故障，并将其转发给客户端。在收到故障、中介组织和客户端故障其客户端\-端通道。中介机构的服务端信道因为WCF不知道故障仍保持打开的不过是致命。  
  
 在此方案中，最佳做法是检测如果来自该服务的故障是致命，若然中介机构应故障及其服务\-侧信道，如以下代码片段中所示。  
  
```csharp  
catch (Exception e)  
{  
    bool faulted = service.State == CommunicationState.Faulted;  
    service.Abort();  
    if (faulted)  
    {  
        throw new ApplicationException(e.Message);  
    }  
    Else  
    {  
        throw;  
    }  
}  
  
```  
  
## 请参阅  
 [WCF 错误处理](../../../docs/framework/wcf/wcf-error-handling.md)   
 [在协定和服务中指定和处理错误](../../../docs/framework/wcf/specifying-and-handling-faults-in-contracts-and-services.md)