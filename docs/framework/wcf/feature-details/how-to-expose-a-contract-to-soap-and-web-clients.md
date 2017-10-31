---
title: "如何：向 SOAP 和 Web 客户端公开协定 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: bb765a48-12f2-430d-a54d-6f0c20f2a23a
caps.latest.revision: 21
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 21
---
# 如何：向 SOAP 和 Web 客户端公开协定
默认情况下，[!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] 使终结点只可用于 SOAP 客户端。  在[如何：创建基本 WCF Web HTTP 服务](../../../../docs/framework/wcf/feature-details/how-to-create-a-basic-wcf-web-http-service.md)中，非 SOAP 客户端可以使用终结点。  有时可能需要使相同的协定可以同时作为 Web 终结点和 SOAP 终结点使用。  本主题演示了如何实现此目的的示例。  
  
### 定义服务协定  
  
1.  使用通过 <xref:System.ServiceModel.ServiceContractAttribute>、<xref:System.ServiceModel.Web.WebInvokeAttribute> 和 <xref:System.ServiceModel.Web.WebGetAttribute> 特性进行标记的接口来定义服务协定，如下面的代码所示。  
  
     [!code-csharp[htSoapWeb#0](../../../../samples/snippets/csharp/VS_Snippets_CFX/htsoapweb/cs/program.cs#0)]
     [!code-vb[htSoapWeb#0](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/htsoapweb/vb/program.vb#0)]  
  
    > [!NOTE]
    >  默认情况下，<xref:System.ServiceModel.Web.WebInvokeAttribute> 将 POST 调用映射到操作。  但是，可以通过指定“method\=”参数指定要映射到操作的方法。  <xref:System.ServiceModel.Web.WebGetAttribute> 不具有“method\=”参数，仅将 GET 调用映射到服务操作。  
  
2.  实现服务协定，如下面的代码所示。  
  
     [!code-csharp[htSoapWeb#1](../../../../samples/snippets/csharp/VS_Snippets_CFX/htsoapweb/cs/program.cs#1)]
     [!code-vb[htSoapWeb#1](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/htsoapweb/vb/program.vb#1)]  
  
### 承载服务  
  
1.  创建 <xref:System.ServiceModel.ServiceHost> 对象，如下面的代码所示。  
  
     [!code-csharp[htSoapWeb#2](../../../../samples/snippets/csharp/VS_Snippets_CFX/htsoapweb/cs/program.cs#2)]
     [!code-vb[htSoapWeb#2](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/htsoapweb/vb/program.vb#2)]  
  
2.  添加一个带有针对 SOAP 终结点的 <xref:System.ServiceModel.BasicHttpBinding> 的 <xref:System.ServiceModel.Description.ServiceEndpoint>，如下面的代码所示。  
  
     [!code-csharp[htSoapWeb#3](../../../../samples/snippets/csharp/VS_Snippets_CFX/htsoapweb/cs/program.cs#3)]
     [!code-vb[htSoapWeb#3](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/htsoapweb/vb/program.vb#3)]  
  
3.  添加一个带有针对非 SOAP 终结点的 <xref:System.ServiceModel.WebHttpBinding> 的 <xref:System.ServiceModel.Description.ServiceEndpoint>，并将 <xref:System.ServiceModel.Description.WebHttpBehavior> 添加到该终结点，如下面的代码所示。  
  
     [!code-csharp[htSoapWeb#4](../../../../samples/snippets/csharp/VS_Snippets_CFX/htsoapweb/cs/program.cs#4)]
     [!code-vb[htSoapWeb#4](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/htsoapweb/vb/program.vb#4)]  
  
4.  在 <xref:System.ServiceModel.ServiceHost> 实例上调用 `Open()` 以打开服务主机，如下面的代码所示。  
  
     [!code-csharp[htSoapWeb#5](../../../../samples/snippets/csharp/VS_Snippets_CFX/htsoapweb/cs/program.cs#5)]
     [!code-vb[htSoapWeb#5](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/htsoapweb/vb/program.vb#5)]  
  
### 在 Internet Explorer 中调用映射到 GET 的服务操作  
  
1.  打开 Internet Explorer，键入 `http://localhost:8000/Web/EchoWithGet?s=Hello, world!`，然后按 Enter。  该 URL 包含服务的基址 \("http:\/\/localhost:8000\/"\)、终结点的相对地址 \(""\)、要调用的服务操作 \("EchoWithGet"\)、一个问号以及其后通过“and”符号 \(&\) 分隔的命名参数的列表。  
  
### 使用代码在 Web 终结点上调用服务操作  
  
1.  在 `using` 块中创建 <xref:System.ServiceModel.Web.WebChannelFactory%601> 的实例，如下面的代码所示。  
  
     [!code-csharp[htSoapWeb#6](../../../../samples/snippets/csharp/VS_Snippets_CFX/htsoapweb/cs/program.cs#6)]
     [!code-vb[htSoapWeb#6](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/htsoapweb/vb/program.vb#6)]  
  
> [!NOTE]
>  将自动在 `using` 块末尾处的通道上调用 `Close()`。  
  
1.  创建通道并调用服务，如下面的代码所示。  
  
     [!code-csharp[htSoapWeb#8](../../../../samples/snippets/csharp/VS_Snippets_CFX/htsoapweb/cs/program.cs#8)]
     [!code-vb[htSoapWeb#8](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/htsoapweb/vb/program.vb#8)]  
  
### 在 SOAP 终结点上调用服务操作  
  
1.  在 `using` 块中创建 <xref:System.ServiceModel.ChannelFactory> 的实例，如下面的代码所示。  
  
     [!code-csharp[htSoapWeb#10](../../../../samples/snippets/csharp/VS_Snippets_CFX/htsoapweb/cs/program.cs#10)]
     [!code-vb[htSoapWeb#10](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/htsoapweb/vb/program.vb#10)]  
  
2.  创建通道并调用服务，如下面的代码所示。  
  
     [!code-csharp[htSoapWeb#11](../../../../samples/snippets/csharp/VS_Snippets_CFX/htsoapweb/cs/program.cs#11)]
     [!code-vb[htSoapWeb#11](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/htsoapweb/vb/program.vb#11)]  
  
### 关闭服务主机  
  
1.  关闭服务主机，如下面的代码所示。  
  
     [!code-csharp[htSoapWeb#9](../../../../samples/snippets/csharp/VS_Snippets_CFX/htsoapweb/cs/program.cs#9)]
     [!code-vb[htSoapWeb#9](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/htsoapweb/vb/program.vb#9)]  
  
## 示例  
 下面列出了此主题的完整代码。  
  
 [!code-csharp[htSoapWeb#13](../../../../samples/snippets/csharp/VS_Snippets_CFX/htsoapweb/cs/program.cs#13)]
 [!code-vb[htSoapWeb#13](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/htsoapweb/vb/program.vb#13)]  
  
## 编译代码  
 编译 Service.cs 时，请参考 System.ServiceModel.dll 和 System.ServiceModel.Web.dll。  
  
## 请参阅  
 <xref:System.ServiceModel.WebHttpBinding>   
 <xref:System.ServiceModel.Web.WebGetAttribute>   
 <xref:System.ServiceModel.Web.WebInvokeAttribute>   
 <xref:System.ServiceModel.Web.WebServiceHost>   
 <xref:System.ServiceModel.ChannelFactory>   
 <xref:System.ServiceModel.Description.WebHttpBehavior>   
 [WCF Web HTTP 编程模型](../../../../docs/framework/wcf/feature-details/wcf-web-http-programming-model.md)