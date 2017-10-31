---
title: "使用会话 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "会话 [WCF]"
ms.assetid: 864ba12f-3331-4359-a359-6d6d387f1035
caps.latest.revision: 32
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 32
---
# 使用会话
在 [!INCLUDE[indigo1](../../../includes/indigo1-md.md)] 应用程序中，“会话”将一组消息相互关联，从而形成对话。[!INCLUDE[indigo2](../../../includes/indigo2-md.md)] 会话与 [!INCLUDE[vstecasp](../../../includes/vstecasp-md.md)] 应用程序中提供的会话对象不同，它们支持不同的行为，并且可通过不同的方式进行控制。 本主题描述了会话在 [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] 应用程序中启用的功能以及如何使用这些功能。  
  
## Windows Communication Foundation 应用程序中的会话  
 当某个服务协定指定它需要会话时，该协定会指定所有调用（即，支持调用的基础消息交换）必须是同一对话的一部分。 如果某个协定指定它允许使用会话但不要求使用会话，则客户端可以进行连接，并选择建立会话或不建立会话。 如果会话结束，然后在同一个通道上发送消息，将会引发异常。  
  
 [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] 会话具有下列主要概念性功能：  
  
-   它们由调用应用程序（WCF 客户端）显式启动和终止。  
  
-   会话期间传递的消息按照接收消息的顺序进行处理。  
  
-   会话将一组消息相互关联，从而形成对话。 可以有不同类型的关联。 例如，一个基于会话的通道可能会根据共享网络连接来关联消息，而另一个基于会话的通道可能会根据消息正文中的共享标记来关联消息。 可以从会话派生的功能取决于关联的性质。  
  
-   不存在与 [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] 会话相关联的常规数据存储区。  
  
 如果您熟悉 <xref:System.Web.SessionState.HttpSessionState?displayProperty=fullName> 应用程序中的 [!INCLUDE[vstecasp](../../../includes/vstecasp-md.md)] 类以及该类提供的功能，则您可能会注意到，该类型的会话和 [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] 会话之间存在以下区别：  
  
-   [!INCLUDE[vstecasp](../../../includes/vstecasp-md.md)] 会话总是由服务器启动。  
  
-   [!INCLUDE[vstecasp](../../../includes/vstecasp-md.md)] 会话原本是无序的。  
  
-   [!INCLUDE[vstecasp](../../../includes/vstecasp-md.md)] 会话提供了一种跨请求的常规数据存储机制。  
  
 本主题描述：  
  
-   在服务模型层中使用基于会话的绑定时的默认执行行为。  
  
-   基于 [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] 会话的、系统提供的绑定所提供的功能的类型。  
  
-   如何创建声明会话要求的协定。  
  
-   如何了解和控制会话的创建和终止以及会话与服务实例的关系。  
  
## 使用会话的默认执行行为  
 尝试启动会话的绑定称为基于会话的绑定。 通过将服务协定接口（或类）上的 <xref:System.ServiceModel.ServiceContractAttribute.SessionMode%2A?displayProperty=fullName> 属性设置为 <xref:System.ServiceModel.SessionMode?displayProperty=fullName> 枚举值之一，服务协定指定它们要求、允许或拒绝基于会话的绑定。 默认情况下，此属性的值为 <xref:System.ServiceModel.SessionMode>，这意味着，如果客户端将基于会话的绑定用于 [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] 服务实现，则服务将建立并使用提供的会话。  
  
 当 [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] 服务接受客户端会话时，默认情况下启用以下功能：  
  
1.  通过同一服务实例来处理 [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] 客户端对象之间的所有调用。  
  
2.  不同的基于会话的绑定还会提供其他功能。  
  
## 系统提供的会话类型  
 基于会话的绑定支持服务实例与特定会话的默认关联。 但是，除了启用前面介绍的基于会话的实例化控制之外，不同的基于会话的绑定还支持不同的功能。  
  
 [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] 提供下列类型的基于会话的应用程序行为：  
  
-   <xref:System.ServiceModel.Channels.SecurityBindingElement?displayProperty=fullName> 支持基于安全的会话，其中，两个通信端采用统一的安全对话。[!INCLUDE[crdefault](../../../includes/crdefault-md.md)] [保证服务的安全](../../../docs/framework/wcf/securing-services.md). 例如，<xref:System.ServiceModel.WSHttpBinding?displayProperty=fullName> 绑定（包含对安全会话和可靠会话的支持）默认情况下只使用对消息进行加密和数字签名的安全会话。  
  
-   <xref:System.ServiceModel.NetTcpBinding?displayProperty=fullName> 绑定支持基于 TCP\/IP 的会话，以确保所有消息都由套接字级别的连接进行关联。  
  
-   <xref:System.ServiceModel.Channels.ReliableSessionBindingElement?displayProperty=fullName> 元素实现 WS\-ReliableMessaging 规范，并提供对可靠会话的支持。在可靠会话中，可以配置消息以按顺序传递并且只传递一次，从而使消息在对话期间即使经过多个节点也可以确保收到。[!INCLUDE[crdefault](../../../includes/crdefault-md.md)] [可靠会话](../../../docs/framework/wcf/feature-details/reliable-sessions.md).  
  
-   <xref:System.ServiceModel.NetMsmqBinding?displayProperty=fullName> 绑定提供 MSMQ 数据报会话。[!INCLUDE[crdefault](../../../includes/crdefault-md.md)] [WCF 中的队列](../../../docs/framework/wcf/feature-details/queues-in-wcf.md).  
  
 设置 <xref:System.ServiceModel.ServiceContractAttribute.SessionMode%2A> 属性并不指定协定需要的会话类型，而只是指定协定需要一个会话。  
  
## 创建一个需要会话的协定  
 创建需要会话的协定的原则是，必须在同一会话内执行服务协定声明的所有操作组，并且必须按顺序传递消息。 若要断言服务协定需要的会话支持级别，请将服务协定接口或类上的 <xref:System.ServiceModel.ServiceContractAttribute.SessionMode%2A?displayProperty=fullName> 属性设置为 <xref:System.ServiceModel.SessionMode?displayProperty=fullName> 枚举的值以指定协定是否：  
  
-   需要会话。  
  
-   允许客户端建立会话。  
  
-   禁止会话。  
  
 但是，设置 <xref:System.ServiceModel.ServiceContractAttribute.SessionMode%2A> 属性并不指定协定需要的基于会话的行为的类型。 它指示 [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] 在运行时确认：在实现服务时，为服务配置的绑定（用于创建通信通道）是执行会话、不执行会话还是可以建立会话。 同样，绑定可以使用它选择的任何类型的基于会话的行为（安全、传输、可靠或某种组合）来满足该要求。 具体的行为取决于选择的 <xref:System.ServiceModel.SessionMode?displayProperty=fullName> 值。 如果为服务配置的绑定不符合 <xref:System.ServiceModel.ServiceContractAttribute.SessionMode%2A> 的值，则会引发异常。 绑定及其创建的支持会话的通道可认为是基于会话的。  
  
 下面的服务协定指定 `ICalculatorSession` 中的所有操作必须在会话中进行交换。 除了 `Equals` 方法之外，任何操作都不会向调用方返回值。 但是，`Equals` 方法不使用参数，因此，在已将其中的数据传递到其他操作的会话内部只可以返回非零值。 此协定需要会话正常工作。 如果没有与特定客户端相关联的会话，则服务实例无法知道此客户端前面已经发送了哪些数据。  
  
 [!code-csharp[S_Service_Session#1](../../../samples/snippets/csharp/VS_Snippets_CFX/s_service_session/cs/service.cs#1)]
 [!code-vb[S_Service_Session#1](../../../samples/snippets/visualbasic/VS_Snippets_CFX/s_service_session/vb/service.vb#1)]  
  
 如果服务允许会话，则当客户端启动一个会话时将建立并使用该会话；否则，不建立会话。  
  
## 会话和服务实例  
 如果使用 [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] 中的默认实例化行为，则通过同一服务实例来处理 [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] 客户端对象之间的所有调用。 因此，在应用程序级别上，可以将会话视为启用与本地调用行为相似的应用程序行为。 例如，在创建本地对象时：  
  
-   调用构造函数。  
  
-   由同一个对象实例来处理对 [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] 客户端对象引用所做的所有后续调用。  
  
-   在销毁对象引用时调用析构函数。  
  
 只要使用默认的服务实例行为，会话就会在客户端和服务之间启用一个相似的行为。 如果服务协定需要或支持会话，则通过设置 <xref:System.ServiceModel.OperationContractAttribute.IsInitiating%2A> 和 <xref:System.ServiceModel.OperationContractAttribute.IsTerminating%2A> 属性，可以将一个或多个协定操作标记为启动或终止会话。  
  
 启动操作是必须作为新会话的第一个操作而调用的操作。 只有在已调用至少一个启动操作之后才可以调用非启动操作。 因此，可以通过声明一个启动操作来为服务创建某种会话构造函数，启动操作应设计为从与服务实例的开始相对应的客户端接收输入。 （状态与会话相关联，但是，不与服务对象相关联。）  
  
 相反，终止操作是必须作为现有会话中的最后消息而调用的操作。 默认情况下，在关闭与服务关联的会话之后，[!INCLUDE[indigo2](../../../includes/indigo2-md.md)] 将回收服务对象及其上下文。 因此，可以通过声明终止操作来创建某种析构函数，终止操作应设计为执行与服务实例的结束相对应的函数。  
  
> [!NOTE]
>  尽管默认的行为与本地构造函数和析构函数有相似之处，但仅仅是相似。 任何 [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] 服务操作都可以是启动或终止操作，或同时为这两种操作。 另外，在默认情况下，可以按任意顺序调用启动操作任意次数；一旦建立会话并与实例相关联后，便不会再创建其他会话，除非显式控制服务实例的生存期（通过操作 <xref:System.ServiceModel.InstanceContext?displayProperty=fullName> 对象）。 最后，状态与会话相关联，而不是与服务对象相关联。  
  
 例如，在上一实例中使用的 `ICalculatorSession` 协定需要 [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] 客户端对象在任何其他操作之前调用 `Clear` 操作，并且在它调用 [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] 操作时与此 `Equals` 客户端对象的会话应该终止。 下面的代码示例演示强制执行这些要求的协定。 必须首先调用 `Clear` 来启动会话，并且会话在调用 `Equals` 时结束。  
  
 [!code-csharp[SCA.IsInitiatingIsTerminating#1](../../../samples/snippets/csharp/VS_Snippets_CFX/sca.isinitiatingisterminating/cs/service.cs#1)]
 [!code-vb[SCA.IsInitiatingIsTerminating#1](../../../samples/snippets/visualbasic/VS_Snippets_CFX/sca.isinitiatingisterminating/vb/service.vb#1)]  
  
 服务不会启动与客户端的会话。 在 [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] 客户端应用程序中，直接关系存在于基于会话的通道的生存期和会话本身的生存期之间。 因此，客户端可通过创建新的基于会话的通道来创建新会话，并通过正常关闭基于会话的通道来关闭现有的会话。 客户端通过调用以下项目之一来启动与服务终结点的会话：  
  
-   通过调用 <xref:System.ServiceModel.ICommunicationObject.Open%2A?displayProperty=fullName> 返回的通道上的 <xref:System.ServiceModel.ChannelFactory%601.CreateChannel%2A?displayProperty=fullName>。  
  
-   由 [ServiceModel 元数据实用工具 \(Svcutil.exe\)](../../../docs/framework/wcf/servicemodel-metadata-utility-tool-svcutil-exe.md) 生成的 [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] 客户端对象上的 <xref:System.ServiceModel.ClientBase%601.Open%2A?displayProperty=fullName>。  
  
-   任一类型的 [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] 客户端对象上的启动操作（默认情况下，所有操作都会启动）。 当调用第一个操作时，[!INCLUDE[indigo2](../../../includes/indigo2-md.md)] 客户端对象自动打开通道并启动会话。  
  
 通常，客户端通过调用以下项目之一来结束与服务终结点的会话：  
  
-   通过调用 <xref:System.ServiceModel.ICommunicationObject.Close%2A?displayProperty=fullName> 返回的通道上的 <xref:System.ServiceModel.ChannelFactory%601.CreateChannel%2A?displayProperty=fullName>。  
  
-   由 Svcutil.exe 生成的 <xref:System.ServiceModel.ClientBase%601.Close%2A?displayProperty=fullName> 客户端对象上的 [!INCLUDE[indigo2](../../../includes/indigo2-md.md)]。  
  
-   任一类型 [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] 客户端对象上的终止操作（默认情况下，不终止任何操作；协定必须显式指定终止操作）。 当调用第一个操作时，[!INCLUDE[indigo2](../../../includes/indigo2-md.md)] 客户端对象自动打开通道并启动会话。  
  
 有关示例，请参阅[如何：创建要求会话的服务](../../../docs/framework/wcf/feature-details/how-to-create-a-service-that-requires-sessions.md)以及[默认服务行为](../../../docs/framework/wcf/samples/default-service-behavior.md)和[实例化](../../../docs/framework/wcf/samples/instancing.md)示例。  
  
 [!INCLUDE[crabout](../../../includes/crabout-md.md)]客户端和会话，请参阅[使用 WCF 客户端访问服务](../../../docs/framework/wcf/feature-details/accessing-services-using-a-client.md)。  
  
## 会话与 InstanceContext 设置进行交互  
 协定中的 <xref:System.ServiceModel.SessionMode> 枚举与 <xref:System.ServiceModel.ServiceBehaviorAttribute.InstanceContextMode%2A?displayProperty=fullName> 属性之间存在交互，该属性可控制通道和特定服务对象之间的关联。[!INCLUDE[crdefault](../../../includes/crdefault-md.md)] [会话、实例化和并发](../../../docs/framework/wcf/feature-details/sessions-instancing-and-concurrency.md).  
  
### 共享 InstanceContext 对象  
 通过自己执行关联，您还可以控制将哪个基于会话的通道或调用与哪个 <xref:System.ServiceModel.InstanceContext> 对象相关联。 有关完整示例，请参见[InstanceContextSharing](http://msdn.microsoft.com/zh-cn/4a6a46d7-b7d7-4bb5-a0dd-03ffa3cbc230)。  
  
## 会话和流  
 当您有大量的数据要传输时，[!INCLUDE[indigo2](../../../includes/indigo2-md.md)] 中的流传输模式是整个在内存中缓冲和处理消息的默认行为的一个可行的替代方法。 在流与基于会话的绑定一起调用时可能会产生意外行为。 可通过单一通道（数据报通道）执行所有流调用，该通道不支持会话，即使将正在使用的绑定配置为使用会话也是如此。 如果多个客户端通过基于会话的绑定对相同的服务对象进行流调用，并且将服务对象的并发模式设置为 single，同时将其实例上下文模式设置为 `PerSession`，则所用的调用必须经过数据报通道，因此一次只处理一个调用。 一个或多个客户端因此可能会超时。 通过将服务对象的 `InstanceContextMode` 设置为 `PerCall` 或者将 Concurrency 设置为 multiple，可以解决此问题。  
  
> [!NOTE]
>  MaxConcurrentSessions 在此情况下不会产生任何影响，因为只有一个“会话”可用。  
  
## 请参阅  
 <xref:System.ServiceModel.OperationContractAttribute.IsInitiating%2A>   
 <xref:System.ServiceModel.OperationContractAttribute.IsTerminating%2A>