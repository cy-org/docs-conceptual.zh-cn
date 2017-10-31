---
title: "发送和接收错误 | Microsoft Docs"
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
  - "处理错误 [WCF], 发送"
ms.assetid: 7be6fb96-ce2a-450b-aebe-f932c6a4bc5d
caps.latest.revision: 10
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 10
---
# 发送和接收错误
SOAP 错误将错误条件信息从服务传送到客户端，并且在双工情况下，将这些信息以互操作方式从客户端传送到服务。通常情况下，服务会定义自定义错误内容并指定可以返回错误的操作。（有关更多信息，请参见[定义和指定错误](../../../docs/framework/wcf/defining-and-specifying-faults.md)。）本主题讨论在出现相应的错误条件时服务或双工客户端如何发送这些错误，以及客户端或服务应用程序如何处理这些错误。有关 [!INCLUDE[indigo1](../../../includes/indigo1-md.md)] 应用程序中的错误处理的概述，请参见[在协定和服务中指定和处理错误](../../../docs/framework/wcf/specifying-and-handling-faults-in-contracts-and-services.md)。  
  
## 发送 SOAP 错误  
 声明的 SOAP 错误是指其中的某个操作具有 <xref:System.ServiceModel.FaultContractAttribute?displayProperty=fullName> 的错误，该属性指定自定义 SOAP 错误类型。未声明的 SOAP 错误是指那些未在相应操作的协定中指定的错误。  
  
### 发送已声明的错误  
 若要发送已声明的 SOAP 错误，需要检测与 SOAP 错误相对应的错误条件，并引发一个新的 <xref:System.ServiceModel.FaultException%601?displayProperty=fullName>，其中类型参数是在该操作的 <xref:System.ServiceModel.FaultContractAttribute> 中指定的类型的新对象。下面的代码示例演示如何使用 <xref:System.ServiceModel.FaultContractAttribute> 来指定 `SampleMethod` 操作可以使用详细信息类型 `GreetingFault` 返回 SOAP 错误。  
  
 [!code-csharp[FaultContractAttribute#4](../../../samples/snippets/csharp/VS_Snippets_CFX/faultcontractattribute/cs/services.cs#4)]
 [!code-vb[FaultContractAttribute#4](../../../samples/snippets/visualbasic/VS_Snippets_CFX/faultcontractattribute/vb/services.vb#4)]  
  
 若要向客户端传送 `GreetingFault` 错误信息，需要捕捉相应的错误条件，并引发一个类型为 `GreetingFault` 的新 <xref:System.ServiceModel.FaultException%601?displayProperty=fullName>，其参数为一个新的 `GreetingFault` 对象，如下面的代码示例所示。如果客户端是 [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] 客户端应用程序，它会将其视为托管异常，其中，异常类型是 `GreetingFault` 类型的 <xref:System.ServiceModel.FaultException%601?displayProperty=fullName>。  
  
 [!code-csharp[FaultContractAttribute#5](../../../samples/snippets/csharp/VS_Snippets_CFX/faultcontractattribute/cs/services.cs#5)]
 [!code-vb[FaultContractAttribute#5](../../../samples/snippets/visualbasic/VS_Snippets_CFX/faultcontractattribute/vb/services.vb#5)]  
  
### 发送未声明的错误  
 发送未声明的错误对于快速诊断和排除 [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] 应用程序中的问题而言非常有用，但是它作为调试工具的用处却很有限。一般来讲，在进行调试时，建议您使用 <xref:System.ServiceModel.Description.ServiceDebugBehavior.IncludeExceptionDetailInFaults%2A?displayProperty=fullName> 属性。在将此值设置为 true 时，客户端会将此类错误视为类型为 <xref:System.ServiceModel.ExceptionDetail> 的 <xref:System.ServiceModel.FaultException%601> 异常。  
  
> [!IMPORTANT]
>  因为托管异常可以公开内部应用程序信息，所以将 <xref:System.ServiceModel.ServiceBehaviorAttribute.IncludeExceptionDetailInFaults%2A?displayProperty=fullName> 或 <xref:System.ServiceModel.Description.ServiceDebugBehavior.IncludeExceptionDetailInFaults%2A?displayProperty=fullName> 设置为 `true` 可以允许 [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] 客户端获得有关内部服务操作异常的信息，包括个人身份信息或其他敏感信息。  
>   
>  因此，仅建议将 <xref:System.ServiceModel.ServiceBehaviorAttribute.IncludeExceptionDetailInFaults%2A?displayProperty=fullName> 或 <xref:System.ServiceModel.Description.ServiceDebugBehavior.IncludeExceptionDetailInFaults%2A?displayProperty=fullName> 设置为 `true` 作为一种临时调试服务应用程序的方法。此外，以这种方式返回未处理的托管异常的方法的 WSDL 并不包含类型为 <xref:System.ServiceModel.ExceptionDetail> 的 <xref:System.ServiceModel.FaultException%601> 的协定。客户端必须预见到发生未知 SOAP 错误（作为 <xref:System.ServiceModel.FaultException?displayProperty=fullName> 对象返回到 [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] 客户端）的可能性，以便正确获取调试信息。  
  
 若要发送未声明的 SOAP 错误，会引发一个 <xref:System.ServiceModel.FaultException?displayProperty=fullName> 对象（即，不是泛型类型 <xref:System.ServiceModel.FaultException%601>）并将该字符串传递给构造函数。它会作为一个已引发的 <xref:System.ServiceModel.FaultException?displayProperty=fullName> 异常向 [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] 客户端应用程序公开，其中，可以通过调用 <xref:System.ServiceModel.FaultException%601.ToString%2A?displayProperty=fullName> 方法获得字符串。  
  
> [!NOTE]
>  如果声明了一个字符串类型的 SOAP 错误，然后将其作为一个 <xref:System.ServiceModel.FaultException%601> 在服务中引发（其中，类型参数是一个 <xref:System.String?displayProperty=fullName>），则会将字符串值赋给 <xref:System.ServiceModel.FaultException%601.Detail%2A?displayProperty=fullName> 属性，并且无法从 <xref:System.ServiceModel.FaultException%601.ToString%2A?displayProperty=fullName> 获得此值。  
  
## 处理错误  
 在 [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] 客户端中，客户端应用程序感兴趣的、在通信过程中发生的 SOAP 错误将作为托管异常引发。尽管在任何程序的执行过程中都可能发生许多异常，但使用 [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] 客户端编程模型的应用程序可以期望处理由通信问题引发的以下两种类型的异常。  
  
-   <xref:System.TimeoutException>  
  
-   <xref:System.ServiceModel.CommunicationException>  
  
 当某个操作超过指定的超时期限时，引发 <xref:System.TimeoutException> 对象。  
  
 当服务或客户端上存在某些可恢复的通信错误条件时，引发 <xref:System.ServiceModel.CommunicationException> 对象。  
  
 <xref:System.ServiceModel.CommunicationException> 类具有两个重要的派生类型：<xref:System.ServiceModel.FaultException> 和泛型 <xref:System.ServiceModel.FaultException%601> 类型。  
  
 当侦听器接收到操作协定中未预料到或未指定的错误时，引发 <xref:System.ServiceModel.FaultException> 异常；这通常在对应用程序进行调试并且服务的 <xref:System.ServiceModel.Description.ServiceDebugBehavior.IncludeExceptionDetailInFaults%2A?displayProperty=fullName> 属性设置为 `true` 时发生。  
  
 如果在对双向操作（即，一个具有 <xref:System.ServiceModel.OperationContractAttribute> 属性并将其 <xref:System.ServiceModel.OperationContractAttribute.IsOneWay%2A> 设置为 `false` 的方法）进行响应时接收到操作协定中指定的错误，则会在客户端上引发 <xref:System.ServiceModel.FaultException%601> 异常。  
  
> [!NOTE]
>  当 [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] 服务的 <xref:System.ServiceModel.ServiceBehaviorAttribute.IncludeExceptionDetailInFaults%2A?displayProperty=fullName> 或 <xref:System.ServiceModel.Description.ServiceDebugBehavior.IncludeExceptionDetailInFaults%2A?displayProperty=fullName> 属性设置为 `true` 时，客户端会将此错误视为类型为 <xref:System.ServiceModel.ExceptionDetail> 的未声明 <xref:System.ServiceModel.FaultException%601>。客户端可以捕捉这一特定错误，也可以在 <xref:System.ServiceModel.FaultException> 的 catch 块中处理该错误。  
  
 通常，客户端和服务只对 <xref:System.ServiceModel.FaultException%601>、<xref:System.TimeoutException> 和 <xref:System.ServiceModel.CommunicationException> 异常感兴趣。  
  
> [!NOTE]
>  当然，还会发生其他异常。意外的异常包括灾难性故障，如 <xref:System.OutOfMemoryException?displayProperty=fullName>；通常情况下，应用程序不应该捕捉这些异常。  
  
### 按照正确的顺序捕捉错误异常  
 因为 <xref:System.ServiceModel.FaultException%601> 派生自 <xref:System.ServiceModel.FaultException>，而 <xref:System.ServiceModel.FaultException> 派生自 <xref:System.ServiceModel.CommunicationException>，所以按照正确的顺序捕捉这些异常非常重要。例如，如果您首先在 try\/catch 块中捕捉 <xref:System.ServiceModel.CommunicationException>，则会在此块中处理所有已指定的和未指定的 SOAP 错误；用于处理自定义 <xref:System.ServiceModel.FaultException%601> 异常的任何后续 catch 块永远得不到调用。  
  
 请牢记，一个操作可以返回任意数量的指定错误。每个错误都具有唯一的类型，必须单独进行处理。  
  
### 在关闭通道时处理异常  
 以上大多数讨论都与在处理应用程序消息（即，在客户端应用程序调用 [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] 客户端对象上的操作时由客户端显式发送的消息）期间发送的错误有关。  
  
 即使对于本地对象，释放对象也会引发或者屏蔽在回收过程中发生的异常。使用 [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] 客户端对象时，也可能发生类似的情况。当您调用操作时，您是在通过已建立的连接发送消息。如果无法完全关闭连接或连接已经关闭，那么即使所有操作都正确返回，关闭通道也会引发异常。  
  
 通常，客户端对象通道以下列方式之一关闭：  
  
-   在回收 [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] 客户端对象时。  
  
-   在客户端应用程序调用 <xref:System.ServiceModel.ClientBase%601.Close%2A?displayProperty=fullName> 时。  
  
-   在客户端应用程序调用 <xref:System.ServiceModel.ICommunicationObject.Close%2A?displayProperty=fullName> 时。  
  
-   在客户端应用程序调用会话的终止操作时。  
  
 在所有情况下，关闭通道都会指示通道开始关闭所有可能正在发送消息以支持应用程序级复杂功能的基础通道。例如，当协定需要使用会话时，绑定便会尝试通过与服务通道交换消息来建立会话，直到会话建立。当通道关闭时，基础会话通道会通知服务会话已终止。在此情况下，如果通道已经中止、关闭或由于其他原因（例如，网络电缆被拔出）而变得不可用，则客户端通道无法通知服务通道会话已终止，从而引发异常。  
  
### 在需要时中止通道  
 因为关闭通道还会引发异常，所以，建议您除了按照正确的顺序捕捉错误异常以外，还需要在 catch 块中中止在进行调用时使用的通道。  
  
 如果错误传送了特定于某个操作的错误信息，并且其他操作仍有可能使用该通道，则无需中止该通道（尽管这种情况非常少见）。在其他所有情况下，都建议您中止该通道。有关演示上述所有要点的示例，请参见[预期异常](../../../docs/framework/wcf/samples/expected-exceptions.md)。  
  
 下面的代码示例演示如何在基本客户端应用程序中处理 SOAP 错误异常，包括已声明的错误和未声明的错误。  
  
> [!NOTE]
>  这些示例代码没有使用 `using` 协定。因为关闭通道可能引发异常，所以建议您首先让应用程序创建一个 [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] 客户端，然后在同一个 try 块中打开、使用和关闭该 [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] 客户端。有关详细信息，请参见 [WCF 客户端概述](../../../docs/framework/wcf/wcf-client-overview.md)和[避免出现与 Using 语句有关的问题](../../../docs/framework/wcf/samples/avoiding-problems-with-the-using-statement.md)。  
  
 [!code-csharp[FaultContractAttribute#3](../../../samples/snippets/csharp/VS_Snippets_CFX/faultcontractattribute/cs/client.cs#3)]
 [!code-vb[FaultContractAttribute#3](../../../samples/snippets/visualbasic/VS_Snippets_CFX/faultcontractattribute/vb/client.vb#3)]  
  
## 请参阅  
 <xref:System.ServiceModel.FaultException>   
 <xref:System.ServiceModel.FaultException%601>   
 <xref:System.ServiceModel.CommunicationException?displayProperty=fullName>   
 [预期异常](../../../docs/framework/wcf/samples/expected-exceptions.md)   
 [避免出现与 Using 语句有关的问题](../../../docs/framework/wcf/samples/avoiding-problems-with-the-using-statement.md)