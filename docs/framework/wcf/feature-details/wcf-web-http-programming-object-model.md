---
title: "WCF Web HTTP 编程对象模型 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: ed96b5fc-ca2c-4b0d-bdba-d06b77c3cb2a
caps.latest.revision: 40
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 40
---
# WCF Web HTTP 编程对象模型
WCF WEB HTTP 编程模型使开发人员无需 SOAP，通过基本 HTTP 请求即可公开 [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] Web 服务。  WCF WEB HTTP 编程模型是基于现有 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 扩展性模型生成的。  它定义以下各类：  
  
 **编程模型：**  
  
-   <xref:System.ServiceModel.Web.AspNetCacheProfileAttribute>  
  
-   <xref:System.ServiceModel.Web.WebGetAttribute>  
  
-   <xref:System.ServiceModel.Web.WebInvokeAttribute>  
  
-   <xref:System.ServiceModel.Web.WebServiceHost>  
  
 **通道和调度程序基础结构：**  
  
-   <xref:System.ServiceModel.WebHttpBinding>  
  
-   <xref:System.ServiceModel.Description.WebHttpBehavior>  
  
 **实用工具类和扩展点：**  
  
-   <xref:System.UriTemplate>  
  
-   <xref:System.UriTemplateTable>  
  
-   <xref:System.ServiceModel.Dispatcher.QueryStringConverter>  
  
-   <xref:System.ServiceModel.Dispatcher.WebHttpDispatchOperationSelector>  
  
## AspNetCacheProfileAttribute  
 当应用于服务操作时，<xref:System.ServiceModel.Web.AspNetCacheProfileAttribute> 指示配置文件中的 ASP.NET 输出缓存配置文件，应使用该配置文件在 ASP .NET 输出缓存中缓存来自操作的响应。  此属性仅采用一个参数，即指定配置文件中的缓存设置的缓存配置文件名称。  
  
## WebGetAttribute  
 <xref:System.ServiceModel.Web.WebGetAttribute> 特性用于将服务操作标记为响应 HTTP GET 请求的操作。  这是将元数据添加到操作说明中的被动操作行为（<xref:System.ServiceModel.Description.IOperationBehavior> 方法不执行任何操作）。  应用 <xref:System.ServiceModel.Web.WebGetAttribute> 将无任何效果，除非将在操作说明中查找此元数据的行为（具体来说是 <xref:System.ServiceModel.Description.WebHttpBehavior>）添加到服务的行为集合中。  <xref:System.ServiceModel.Web.WebGetAttribute> 特性采用下表所示的可选参数。  
  
|参数|描述|  
|--------|--------|  
|`BodyStyle`|控制是否包装发送到应用该属性的服务操作以及从该操作接收的请求和响应。|  
|`RequestFormat`|控制如何格式化请求消息。|  
|`ResponseFormat`|控制如何格式化响应消息。|  
|`UriTemplate`|指定 URI 模板，该模板控制将哪些 HTTP 请求映射到应用该属性的服务操作。|  
  
## WebHttpBinding  
 <xref:System.ServiceModel.WebHttpBinding> 类使用 <xref:System.ServiceModel.Channels.WebMessageEncodingBindingElement> 集成了对 XML、JSON 和原始二进制数据的支持。  它由 <xref:System.ServiceModel.Channels.HttpsTransportBindingElement>、<xref:System.ServiceModel.Channels.HttpTransportBindingElement> 和 <xref:System.ServiceModel.WebHttpSecurity> 对象组成。  <xref:System.ServiceModel.WebHttpBinding> 专门与 <xref:System.ServiceModel.Description.WebHttpBehavior> 结合使用。  
  
## WebInvokeAttribute  
 <xref:System.ServiceModel.Web.WebInvokeAttribute> 属性类似于 <xref:System.ServiceModel.Web.WebGetAttribute>，但它用于将服务操作标记为响应 HTTP 请求（GET 除外）的操作。  这是将元数据添加到操作说明中的被动操作行为（<xref:System.ServiceModel.Description.IOperationBehavior> 方法不执行任何操作）。  应用 <xref:System.ServiceModel.Web.WebInvokeAttribute> 将无任何效果，除非将在操作说明中查找此元数据的行为（具体来说是 <xref:System.ServiceModel.Description.WebHttpBehavior>）添加到服务的行为集合中。  
  
 <xref:System.ServiceModel.Web.WebInvokeAttribute> 特性采用下表所示的可选参数。  
  
|参数|描述|  
|--------|--------|  
|`BodyStyle`|控制是否包装发送到应用该属性的服务操作以及从该操作接收的请求和响应。|  
|`Method`|指定将服务操作映射到的 HTTP 方法。|  
|`RequestFormat`|控制如何格式化请求消息。|  
|`ResponseFormat`|控制如何格式化响应消息。|  
|`UriTemplate`|指定 URI 模板，该模板控制将哪些 GET 请求映射到应用该属性的服务操作。|  
  
## UriTemplate  
 使用 <xref:System.UriTemplate> 类，可以定义一组结构相似的 URI。  模板由两部分组成，即路径和查询。  路径由一系列由斜杠 \(\/\) 分隔的段组成。  每个段都可以具有文本值、变量值（书写在大括号 \[{ }\] 内，且被限制为仅与一个段的内容匹配）或必须出现在路径末端的通配符（书写为星号 \[\*\]，与“路径的其余部分”匹配）。  查询表达式可以完全省略。  如果出现表达式，则它指定一组无序的名称\/值对。  查询表达式的元素可以是文本对 \(?x\=2\)，也可以是变量对（?x\={*值*}）。  不允许使用不成对的值。  <xref:System.UriTemplate> 由 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] WEB HTTP 编程模型在内部使用，用于将特定 URI 或 URI 组映射到服务操作。  
  
## UriTemplateTable  
 <xref:System.UriTemplateTable> 类表示一组绑定到开发人员所选对象的关联 <xref:System.UriTemplate> 对象。  您可以通过它将候选统一资源标识符 \(URI\) 与集合中的模板进行匹配，然后检索与匹配的模板相关联的数据。  <xref:System.UriTemplateTable> 由 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] WEB HTTP 编程模型在内部使用，用于将特定 URI 或 URI 组映射到服务操作。  
  
## WebServiceHost  
 <xref:System.ServiceModel.Web.WebServiceHost> 扩展 <xref:System.ServiceModel.ServiceHost>，以便更方便地承载非 SOAP Web 样式服务。  如果 <xref:System.ServiceModel.Web.WebServiceHost> 在服务说明中找不到终结点，则它将在服务的基址中自动创建一个默认终结点。  当创建默认 HTTP 终结点时，<xref:System.ServiceModel.Web.WebServiceHost> 同时禁用 HTTP 帮助页和 Web 服务描述语言 \(WSDL\) GET 功能，以使元数据终结点不干扰默认 HTTP 终结点。  <xref:System.ServiceModel.Web.WebServiceHost> 还将确保使用 <xref:System.ServiceModel.WebHttpBinding> 的所有终结点都附加了所需的 <xref:System.ServiceModel.Description.WebHttpBehavior>。  最后，<xref:System.ServiceModel.Web.WebServiceHost> 会自动配置终结点的绑定，以便在安全虚拟目录中使用时与关联的 Internet 信息服务 \(IIS\) 一起工作。  
  
## WebServiceHostFactory  
 当服务承载于 Internet 信息服务 \(IIS\) 或 Windows 进程激活服务 \(WAS\) 中时，<xref:System.ServiceModel.Activation.WebServiceHostFactory> 类用于动态创建 <xref:System.ServiceModel.Web.WebServiceHost>。  与自承载服务（其中，主机应用程序对 <xref:System.ServiceModel.Web.WebServiceHost> 进行实例化）不同，承载于 IIS 或 WAS 中的服务使用此类为服务创建 <xref:System.ServiceModel.Web.WebServiceHost>。  当收到服务的传入请求时，将调用 [CreateServiceHost\(Type, Uri\<xref:System.ServiceModel.Activation.WebServiceHostFactory.CreateServiceHost%28System.Type%2CSystem.Uri%5B%5D%29> 方法。  
  
## WebHttpBehavior  
 <xref:System.ServiceModel.Description.WebHttpBehavior> 类提供服务模型层 Web 样式的服务支持所需的必要格式化程序、操作选择器等。  这会作为终结点行为（与 <xref:System.ServiceModel.WebHttpBinding> 结合使用）实现，并允许为每个终结点指定格式化程序和操作选择器，从而使得同一个服务实现同时公开 SOAP 和 POX 终结点。  
  
### 扩展 WebHttpBehavior  
 可以使用如下多个虚方法来扩展 <xref:System.ServiceModel.Description.WebHttpBehavior>：<xref:System.ServiceModel.Description.WebHttpBehavior.GetOperationSelector%28System.ServiceModel.Description.ServiceEndpoint%29>、<xref:System.ServiceModel.Description.WebHttpBehavior.GetReplyClientFormatter%28System.ServiceModel.Description.OperationDescription%2CSystem.ServiceModel.Description.ServiceEndpoint%29>、<xref:System.ServiceModel.Description.WebHttpBehavior.GetRequestClientFormatter%28System.ServiceModel.Description.OperationDescription%2CSystem.ServiceModel.Description.ServiceEndpoint%29>、<xref:System.ServiceModel.Description.WebHttpBehavior.GetReplyDispatchFormatter%28System.ServiceModel.Description.OperationDescription%2CSystem.ServiceModel.Description.ServiceEndpoint%29> 以及 <xref:System.ServiceModel.Description.WebHttpBehavior.GetRequestDispatchFormatter%28System.ServiceModel.Description.OperationDescription%2CSystem.ServiceModel.Description.ServiceEndpoint%29>。  开发人员可以从 <xref:System.ServiceModel.Description.WebHttpBehavior> 派生类，并重写这些方法来自定义默认行为。  
  
 <xref:System.ServiceModel.Description.WebScriptEnablingBehavior> 是扩展 <xref:System.ServiceModel.Description.WebHttpBehavior> 的示例。  <xref:System.ServiceModel.Description.WebScriptEnablingBehavior> 允许 [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] 终结点接收来自基于浏览器的 ASP.NET AJAX 客户端的 HTTP 请求。  [使用 HTTP POST 的 AJAX 服务](../../../../docs/framework/wcf/samples/ajax-service-using-http-post.md)是一个使用此扩展点的示例。  
  
> [!WARNING]
>  当使用 <xref:System.ServiceModel.Description.WebScriptEnablingBehavior> 时，<xref:System.UriTemplate> 在 <xref:System.ServiceModel.Web.WebGetAttribute> 或 <xref:System.ServiceModel.Web.WebInvokeAttribute> 特性中不受支持。  
  
## WebHttpDispatchOperationSelector  
 <xref:System.ServiceModel.Dispatcher.WebHttpDispatchOperationSelector> 类使用 <xref:System.UriTemplate> 和 <xref:System.UriTemplateTable> 类调度对服务操作的调用。  
  
## 兼容性  
 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] WEB HTTP 编程模型不使用基于 SOAP 的消息，因此不支持 WS\-\* 协议。  但是，您可以通过两个终结点公开同一协定：一个终结点使用 SOAP，另一个终结点不使用 SOAP。  有关示例，请参见 [如何：向 SOAP 和 Web 客户端公开协定](../../../../docs/framework/wcf/feature-details/how-to-expose-a-contract-to-soap-and-web-clients.md)。  
  
## 安全性  
 因为 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] WEB HTTP 编程模型不支持 WS\-\* 协议，因此保证基于 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] WEB HTTP 编程模型生成的 Web 服务安全的唯一方式是通过使用 SSL 公开服务。  [!INCLUDE[crabout](../../../../includes/crabout-md.md)]使用 [!INCLUDE[iisver](../../../../includes/iisver-md.md)] 设置 SSL 的更多信息，请参见[如何在 IIS 中实现 SSL](http://go.microsoft.com/fwlink/?LinkId=131613)（可能为英文网页）  
  
## 请参阅  
 <xref:System.ServiceModel.WebHttpBinding>   
 <xref:System.ServiceModel.Web.WebGetAttribute>   
 <xref:System.ServiceModel.Web.WebInvokeAttribute>   
 <xref:System.ServiceModel.Description.WebHttpBehavior>   
 <xref:System.ServiceModel.Dispatcher.WebHttpDispatchOperationSelector>   
 [WCF Web HTTP 编程模型概述](../../../../docs/framework/wcf/feature-details/wcf-web-http-programming-model-overview.md)