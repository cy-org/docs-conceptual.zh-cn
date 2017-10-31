---
title: "在协定和服务中指定和处理错误 | Microsoft Docs"
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
  - "处理错误 [WCF]"
ms.assetid: a9696563-d404-4905-942d-1e0834c26dea
caps.latest.revision: 22
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 22
---
# 在协定和服务中指定和处理错误
[!INCLUDE[indigo1](../../../includes/indigo1-md.md)] 应用程序通过以下方式来处理错误情况：将托管异常对象映射到 SOAP 错误对象，并将 SOAP 错误对象映射到托管异常对象。本节中的主题讨论如何设计协定以将错误条件作为自定义 SOAP 错误公开、如何作为服务实现的一部分返回这些错误，以及客户端如何捕捉这些错误。  
  
## 错误处理概述  
 在所有托管应用程序中，处理错误由 <xref:System.Exception> 对象表示。在基于 SOAP 的应用程序（如 [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] 应用程序）中，服务方法使用 SOAP 错误消息来传递处理错误信息。SOAP 错误是包括在服务操作元数据中的消息类型，因此会创建一个错误协定，客户端可使用该协定来使操作更加可靠或更具交互性。此外，由于 SOAP 错误在客户端以 XML 格式表示，这是一种任何 SOAP 平台上的客户端都可以使用的具有极好的互操作性的类型系统，可增加 [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] 应用程序的适用范围。  
  
 由于 [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] 应用程序在两种类型的错误系统下都可运行，因此发送到客户端的任何托管异常信息都必须在服务上从异常转换为 SOAP 错误，并在 [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] 客户端中从 SOAP 错误转换为错误异常。对于双工客户端，客户端协定还可以将 SOAP 错误发送回服务。在任一种情况下，您都可以使用默认的服务异常行为，或者可以显式控制是否（以及如何）将异常映射到错误消息。  
  
 可以发送两种类型的 SOAP 错误：已声明的和未声明的。已声明的 SOAP 错误是指其中的某个操作具有 <xref:System.ServiceModel.FaultContractAttribute?displayProperty=fullName> 属性（用于指定自定义 SOAP 错误类型）的错误。未声明的 SOAP 错误是在操作的协定中没有指定的错误。  
  
 强烈建议服务操作使用 <xref:System.ServiceModel.FaultContractAttribute> 属性来声明其错误，以正式指定在正常操作过程中客户端应该可以接收的所有 SOAP 错误。此外，还建议在 SOAP 错误中仅返回客户端必须了解的信息，以将信息泄露的风险降至最低。  
  
 通常，服务（以及双工客户端）使用下列步骤将错误处理成功地集成到其应用程序中：  
  
-   将异常条件映射到自定义 SOAP 错误。  
  
-   客户端和服务将 SOAP 错误作为异常进行发送和接收。  
  
 此外，[!INCLUDE[indigo2](../../../includes/indigo2-md.md)] 客户端和服务可以使用未声明的 SOAP 错误来进行调试，还可以扩展默认的错误行为。下面的部分讨论这些任务和概念。  
  
## 将异常映射到 SOAP 错误  
 创建用于处理错误条件的操作的第一步是：决定在什么条件下应向客户端应用程序通知有关错误的信息。某些操作具有特定于其功能的错误条件。例如，`PurchaseOrder` 操作可能会向不再允许其发起采购订单的用户返回特定信息。在其他情况下（如 `Calculator` 服务），一个更宽泛的 `MathFault` SOAP 错误也许可以描述整个服务内的所有错误条件。在标识服务客户端的错误条件之后，可以构造一个自定义 SOAP 错误，并可以将操作标记为在出现相应的 SOAP 错误条件时返回该 SOAP 错误。  
  
 [!INCLUDE[crabout](../../../includes/crabout-md.md)] 开发服务或客户端的这个步骤的更多信息，请参见[定义和指定错误](../../../docs/framework/wcf/defining-and-specifying-faults.md)。  
  
## 客户端和服务将 SOAP 错误作为异常进行处理  
 在 [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] 应用程序中成功进行错误处理的第一步是：标识操作错误条件，定义自定义 SOAP 错误，并将这些操作标记为返回这些错误。下一步是正确实现这些错误的发送和接收。通常，服务会发送错误以通知客户端应用程序有关错误条件的情况，但是双工客户端也可以向服务发送 SOAP 错误。  
  
 [!INCLUDE[crdefault](../../../includes/crdefault-md.md)] [发送和接收错误](../../../docs/framework/wcf/sending-and-receiving-faults.md).  
  
## 未声明的 SOAP 错误和调试  
 已声明的 SOAP 错误对于生成可靠的并可互操作的分布式应用程序非常有用。但在某些情况下，服务（或双工客户端）发送未声明的 SOAP 错误（即在相应操作的 Web 服务描述语言 \(WSDL\) 中未提及的错误）也很有用。例如，在开发服务时可能会出现意外情况，此时就可以将相关信息发送回客户端以方便调试。此外，可以将 <xref:System.ServiceModel.ServiceBehaviorAttribute.IncludeExceptionDetailInFaults%2A?displayProperty=fullName> 属性或 <xref:System.ServiceModel.Description.ServiceDebugBehavior.IncludeExceptionDetailInFaults%2A?displayProperty=fullName> 属性设置为 `true`，以允许 [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] 客户端获取有关内部服务操作异常的信息。[发送和接收错误](../../../docs/framework/wcf/sending-and-receiving-faults.md)中介绍了如何发送各个错误和设置调试行为属性。  
  
> [!IMPORTANT]
>  因为托管异常可以公开内部应用程序信息，所以将 <xref:System.ServiceModel.ServiceBehaviorAttribute.IncludeExceptionDetailInFaults%2A?displayProperty=fullName> 或 <xref:System.ServiceModel.Description.ServiceDebugBehavior.IncludeExceptionDetailInFaults%2A?displayProperty=fullName> 设置为 `true` 可以允许 [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] 客户端获得有关内部服务操作异常的信息，包括个人身份信息或其他敏感信息。  
>   
>  因此，建议将 <xref:System.ServiceModel.ServiceBehaviorAttribute.IncludeExceptionDetailInFaults%2A?displayProperty=fullName> 或 <xref:System.ServiceModel.Description.ServiceDebugBehavior.IncludeExceptionDetailInFaults%2A?displayProperty=fullName> 设置为 `true` 仅用作一种临时调试应用程序的方法。此外，以这种方式返回未处理的托管异常的方法的 WSDL 并不包含类型为 <xref:System.ServiceModel.ExceptionDetail> 的 <xref:System.ServiceModel.FaultException%601> 的协定。客户端必须预见到发生未知 SOAP 错误（作为 <xref:System.ServiceModel.FaultException?displayProperty=fullName> 对象返回到 [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] 客户端）的可能性，以便正确获取调试信息。  
  
## 使用 IErrorHandler 自定义错误处理  
 如果对于自定义在发生应用程序级别的异常时发送给客户端的响应消息有特殊要求，或者对于在返回响应消息之后执行某些自定义处理有特殊的要求，请实现 <xref:System.ServiceModel.Dispatcher.IErrorHandler?displayProperty=fullName> 接口。  
  
## 错误的序列化问题  
 在反序列化错误协定时，WCF 首先尝试将 SOAP 消息中的错误协定名称与错误协定类型相匹配。如果找不到精确匹配项，它将按字母顺序在可用错误协定列表中搜索兼容类型。如果两个错误协定是兼容类型（例如，一个是另一个的子类），则可能会使用错误类型对错误进行反序列化。仅当错误协定未指定名称、命名空间和操作时，才会发生此状况。若要防止此问题发生，则通过指定名称、命名空间和操作特性来始终完全限定错误协定。此外，如果您定义了许多派生自共享基类的相关错误协定，请确保使用 `[DataMember(IsRequired=true)]` 标记所有新成员。有关此 `IsRequired` 特性的更多信息，请参见 <xref:System.Runtime.Serialization.DataMemberAttribute>。这将防止基类成为兼容类型，并强制将错误反序列化为正确的派生类型。  
  
## 请参阅  
 <xref:System.ServiceModel.FaultException>   
 <xref:System.ServiceModel.FaultContractAttribute>   
 <xref:System.ServiceModel.FaultException>   
 <xref:System.Xml.Serialization.XmlSerializer>   
 <xref:System.ServiceModel.XmlSerializerFormatAttribute>   
 <xref:System.ServiceModel.FaultContractAttribute>   
 <xref:System.ServiceModel.CommunicationException>   
 <xref:System.ServiceModel.FaultContractAttribute.Action%2A>   
 <xref:System.ServiceModel.FaultException.Code%2A>   
 <xref:System.ServiceModel.FaultException.Reason%2A>   
 <xref:System.ServiceModel.FaultCode.SubCode%2A>   
 <xref:System.ServiceModel.OperationContractAttribute.IsOneWay%2A>   
 [定义和指定错误](../../../docs/framework/wcf/defining-and-specifying-faults.md)