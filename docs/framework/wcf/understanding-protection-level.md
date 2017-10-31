---
title: "了解保护级别 | Microsoft Docs"
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
  - "ProtectionLevel 属性"
  - "WCF, 安全"
ms.assetid: 0c034608-a1ac-4007-8287-b1382eaa8bf2
caps.latest.revision: 22
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 22
---
# 了解保护级别
在许多不同的类中可以找到 `ProtectionLevel` 属性，例如 <xref:System.ServiceModel.ServiceContractAttribute> 和 <xref:System.ServiceModel.OperationContractAttribute> 类。此属性控制部分（或整个）消息的保护方式。本主题说明 [!INCLUDE[indigo1](../../../includes/indigo1-md.md)] 功能及其原理。  
  
 有关设置保护级别的说明，请参见 [如何：设置 ProtectionLevel 属性](../../../docs/framework/wcf/how-to-set-the-protectionlevel-property.md)。  
  
> [!NOTE]
>  只能在代码中设置保护级别，不能在配置中设置。  
  
## 基本知识  
 若要了解保护级别功能，以下基本语句适用：  
  
-   消息的任何部分都存在三种基本保护级别。属性（无论它出现在哪里）设置为 <xref:System.Net.Security.ProtectionLevel> 枚举值之一。按升序的保护顺序，它们包括：  
  
    -   `None`.  
  
    -   `Sign`.受保护的部分进行数字签名。这样做可以保证检测到对受保护的消息部分进行的任何篡改。  
  
    -   `EncryptAndSign`.签名前会对消息部分进行加密，以确保其保密性。  
  
-   使用此功能只能为应用程序数据设置保护要求。例如，WS\-Addressing 标头是基础结构数据，因此不受 `ProtectionLevel` 影响。  
  
-   当安全模式设置为 `Transport` 时，整个消息由传输机制进行保护。因此，为消息的不同部分设置单独的保护级别没有作用。  
  
-   对开发人员来说，`ProtectionLevel` 是设置绑定必须符合的最低级别的一种方法。在部署了服务时，在配置中指定的实际绑定不一定支持最低级别。例如，默认情况下，<xref:System.ServiceModel.BasicHttpBinding> 类不提供安全性（尽管可以启用安全性）。因此，将它与具有任何非 `None` 设置的协定一起使用将导致引发异常。  
  
-   如果服务要求所有消息的最低 `ProtectionLevel` 为 `Sign`，则客户端（可能由非 [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] 技术创建）可以对所消息进行加密和签名（这高于最低要求）。在这种情况下，[!INCLUDE[indigo2](../../../includes/indigo2-md.md)] 将不会引发异常，因为客户端的处理高于最低要求。但是，请注意，[!INCLUDE[indigo2](../../../includes/indigo2-md.md)] 应用程序（服务或客户端）在可能的情况下不会过度保护消息部分，而是遵循最低级别。还要注意，当使用 `Transport` 作为安全模式时，传输可能过度保护消息流，因为它在本质上无法以更精细的级别进行保护。  
  
-   如果将 `ProtectionLevel` 显式设置为 `Sign` 或 `EncryptAndSign`，则您必须使用启用安全的绑定，否则将会引发异常。  
  
-   如果您选择启用安全的绑定，并且未在协定的任何位置设置 `ProtectionLevel` 属性，则将对所有的应用程序数据进行加密或签名。  
  
-   如果您选择未启用安全的绑定（例如，`BasicHttpBinding` 类在默认情况下禁用安全），并且没有显式设置 `ProtectionLevel`，那么所有应用程序数据都不会受到保护。  
  
-   如果所使用的绑定应用传输级别的安全，则将根据传输的功能对所有应用程序数据进行保护。  
  
-   如果所使用的绑定应用消息级别的安全，则将根据协定上设置的保护级别对应用程序数据进行保护。如果不指定保护级别，则将对消息中所有的应用程序数据进行加密和签名。  
  
-   可以在不同范围级别设置 `ProtectionLevel`。有一个与范围关联的层次结构，这将在下一节中进行说明。  
  
## 范围  
 设置最顶层 API 上的 `ProtectionLevel` 可以为它下面所有级别设置级别。如果 `ProtectionLevel` 在较低级别上设置为其他值，该层次结构中该级别下的所有 API 都将立即重置为新级别（然而它上面的 API 仍将受最顶层级别影响）。该层次结构如下所示。同一级别的属性是对等的。  
  
 <xref:System.ServiceModel.ServiceContractAttribute>  
  
 <xref:System.ServiceModel.OperationContractAttribute>  
  
 <xref:System.ServiceModel.FaultContractAttribute>  
  
 <xref:System.ServiceModel.MessageContractAttribute>  
  
 <xref:System.ServiceModel.MessageHeaderAttribute>  
  
 <xref:System.ServiceModel.MessageBodyMemberAttribute>  
  
## ProtectionLevel 的编程  
 若要在层次结构中的任意点对 `ProtectionLevel` 进行编程，只需在应用此属性 \(Attribute\) 时将其属性 \(Property\) 设置为适当的值即可。有关示例，请参见[如何：设置 ProtectionLevel 属性](../../../docs/framework/wcf/how-to-set-the-protectionlevel-property.md)。  
  
> [!NOTE]
>  要设置错误和消息协定的属性，需要了解这些功能的工作原理。[!INCLUDE[crdefault](../../../includes/crdefault-md.md)][如何：设置 ProtectionLevel 属性](../../../docs/framework/wcf/how-to-set-the-protectionlevel-property.md) 和 [使用消息约定](../../../docs/framework/wcf/feature-details/using-message-contracts.md)。  
  
## WS\-Addressing 依赖性  
 在大多数情况下，使用 [ServiceModel 元数据实用工具 \(Svcutil.exe\)](../../../docs/framework/wcf/servicemodel-metadata-utility-tool-svcutil-exe.md) 生成客户端可以确保此客户端和服务协定相同。但是，看起来相同的协定却可能导致客户端引发异常。只要绑定不支持 WS\-Addressing 规范并且在协定上指定了多个保护级别，就会发生这种情况。例如，<xref:System.ServiceModel.BasicHttpBinding> 类不支持此规范，或者您创建一个不支持 WS\-Addressing 的自定义绑定。`ProtectionLevel` 功能依靠 WS\-Addressing 规范在单个协定上启用不同的保护级别。如果绑定不支持 WS\-Addressing 规范，所有级别都将设置为同一保护级别。协定上所有范围的有效保护级别将设置为在协定上使用的最高保护级别。  
  
 这可能会引起初看上去难以调试的问题。可以创建一个包括多个服务的方法的客户端协定（一个接口）。也就是说，使用同一接口创建一个与许多服务通信的客户端，而该单个接口包含针对所有服务的方法。在这种罕见的情况下，开发人员必须注意仅调用那些适用于每个特定服务的方法。如果绑定是 <xref:System.ServiceModel.BasicHttpBinding> 类，则不支持多个保护级别。但是，对客户端进行答复的服务可能会对保护级别比要求的为低的客户端进行响应。在这种情况下，客户端将会引发异常，因为它需要更高的保护级别。  
  
 可用一个代码示例解释这个问题。下面的示例显示一个服务和一个客户端协定。假定绑定为 [\<basicHttpBinding\>](../../../docs/framework/configure-apps/file-schema/wcf/basichttpbinding.md) 元素。因此，对协定的所有操作都具有相同的保护级别。这一统一的保护级别被确定为所有操作中的最高保护级别。  
  
 服务协定为：  
  
 [!code-csharp[c_ProtectionLevel#7](../../../samples/snippets/csharp/VS_Snippets_CFX/c_protectionlevel/cs/source.cs#7)]
 [!code-vb[c_ProtectionLevel#7](../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_protectionlevel/vb/source.vb#7)]  
  
 下面的代码显示客户端协定接口。请注意它包括一个 `Tax` 方法，此方法旨在与一个不同的服务一起使用：  
  
 [!code-csharp[c_ProtectionLevel#8](../../../samples/snippets/csharp/VS_Snippets_CFX/c_protectionlevel/cs/source.cs#8)]
 [!code-vb[c_ProtectionLevel#8](../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_protectionlevel/vb/source.vb#8)]  
  
 当客户端调用 `Price` 方法时，它在接收到服务的答复时引发异常。发生这种情况是因为客户端未指定 `ServiceContractAttribute` 的 `ProtectionLevel`，所以客户端为所有方法使用默认值 \(<xref:System.Net.Security.ProtectionLevel>\)，包括 `Price` 方法。但是，服务返回该值时使用 <xref:System.Net.Security.ProtectionLevel> 级别，因为服务协定定义了一个单一的方法，此方法将其保护级别设置为 <xref:System.Net.Security.ProtectionLevel>。在这种情况下，客户端在验证服务的响应时将引发错误。  
  
## 请参阅  
 <xref:System.ServiceModel.ServiceContractAttribute>   
 <xref:System.ServiceModel.OperationContractAttribute>   
 <xref:System.ServiceModel.FaultContractAttribute>   
 <xref:System.ServiceModel.MessageContractAttribute>   
 <xref:System.ServiceModel.MessageHeaderAttribute>   
 <xref:System.ServiceModel.MessageBodyMemberAttribute>   
 <xref:System.Net.Security.ProtectionLevel>   
 [保证服务的安全](../../../docs/framework/wcf/securing-services.md)   
 [如何：设置 ProtectionLevel 属性](../../../docs/framework/wcf/how-to-set-the-protectionlevel-property.md)   
 [在协定和服务中指定和处理错误](../../../docs/framework/wcf/specifying-and-handling-faults-in-contracts-and-services.md)   
 [使用消息约定](../../../docs/framework/wcf/feature-details/using-message-contracts.md)