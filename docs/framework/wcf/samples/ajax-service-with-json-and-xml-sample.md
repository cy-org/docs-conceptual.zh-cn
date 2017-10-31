---
title: "具有 JSON 和 XML 的 AJAX 服务示例 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 8ea5860d-0c42-4ae9-941a-e07efdd8e29c
caps.latest.revision: 15
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 15
---
# 具有 JSON 和 XML 的 AJAX 服务示例
此示例演示如何使用 [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] 来创建异步 JavaScript 和 XML \(AJAX\) 服务，该服务返回 JavaScript 对象表示法 \(JSON\) 或 XML 数据。可以从 Web 浏览器客户端使用 JavaScript 代码来访问 AJAX 服务。此示例是基于[基本 AJAX 服务](../../../../docs/framework/wcf/samples/basic-ajax-service.md)示例生成的。  
  
 与其他 AJAX 示例不同的是，此示例不使用 ASP.NET AJAX 和 <xref:System.Web.UI.ScriptManager> 控件。在某个其他配置下，[!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] AJAX 服务可以从任何 HTML 页面通过 JavaScript 来访问，此处对该方案进行了演示。有关将 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 与 ASP.NET AJAX 一起使用的示例，请参见 [AJAX Samples](http://msdn.microsoft.com/zh-cn/f3fa45b3-44d5-4926-8cc4-a13c30a3bf3e)。  
  
 此示例演示如何在 JSON 和 XML 之间切换操作的响应类型。无论服务是配置为由 ASP.NET AJAX 访问还是由 HTML\/JavaScript 客户端页面访问，此功能均可用。  
  
> [!NOTE]
>  本主题的最后介绍了此示例的设置过程和生成说明。  
  
 若要能够使用非 ASP.NET AJAX 客户端，请在 .svc 文件中使用 <xref:System.ServiceModel.Activation.WebServiceHostFactory>（不是 <xref:System.ServiceModel.Activation.WebScriptServiceHostFactory>）。<xref:System.ServiceModel.Activation.WebServiceHostFactory> 添加 <xref:System.ServiceModel.Description.WebHttpEndpoint> 标准终结点到服务中。终结点配置在一个相对于 .svc 文件的空地址；这意味着服务的地址是 http:\/\/localhost\/ServiceModelSamples\/service.svc，除了操作名以外没有其他后缀。  
  
```html  
<%@ServiceHost language="c#" Debug="true" Service="Microsoft.Samples.XmlAjaxService.CalculatorService" Factory="System.ServiceModel.Activation.WebServiceHostFactory" %>  
  
```  
  
 可以使用 Web.config 中的以下节对终结点进行其他配置更改。如果不需要额外更改，则可以移除该节。  
  
```xml  
<system.serviceModel>  
  <standardEndpoints>  
    <webHttpEndpoint>  
      <!-- Use this element to configure the endpoint -->  
      <standardEndpoint name="" />  
    </webHttpEndpoint>  
  </standardEndpoints>  
</system.serviceModel>  
  
```  
  
 <xref:System.ServiceModel.Description.WebHttpEndpoint> 的默认数据格式为 XML，而 [for T:System.ServiceModel.Description.WebScriptEndpoint](assetId:///for T:System.ServiceModel.Description.WebScriptEndpoint?qualifyHint=False&autoUpgrade=True) 的默认数据格式为 JSON。有关更多信息，请参见[创建不使用 ASP.NET 的 WCF AJAX 服务](../../../../docs/framework/wcf/feature-details/creating-wcf-ajax-services-without-aspnet.md)。  
  
 以下示例中的服务是一个标准的 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 服务，它具有两个操作。这两个操作都需要针对 <xref:System.ServiceModel.Web.WebGetAttribute> 或 <xref:System.ServiceModel.Web.WebInvokeAttribute> 属性使用 <xref:System.ServiceModel.Web.WebMessageBodyStyle> 正文样式，该样式特定于 `webHttp` 行为，对于 JSON\/XML 数据格式开关没有任何影响。  
  
```  
[OperationContract]  
[WebInvoke(ResponseFormat = WebMessageFormat.Xml, BodyStyle = WebMessageBodyStyle.Wrapped)]  
MathResult DoMathXml(double n1, double n2);  
```  
  
 操作的响应格式被指定为 XML，这是 [\<webHttp\>](../../../../docs/framework/configure-apps/file-schema/wcf/webhttp.md) 行为的默认设置。但是，最好显式指定响应格式。  
  
 另一个操作使用 `WebInvokeAttribute` 属性并显式指定响应的 JSON（而不是 XML）。  
  
```  
[OperationContract]  
[WebInvoke(ResponseFormat = WebMessageFormat.Json, BodyStyle = WebMessageBodyStyle.Wrapped)]  
MathResult DoMathJson(double n1, double n2);  
```  
  
 请注意，在这两种情况下，操作均返回一个复杂类型 `MathResult`，该类型是一个标准的 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 数据协定类型。  
  
 客户端网页 XmlAjaxClientPage.htm 包含 JavaScript 代码，当用户单击页面上的**“Perform calculation \(return JSON\)”（执行计算\(返回 JSON\)）**或**“Perform calculation \(return XML\)”（执行计算\(返回 XML\)）**按钮时，该代码会调用上面的两个操作之一。用来调用服务的代码将构造 JSON 正文并使用 HTTP POST 发送它。请求是用 JavaScript 手动创建的，这与[基本 AJAX 服务](../../../../docs/framework/wcf/samples/basic-ajax-service.md)示例和使用 ASP.NET AJAX 的其他示例不同。  
  
```  
// Create HTTP request  
var xmlHttp;  
// Request instantiation code omitted…  
// Result handler code omitted…  
  
// Build the operation URL  
var url = "service.svc/ajaxEndpoint/";  
url = url + operation;  
  
// Build the body of the JSON message  
var body = '{"n1":';  
body = body + document.getElementById("num1").value + ',"n2":';  
body = body + document.getElementById("num2").value + '}';  
  
// Send the HTTP request  
xmlHttp.open("POST", url, true);  
xmlHttp.setRequestHeader("Content-type", "application/json");  
xmlHttp.send(body);  
```  
  
 当服务进行响应时，响应将显示出来，而不会在页面上的文本框中进一步执行任何处理。这是为了进行演示而实现的，您可以直接遵循所使用的 XML 和 JSON 数据格式。  
  
```  
// Create result handler   
xmlHttp.onreadystatechange=function(){  
     if(xmlHttp.readyState == 4){  
          document.getElementById("result").value = xmlHttp.responseText;  
     }  
}  
```  
  
> [!IMPORTANT]
>  您的计算机上可能已安装这些示例。在继续操作之前，请先检查以下（默认）目录。  
>   
>  `<安装驱动器>:\WF_WCF_Samples`  
>   
>  如果此目录不存在，请访问[针对 .NET Framework 4 的 Windows Communication Foundation \(WCF\) 和 Windows Workflow Foundation \(WF\) 示例](http://go.microsoft.com/fwlink/?LinkId=150780)（可能为英文网页），下载所有 [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] 和 [!INCLUDE[wf1](../../../../includes/wf1-md.md)] 示例。此示例位于以下目录。  
>   
>  `<安装驱动器>:\WF_WCF_Samples\WCF\Basic\AJAX\XmlAjaxService`  
  
#### 设置、生成和运行示例  
  
1.  请确保已经执行了 [Windows Communication Foundation 示例的一次性安装过程](../../../../docs/framework/wcf/samples/one-time-setup-procedure-for-the-wcf-samples.md)。  
  
2.  按照[生成 Windows Communication Foundation 示例](../../../../docs/framework/wcf/samples/building-the-samples.md)中的说明生成解决方案 XmlAjaxService.sln。  
  
3.  定位到 http:\/\/localhost\/ServiceModelSamples\/XmlAjaxClientPage.htm（不要在浏览器中从项目目录中打开 XmlAjaxClientPage.htm）。  
  
## 请参阅  
 [使用 HTTP POST 的 AJAX 服务](../../../../docs/framework/wcf/samples/ajax-service-using-http-post.md)