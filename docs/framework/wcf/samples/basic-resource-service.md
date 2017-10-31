---
title: "基本资源服务 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 4360063e-cc8c-4648-846e-c05a5af51a7a
caps.latest.revision: 8
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 8
---
# 基本资源服务
此示例演示如何使用 [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] REST 编程模型实现基于 HTTP 的服务，该模型公开支持检索、添加、删除和替换操作的客户集合。此示例由两个组件组成：一个自承载 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] HTTP 服务 \(Service.cs\) 和一个创建服务并对该服务进行调用的控制台应用程序 \(program.cs\)。  
  
## 示例详细信息  
 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 服务以面向资源的\/REST 方式公开客户集合。简而言之，这涉及拥有客户集合以及该集合中每个客户的唯一 URI。该服务支持在集合 URI 上发送 HTTP `GET` 以检索整个集合，并在结合 URI 上发送 HTTP `POST` 以向该集合添加新客户。另外，单个客户的 URI 上，它还支持 HTTP `GET` 以获取客户详细信息，支持 HTTP `PUT` 以替换该客户的详细信息，并支持 HTTP `DELETE` 以将该客户从集合中移除。将新客户添加到集合中时，该服务会向其分配一个唯一的 URI，并将该 URI 作为客户详细信息的一部分存储。此外，该服务还使用响应的位置 HTTP 标头将该 URI 通知客户端。  
  
 App.config 文件使用 <xref:System.ServiceModel.Description.WebHttpEndpoint.HelpEnabled%2A> 属性设置为 `true` 的默认 <xref:System.ServiceModel.Description.WebHttpEndpoint> 来配置 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 服务。因此，[!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 将在 `http://localhost:8000/Customers/help` 上创建一个基于 HTML 的自动帮助页，该帮助页可提供有关如何构造服务的 HTTP 请求以及如何访问服务的 HTTP 响应的信息 – 例如，如何以 XML 和 JSON 表示客户详细信息的示例。  
  
 通过以这种方式公开客户集合（一般来说是任何资源），客户端可以使用 URI 和 HTTP `GET`、`PUT`、`DELETE` 和 `POST` 以一种统一的方式与服务进行交互。Program.cs 演示如何使用 <xref:System.Net.HttpWebRequest> 来创作这种客户端。请注意，这只是访问 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] REST 服务的一种方式。还可以使用其他 .NET Framework 类（如 <xref:System.ServiceModel.ChannelFactory> 和 <xref:System.Net.WebClient>）来访问该服务。SDK 中的其他示例（如[基本 HTTP 服务](../../../../docs/framework/wcf/samples/basic-http-service.md)示例和[自动格式选择](../../../../docs/framework/wcf/samples/automatic-format-selection.md)示例）演示如何使用这些类与 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 服务进行通信。  
  
 此示例包含一个自承载服务和一个客户端，它们都在一个控制台应用程序内运行。在控制台应用程序运行时，客户端会向该服务发出请求，并将响应中的相关信息写入控制台窗口。  
  
#### 使用此示例  
  
1.  打开基本资源服务示例的解决方案。在启动 [!INCLUDE[vs_current_long](../../../../includes/vs-current-long-md.md)] 时，必须以管理员身份运行才能成功执行该示例。通过右击 [!INCLUDE[vs_current_long](../../../../includes/vs-current-long-md.md)] 图标并从上下文菜单选择**“以管理员身份运行”**来完成此操作。  
  
2.  按 Ctrl\+Shift\+B 生成解决方案，然后按 Ctrl\+F5 运行控制台应用程序。将出现控制台窗口，它提供了正在运行的服务的 URI，以及该服务的 HTML 帮助页的 URI。可随时通过在浏览器中键入 HTML 帮助页的 URI 来查看该帮助页。在示例运行时，客户端将写入当前活动的状态。  
  
3.  按任意键可终止示例。  
  
> [!IMPORTANT]
>  您的计算机上可能已安装这些示例。在继续操作之前，请先检查以下（默认）目录：  
>   
>  `<安装驱动器>:\WF_WCF_Samples`  
>   
>  如果此目录不存在，请访问[针对 .NET Framework 4 的 Windows Communication Foundation \(WCF\) 和 Windows Workflow Foundation \(WF\) 示例](http://go.microsoft.com/fwlink/?LinkId=150780)（可能为英文网页），下载所有 [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] 和 [!INCLUDE[wf1](../../../../includes/wf1-md.md)] 示例。此示例位于以下目录。  
>   
>  `<安装驱动器>:\WF_WCF_Samples\WCF\Basic\Web\BasicResourceService`  
  
## 请参阅  
 [基本 HTTP 服务](../../../../docs/framework/wcf/samples/basic-http-service.md)   
 [自动格式选择](../../../../docs/framework/wcf/samples/automatic-format-selection.md)