---
title: "使用 Discovery 客户端通道 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 1494242a-1d64-4035-8ecd-eb4f06c8d2ba
caps.latest.revision: 6
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 6
---
# 使用 Discovery 客户端通道
编写 WCF 客户端应用程序时，需要了解所调用服务的终结点地址。在许多情况下，事先并不知晓服务的终结点地址，或者服务地址会随时间变化。Discovery 客户端通道可用于编写 WCF 客户端应用程序，描述您要调用的服务，并且自动发送探测请求。如果有服务做出响应，Discovery 客户端通道会从探测响应中检索该服务的终结点地址，并使用该地址调用服务。  
  
## 使用 Discovery 客户端通道  
 若要使用 Discovery 客户端通道，请将 <xref:System.ServiceModel.Discovery.DiscoveryClientBindingElement> 实例添加到客户端通道堆栈。此外，也可以使用 <xref:System.ServiceModel.Discovery.DynamicEndpoint>。如果尚不存在 <xref:System.ServiceModel.Discovery.DiscoveryClientBindingElement>，则会自动将该绑定元素添加到绑定。  
  
> [!CAUTION]
>  建议将 <xref:System.ServiceModel.Discovery.DiscoveryClientBindingElement> 作为客户端通道堆栈的最顶层元素。在 <xref:System.ServiceModel.Discovery.DiscoveryClientBindingElement> 之上添加的任何绑定元素都必须确保 <xref:System.ServiceModel.ChannelFactory> 或自己创建的通道不使用终结点地址或 `Via` 地址（传递到 `CreateChannel` 方法），因为它们包含的地址可能不正确。  
  
 <xref:System.ServiceModel.Discovery.DiscoveryClientBindingElement> 类包含两个公共属性：  
  
1.  <xref:System.ServiceModel.Discovery.DiscoveryClientBindingElement.FindCriteria%2A>，用于描述您要调用的服务。  
  
2.  <xref:System.ServiceModel.Discovery.DiscoveryClientBindingElement.DiscoveryEndpoint%2A>，用于指定将发现消息发送到的发现终结点。  
  
 <xref:System.ServiceModel.Discovery.DiscoveryClientBindingElement.FindCriteria%2A> 属性可用于指定要搜索的服务协定、任何必需的范围 URI 以及打开通道的最大尝试次数。调用构造函数 <xref:System.ServiceModel.Discovery.FindCriteria%2A> 可指定协定类型。可以将范围 URI 添加到 <xref:System.ServiceModel.Discovery.FindCriteria.Scopes%2A> 属性。<xref:System.ServiceModel.Discovery.FindCriteria.MaxResults%2A> 属性可用于指定客户端尝试连接的最大结果数。客户端收到探测响应时，会尝试使用探测响应提供的终结点地址打开通道。如果出现异常，客户端会转到下一个探测响应，如有必要，会等待接收更多响应。客户端将继续执行此操作，直至成功打开通道或者达到最大结果数。[!INCLUDE[crabout](../../../../includes/crabout-md.md)]这些设置的更多信息，请参见 <xref:System.ServiceModel.Discovery.FindCriteria%2A>。  
  
 <xref:System.ServiceModel.Discovery.DiscoveryClientBindingElement.DiscoveryEndpoint%2A> 属性可用于指定要使用的搜索终结点。该终结点通常是 <xref:System.ServiceModel.Discovery.UdpDiscoveryEndpoint>，但也可能是任何有效的终结点。  
  
 创建用于与服务通信的绑定时，必须注意使用与服务完全相同的绑定。唯一的区别是客户端绑定在堆栈顶层有一个 <xref:System.ServiceModel.Discovery.DiscoveryClientBindingElement>。如果服务使用系统提供的绑定之一，则创建新 <xref:System.ServiceModel.Channels.CustomBinding>，并在系统提供的绑定中将新绑定传递到 <xref:System.ServiceModel.CustomBinding.CustomBinding%2A> 构造函数。然后，可以对 <xref:System.ServiceModel.Channels.Binding.Elements%2A> 属性调用 `Insert` 来添加 <xref:System.ServiceModel.Discovery.DiscoveryClientBindingElement>。  
  
 将 <xref:System.ServiceModel.Discovery.DiscoveryClientBindingElement> 添加到绑定并进行配置之后，即可创建 WCF 客户端类的实例、打开该实例以及调用该实例的方法。下面的示例使用 Discovery 客户端通道发现某个 WCF 服务，该服务实现 `ICalculator` 类（在“WCF 入门教程”中使用该类）并调用该类的 `Add` 方法。  
  
```  
// Create the DiscoveryClientBindingElement  
DiscoveryClientBindingElement bindingElement = new DiscoveryClientBindingElement();  
// Search for a service that implements the ICalculator interface, attempting to open  
// the channel a maximum of 2 times  
bindingElement.FindCriteria = new FindCriteria(typeof(ICalculator)) { MaxResults = 2 };  
// Use the UdpDiscoveryEndpoint  
bindingElement.DiscoveryEndpoint = new UdpDiscoveryEndpoint();  
  
// The service uses the BasicHttpBinding, so use that and insert the DiscoveryClientBindingElement at the   
// top of the stack  
CustomBinding binding = new CustomBinding(new BasicHttpBinding());  
binding.Elements.Insert(0,bindingElement);  
  
try  
{  
    // Create the WCF client and call a method  
    CalculatorClient client = new CalculatorClient(binding, new EndpointAddress("http://schemas.microsoft.com/dynamic"));  
    client.Open();  
    client.Add(1, 1);  
}  
catch (EndpointNotFoundException ex)  
{  
    Console.WriteLine("An exception occurred: " + ex.Message);  
}  
```  
  
## 安全性和 Discovery 客户端通道  
 使用 Discovery 客户端通道时，同时指定了两个终结点：其中一个用于发现消息，通常为 <xref:System.ServiceModel.Discovery.UdpDiscoveryEndpoint>；另一个是应用程序终结点。实现安全服务时，必须谨慎以确保这两个终结点的安全。[!INCLUDE[crabout](../../../../includes/crabout-md.md)]安全的更多信息，请参见[保护服务和客户端的安全](../../../../docs/framework/wcf/feature-details/securing-services-and-clients.md)。