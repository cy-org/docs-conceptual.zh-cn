---
title: "独立诊断源示例 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: d31c6c1f-292c-4d95-8e23-ed8565970ea5
caps.latest.revision: 26
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 26
---
# 独立诊断源示例
此示例演示如何创建一个 RSS\/Atom 源，以便与 [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] 整合。  它是一个基本的“Hello World”程序，演示了对象模型的基础知识以及如何在 [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] 服务上设置对象模型。  
  
 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 以服务操作的形式建立整合源的模型，这些服务操作返回一个特殊的数据类型：<xref:System.ServiceModel.Syndication.SyndicationFeedFormatter>。  <xref:System.ServiceModel.Syndication.SyndicationFeedFormatter> 的实例可以将源序列化为 RSS 2.0 和 Atom 1.0 格式。  下面的示例代码演示所使用的协定。  
  
```  
[ServiceContract(Namespace = "")]  
    interface IDiagnosticsService  
    {  
        [OperationContract]  
        //The [WebGet] attribute controls how WCF dispatches  
        //HTTP requests to service operations based on a URI suffix  
        //(the part of the request URI after the endpoint address)  
        //using the HTTP GET method. The UriTemplate specifies a relative  
        //path of 'feed', and specifies that the format is  
        //supplied using a query string.   
        [WebGet(UriTemplate="feed?format={format}")]  
        [ServiceKnownType(typeof(Atom10FeedFormatter))]  
        [ServiceKnownType(typeof(Rss20FeedFormatter))]  
        SyndicationFeedFormatter GetProcesses(string format);  
    }  
```  
  
 使用 <xref:System.ServiceModel.Web.WebGetAttribute> 属性对 `GetProcesses` 操作进行批注，该属性使您能够控制 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 如何向服务操作发出 HTTP GET 请求并指定所发送消息的格式。  
  
 如同任何 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 服务一样，联合源可以自承载于任何托管应用程序中。  联合服务需要使用特定绑定 \(<xref:System.ServiceModel.WebHttpBinding>\) 和特定终结点行为 \(<xref:System.ServiceModel.Description.WebHttpBehavior>\) 才能正常运行。  新的 <xref:System.ServiceModel.Web.WebServiceHost> 类提供了一个方便的 API，用于在不使用特定配置的情况下创建此类终结点。  
  
```  
WebServiceHost host = new WebServiceHost(typeof(ProcessService), new Uri("http://localhost:8000/diagnostics"));  
  
            //The WebServiceHost will automatically provide a default endpoint at the base address  
            //using the proper binding (the WebHttpBinding) and endpoint behavior (the WebHttpBehavior)  
```  
  
 或者，可在 IIS 承载的 .svc 文件中使用 <xref:System.ServiceModel.Activation.WebServiceHostFactory> 来提供等效的功能（此技术未在此示例代码中演示）。  
  
```  
<%@ ServiceHost Language="C#|VB" Debug="true" Service="ProcessService" %>  
```  
  
 由于此服务使用标准 HTTP GET 接收请求，因此可以使用任何识别 RSS 或 ATOM 的客户端来访问此服务。  例如，可以通过在识别 RSS 的浏览器（如 Internet Explorer 7）中导航到 http:\/\/localhost:8000\/diagnostics\/feed\/?format\=atom 或 http:\/\/localhost:8000\/diagnostics\/feed\/?format\=rss 来查看此服务的输出。  
  
 还可以使用 [WCF 联合对象模型如何映射到 Atom 和 RSS](../../../../docs/framework/wcf/feature-details/how-the-wcf-syndication-object-model-maps-to-atom-and-rss.md)，通过命令性代码读取联合数据并对其进行处理。  
  
```  
XmlReader reader = XmlReader.Create( "http://localhost:8000/diagnostics/feed/?format=rss",  
new XmlReaderSettings()  
{  
//MaxCharactersInDocument can be used to control the maximum amount of data   
//read from the reader and helps prevent OutOfMemoryException  
MaxCharactersInDocument = 1024 * 64  
} );  
  
SyndicationFeed feed = SyndicationFeed.Load( reader );  
  
foreach (SyndicationItem i in feed.Items)  
{  
        XmlSyndicationContent content = i.Content as XmlSyndicationContent;  
        ProcessData pd = content.ReadContent<ProcessData>();  
  
        Console.WriteLine(i.Title.Text);  
        Console.WriteLine(pd.ToString());  
}  
```  
  
### 设置、生成和运行示例  
  
1.  在 [Windows Communication Foundation 示例的一次性安装过程](../../../../docs/framework/wcf/samples/one-time-setup-procedure-for-the-wcf-samples.md)中的安装说明中介绍的计算机上，确保您对于 HTTP 和 HTTPS 具有正确的地址注册权限。  
  
2.  生成解决方案。  
  
3.  运行控制台应用程序。  
  
4.  当控制台应用程序正在运行时，使用识别 RSS 的浏览器导航到 http:\/\/localhost:8000\/diagnostics\/feed\/?format\=atom 或 http:\/\/localhost:8000\/diagnostics\/feed\/?format\=rss。  
  
> [!IMPORTANT]
>  您的计算机上可能已安装这些示例。  在继续操作之前，请先检查以下（默认）目录：  
>   
>  `<安装驱动器>:\WF_WCF_Samples`  
>   
>  如果此目录不存在，请访问[针对 .NET Framework 4 的 Windows Communication Foundation \(WCF\) 和 Windows Workflow Foundation \(WF\) 示例](http://go.microsoft.com/fwlink/?LinkId=150780)（可能为英文网页），下载所有 [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] 和 [!INCLUDE[wf1](../../../../includes/wf1-md.md)] 示例。  此示例位于以下目录：  
>   
>  `<安装驱动器>:\WF_WCF_Samples\WCF\Basic\Syndication\DiagnosticsFeed`  
  
## 请参阅  
 [WCF Web HTTP 编程模型](../../../../docs/framework/wcf/feature-details/wcf-web-http-programming-model.md)   
 [WCF 联合](../../../../docs/framework/wcf/feature-details/wcf-syndication.md)