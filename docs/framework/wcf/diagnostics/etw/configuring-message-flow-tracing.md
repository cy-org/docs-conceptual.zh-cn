---
title: "配置消息流跟踪 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 15571ca2-bee2-47fb-ba10-fcbc09152ad0
caps.latest.revision: 8
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 8
---
# 配置消息流跟踪
启用 [!INCLUDE[indigo1](../../../../../includes/indigo1-md.md)] 活动跟踪后，系统会将端对端活动 ID 分配到整个 [!INCLUDE[indigo2](../../../../../includes/indigo2-md.md)] 堆栈中的逻辑活动。  在 [!INCLUDE[netfx_current_short](../../../../../includes/netfx-current-short-md.md)] 中，此功能现在具备性能更高的版本。它与 Windows 事件跟踪 \(ETW\) 一起使用，称为消息流跟踪。  启用此功能时，端对端活动 ID 取自（如果为空，则分配到）传入消息，并传播到在通道解码消息之后发出的所有跟踪事件。  客户通过此功能，可以在解码来自不同服务的跟踪日志后重新构造消息流。  
  
 检测到应用程序存在问题后，可以启用跟踪，然后在解决问题之后立即禁用跟踪。  
  
## 启用跟踪  
 通过将 .NET Framework 4 `messageFlowTracing` 配置元素设置为 `true`，可以启用消息流跟踪，如下面的示例所示。  
  
```  
<system.servicemodel>  
  <diagnostics>  
    <endToEndTracing propagateActivity="true" messageFlowTracing="true" />  
  </diagnostics>  
</system.servicemodel>  
  
```  
  
> [!NOTE]
>  由于 `endToEndTracing` 配置元素驻留在 Web.config 文件中，因此不能采用与 ETW 一样的方法来动态配置该配置元素。  若要使 `endToEndTracing` 配置元素生效，必须回收应用程序。  
  
 活动通过一个标识符（称为活动 ID）的交换进行关联。  此标识符是 GUID，由 System.Diagnostics.CorrelationManager 类生成。  如果您操作 System.Diagnostics.Trace.CorrelationManager.ActivityID，请确保在执行控制传输回 WCF 代码时，值设置为原始值。  此外，如果您使用异步 WCF 编程模型，请确保在线程之间传输 System.Diagnostics.Trace.CorrelationManager.ActivityID。  
  
## 消息流跟踪和 REST 服务  
 消息流跟踪使您能够端对端跟踪请求。  借助于基于 SOAP 的服务，将在 SOAP 消息标头中发送活动 ID。  REST 请求不包含此标头，因此改用特殊的 HTTP 事件标头。  下面的代码段演示如何以编程方式检索活动 ID的值：  
  
```vb  
  
Object output = null;                    
if (OperationContext.Current.IncomingMessageProperties.TryGetValue(HttpRequestMessageProperty.Name, out output))  
{  
   HttpRequestMessageProperty httpHeaders = output as HttpRequestMessageProperty;       
   // Retrieve the Activity Id from the HTTP header    string e2eId = httpHeaders.Headers["E2EActivity"];  
   // ...  
}  
  
```  
  
 您可以使用下面的代码，以编程方式添加标头：  
  
```csharp  
  
HttpContent content = new StreamContent(contentStream);  
Guid correlation = Guid.NewGuid();  
content.Headers.Add("E2EActivity", Convert.ToBase64String(correlation.ToByteArray()));  
  
```