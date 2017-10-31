---
title: "与 POX 应用程序的互操作性 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 449276b8-4633-46f0-85c9-81f01d127636
caps.latest.revision: 15
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 15
---
# 与 POX 应用程序的互操作性
“Plain Old XML”\(POX\) 应用程序通过交换原始 HTTP 消息进行通信，该消息仅包含未封入 SOAP 信封内的 XML 应用程序数据。[!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] 可以提供使用 POX 消息的服务和客户端。就服务而言，可以使用 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 实现向客户端（例如，发送和接收 POX 消息的 Web 浏览器和脚本语言）公开终结点的服务。就客户端而言，可以使用 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 编程模型实现与基于 POX 的服务进行通信的客户端。  
  
> [!NOTE]
>  本文档最初是针对 [!INCLUDE[dnprdnshort](../../../../includes/dnprdnshort-md.md)] 3.0 编写的。[!INCLUDE[dnprdnshort](../../../../includes/dnprdnshort-md.md)] 3.5 具有对处理 POX 应用程序的内置支持。[!INCLUDE[crabout](../../../../includes/crabout-md.md)] 请参见[WCF Web HTTP 编程模型](../../../../docs/framework/wcf/feature-details/wcf-web-http-programming-model.md)  
  
## 使用 WCF 进行 POX 编程  
 使用 POX 消息通过 HTTP 进行通信的 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 服务使用 [\<customBinding\>](../../../../docs/framework/configure-apps/file-schema/wcf/custombinding.md)。  
  
```  
<customBinding>  
   <binding name="poxServerBinding">  
       <textMessageEncoding messageVersion="None" />  
       <httpTransport />  
   </binding>  
</customBinding>  
  
```  
  
 此自定义绑定包含两个元素：  
  
-   [\<httpTransport\>](../../../../docs/framework/configure-apps/file-schema/wcf/httptransport.md)和  
  
-   [\<textMessageEncoding\>](../../../../docs/framework/configure-apps/file-schema/wcf/textmessageencoding.md)。  
  
 标准 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 文本消息编码器被专门配置为使用 <xref:System.ServiceModel.Channels.MessageVersion.None%2A> 值，从而使其可以处理未封装在 SOAP 信封内到达的 XML 消息负载。  
  
 使用 POX 消息通过 HTTP 进行通信的 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 客户端使用类似的绑定（如下面的命令性代码所示）。  
  
```  
private static Binding CreatePoxBinding()  
{  
    TextMessageEncodingBindingElement encoder =   
    new TextMessageEncodingBindingElement( MessageVersion.None, Encoding.UTF8 );  
    HttpTransportBindingElement transport = new HttpTransportBindingElement();  
    transport.ManualAddressing = true;  
    return new CustomBinding( new BindingElement[] { encoder, transport } );  
}   
```  
  
 因为 POX 客户端必须显式指定将消息发送到的 URI，所以它们通常必须将 <xref:System.ServiceModel.Channels.HttpTransportBindingElement> 配置为手动寻址模式，方法是将该元素的 <xref:System.ServiceModel.Channels.TransportBindingElement.ManualAddressing%2A> 属性设置为 `true`。这样，应用程序代码就可以对消息进行显式寻址，因此，当应用程序将消息发送到不同的 HTTP URI 时，不必每次都创建一个新的 <xref:System.ServiceModel.ChannelFactory>。  
  
 因为 POX 消息不使用 SOAP 标头传送重要的协议信息，所以 POX 客户端和服务通常必须操作用于发送或接收消息的基础 HTTP 请求片段。HTTP 特定的协议信息（例如 HTTP 标头和状态代码）通过以下两个类在 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 编程模型中加以表示：  
  
-   <xref:System.ServiceModel.Channels.HttpRequestMessageProperty>，包含有关 HTTP 请求的信息，例如 HTTP 方法和请求标头。  
  
-   <xref:System.ServiceModel.Channels.HttpResponseMessageProperty>，包含有关 HTTP 响应的信息（例如 HTTP 状态代码和状态说明）以及任何 HTTP 响应标头。  
  
 下面的代码示例演示如何创建一个发送到 http:\/\/localhost:8100\/customers 的 HTTP GET 请求消息。  
  
```  
Message request = Message.CreateMessage( MessageVersion.None, String.Empty );  
request.Headers.To = “http://localhost:8100/customers”;  
  
HttpRequestMessageProperty property = new HttpRequestMessageProperty();  
property.Method = “GET”;  
property.SuppressEntityBody = true;  
request.Properties.Add( HttpRequestMessageProperty.Name, property );  
```  
  
 首先，通过调用 <xref:System.ServiceModel.Channels.Message.CreateMessage%28System.ServiceModel.Channels.MessageVersion%2CSystem.String%29> 创建一个空请求 <xref:System.ServiceModel.Channels.Message>。<xref:System.ServiceModel.Channels.MessageVersion.None%2A> 参数用于指示 SOAP 信封不是必需的并且 <xref:System.String.Empty> 参数作为 Action 传递。然后，通过将 <xref:System.ServiceModel.Channels.MessageHeaders.To%2A> 标头设置为所需的 URI，对请求消息进行寻址。接下来，创建一个 <xref:System.ServiceModel.Channels.HttpRequestMessageProperty>，并将 <xref:System.ServiceModel.Channels.HttpRequestMessageProperty.Method%2A> 设置为 HTTP 谓词 GET 方法，将 <xref:System.ServiceModel.Channels.HttpRequestMessageProperty.SuppressEntityBody%2A> 设置为 `true`，以指示不应在传出 HTTP 请求消息的消息正文中发送任何数据。最后，将请求属性添加到请求消息的 <xref:System.ServiceModel.Channels.Message.Properties%2A> 集合中，以便它能影响 HTTP 传输协议发送该请求的方式。这样，该消息就准备好通过 <xref:System.ServiceModel.Channels.IRequestChannel> 的相应实例进行发送了。  
  
 可以对服务使用类似的技术，以便从传入的消息中提取 <xref:System.ServiceModel.Channels.HttpRequestMessageProperty> 并构造响应。