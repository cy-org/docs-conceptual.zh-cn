---
title: "扩展客户端 | Microsoft Docs"
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
  - "代理扩展 [WCF]"
ms.assetid: 1328c61c-06e5-455f-9ebd-ceefb59d3867
caps.latest.revision: 17
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 17
---
# 扩展客户端
在调用应用程序中，服务模型层负责将应用程序代码中的方法调用转换成出站消息、将它们推送到基础通道、将结果转换回应用程序代码中的返回值和 out 参数并将结果返回到调用方。服务模型扩展将修改或实现执行或通信行为与功能，包括客户端或调度程序功能、自定义行为、消息和参数截获以及其他扩展功能。  
  
 本主题说明如何在 [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] 应用程序中使用 <xref:System.ServiceModel.Dispatcher.ClientRuntime> 和 <xref:System.ServiceModel.Dispatcher.ClientOperation> 类更改 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 客户端的默认执行行为，或在发送或从通道层检索消息、参数或返回值之前或之后截获或更改它们。有关扩展服务运行时的更多信息，请参见[扩展调度程序](../../../../docs/framework/wcf/extending/extending-dispatchers.md)。有关修改自定义对象和将其插入客户端运行时的行为的更多信息，请参见[使用行为配置和扩展运行时](../../../../docs/framework/wcf/extending/configuring-and-extending-the-runtime-with-behaviors.md)。  
  
## 客户端  
 在客户端上，[!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 客户端对象或客户端通道会将对出站消息和入站消息的方法调用转换为返回到调用应用程序的操作结果。（有关客户端类型的更多信息，请参见[WCF 客户端体系结构](../../../../docs/framework/wcf/feature-details/client-architecture.md)。）  
  
 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 客户端类型具有处理此终结点级别或操作级别功能的运行时类型。当应用程序调用操作时，<xref:System.ServiceModel.Dispatcher.ClientOperation> 会将出站对象转换为消息、处理拦截器、确认出站调用符合目标约定并将出站消息传递给 <xref:System.ServiceModel.Dispatcher.ClientRuntime>，而后者负责创建和管理出站通道（和双工服务情况下的入站通道）、处理额外的出站消息处理（比如标头修改）、处理双向消息拦截器以及将入站双向调用路由到相应的客户端 <xref:System.ServiceModel.Dispatcher.DispatchRuntime> 对象。当消息（包括错误）返回到客户端时，<xref:System.ServiceModel.Dispatcher.ClientOperation> 和 <xref:System.ServiceModel.Dispatcher.ClientRuntime> 提供相似的服务。  
  
 这两个运行时类是自定义 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 客户端对象和通道的处理的主要扩展。<xref:System.ServiceModel.Dispatcher.ClientRuntime> 类允许用户截获和扩展约定中所有消息的客户端执行。<xref:System.ServiceModel.Dispatcher.ClientOperation> 类允许用户截获和扩展给定操作中所有消息的客户端执行。  
  
 修改属性或插入自定义可以通过使用约定、终结点和操作行为来完成。有关如何使用这些类型的行为来执行客户端运行时自定义的更多信息，请参见[使用行为配置和扩展运行时](../../../../docs/framework/wcf/extending/configuring-and-extending-the-runtime-with-behaviors.md)。  
  
## 方案  
 扩展客户端系统有多个理由，包括：  
  
-   自定义消息验证。用户可能需要强制消息对某些架构有效。通过实现 <xref:System.ServiceModel.Dispatcher.IClientMessageInspector> 接口并将该实现分配给 <xref:System.ServiceModel.Dispatcher.DispatchRuntime.MessageInspectors%2A> 属性可以做到这一点。有关示例，请参见[如何：检查或修改客户端的消息](../../../../docs/framework/wcf/extending/how-to-inspect-or-modify-messages-on-the-client.md)和[如何：检查或修改客户端的消息](../../../../docs/framework/wcf/extending/how-to-inspect-or-modify-messages-on-the-client.md)。  
  
-   自定义消息日志记录。用户可能需要检查和记录流过某个终结点的应用程序消息集。此操作也可以使用消息拦截器接口完成。  
  
-   自定义消息转换。用户可能需要在运行时对消息应用某些转换而不修改应用程序代码（例如，对于版本控制）。此操作也可以使用消息拦截器接口完成。  
  
-   自定义数据模型。用户可能需要有 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 中默认支持的数据或序列化模型（即 <xref:System.Runtime.Serialization.DataContractSerializer?displayProperty=fullName>、<xref:System.Xml.Serialization.XmlSerializer?displayProperty=fullName> 和 <xref:System.ServiceModel.Channels.Message?displayProperty=fullName> 对象）之外的数据或序列化模型。这可以通过实现消息格式化程序接口来完成。有关更多信息，请参见 <xref:System.ServiceModel.Dispatcher.IClientMessageFormatter?displayProperty=fullName> 和 <xref:System.ServiceModel.Dispatcher.ClientOperation.Formatter%2A?displayProperty=fullName> 属性。  
  
-   自定义参数验证。用户可能需要强制类型化参数有效（与 XML 相对）。可以使用参数检查器来完成此操作。有关示例，请参见[如何：检查或修改参数](../../../../docs/framework/wcf/extending/how-to-inspect-or-modify-parameters.md)或[客户端验证](../../../../docs/framework/wcf/samples/client-validation.md)。  
  
### 使用 ClientRuntime 类  
 <xref:System.ServiceModel.Dispatcher.ClientRuntime> 类是一个扩展点，您可以将截获消息和扩展客户端行为的扩展对象添加到该扩展点。截获对象可以在特定的约定中处理所有消息，仅处理特定操作的消息，执行自定义通道初始化，以及实现其他自定义客户端应用程序行为。  
  
-   <xref:System.ServiceModel.Dispatcher.ClientRuntime.CallbackDispatchRuntime%2A> 属性返回服务启动的回调客户端的调度运行时对象。  
  
-   <xref:System.ServiceModel.Dispatcher.ClientRuntime.OperationSelector%2A> 属性接受自定义操作选择器对象。  
  
-   使用 <xref:System.ServiceModel.Dispatcher.ClientRuntime.ChannelInitializers%2A> 属性可以添加检查或修改客户端通道的通道初始值设定项。  
  
-   <xref:System.ServiceModel.Dispatcher.ClientRuntime.Operations%2A> 属性获取 <xref:System.ServiceModel.Dispatcher.ClientOperation> 对象的集合，您可以将提供特定于该操作的消息的功能的自定义消息拦截器添加到该集合。  
  
-   使用 <xref:System.ServiceModel.Dispatcher.ClientRuntime.ManualAddressing%2A> 属性，应用程序可以关闭某些自动寻址标头来直接控制寻址。  
  
-   <xref:System.ServiceModel.Dispatcher.ClientRuntime.Via%2A> 属性在传输级别设置消息目标值来支持中介以及其他方案。  
  
-   <xref:System.ServiceModel.Dispatcher.ClientRuntime.MessageInspectors%2A> 属性获取 <xref:System.ServiceModel.Dispatcher.IClientMessageInspector> 对象的集合，您可以将通过 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 客户端的所有消息的自定义消息拦截器添加到该集合。  
  
 另外，还有其他多个属性可以检索约定信息：  
  
-   <xref:System.ServiceModel.Dispatcher.ClientRuntime.ContractName%2A>  
  
-   <xref:System.ServiceModel.Dispatcher.ClientRuntime.ContractNamespace%2A>  
  
-   <xref:System.ServiceModel.Dispatcher.ClientRuntime.ContractClientType%2A>  
  
 如果 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 客户端是双工 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 客户端，以下属性还可以检索回调 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 客户端信息：  
  
-   <xref:System.ServiceModel.Dispatcher.ClientRuntime.CallbackClientType%2A>  
  
-   <xref:System.ServiceModel.Dispatcher.ClientRuntime.CallbackDispatchRuntime%2A>  
  
 若要在整个 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 客户端中扩展 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 客户端执行，请检查 <xref:System.ServiceModel.Dispatcher.ClientRuntime> 类中可用的属性，以查看修改属性或实现接口并将其添加到属性是否可创建您正在寻求的功能。在选择了要生成的特定扩展后，通过实现调用时可访问 <xref:System.ServiceModel.Dispatcher.ClientRuntime> 类的客户端行为来将您的扩展插入相应的 <xref:System.ServiceModel.Dispatcher.ClientRuntime> 属性。  
  
 您可以使用操作行为（实现 <xref:System.ServiceModel.Description.IOperationBehavior> 的对象）、约定行为（实现 <xref:System.ServiceModel.Description.IContractBehavior> 的对象）或终结点行为（实现 <xref:System.ServiceModel.Description.IEndpointBehavior> 的对象）将自定义扩展对象插入到集合中。安装行为对象可以编程方式、声明方式（通过实现自定义属性）或通过实现自定义 <xref:System.ServiceModel.Configuration.BehaviorExtensionElement> 对象的方式添加到相应的行为集合中，以使该行为可以使用应用程序配置文件进行插入。有关详细信息，请参见 [使用行为配置和扩展运行时](../../../../docs/framework/wcf/extending/configuring-and-extending-the-runtime-with-behaviors.md)。  
  
 有关演示在 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 客户端中执行截获的示例，请参见[如何：检查或修改客户端的消息](../../../../docs/framework/wcf/extending/how-to-inspect-or-modify-messages-on-the-client.md)。  
  
### 使用 ClientOperation 类  
 <xref:System.ServiceModel.Dispatcher.ClientOperation> 类是仅一个服务操作范围内的自定义扩展的客户端运行时修改和插入点的位置。（若要在约定中修改所有消息的客户端运行时行为，请使用 <xref:System.ServiceModel.Dispatcher.ClientRuntime> 类。）  
  
 使用 <xref:System.ServiceModel.Dispatcher.ClientRuntime.Operations%2A> 属性可定位表示特定服务操作的 <xref:System.ServiceModel.Dispatcher.ClientOperation> 对象。您可以使用下面的属性将自定义对象插入到 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 客户端系统中：  
  
-   使用 <xref:System.ServiceModel.Dispatcher.ClientOperation.Formatter%2A> 属性插入某一操作的自定义 <xref:System.ServiceModel.Dispatcher.IClientMessageFormatter> 实现或修改当前格式化程序。  
  
-   使用 <xref:System.ServiceModel.Dispatcher.ClientOperation.ParameterInspectors%2A> 属性插入自定义 <xref:System.ServiceModel.Dispatcher.IParameterInspector> 实现或修改当前实现。  
  
 您可以使用下面的属性修改与格式化程序和自定义参数检查器进行交互的系统：  
  
-   使用 <xref:System.ServiceModel.Dispatcher.ClientOperation.SerializeRequest%2A> 属性控制出站消息的序列化。  
  
-   使用 <xref:System.ServiceModel.Dispatcher.ClientOperation.DeserializeReply%2A> 属性控制入站消息的反序列化。  
  
-   使用 <xref:System.ServiceModel.Dispatcher.ClientOperation.Action%2A> 属性控制请求消息的 WS\-Addressing 操作。  
  
-   使用 <xref:System.ServiceModel.Dispatcher.ClientOperation.BeginMethod%2A> 和 <xref:System.ServiceModel.Dispatcher.ClientOperation.EndMethod%2A> 指定哪些 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 客户端方法与异步操作相关联。  
  
-   使用 <xref:System.ServiceModel.Dispatcher.ClientOperation.FaultContractInfos%2A> 属性获取包含可在 SOAP 错误中显示为详细信息类型的类型集合。  
  
-   使用 <xref:System.ServiceModel.Dispatcher.ClientOperation.IsInitiating%2A> 和 <xref:System.ServiceModel.Dispatcher.ClientOperation.IsTerminating%2A> 属性分别控制当调用操作时会话是已启动还是被撤销。  
  
-   使用 <xref:System.ServiceModel.Dispatcher.ClientOperation.IsOneWay%2A> 属性控制操作是否为单向操作。  
  
-   使用 <xref:System.ServiceModel.Dispatcher.ClientOperation.Parent%2A> 属性获取包含 <xref:System.ServiceModel.Dispatcher.ClientRuntime> 对象。  
  
-   使用 <xref:System.ServiceModel.Dispatcher.ClientOperation.Name%2A> 属性获取操作的名称。  
  
-   使用 <xref:System.ServiceModel.Dispatcher.ClientOperation.SyncMethod%2A> 属性控制将哪个方法映射到操作。  
  
 若要仅在一个服务操作中扩展 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 客户端执行，请检查 <xref:System.ServiceModel.Dispatcher.ClientOperation> 类中可用的属性，以查看修改属性或实现接口并将其添加到属性是否会创建您正在寻求的功能。在选择了要生成的特定扩展后，通过实现调用时可访问 <xref:System.ServiceModel.Dispatcher.ClientOperation> 类的客户端行为来将您的扩展插入相应的 <xref:System.ServiceModel.Dispatcher.ClientOperation> 属性。然后，您可以在该行为中修改 <xref:System.ServiceModel.Dispatcher.ClientRuntime> 属性来符合您的要求。  
  
 通常情况下，实现操作行为（实现 <xref:System.ServiceModel.Description.IOperationBehavior> 接口的对象）就可以满足需要，但是也可以使用终结点行为和约定行为，通过定位特定操作的 <xref:System.ServiceModel.Description.OperationDescription> 并在其中附加行为，以此达到相同的效果。有关详细信息，请参见 [使用行为配置和扩展运行时](../../../../docs/framework/wcf/extending/configuring-and-extending-the-runtime-with-behaviors.md)。  
  
 若要在配置中使用自定义行为，请使用自定义行为配置节处理程序安装您的行为。也可以通过创建自定义属性来安装您的行为。  
  
 有关演示在 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 客户端中执行截获的示例，请参见[如何：检查或修改参数](../../../../docs/framework/wcf/extending/how-to-inspect-or-modify-parameters.md)。  
  
## 请参阅  
 <xref:System.ServiceModel.Dispatcher.ClientRuntime>   
 <xref:System.ServiceModel.Dispatcher.ClientOperation>   
 [如何：检查或修改客户端的消息](../../../../docs/framework/wcf/extending/how-to-inspect-or-modify-messages-on-the-client.md)   
 [如何：检查或修改参数](../../../../docs/framework/wcf/extending/how-to-inspect-or-modify-parameters.md)