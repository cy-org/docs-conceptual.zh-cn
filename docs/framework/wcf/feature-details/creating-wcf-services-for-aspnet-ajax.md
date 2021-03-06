---
title: "为 ASP.NET AJAX 创建 WCF 服务 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 04c0402c-e617-4ba5-aedf-d17692234776
caps.latest.revision: 18
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 18
---
# 为 ASP.NET AJAX 创建 WCF 服务
使用 Microsoft ASP.NET AJAX，可以通过快速响应的熟悉用户界面元素快速创建包括丰富用户体验的网页。ASP.NET AJAX 提供了并入跨浏览器 ECMAScript \(JavaScript\) 和动态 HTML \(DHTML\) 技术的客户端脚本库，并将其与基于 ASP.NET 2.0 服务器的开发平台集成在一起。通过使用 ASP.NET AJAX，可以改进用户体验和 Web 应用程序的效率。  
  
 ASP.NET AJAX 由客户端脚本库和集成的服务器组件组成，以提供稳定的开发框架。从 ASP.NET 页访问服务：将服务 URL 添加到页上的 ASP.NET 脚本管理器控件后，就可以使用看起来与常规 JavaScript 函数调用完全相同的 JavaScript 代码调用服务操作。有关 AJAX 框架中 Web 服务的用法，请参见[了解 ASP.NET AJAX](http://go.microsoft.com/fwlink/?LinkId=186475)（可能为英文网页）。  
  
 通过添加相应的 ASP.NET AJAX 终结点，可以将大多数 [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] 服务作为与 ASP.NET AJAX 兼容的服务公开。  
  
 如果使用的是 Visual Studio，则在处理 ASP.NET 网站或 Web 应用程序时可以使用启用了 AJAX 的 WCF 服务的预建模板（可以从**“添加新项目”**对话框访问）。  
  
 如果未使用 Visual Studio 模板，则创建 ASP.NET AJAX 终结点有以下两种方法：  
  
-   使用动态主机激活（而不使用任何配置）创建终结点。如果您不熟悉 WCF 配置系统，则这是最基本的方法。[!INCLUDE[crdefault](../../../../includes/crdefault-md.md)][如何：在不使用配置的情况下添加 ASP.NET AJAX 终结点](../../../../docs/framework/wcf/feature-details/how-to-add-an-aspnet-ajax-endpoint-without-using-configuration.md).  
  
-   使用配置将启用了 AJAX 的终结点添加到 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 服务。[!INCLUDE[crdefault](../../../../includes/crdefault-md.md)][如何：使用配置来添加 ASP.NET AJAX 终结点](../../../../docs/framework/wcf/feature-details/how-to-use-configuration-to-add-an-aspnet-ajax-endpoint.md).  
  
 [WCF Web HTTP 编程模型概述](../../../../docs/framework/wcf/feature-details/wcf-web-http-programming-model-overview.md)中所述的 Web 编程模型可能用于 ASP.NET AJAX 服务。尤其是在下列情况下：  
  
-   可以使用 <xref:System.ServiceModel.Web.WebGetAttribute> 和 <xref:System.ServiceModel.Web.WebInvokeAttribute> 属性在 HTTP GET 和 HTTP POST 动词之间进行选择。如果正确使用它们，则这可能会大大提高应用程序的性能。[!INCLUDE[crdefault](../../../../includes/crdefault-md.md)][如何：在 ASP.NET AJAX 终结点的 HTTP POST 和 HTTP GET 请求之间进行选择](../../../../docs/framework/wcf/feature-details/http-post-and-http-get-requests-for-aspnet-ajax-endpoints.md).  
  
-   可以使用 <xref:System.ServiceModel.Web.WebGetAttribute.ResponseFormat%2A> 和 <xref:System.ServiceModel.Web.WebInvokeAttribute.ResponseFormat%2A> 属性使服务返回 XML 数据而不是默认的 Javascript 对象表示法 \(JSON\)。使用 ASP.NET AJAX 框架执行此操作可导致 JavaScript 客户端接收 XML DOM 对象。  
  
    > [!WARNING]
    >  您的操作必须将内容类型设置为文本\/xml 才能生效。否则，JavaScript 客户端会接收包含 XML 的字符串而不是 XML DOM 对象。  
  
     下面是返回正确设置了内容类型的 XML 数据的操作示例：  
  
    ```  
    [OperationContract, WebGet(ResponseFormat=WebMessageFormat.Xml)]  
    public XElement GetData()  
    {  
    XElement x;  
    //Get some data here...  
  
    WebOperationContext.Current.OutgoingResponse.ContentType = "text/xml";      
    return x;  
    }  
  
    ```  
  
-   如果要求与 ASP.NET AJAX 兼容，则不能更改 <xref:System.ServiceModel.Web.WebGetAttribute> 和 <xref:System.ServiceModel.Web.WebInvokeAttribute> 特性上的任何其他属性。只要不违反 ASP.NET AJAX 调用约定，就可以使用 Web 编程模型的其他方面。  
  
 更高级的方案要求了解 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 中 AJAX 支持的某些其他详细信息：  
  
-   若要了解如何使用 JavaScript 在 AJAX 页客户端和 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 服务之间传输数据，以及有关 .NET Framework 类型如何映射到 JavaScript 类型的详细信息，请参见[对 JSON 和其他数据传输格式的支持](../../../../docs/framework/wcf/feature-details/support-for-json-and-other-data-transfer-formats.md)。  
  
-   若要利用 ASP.NET 功能（例如，基于 URL 的身份验证和访问 ASP.NET 会话信息），可能希望通过配置启用 ASP.NET 兼容性模式。  
  
 甚至在没有 ASP.NET AJAX 框架时，也可能使用 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 中的 AJAX 终结点。执行此操作需要了解 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 中 AJAX 支持的支持体系结构。有关此体系结构的讨论，请参见 [WCF Web HTTP 编程对象模型](../../../../docs/framework/wcf/feature-details/wcf-web-http-programming-object-model.md)。有关演示此方法的代码示例，请参见 [具有 JSON 和 XML 的 AJAX 服务](../../../../docs/framework/wcf/samples/ajax-service-with-json-and-xml-sample.md)。  
  
## 请参阅  
 [WCF Web HTTP 编程模型](../../../../docs/framework/wcf/feature-details/wcf-web-http-programming-model.md)   
 [如何：在不使用配置的情况下添加 ASP.NET AJAX 终结点](../../../../docs/framework/wcf/feature-details/how-to-add-an-aspnet-ajax-endpoint-without-using-configuration.md)   
 [如何：使用配置来添加 ASP.NET AJAX 终结点](../../../../docs/framework/wcf/feature-details/how-to-use-configuration-to-add-an-aspnet-ajax-endpoint.md)   
 [如何：在 ASP.NET AJAX 终结点的 HTTP POST 和 HTTP GET 请求之间进行选择](../../../../docs/framework/wcf/feature-details/http-post-and-http-get-requests-for-aspnet-ajax-endpoints.md)