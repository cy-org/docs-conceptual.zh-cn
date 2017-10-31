---
title: "WCF Web HTTP 格式设置 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: e2414896-5463-41cd-b0a6-026a713eac2c
caps.latest.revision: 8
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 8
---
# WCF Web HTTP 格式设置
通过 WCF Web HTTP 编程模型，您可以动态确定服务操作返回其响应所采用的最佳格式。  支持使用以下两种方法来确定相应格式：即自动和显式。  
  
## 自动格式设置  
 启用后，自动格式设置将选择返回响应所采用的最佳格式。  该功能按以下顺序检查下列各项，以此来确定最佳格式：  
  
1.  请求消息的 Accept 标头中的媒体类型。  
  
2.  请求消息的内容类型。  
  
3.  操作中的默认格式设置。  
  
4.  WebHttpBehavior 中的默认格式设置。  
  
 如果请求消息包含 Accept 标头，[!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] 基础结构将搜索其支持的类型。  如果 `Accept` 标头指定了其媒体类型的优先级，则会遵循这些优先级。  如果未在 `Accept` 标头中找到适当的格式，则使用请求消息的内容类型。  如果未指定适当的内容类型，则使用操作的默认格式设置。  默认格式使用 <xref:System.ServiceModel.Web.WebGetAttribute> 和 <xref:System.ServiceModel.Web.WebInvokeAttribute> 特性的 `ResponseFormat` 参数设置。  如果未对操作指定默认格式，则使用 <xref:System.ServiceModel.Description.WebHttpBehavior.DefaultOutgoingResponseFormat%2A> 属性的值。  自动格式设置依赖于 <xref:System.ServiceModel.Description.WebHttpBehavior.AutomaticFormatSelectionEnabled%2A> 属性。  如果此属性设置为 `true`，[!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 基础结构将确定要使用的最佳格式。  默认情况下，禁用自动格式选择，以保证向后兼容性。  可以通过编程方式或配置启用自动格式选择。  下面的示例演示如何在代码中启用自动格式选择。  
  
```  
// This code assumes the service name is MyService and the service contract is IMyContract     
Uri baseAddress = new Uri("http://localhost:8000");  
  
WebServiceHost host = new WebServiceHost(typeof(MyService), baseAddress)  
try  
{  
   ServiceEndpoint sep = host.AddServiceEndpoint(typeof(IMyContract), new WebHttpBinding(), "");  
   // Check it see if the WebHttpBehavior already exists  
   WebHttpBehavior whb = sep.Behaviors.Find<WebHttpBehavior>();  
  
   if (whb != null)  
   {  
      whb.AutomaticFormatSelectionEnabled = true;  
   }  
   else  
   {  
      WebHttpBehavior webBehavior = new WebHttpBehavior();  
      webBehavior.AutomaticFormatSelectionEnabled = true;  
      sep.Behaviors.Add(webBehavior);  
   }  
         // Open host to start listening for messages  
   host.Open();        
  
  // ...  
}  
  catch(CommunicationException ex)  
  {  
     Console.WriteLine(“An exception occurred: “ + ex.Message());  
  }  
  
```  
  
 还可通过配置启用自动格式设置。  您可以直接在 <xref:System.ServiceModel.Description.WebHttpBehavior> 上设置 <xref:System.ServiceModel.Description.WebHttpBehavior.AutomaticFormatSelectionEnabled%2A> 属性，也可以使用 <xref:System.ServiceModel.Description.WebHttpEndpoint> 进行设置。  下面的示例演示如何在 <xref:System.ServiceModel.Description.WebHttpBehavior> 上启用自动格式选择。  
  
```  
<system.serviceModel>  
  <behaviors>  
    <endpointBehaviors>  
      <behavior>  
        <webHttp automaticFormatSelectionEnabled="true" />  
      </behavior>  
    </endpointBehaviors>  
  </behaviors>  
  <standardEndpoints>  
    <webHttpEndpoint>  
      <!-- the "" standard endpoint is used by WebServiceHost for auto creating a web endpoint. -->  
      <standardEndpoint name="" helpEnabled="true" />  
    </webHttpEndpoint>  
  </standardEndpoints>  
</system.serviceModel>  
```  
  
 下面的示例演示如何使用 <xref:System.ServiceModel.Description.WebHttpEndpoint> 启用自动格式选择。  
  
```  
<system.serviceModel>  
    <standardEndpoints>  
      <webHttpEndpoint>  
        <!-- the "" standard endpoint is used by WebServiceHost for auto creating a web endpoint. -->  
        <standardEndpoint name="" helpEnabled="true" automaticFormatSelectionEnabled="true"  />  
      </webHttpEndpoint>  
    </standardEndpoints>  
  </system.serviceModel>  
```  
  
## 显式格式设置  
 顾名思义，在显式格式设置过程中，开发人员在操作代码中确定要使用的最佳格式。  如果最佳格式为 XML 或 JSON，开发人员会将 <xref:System.ServiceModel.Web.OutgoingWebResponseContext.Format%2A> 设置为 <xref:System.ServiceModel.Web.WebMessageFormat> 或 <xref:System.ServiceModel.Web.WebMessageFormat>。  如果未显式设置 <xref:System.ServiceModel.Web.OutgoingWebResponseContext.Format%2A> 属性，则使用操作的默认格式。  
  
 下面的示例检查格式查询字符串参数，以获取要采用的格式。  如果已指定该参数，则使用 <xref:System.ServiceModel.Web.OutgoingWebResponseContext.Format%2A> 设置操作的格式。  
  
```  
public class Service : IService  
{  
    [WebGet]  
     public string EchoWithGet(string s)  
    {  
         // if a format query string parameter has been specified, set the response format to that. If no such  
         // query string parameter exists the Accept header will be used  
        string formatQueryStringValue = WebOperationContext.Current.IncomingRequest.UriTemplateMatch.QueryParameters["format"];  
        if (!string.IsNullOrEmpty(formatQueryStringValue))  
        {  
             if (formatQueryStringValue.Equals("xml", System.StringComparison.OrdinalIgnoreCase))  
             {  
                  WebOperationContext.Current.OutgoingResponse.Format = WebMessageFormat.Xml;  
             }  
             else if (formatQueryStringValue.Equals("json", System.StringComparison.OrdinalIgnoreCase))  
            {  
                WebOperationContext.Current.OutgoingResponse.Format = WebMessageFormat.Json;  
            }  
            else  
            {  
                 throw new WebFaultException<string>(string.Format("Unsupported format '{0}'", formatQueryStringValue), HttpStatusCode.BadRequest);  
            }  
        }  
        return "You said " + s;  
    }  
```  
  
 如果您需要支持除 XML 或 JSON 以外的其他格式，请定义您的操作，并将返回类型设置为 <xref:System.ServiceModel.Channels.Message>。  在操作代码中，确定要使用的相应格式，然后使用下列方法之一创建 <xref:System.ServiceModel.Channels.Message> 对象：  
  
-   `WebOperationContext.CreateAtom10Response`  
  
-   `WebOperationContext.CreateJsonResponse`  
  
-   `WebOperationContext.CreateStreamResponse`  
  
-   `WebOperationContext.CreateTextResponse`  
  
-   `WebOperationContext.CreateXmlResponse`  
  
 上述每种方法都会采取相应内容，并创建具有相应格式的消息。  `WebOperationContext.Current.IncomingRequest.GetAcceptHeaderElements` 方法可用于获取客户端首选格式的列表（按首选项的降序顺序）。  下面的示例演示如何使用 `WebOperationContext.Current.IncomingRequest.GetAcceptHeaderElements` 确定要使用的格式，然后使用相应的响应创建方法创建响应消息。  
  
```  
  
public class Service : IService  
{  
    public Message EchoListWithGet(string list)  
    {  
        List<string> returnList = new List<string>(list.Split(new char[] { ',' }, StringSplitOptions.RemoveEmptyEntries));  
        IList<ContentType> acceptHeaderElements = WebOperationContext.Current.IncomingRequest.GetAcceptHeaderElements();  
        for (int x = 0; x < acceptHeaderElements.Count; x++)  
        {  
            string normalizedMediaType = acceptHeaderElements[x].MediaType.ToLowerInvariant();  
            switch (normalizedMediaType)  
            {  
                case "image/jpeg": return CreateJpegResponse(returnList);  
                case "application/xhtml+xml": return CreateXhtmlResponse(returnList);  
                case "application/atom+xml": return CreateAtom10Response(returnList);  
                case "application/xml": return CreateXmlResponse(returnList);  
                case "application/json": return CreateJsonResponse(returnList);  
          }  
    }  
  
    // Default response format is XML  
    return CreateXmlResponse(returnList);  
    }  
}  
  
```  
  
## 请参阅  
 <xref:System.UriTemplate>   
 <xref:System.UriTemplateMatch>   
 [WCF Web HTTP 编程模型](../../../../docs/framework/wcf/feature-details/wcf-web-http-programming-model.md)   
 [UriTemplate 和 UriTemplateTable](../../../../docs/framework/wcf/feature-details/uritemplate-and-uritemplatetable.md)   
 [WCF Web HTTP 编程模型概述](../../../../docs/framework/wcf/feature-details/wcf-web-http-programming-model-overview.md)   
 [WCF Web HTTP 编程对象模型](../../../../docs/framework/wcf/feature-details/wcf-web-http-programming-object-model.md)