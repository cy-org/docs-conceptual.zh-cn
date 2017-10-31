---
title: "如何：创建基本 WCF Web HTTP 服务 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 877662d3-d372-4e08-b417-51f66a0095cd
caps.latest.revision: 26
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 26
---
# 如何：创建基本 WCF Web HTTP 服务
[!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] 允许您创建公开 Web 终结点的服务。Web 终结点通过 XML 或 JSON 发送数据，没有 SOAP 信封。本主题演示如何公开这类终结点。  
  
> [!NOTE]
>  确保 Web 终结点安全的唯一方式是使用传输安全通过 HTTPS 将其公开。使用基于消息的安全性时，通常将安全信息放置在 SOAP 标头中，原因是发送到非 SOAP 终结点的信息不包含 SOAP 信封，没有地方放置安全信息，因而必须依赖于传输安全性。  
  
### 创建 Web 终结点  
  
1.  使用以 <xref:System.ServiceModel.ServiceContractAttribute>, <xref:System.ServiceModel.Web.WebInvokeAttribute> 和 <xref:System.ServiceModel.Web.WebGetAttribute> 特性标记的接口来定义服务协定。  
  
     [!code-csharp[htBasicService#0](../../../../samples/snippets/csharp/VS_Snippets_CFX/htbasicservice/cs/service.cs#0)]
     [!code-vb[htBasicService#0](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/htbasicservice/vb/service.vb#0)]  
  
    > [!NOTE]
    >  默认情况下，<xref:System.ServiceModel.Web.WebInvokeAttribute> 将 POST 调用映射到操作。但是，可以通过指定“方法\=”参数指定要映射到操作的 HTTP 方法（例如，HEAD、PUT 或 DELETE）。<xref:System.ServiceModel.Web.WebGetAttribute> 不具有“方法\=”参数，并且仅将 GET 调用映射到服务操作。  
  
2.  实现服务协定。  
  
     [!code-csharp[htBasicService#1](../../../../samples/snippets/csharp/VS_Snippets_CFX/htbasicservice/cs/service.cs#1)]
     [!code-vb[htBasicService#1](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/htbasicservice/vb/service.vb#1)]  
  
### 承载服务  
  
1.  创建 <xref:System.ServiceModel.Web.WebServiceHost> 对象。  
  
     [!code-csharp[htBasicService#2](../../../../samples/snippets/csharp/VS_Snippets_CFX/htbasicservice/cs/service.cs#2)]
     [!code-vb[htBasicService#2](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/htbasicservice/vb/service.vb#2)]  
  
2.  添加一个带有 <xref:System.ServiceModel.Description.ServiceEndpoint> 的 <xref:System.ServiceModel.Description.WebHttpBehavior>。  
  
     [!code-csharp[htBasicService#3](../../../../samples/snippets/csharp/VS_Snippets_CFX/htbasicservice/cs/service.cs#3)]
     [!code-vb[htBasicService#3](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/htbasicservice/vb/service.vb#3)]  
  
    > [!NOTE]
    >  如果不添加终结点，则 <xref:System.ServiceModel.Web.WebServiceHost> 自动创建默认终结点。<xref:System.ServiceModel.Web.WebServiceHost> 还添加 <xref:System.ServiceModel.Description.WebHttpBehavior>并禁用 HTTP 帮助页和 Web 服务描述语言 \(WSDL\) GET 功能，因此元数据终结点不会影响默认的 HTTP 终结点。  
    >   
    >  当尝试调用终结点上的操作时，添加 URL 为 "" 的非 SOAP 终结点会导致意外行为。其原因是终结点的侦听 URI 与帮助页（在浏览到 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 服务的基址时显示的页）的 URI 相同。  
  
     要防止此类情况发生，可以执行下列操作之一：  
  
    -   总是为非 SOAP 终结点指定非空白 URI。  
  
    -   关闭帮助页。这可以通过以下代码来实现。  
  
     [!code-csharp[htBasicService#4](../../../../samples/snippets/csharp/VS_Snippets_CFX/htbasicservice/cs/snippets.cs#4)]
     [!code-vb[htBasicService#4](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/htbasicservice/vb/snippets.vb#4)]  
  
3.  打开服务主机并等待用户按 Enter。  
  
     [!code-csharp[htBasicService#5](../../../../samples/snippets/csharp/VS_Snippets_CFX/htbasicservice/cs/snippets.cs#5)]
     [!code-vb[htBasicService#5](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/htbasicservice/vb/snippets.vb#5)]  
  
     此示例演示如何使用控制台应用程序来承载 Web 样式服务。还可以在 IIS 内承载这类服务。为此，在 .svc 文件中指定 <xref:System.ServiceModel.Activation.WebServiceHostFactory> 类，如以下代码所示。  
  
    ```  
    <%ServiceHost   
        language=c#  
        Debug="true"  
        Service="Microsoft.Samples.Service"  
        Factory=System.ServiceModel.Activation.WebServiceHostFactory%>  
    ```  
  
### 在 Internet Explorer 中调用映射到 GET 的服务操作  
  
1.  打开 Internet Explorer 并键入“`http://localhost:8000/EchoWithGet?s=Hello, world!`”，然后按 Enter。该 URL 包含服务的基址 \("http:\/\/localhost:8000\/"\)、终结点的相对地址 \(""\)、要调用的服务操作 \("EchoWithGet"\)、一个问号以及其后通过“and”符号 \(&\) 分隔的命名参数的列表。  
  
### 在代码中调用服务操作  
  
1.  在 `using` 块中创建 <xref:System.ServiceModel.Web.WebChannelFactory> 的实例。  
  
     [!code-csharp[htBasicService#6](../../../../samples/snippets/csharp/VS_Snippets_CFX/htbasicservice/cs/service.cs#6)]
     [!code-vb[htBasicService#6](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/htbasicservice/vb/service.vb#6)]  
  
2.  将 <xref:System.ServiceModel.Description.WebHttpBehavior> 添加到 <xref:System.ServiceModel.ChannelFactory> 调用的终结点。  
  
     [!code-csharp[htBasicService#7](../../../../samples/snippets/csharp/VS_Snippets_CFX/htbasicservice/cs/service.cs#7)]
     [!code-vb[htBasicService#7](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/htbasicservice/vb/service.vb#7)]  
  
3.  创建通道并调用服务。  
  
     [!code-csharp[htBasicService#8](../../../../samples/snippets/csharp/VS_Snippets_CFX/htbasicservice/cs/service.cs#8)]
     [!code-vb[htBasicService#8](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/htbasicservice/vb/service.vb#8)]  
  
4.  关闭 <xref:System.ServiceModel.Web.WebServiceHost>。  
  
     [!code-csharp[htBasicService#9](../../../../samples/snippets/csharp/VS_Snippets_CFX/htbasicservice/cs/service.cs#9)]
     [!code-vb[htBasicService#9](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/htbasicservice/vb/service.vb#9)]  
  
## 示例  
 下面列出了此示例的完整代码清单。  
  
 [!code-csharp[htBasicService#10](../../../../samples/snippets/csharp/VS_Snippets_CFX/htbasicservice/cs/service.cs#10)]
 [!code-vb[htBasicService#10](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/htbasicservice/vb/service.vb#10)]  
  
## 编译代码  
 编译 Service.cs 时，请引用 System.ServiceModel.dll 和 System.ServiceModel.Web.dll。  
  
## 请参阅  
 <xref:System.ServiceModel.WebHttpBinding>   
 <xref:System.ServiceModel.Web.WebGetAttribute>   
 <xref:System.ServiceModel.Web.WebInvokeAttribute>   
 <xref:System.ServiceModel.Web.WebServiceHost>   
 <xref:System.ServiceModel.Web.WebChannelFactory>   
 <xref:System.ServiceModel.Description.WebHttpBehavior>   
 [WCF Web HTTP 编程模型](../../../../docs/framework/wcf/feature-details/wcf-web-http-programming-model.md)