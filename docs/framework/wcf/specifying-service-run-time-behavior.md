---
title: "指定服务运行时行为 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 5c5450ea-6af1-4b75-a267-613d0ac54707
caps.latest.revision: 12
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 12
---
# 指定服务运行时行为
在已经设计（[设计服务协定](../../../docs/framework/wcf/designing-service-contracts.md)）并实现服务协定（[实现服务协定](../../../docs/framework/wcf/implementing-service-contracts.md)）之后，就可以配置服务运行时的操作行为。 本主题讨论系统提供的服务和操作行为，并说明在何处查找更多信息来创建新行为。 尽管有些行为是作为属性应用的，但很多行为是使用应用程序配置文件或以编程方式应用的。[!INCLUDE[crabout](../../../includes/crabout-md.md)]配置服务应用程序，请参阅[正在配置服务](../../../docs/framework/wcf/configuring-services.md)。  
  
## 概述  
 协定定义相应类型的服务的输入、输出、数据类型和功能。 实现一个服务协定将会创建一个类，当使用某个地址的绑定对该类进行配置时，该类会满足其实现的协定。 客户端了解协定、绑定和地址信息等所有信息，如果没有它们，客户端将不能使用相应服务。  
  
 但是，操作详细信息（例如，线程处理问题或实例管理）对客户端是不透明的。 在已实现服务协定之后，就可以使用行为配置大量操作特征。 行为是一些对象，可通过设置运行时属性或通过在运行时中插入自定义类型来修改 [!INCLUDE[indigo1](../../../includes/indigo1-md.md)] 运行时。[!INCLUDE[crabout](../../../includes/crabout-md.md)]通过创建用户定义的行为来修改运行时，请参阅[扩展 ServiceHost 和服务模块层](../../../docs/framework/wcf/extending/extending-servicehost-and-the-service-model-layer.md)。  
  
 <xref:System.ServiceModel.ServiceBehaviorAttribute?displayProperty=fullName> 和 <xref:System.ServiceModel.OperationBehaviorAttribute?displayProperty=fullName> 属性是用途最广泛的行为，公开了最常请求的操作功能。 因为它们是属性，所以应将其应用于服务或操作实现。 其他行为（例如，<xref:System.ServiceModel.Description.ServiceMetadataBehavior?displayProperty=fullName> 或 <xref:System.ServiceModel.Description.ServiceDebugBehavior?displayProperty=fullName>）通常是使用应用程序配置文件进行应用的，但可以以编程方式使用它们。  
  
 本主题提供 <xref:System.ServiceModel.ServiceBehaviorAttribute> 和 <xref:System.ServiceModel.OperationBehaviorAttribute> 属性的概述，描述行为可以操作的不同范围，并为很多系统提供的不同范围的行为（[!INCLUDE[indigo2](../../../includes/indigo2-md.md)] 开发人员可能此感兴趣）提供快速说明。  
  
## ServiceBehaviorAttribute 和 OperationBehaviorAttribute  
 最重要的行为是 <xref:System.ServiceModel.ServiceBehaviorAttribute> 和 <xref:System.ServiceModel.OperationBehaviorAttribute> 属性，可以使用这两个属性来控制以下各项：  
  
-   实例生存期  
  
-   并发和同步支持  
  
-   配置行为  
  
-   事务行为  
  
-   序列化行为  
  
-   元数据转换  
  
-   会话生存期  
  
-   地址筛选和标头处理  
  
-   模拟  
  
-   若要使用这些属性，请使用适合对应范围的属性来标记服务或操作实现并设置属性。 例如，下面的代码示例演示了一个操作实现，该实现使用 <xref:System.ServiceModel.OperationBehaviorAttribute.Impersonation%2A?displayProperty=fullName> 属性来要求此操作的调用方支持模拟。  
  
 [!code-csharp[OperationBehaviorAttribute_Impersonation#1](../../../samples/snippets/csharp/VS_Snippets_CFX/operationbehaviorattribute_impersonation/cs/services.cs#1)]
 [!code-vb[OperationBehaviorAttribute_Impersonation#1](../../../samples/snippets/visualbasic/VS_Snippets_CFX/operationbehaviorattribute_impersonation/vb/services.vb#1)]  
  
 许多属性需要来自绑定的附加支持。 例如，要求来自客户端的事务的操作必须配置为使用支持流事务的绑定。  
  
### 已知的单一实例服务  
 可以使用 <xref:System.ServiceModel.ServiceBehaviorAttribute> 和 <xref:System.ServiceModel.OperationBehaviorAttribute> 属性来控制某些生存期，包括 <xref:System.ServiceModel.InstanceContext> 的生存期和实现操作的服务对象的生存期。  
  
 例如，<xref:System.ServiceModel.ServiceBehaviorAttribute.InstanceContextMode%2A?displayProperty=fullName> 属性控制释放 <xref:System.ServiceModel.InstanceContext> 的频率，而 <xref:System.ServiceModel.OperationBehaviorAttribute.ReleaseInstanceMode%2A?displayProperty=fullName> 和 <xref:System.ServiceModel.ServiceBehaviorAttribute.ReleaseServiceInstanceOnTransactionComplete%2A?displayProperty=fullName> 属性控制释放服务对象的时间。  
  
 但是，也可以自己创建服务对象以及创建使用该对象的服务主机。 为此，您还必须将 <xref:System.ServiceModel.ServiceBehaviorAttribute.InstanceContextMode%2A?displayProperty=fullName> 属性设置为 <xref:System.ServiceModel.InstanceContextMode>，否则在打开该服务主机时将引发异常。  
  
 可使用 [ServiceHost.ServiceHost\(Object, Uri\<xref:System.ServiceModel.ServiceHost.%23ctor%28System.Object%2CSystem.Uri%5B%5D%29?displayProperty=fullName> 构造函数创建此类服务。 当您希望提供一个特定的对象实例供单一实例服务使用时，可以使用它作为实现自定义 <xref:System.ServiceModel.Dispatcher.IInstanceContextInitializer?displayProperty=fullName> 的替代方法。 当服务实现类型难以构造时（例如，它没有实现默认的无参数的公共构造函数），可以使用此重载。  
  
 请注意，在为此构造函数提供对象时，一些与 [!INCLUDE[indigo1](../../../includes/indigo1-md.md)] 实例化行为相关的功能将有不同的工作方式。 例如，在提供已知对象实例时，调用 <xref:System.ServiceModel.InstanceContext.ReleaseServiceInstance%2A?displayProperty=fullName> 没有任何效果。 同样，也将忽略所有其他实例释放机制。<xref:System.ServiceModel.ServiceHost> 类的行为总是像对于所有操作都将 <xref:System.ServiceModel.OperationBehaviorAttribute.ReleaseInstanceMode%2A?displayProperty=fullName> 属性设置为 <xref:System.ServiceModel.ReleaseInstanceMode?displayProperty=fullName> 一样。  
  
## 其他服务、终结点、协定和操作行为  
 服务行为（如 <xref:System.ServiceModel.ServiceBehaviorAttribute> 属性）在整个服务中运行。 例如，如果将 <xref:System.ServiceModel.ServiceBehaviorAttribute.ConcurrencyMode%2A?displayProperty=fullName> 属性设置为 <xref:System.ServiceModel.ConcurrencyMode?displayProperty=fullName>，则必须自己在服务中的每个操作内处理线程同步问题。 终结点行为在终结点上运行，许多系统提供的终结点行为是针对客户端功能的。 协定行为在协定级别上运行，并且操作行为修改操作传递。  
  
 许多这些行为在属性上进行实现，并且可以像操作 <xref:System.ServiceModel.ServiceBehaviorAttribute> 和 <xref:System.ServiceModel.OperationBehaviorAttribute> 属性一样使用它们（通过将这些行为应用于相应的服务类或操作实现）。 其他行为（如 <xref:System.ServiceModel.Description.ServiceMetadataBehavior> 或 <xref:System.ServiceModel.Description.ServiceDebugBehavior> 对象）通常使用应用程序配置文件进行应用，但也可以以编程方式使用它们。  
  
 例如，可以通过使用 <xref:System.ServiceModel.Description.ServiceMetadataBehavior> 对象来配置元数据的发布。 下面的应用程序配置文件演示了最常见的用法。  
  
 [!code-csharp[ServiceMetadataBehavior#1](../../../samples/snippets/csharp/VS_Snippets_CFX/servicemetadatabehavior/cs/hostapplication.cs#1)]  
  
 下面的章节描述了许多最有用的系统提供的行为，您可以使用这些行为修改服务或客户端的运行时传递。 请参见相应的参考主题以确定如何使用每种行为。  
  
### 服务行为  
 下面的行为在服务上运行。  
  
-   <xref:System.ServiceModel.Activation.AspNetCompatibilityRequirementsAttribute>。 应用于 [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] 服务以指示该服务是否可以在 [!INCLUDE[vstecasp](../../../includes/vstecasp-md.md)] 兼容模式下运行。  
  
-   <xref:System.ServiceModel.Description.ServiceAuthorizationBehavior>。 控制服务如何向客户端声明授权。  
  
-   <xref:System.ServiceModel.Description.ServiceCredentials>。 配置服务凭据。 使用此类可指定服务的凭据，如 X.509 证书。  
  
-   <xref:System.ServiceModel.Description.ServiceDebugBehavior>。 启用 [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] 服务的调试和帮助信息功能。  
  
-   <xref:System.ServiceModel.Description.ServiceMetadataBehavior>。 控制服务元数据和相关信息的发布。  
  
-   <xref:System.ServiceModel.Description.ServiceSecurityAuditBehavior>。 指定安全性事件的审核行为。  
  
-   <xref:System.ServiceModel.Description.ServiceThrottlingBehavior>。 配置运行时吞吐量设置，这些设置可以让您优化服务性能。  
  
### 终结点行为  
 下面的行为在终结点上运行。 许多这些行为在客户端应用程序中使用。  
  
-   <xref:System.ServiceModel.CallbackBehaviorAttribute>。 在双工客户端应用程序中配置回调服务实现。  
  
-   <xref:System.ServiceModel.Description.CallbackDebugBehavior>。 启用 [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] 回调对象的服务调试。  
  
-   <xref:System.ServiceModel.Description.ClientCredentials>。 允许用户配置客户端和服务凭据以及服务凭据身份验证设置以便在客户端上使用。  
  
-   <xref:System.ServiceModel.Description.ClientViaBehavior>。 由客户端使用以指定应为其创建传输通道的统一资源标识符 \(URI\)。  
  
-   <xref:System.ServiceModel.Description.MustUnderstandBehavior>。 指示 [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] 禁用 `MustUnderstand` 处理。  
  
-   <xref:System.ServiceModel.Description.SynchronousReceiveBehavior>。 指示运行库对通道使用同步接收进程。  
  
-   <xref:System.ServiceModel.Description.TransactedBatchingBehavior>。 优化支持事务性接收的传输的接收操作。  
  
### 协定行为  
 <xref:System.ServiceModel.DeliveryRequirementsAttribute>。 指定绑定必须提供给服务或客户端实现的功能要求。  
  
### 操作行为  
 下面的操作行为指定操作的序列化和事务控制。  
  
-   <xref:System.ServiceModel.Description.DataContractSerializerOperationBehavior>。 表示 <xref:System.Runtime.Serialization.DataContractSerializer?displayProperty=fullName> 的运行时行为。  
  
-   <xref:System.ServiceModel.Description.XmlSerializerOperationBehavior>。 控制 `XmlSerializer` 的运行时行为并将其与某个操作相关联。  
  
-   <xref:System.ServiceModel.TransactionFlowAttribute>。 指定服务操作接受事务标头所处的级别。  
  
## 请参阅  
 [正在配置服务](../../../docs/framework/wcf/configuring-services.md)   
 [如何：控制服务实例化](../../../docs/framework/wcf/feature-details/how-to-control-service-instancing.md)