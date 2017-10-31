---
title: "自动格式选择 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: dab51e56-8517-4a6a-bb54-b55b15ab37bb
caps.latest.revision: 8
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 8
---
# 自动格式选择
本示例演示如何通过 [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] REST 编程模型启用自动格式选择（XML 或 JSON），以及如何在操作代码中显式设置格式。  
  
## 示例详细信息  
 本示例包含一个服务以及向该服务进行请求的客户端代码。  该服务支持一个 HTTP `GET` 操作 \(`EchoWithGet`\) 和一个 HTTP `POST` 操作 \(`EchoWithPost`\)。  这两个操作都需要一个字符串，然后在响应中返回字符串。  对于 `GET` 操作，字符串在 URI 查询字符串参数中提供。  对于 `POST` 操作，字符串在请求正文中提供（以 XML 格式序列化）。  利用 [!INCLUDE[netfx40_long](../../../../includes/netfx40-long-md.md)] 中新的自动格式选择和命令性格式选择功能，服务能够以 XML 或 JSON 格式返回响应。  
  
 在本示例中，使用 App.config 文件启用自动格式选择。  在默认的 Web HTTP 终结点上，为 `automaticFormatSelectionEnabled` 特性提供值 `true`。  启用自动格式选择后，给定请求的 HTTP Accept 或 Content\-Type 标头，[!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 基础结构会选择最合适的响应格式（XML 或 JSON）。  除了将 `automaticFormatSelectionEnabled` 特性设置为 `true`，开发人员不需要提供任何其他代码或配置便可使用此新功能。  在 Program.cs 的客户端代码中，请求会发送到服务的 `GET` 和 `POST` 操作（HTTP Accept 标头指定为“application\/xml”或“application\/json”），服务以相应的格式返回响应。  
  
 在 `GET` 操作中，还使用了命令性格式选择。  `GET` 操作检查是否存在可选的 `format` 查询字符串参数，如果存在，则在 <xref:System.ServiceModel.Web.WebOperationContext.OutgoingResponse%2A> 属性上设置响应格式。  以这种方式强制设置响应格式会重写 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 基础结构进行的自动格式选择。  
  
 此示例包含一个自承载服务和一个客户端，它们都在一个控制台应用程序内运行。  在控制台应用程序运行时，客户端会对服务进行请求，并将响应中的相关信息写入控制台窗口。  
  
#### 使用此示例  
  
1.  打开自动格式选择示例的解决方案。  在启动 [!INCLUDE[vs_current_long](../../../../includes/vs-current-long-md.md)] 时，必须以管理员身份运行才能成功执行该示例。  通过右击 [!INCLUDE[vs_current_long](../../../../includes/vs-current-long-md.md)] 图标并从上下文菜单选择**“以管理员身份运行”**来完成此操作。  
  
2.  按 Ctrl\+Shift\+B 生成解决方案，然后按 Ctrl\+F5 运行控制台应用程序 AutomaticFormatSelection 项目。  将出现控制台窗口，它提供了正在运行的服务的 URI，以及该服务的 HTML 帮助页的 URI。  
  
3.  在示例运行时，客户端会向服务发送请求，并将响应写入控制台窗口。  请注意采用 XML 和 JSON 的不同格式的响应。  
  
4.  按任何键可终止示例。  
  
> [!IMPORTANT]
>  您的计算机上可能已安装这些示例。  在继续操作之前，请先检查以下（默认）目录：  
>   
>  `<安装驱动器>:\WF_WCF_Samples`  
>   
>  如果此目录不存在，请访问[针对 .NET Framework 4 的 Windows Communication Foundation \(WCF\) 和 Windows Workflow Foundation \(WF\) 示例](http://go.microsoft.com/fwlink/?LinkId=150780)（可能为英文网页），下载所有 [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] 和 [!INCLUDE[wf1](../../../../includes/wf1-md.md)] 示例。  此示例位于以下目录：  
>   
>  `<安装驱动器>:\WF_WCF_Samples\WCF\Basic\Web\AutomaticFormatSelection`  
  
## 请参阅