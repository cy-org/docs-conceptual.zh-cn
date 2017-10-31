---
title: "高级格式选择 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: e02d9082-4d55-41d8-9329-98f6d1c77f06
caps.latest.revision: 9
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 9
---
# 高级格式选择
本示例演示如何扩展 [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] REST 编程模型以支持新的传出响应格式。  此外，本示例使用 T4 模板以 HTML 页的形式返回响应，从而演示如何实现视图样式编程模型。  
  
## 示例详细信息  
 本示例包含一个简单服务以及向该服务进行请求的客户端代码。  该服务支持一个 \[WebGet\] 操作，该操作具有以下方法签名：`Message EchoListWithGet(string list);`  
  
 当客户端向服务进行请求时，会通过 `list` 查询字符串参数提供一个逗号分隔的项列表，服务以下列格式之一返回同一个列表：XML、JSON、Atom、XHTML 或 jpeg。  
  
 服务返回的响应格式首先由 `format` 查询字符串参数确定，其次由与请求一起提供的 HTTP Accept 标头确定。  如果 `format` 查询字符串参数的值是上面格式中的一种，则以该格式返回响应。  如果不存在 `format` 查询字符串，则服务会遍历来自请求的 Accept 标头元素并返回服务支持的第一个内容类型的格式。  
  
 需要注意操作的返回类型。  当操作返回的类型不是 <xref:System.ServiceModel.Channels.Message> 时，[!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] REST 编程模型本身只支持 XML 和 JSON 响应格式。  但是，当使用 <xref:System.ServiceModel.Channels.Message> 作为返回类型时，开发人员可以完全控制应如何格式化消息内容。  
  
 本示例使用 <xref:System.ServiceModel.Web.WebOperationContext.CreateXmlResponse%2A>、<xref:System.ServiceModel.Web.WebOperationContext.CreateJsonResponse%2A> 和 <xref:System.ServiceModel.Web.WebOperationContext.CreateAtom10Response%2A> 方法将字符串列表分别序列化为 XML、JSON 和 ATOM 消息。  对于 jpeg 响应格式，使用 <xref:System.ServiceModel.Web.WebOperationContext.CreateStreamResponse%2A> 方法并将图像保存到流中。  对于 XHTML 响应，使用 <xref:System.ServiceModel.Web.WebOperationContext.CreateTextResponse%2A> 以及预处理的 T4 模板，该模板由一个 .tt 文件和一个自动生成的 .cs 文件组成。  通过 .tt 文件，开发人员可以采用包含变量和控制结构的模板形式编写响应。  [!INCLUDE[crabout](../../../../includes/crabout-md.md)] T4 的更多信息，请参见[使用文本模板生成项目](http://go.microsoft.com/fwlink/?LinkId=166023)（可能为英文网页）。  
  
 此示例包含一个自承载服务和一个客户端，它们都在一个控制台应用程序内运行。  在控制台应用程序运行时，客户端会对服务进行请求，并将响应中的相关信息写入控制台窗口。  
  
#### 运行此示例  
  
1.  打开高级格式选择示例的解决方案。  在启动 [!INCLUDE[vs_current_long](../../../../includes/vs-current-long-md.md)] 时，应以管理员身份运行才能成功执行该示例。  通过右击 [!INCLUDE[vs_current_long](../../../../includes/vs-current-long-md.md)] 图标并从上下文菜单选择**“以管理员身份运行”**来完成此操作。  
  
2.  按 Ctrl\+Shift\+B 生成解决方案，然后按 Ctrl\+F5 运行控制台应用程序 AdvancedFormatSelection 项目而不进行调试。  将出现控制台窗口，它提供了正在运行的服务的 URI，以及该服务的 HTML 帮助页的 URI。  
  
3.  在示例运行时，客户端会向服务发送请求，并将响应写入控制台窗口。  请注意响应的不同格式：XML、JSON、Atom 和 XHTML。  
  
4.  随后会提示您浏览到可以用于请求 .jpeg 格式的响应的 URI。  打开浏览器并浏览至给定 URI。  
  
5.  按任何键可终止示例。  
  
> [!IMPORTANT]
>  您的计算机上可能已安装这些示例。  在继续操作之前，请先检查以下（默认）目录：  
>   
>  `<安装驱动器>:\WF_WCF_Samples`  
>   
>  如果此目录不存在，请访问[针对 .NET Framework 4 的 Windows Communication Foundation \(WCF\) 和 Windows Workflow Foundation \(WF\) 示例](http://go.microsoft.com/fwlink/?LinkId=150780)（可能为英文网页），下载所有 [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] 和 [!INCLUDE[wf1](../../../../includes/wf1-md.md)] 示例。  此示例位于以下目录：  
>   
>  `<安装驱动器>:\WF_WCF_Samples\WCF\Basic\Web\AdvancedFormatSelection`  
  
## 请参阅