---
title: "如何：以异步方式调用 WCF 服务操作 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 0face17f-43ca-417b-9b33-737c0fc360df
caps.latest.revision: 18
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 18
---
# 如何：以异步方式调用 WCF 服务操作
本主题介绍客户端如何以异步方式访问服务操作。本主题中的服务可实现 `ICalculator` 接口。通过使用事件驱动的异步调用模型，客户端可以对此接口异步调用操作。（有关基于事件的详细信息基于异步调用模型，请参阅 [使用基于事件的异步模式的多线程编程](http://go.microsoft.com/fwlink/?LinkId=248184)）。有关演示如何在服务中异步实现操作的示例，请参见[如何：实现异步服务操作](../../../../docs/framework/wcf/how-to-implement-an-asynchronous-service-operation.md)。有关同步操作和异步操作的更多信息，请参见[同步和异步操作](../../../../docs/framework/wcf/synchronous-and-asynchronous-operations.md)。  
  
> [!NOTE]
>  使用 <xref:System.ServiceModel.ChannelFactory%601> 时，不支持事件驱动的异步调用模型。有关使用 <xref:System.ServiceModel.ChannelFactory%601> 进行异步调用的信息，请参见[如何：使用通道工厂以异步方式调用操作](../../../../docs/framework/wcf/feature-details/how-to-call-operations-asynchronously-using-a-channel-factory.md)。  
  
## 过程  
  
#### 以异步方式调用 WCF 服务操作  
  
1.  运行同时带有 `/async` 和 `/tcv:Version35` 命令选项的 [ServiceModel 元数据实用工具 \(Svcutil.exe\)](../../../../docs/framework/wcf/servicemodel-metadata-utility-tool-svcutil-exe.md) 工具，如下面的命令所示。  
  
    ```  
    svcutil /n:http://Microsoft.ServiceModel.Samples,Microsoft.ServiceModel.Samples http://localhost:8000/servicemodelsamples/service/mex /a /tcv:Version35  
    ```  
  
     除了同步操作和基于委托的标准异步操作之外，此操作还会生成 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 客户端类，其中包含以下内容：  
  
    -   两个与基于事件的异步调用方法一起使用的 \<`operationName`\>`Async` 操作。例如：  
  
         [!code-csharp[EventAsync#1](../../../../samples/snippets/csharp/VS_Snippets_CFX/eventasync/cs/generatedclient.cs#1)]
         [!code-vb[EventAsync#1](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/eventasync/vb/generatedclient.vb#1)]  
  
    -   与基于事件的异步调用方法一起使用且形式为 \<`operationName`\>`Completed` 的操作完成事件。例如：  
  
         [!code-csharp[EventAsync#2](../../../../samples/snippets/csharp/VS_Snippets_CFX/eventasync/cs/generatedclient.cs#2)]
         [!code-vb[EventAsync#2](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/eventasync/vb/generatedclient.vb#2)]  
  
    -   与基于事件的异步调用方法一起使用的每个操作的 <xref:System.EventArgs?displayProperty=fullName> 类型（形式为 \<`operationName`\>`CompletedEventArgs`）。例如：  
  
         [!code-csharp[EventAsync#3](../../../../samples/snippets/csharp/VS_Snippets_CFX/eventasync/cs/generatedclient.cs#3)]
         [!code-vb[EventAsync#3](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/eventasync/vb/generatedclient.vb#3)]  
  
2.  在调用应用程序中，创建一个要在异步操作完成时调用的回调方法，如下面的示例代码所示。  
  
     [!code-csharp[EventAsync#4](../../../../samples/snippets/csharp/VS_Snippets_CFX/eventasync/cs/client.cs#4)]
     [!code-vb[EventAsync#4](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/eventasync/vb/client.vb#4)]  
  
3.  调用该操作之前，请使用 \<`operationName`\>`EventArgs` 类型的新泛型 <xref:System.EventHandler%601?displayProperty=fullName>，将处理程序方法（在上一步中创建）添加到 \<`operationName`\>`Completed` 事件。然后，调用 \<`operationName`\>`Async` 方法。例如：  
  
     [!code-csharp[EventAsync#5](../../../../samples/snippets/csharp/VS_Snippets_CFX/eventasync/cs/client.cs#5)]
     [!code-vb[EventAsync#5](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/eventasync/vb/client.vb#5)]  
  
## 示例  
  
> [!NOTE]
>  基于事件的异步模型设计准则规定，如果返回了多个值，则一个值会作为 `Result` 属性返回，其他值会作为 <xref:System.EventArgs> 对象上的属性返回。因此产生的结果之一是，如果客户端使用基于事件的异步命令选项导入元数据，且该操作返回多个值，则默认的 <xref:System.EventArgs> 对象返回一个值作为 `Result` 属性，返回的其余值是 <xref:System.EventArgs> 对象的属性。如果要将消息对象作为 `Result` 属性来接收并要使返回的值作为该对象上的属性，请使用 `/messageContract` 命令选项。这会生成一个签名，该签名会将响应消息作为 <xref:System.EventArgs> 对象上的 `Result` 属性返回。然后，所有内部返回值就都是响应消息对象的属性了。  
  
 [!code-csharp[EventAsync#6](../../../../samples/snippets/csharp/VS_Snippets_CFX/eventasync/cs/client.cs#6)]
 [!code-vb[EventAsync#6](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/eventasync/vb/client.vb#6)]  
  
## 请参阅  
 [如何：实现异步服务操作](../../../../docs/framework/wcf/how-to-implement-an-asynchronous-service-operation.md)