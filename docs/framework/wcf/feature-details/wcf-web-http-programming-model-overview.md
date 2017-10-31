---
title: "WCF Web HTTP 编程模型概述 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 381fdc3a-6e6c-4890-87fe-91cca6f4b476
caps.latest.revision: 45
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 45
---
# WCF Web HTTP 编程模型概述
[!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] WEB HTTP 编程模型提供使用 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 生成 WEB HTTP 服务所需的基本元素。[!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] WEB HTTP 服务旨在提供给最大范围的可能客户端（包括 Web 浏览器）访问，并且具有以下独特要求：  
  
-   **URI 和 URI 处理** URI 在 WEB HTTP 服务的设计中扮演着核心角色。[!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] WEB HTTP 编程模型使用 <xref:System.UriTemplate> 和 <xref:System.UriTemplateTable> 类来提供 URI 处理功能。  
  
-   **支持 GET 和 POST 操作** 除了使用各种调用谓词来进行数据修改和远程调用之外，WEB HTTP 服务还使用 GET 谓词进行数据检索。[!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] WEB HTTP 编程模型使用 <xref:System.ServiceModel.Web.WebGetAttribute> 和 <xref:System.ServiceModel.Web.WebInvokeAttribute> 将服务操作与 GET 和其他 HTTP 谓词（如 PUT、POST 和 DELETE）相关联。  
  
-   **多种数据格式** Web 样式服务除了处理 SOAP 消息之外，还可处理很多种数据。[!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] WEB HTTP 编程模型使用 <xref:System.ServiceModel.WebHttpBinding> 和 <xref:System.ServiceModel.Description.WebHttpBehavior> 来支持许多不同的数据格式，包括 XML 文档、JSON 数据对象和二进制内容（例如图像、视频文件或纯文本）的流。  
  
 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] WEB HTTP 编程模型将 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 扩展到覆盖 Web 样式的方案，包括 WEB HTTP 服务、AJAX 和 JSON 服务以及联合 \(ATOM\/RSS\) 源。[!INCLUDE[crabout](../../../../includes/crabout-md.md)] AJAX 和 JSON 服务的更多信息，请参见 [AJAX 集成和 JSON 支持](../../../../docs/framework/wcf/feature-details/ajax-integration-and-json-support.md)。[!INCLUDE[crabout](../../../../includes/crabout-md.md)]联合的更多信息，请参见 [WCF 联合概述](../../../../docs/framework/wcf/feature-details/wcf-syndication-overview.md)。  
  
 对于可从 WEB HTTP 服务返回的数据的类型没有额外的限制。任何可序列化类型都可以从 WEB HTTP 服务操作返回。因为 WEB HTTP 服务操作可以通过 Web 浏览器调用，所以对可在 URL 中指定的数据类型有一个限制。有关默认情况下支持的类型的更多信息，请参见下面的 **UriTemplate 查询字符串参数和 URL** 一节。通过提供您自己的 T:System.ServiceModel.Dispatcher.QueryStringConverter 实现来指定如何将 URL 中指定的参数转换为实际参数类型，可以更改默认行为。[!INCLUDE[crdefault](../../../../includes/crdefault-md.md)]<xref:System.ServiceModel.Dispatcher.QueryStringConverter>  
  
> [!CAUTION]
>  使用 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] WEB HTTP 编程模型编写的服务不使用 SOAP 消息。由于不使用 SOAP，因此无法使用 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 提供的安全功能。然而，您可通过使用 HTTP 承载服务来使用基于传输的安全性。[!INCLUDE[crabout](../../../../includes/crabout-md.md)][!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 安全的更多信息，请参见[安全性概述](../../../../docs/framework/wcf/feature-details/security-overview.md)  
  
> [!WARNING]
>  为 IIS 安装 WebDAV 扩展会导致 Web HTTP 服务返回 HTTP 405 错误，因为 WebDAV 扩展试图处理所有 PUT 请求。若要解决此问题，您可卸载 WebDAV 扩展或为网站禁用 WebDAV 扩展。[!INCLUDE[crdefault](../../../../includes/crdefault-md.md)][IIS 和 WebDav](http://learn.iis.net/page.aspx/357/webdav-for-iis-70/)  
  
## 使用 UriTemplate 和 UriTemplateTable 进行 URI 处理  
 URI 模板提供了一种可以高效地表示很大的结构相似的 URI 集的语法。例如，下面的模板表示所有以“a”开始并以“c”结束而中间段的值不限的、由三个段组成的 URI：a\/{segment}\/c  
  
 此模板描述如下所示的 URI：  
  
-   a\/x\/c  
  
-   a\/y\/c  
  
-   a\/z\/c  
  
-   等等。  
  
 在此模板中，大括号表示法 \("{segment}"\) 指示变量段而不是文本值。  
  
 .NET Framework 提供了一个 API 来处理名为 <xref:System.UriTemplate> 的 URI 模板。`UriTemplates` 允许执行下列操作：  
  
-   可以使用一组参数来调用 `Bind` 方法之一，以生成一个与模板匹配的完全封闭的 URI。这意味着，URI 模板中的所有变量均由实际值替换。  
  
-   可以使用候选 URI 调用 `Match`\(\)，此时会使用模板将候选 URI 的各个组成部分分解开来，并会返回一个字典，其中包含根据模板中的变量标记的 URI 的不同部分。  
  
-   `Bind`\(\) 和 `Match`\(\) 互为逆方法，因此可以调用 `Match`\( `Bind`\( x \) \) 并返回到开始时的相同环境。  
  
 有很多时候（尤其是在服务器需要基于 URI 将请求调度到某个服务操作时），对于那些可以单独对包含的每个模板进行寻址的数据结构，您都需要一直跟踪其中的一组 <xref:System.UriTemplate> 对象。<xref:System.UriTemplateTable> 表示一组 URI 模板，并在给定的一组模板和候选 URI 中选择最匹配的项。这与任何特定网络堆栈（包括 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)]）不相关，因此可以在任何需要的地方使用。  
  
 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 服务模型使用 <xref:System.UriTemplate> 和 <xref:System.UriTemplateTable> 将服务操作与由 <xref:System.UriTemplate> 描述的一组 URI 相关联。通过使用 <xref:System.ServiceModel.Web.WebGetAttribute> 或 <xref:System.ServiceModel.Web.WebInvokeAttribute>，将服务操作与 <xref:System.UriTemplate> 相关联。[!INCLUDE[crabout](../../../../includes/crabout-md.md)]<xref:System.UriTemplate> 和 <xref:System.UriTemplateTable> 的更多信息，请参见 [UriTemplate 和 UriTemplateTable](../../../../docs/framework/wcf/feature-details/uritemplate-and-uritemplatetable.md)  
  
## WebGet 和 WebInvoke 特性  
 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] WEB HTTP 服务除了使用各种调用谓词（例如 HTTP POST、PUT 和 DELETE）之外，还使用检索谓词（例如 HTTP GET）。[!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] WEB HTTP 编程模型允许服务开发人员使用 <xref:System.ServiceModel.Web.WebGetAttribute> 和 <xref:System.ServiceModel.Web.WebInvokeAttribute> 控制与其服务操作相关联的 URI 模板和谓词。可以使用 <xref:System.ServiceModel.Web.WebGetAttribute> 和 <xref:System.ServiceModel.Web.WebInvokeAttribute> 来控制各个操作如何绑定到 URI 以及与这些 URI 相关联的 HTTP 方法。例如，在下面的代码中添加 <xref:System.ServiceModel.Web.WebGetAttribute> 和 <xref:System.ServiceModel.Web.WebInvokeAttribute>。  
  
```  
[ServiceContract]  
interface ICustomer  
{  
  //"View It"  
  
  [WebGet]  
  Customer GetCustomer():  
  
  //"Do It"  
    [WebInvoke]  
  Customer UpdateCustomerName( string id,   
                               string newName );  
}  
```  
  
 可以使用上面的代码生成下面的 HTTP 请求。  
  
 `GET /GetCustomer`  
  
 `POST /UpdateCustomerName`  
  
 <xref:System.ServiceModel.Web.WebInvokeAttribute> 的默认值为 POST，但也可以将其用于其他谓词。  
  
```  
[ServiceContract]  
interface ICustomer  
{  
  //"View It" -> HTTP GET  
    [WebGet( UriTemplate="customers/{id}" )]  
  Customer GetCustomer( string id ):  
  
  //"Do It“ -> HTTP PUT  
  [WebInvoke( UriTemplate="customers/{id}", Method="PUT" )]  
  Customer UpdateCustomer( string id, Customer newCustomer );  
}  
```  
  
 若要查看使用 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] WEB HTTP 编程模型的 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 服务的完整示例，请参见[如何：创建基本 WCF Web HTTP 服务](../../../../docs/framework/wcf/feature-details/how-to-create-a-basic-wcf-web-http-service.md)  
  
## UriTemplate 查询字符串参数和 URL  
 可以通过键入与服务操作相关联的 URL 来从 Web 浏览器调用 Web 样式服务。这些服务操作可以采用查询字符串参数，必须在 URL 内使用字符串格式指定这些参数。下表演示可以在 URL 内传递的类型和使用的格式。  
  
|类型|格式|  
|--------|--------|  
|<xref:System.Byte>|0 \- 255|  
|<xref:System.SByte>|\-128 \- 127|  
|<xref:System.Int16>|\-32768 \- 32767|  
|<xref:System.Int32>|\-2,147,483,648 \- 2,147,483,647|  
|<xref:System.Int64>|\-9,223,372,036,854,775,808 \- 9,223,372,036,854,775,807|  
|<xref:System.UInt16>|0 \- 65535|  
|<xref:System.UInt32>|0 \- 4,294,967,295|  
|<xref:System.UInt64>|0 \- 18,446,744,073,709,551,615|  
|<xref:System.Single>|\-3.402823e38 \- 3.402823e38（不需要指数表示法）|  
|<xref:System.Double>|\-1.79769313486232e308 \- 1.79769313486232e308（不需要指数表示法）|  
|<xref:System.Char>|任何单个字符|  
|<xref:System.Decimal>|使用标准表示法的任何小数（无指数）|  
|<xref:System.Boolean>|True 或 False（不区分大小写）|  
|<xref:System.String>|任何字符串（不支持空字符串，且不进行转义）|  
|<xref:System.DateTime>|MM\/DD\/YYYY<br /><br /> MM\/DD\/YYYY HH:MM:SS \[AM&#124;PM\]<br /><br /> 月、日、年<br /><br /> 月、日、年 HH:MM:SS \[AM&#124;PM\]|  
|<xref:System.TimeSpan>|DD.HH:MM:SS<br /><br /> 此处，DD \= 天、HH \= 小时、MM \= 分钟、SS \= 秒钟|  
|<xref:System.Guid>|一个 GUID，例如：<br /><br /> 936DA01F\-9ABD\-4d9d\-80C7\-02AF85C822A8|  
|<xref:System.DateTimeOffset>|MM\/DD\/YYYY HH:MM:SS MM:SS<br /><br /> 此处，DD \= 天、HH \= 小时、MM \= 分钟、SS \= 秒钟|  
|枚举|例如，定义枚举的枚举值，如以下代码中所示。<br /><br /> `public enum Days{ Sunday, Monday, Tuesday, Wednesday, Thursday, Friday, Saturday };`<br /><br /> 可以在查询字符串中指定任何单独的枚举值（或其对应的整数值）。|  
|具有可在类型和字符串表示形式之间来回进行转换的 `TypeConverterAttribute` 的类型。|取决于类型转换器。|  
  
## 格式和 WCF WEB HTTP 编程模型  
 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] WEB HTTP 编程模型具有一些可以处理许多不同的数据格式的新功能。在绑定层上，<xref:System.ServiceModel.WebHttpBinding> 可以读取和写入下列不同种类的数据：  
  
-   XML  
  
-   JSON  
  
-   不透明二进制流  
  
 这意味着 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] WEB HTTP 编程模型可以处理任何类型的数据，但是您可能会对 <xref:System.IO.Stream> 进行编程。  
  
 [!INCLUDE[netfx35_short](../../../../includes/netfx35-short-md.md)] 支持 JSON 数据 \(AJAX\) 和联合源（包括 ATOM 和 RSS）。[!INCLUDE[crabout](../../../../includes/crabout-md.md)]这些功能的更多信息，请参见 [WCF Web HTTP 格式设置](../../../../docs/framework/wcf/feature-details/wcf-web-http-formatting.md)[WCF 联合概述](../../../../docs/framework/wcf/feature-details/wcf-syndication-overview.md) 和 [AJAX 集成和 JSON 支持](../../../../docs/framework/wcf/feature-details/ajax-integration-and-json-support.md)。  
  
## WCF WEB HTTP 编程模型和安全  
 由于 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] WEB HTTP 编程模型不支持 WS\-\* 协议，因此保证 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] WEB HTTP 服务安全的唯一方式是使用 SSL 通过 HTTPS 公开服务。[!INCLUDE[crabout](../../../../includes/crabout-md.md)]使用 [!INCLUDE[iisver](../../../../includes/iisver-md.md)] 设置 SSL 的更多信息，请参见[如何在 IIS 中实现 SSL](http://go.microsoft.com/fwlink/?LinkId=131613)  
  
## WCF WEB HTTP 编程模型疑难解答  
 当使用 <xref:System.ServiceModel.Channels.ChannelFactory%601> 调用 WCF WEB HTTP 服务以创建通道时，即使将其他 <xref:System.ServiceModel.EndpointAddress> 传递给 <xref:System.ServiceModel.Channels.ChannelFactory%601>，<xref:System.ServiceModel.Description.WebHttpBehavior> 也会使用配置文件中设置的 <xref:System.ServiceModel.EndpointAddress>。  
  
## 请参阅  
 [WCF 联合](../../../../docs/framework/wcf/feature-details/wcf-syndication.md)   
 [WCF Web HTTP 编程对象模型](../../../../docs/framework/wcf/feature-details/wcf-web-http-programming-object-model.md)   
 [WCF Web HTTP 编程模型](../../../../docs/framework/wcf/feature-details/wcf-web-http-programming-model.md)