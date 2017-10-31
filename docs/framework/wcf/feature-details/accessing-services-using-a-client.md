---
title: "使用客户端访问服务 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: c8329832-bf66-4064-9034-bf39f153fc2d
caps.latest.revision: 15
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 15
---
# 使用客户端访问服务
客户端应用程序必须创建、配置和使用 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 客户端或通道对象，以便与服务进行通信。  [WCF 客户端概述](../../../../docs/framework/wcf/wcf-client-overview.md)主题概述与创建并使用基本客户端和通道对象有关的对象和步骤。  
  
 本主题提供有关某些客户端应用程序问题以及客户端和通道对象问题的详细信息，根据方案的具体情况，这些信息可能会有用处。  
  
## 概述  
 本主题描述与以下内容相关的行为和问题：  
  
-   通道和会话生存期。  
  
-   处理异常。  
  
-   了解阻塞问题。  
  
-   以交互方式初始化通道。  
  
### 通道和会话生存期  
 [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] 应用程序包含两个类别的通道：数据报通道和会话通道。  
  
 “数据报通道”是指通道内的所有消息都无关联的通道。  使用数据报通道时，如果输入或输出操作失败，下一个操作通常不会受到影响，并且同一个通道可以重用。  因此，数据报通道通常不会出错。  
  
 与其相反，“会话通道”是与另一个终结点有连接的通道。  某一端会话中的消息总是与另一端的同一会话相关联。  另外，会话的两个参与者必须商定，只有彼此的对话要求得到满足，才能认为该会话是成功的。  如果他们无法商定，则会话通道可能会出错。  
  
 通过调用第一个操作显式或隐式打开客户端。  
  
> [!NOTE]
>  试图显式检测出错的会话通道通常是没有用处的，因为您何时得到通知取决于会话实现。  例如，因为 <xref:System.ServiceModel.NetTcpBinding?displayProperty=fullName>（禁用了可靠会话）表现了 TCP 连接会话的状态，所以，如果您在服务或客户端上侦听 <xref:System.ServiceModel.ICommunicationObject.Faulted?displayProperty=fullName> 事件，则在出现网络故障时，您可能会很快得到通知。  但是，可靠会话（由启用了 <xref:System.ServiceModel.Channels.ReliableSessionBindingElement?displayProperty=fullName> 的绑定建立）旨在防止服务受到小型网络故障的影响。  如果可以在一段合理的时间内重新建立会话，则同一绑定（为可靠会话而配置）可能不会出错，除非中断持续了一段较长的时间。  
  
 默认情况下，大多数由系统提供的绑定（它们向应用程序层公开通道）都使用会话，但 <xref:System.ServiceModel.BasicHttpBinding?displayProperty=fullName> 不使用会话。  [!INCLUDE[crdefault](../../../../includes/crdefault-md.md)] [使用会话](../../../../docs/framework/wcf/using-sessions.md).  
  
### 正确使用会话  
 会话提供了一种了解整个消息交换是否已完成以及会话双方是否都认为交换成功的方式。  建议让调用应用程序在一个 try 块内打开、使用和关闭通道。  如果会话通道打开，然后调用了一次 <xref:System.ServiceModel.ICommunicationObject.Close%2A?displayProperty=fullName> 方法，并且该调用成功返回，则会话是成功的。  在此情况下，成功意味着绑定所指定的所有传递保证都得到满足，并且另一方在调用 <xref:System.ServiceModel.ICommunicationObject.Close%2A> 之前没有对通道调用 <xref:System.ServiceModel.ICommunicationObject.Abort%2A?displayProperty=fullName>。  
  
 下一节提供了此客户端方法的一个示例。  
  
### 处理异常  
 在客户端应用程序中处理异常是非常简单的。  如果在一个 try 块内打开、使用并关闭通道，则除非引发了异常，否则对话都是成功的。  通常情况下，如果引发了异常，则会中止对话。  
  
> [!NOTE]
>  建议不要使用 `using` 语句（在 [!INCLUDE[vbprvb](../../../../includes/vbprvb-md.md)] 中为 `Using`）。  这是因为 `using` 语句的末尾会引发异常，这些异常会屏蔽您可能需要了解的其他异常。  [!INCLUDE[crdefault](../../../../includes/crdefault-md.md)] [避免出现与 Using 语句有关的问题](../../../../docs/framework/wcf/samples/avoiding-problems-with-the-using-statement.md).  
  
 下面的代码示例演示使用 try\/catch 块而不是 `using` 语句的推荐客户端模式。  
  
 [!code-csharp[FaultContractAttribute#3](../../../../samples/snippets/csharp/VS_Snippets_CFX/faultcontractattribute/cs/client.cs#3)]
 [!code-vb[FaultContractAttribute#3](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/faultcontractattribute/vb/client.vb#3)]  
  
> [!NOTE]
>  检查 <xref:System.ServiceModel.ICommunicationObject.State%2A?displayProperty=fullName> 属性的值是一个争用条件，建议不要使用此检查来确定是重用还是关闭通道。  
  
 即使在关闭数据报通道时出现异常，这些通道也从来不会出错。  另外，使用安全对话但未能通过身份验证的非双工客户端通常会引发 <xref:System.ServiceModel.Security.MessageSecurityException?displayProperty=fullName>。  但是，与此不同的是，如果使用安全对话的双工客户端未能通过身份验证，该客户端会收到 <xref:System.TimeoutException?displayProperty=fullName>。  
  
 有关在应用程序级处理错误信息的更多详细信息，请参见[在协定和服务中指定和处理错误](../../../../docs/framework/wcf/specifying-and-handling-faults-in-contracts-and-services.md)。  [预期异常](../../../../docs/framework/wcf/samples/expected-exceptions.md)介绍预期的异常并说明如何处理它们。  [!INCLUDE[crabout](../../../../includes/crabout-md.md)]如何在开发通道时处理错误的更多信息，请参见[处理异常和错误](../../../../docs/framework/wcf/extending/handling-exceptions-and-faults.md)。  
  
### 客户端阻塞和性能  
 当应用程序同步调用请求\-答复操作时，客户端会阻塞，直到接收到返回值或引发异常（例如 <xref:System.TimeoutException?displayProperty=fullName>）为止。  此行为与本地行为类似。  当应用程序同步调用 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 客户端对象或通道上的操作时，客户端将直到通道层可以向网络写入数据或引发异常时才返回。  虽然单向消息交换模式（通过标记操作来指定，即将 <xref:System.ServiceModel.OperationContractAttribute.IsOneWay%2A?displayProperty=fullName> 设置为 `true`）可以使某些客户端更快做出响应，但是根据绑定和已经发送的消息的性质，单向操作也可能阻塞。  单向操作仅与消息交换有关。  [!INCLUDE[crdefault](../../../../includes/crdefault-md.md)] [单向服务](../../../../docs/framework/wcf/feature-details/one-way-services.md).  
  
 无论使用何种消息交换模式，大的数据块都会降低客户端的处理速度。  若要了解如何处理这些问题，请参见[大型数据和流](../../../../docs/framework/wcf/feature-details/large-data-and-streaming.md)。  
  
 如果应用程序在操作完成过程中必须做更多的工作，则应在 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 客户端实现的服务协定接口上创建一个异步方法对。  完成此任务的最简单方法是使用 [ServiceModel 元数据实用工具 \(Svcutil.exe\)](../../../../docs/framework/wcf/servicemodel-metadata-utility-tool-svcutil-exe.md) 上的 `/async` 开关。  有关示例，请参见[如何：以异步方式调用服务操作](../../../../docs/framework/wcf/feature-details/how-to-call-wcf-service-operations-asynchronously.md)。  
  
 [!INCLUDE[crabout](../../../../includes/crabout-md.md)]提高客户端性能的更多信息，请参见[中间层客户端应用程序](../../../../docs/framework/wcf/feature-details/middle-tier-client-applications.md)。  
  
### 使用户可以动态选择凭据  
 <xref:System.ServiceModel.Dispatcher.IInteractiveChannelInitializer> 接口使应用程序可以显示一个用户界面，用户可以使用该界面选择凭据，以便用来在超时计时器启动之前创建通道。  
  
 应用程序开发人员可以通过两种方式利用一个插入的 <xref:System.ServiceModel.Dispatcher.IInteractiveChannelInitializer>。  客户端应用程序可以在打开通道之前调用 <xref:System.ServiceModel.ClientBase%601.DisplayInitializationUI%2A?displayProperty=fullName> 或 <xref:System.ServiceModel.IClientChannel.DisplayInitializationUI%2A?displayProperty=fullName> 或异步版本（显式方法），也可以调用第一个操作（隐式方法）。  
  
 如果使用隐式方法，则应用程序必须调用 <xref:System.ServiceModel.ClientBase%601> 或 <xref:System.ServiceModel.IClientChannel> 扩展上的第一个操作。  如果它调用除第一个操作以外的任何操作，则将引发异常。  
  
 如果使用显式方法，应用程序必须按顺序执行下面的操作：  
  
1.  调用 <xref:System.ServiceModel.ClientBase%601.DisplayInitializationUI%2A?displayProperty=fullName> 或 <xref:System.ServiceModel.IClientChannel.DisplayInitializationUI%2A?displayProperty=fullName>（或异步版本）。  
  
2.  当初始值设定项已返回时，针对 <xref:System.ServiceModel.IClientChannel> 对象或从 <xref:System.ServiceModel.ClientBase%601.InnerChannel%2A?displayProperty=fullName> 属性返回的 <xref:System.ServiceModel.IClientChannel> 对象来调用 <xref:System.ServiceModel.ICommunicationObject.Open%2A> 方法。  
  
3.  调用操作。  
  
 建议通过采用显式方法，由可投入实际生产运行的应用程序来控制用户界面过程。  
  
 使用隐式方法的应用程序调用用户界面初始值设定项，但是如果应用程序的用户没有在绑定的发送超时期限内做出响应，则当用户界面返回时，将引发异常。  
  
## 请参阅  
 [双工服务](../../../../docs/framework/wcf/feature-details/duplex-services.md)   
 [如何：使用单向和请求\-答复协定访问服务](../../../../docs/framework/wcf/feature-details/how-to-access-wcf-services-with-one-way-and-request-reply-contracts.md)   
 [如何：使用双工协定访问服务](../../../../docs/framework/wcf/feature-details/how-to-access-services-with-a-duplex-contract.md)   
 [如何：访问 WSE 3.0 服务](../../../../docs/framework/wcf/feature-details/how-to-access-a-wse-3-0-service-with-a-wcf-client.md)   
 [如何：使用 ChannelFactory](../../../../docs/framework/wcf/feature-details/how-to-use-the-channelfactory.md)   
 [如何：以异步方式调用服务操作](../../../../docs/framework/wcf/feature-details/how-to-call-wcf-service-operations-asynchronously.md)   
 [中间层客户端应用程序](../../../../docs/framework/wcf/feature-details/middle-tier-client-applications.md)