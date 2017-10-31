---
title: "窗体发布 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: fa6f84f9-2e07-4e3c-92d0-a245308b7dff
caps.latest.revision: 9
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 9
---
# 窗体发布
此示例演示如何扩展 WCF REST 编程模型以支持新的传入请求格式。  该示例还包含一个格式化程序的实现，该格式化程序可以将请求从 HTML 窗体发布反序列化为 [!INCLUDE[dnprdnshort](../../../../includes/dnprdnshort-md.md)] 类型。  此外，该示例使用一个 T4 模板返回 HTML 页，该页提供用户可以回发到 WCF REST 服务的 HTML 窗体。  
  
## 演示  
  
-   扩展对传入请求格式的支持。  
  
-   集成 T4 模板。  
  
## 讨论  
 此示例由两个项目组成。  一个项目是 HtmlFormProcessing 库，该库包含一个可以将 HTML 窗体发布反序列化为 [!INCLUDE[dnprdnshort](../../../../includes/dnprdnshort-md.md)] 类型的自定义请求格式化程序。  第二个项目是控制台应用程序，该应用程序扩展基本资源服务示例，以使用 HtmlFormProcessing 库的自定义请求格式化程序。  
  
 可以反序列化 HTML 窗体发布的自定义格式化程序 \(HtmlFormRequestDispatchFormatter\) 同时接受可以使用 <xref:System.ServiceModel.Dispatcher.QueryStringConverter> 从字符串进行转换的 [!INCLUDE[dnprdnshort](../../../../includes/dnprdnshort-md.md)] 类型，以及使用 <xref:System.Runtime.Serialization.DataContractAttribute> 标记的类型（仅具有可以使用 QueryStringConverter 从字符串进行转换的成员）。  
  
 HtmlFormProcessing 库项目还包括一个抽象基类 `RequestBodyDispatchFormatter`，该类可以用于创建其他自定义请求格式化程序。  通过从 `RequestBodyDispatchFormatter` 派生，开发人员可以专注于请求正文反序列化逻辑，这使基类可以将 URI 模板参数映射到操作的方法参数。  `HtmlFormProcessingBehavior` 类也同样在 HtmlFormProcessing 库项目中，该类演示如何从 <xref:System.ServiceModel.Description.WebHttpBehavior> 派生，以使用自定义请求格式化程序替换默认请求格式化程序。  
  
 此控制台应用程序项目扩展 [基本资源服务](../../../../docs/framework/wcf/samples/basic-resource-service.md) 示例。  基本资源服务示例演示如何以使用 WCF REST 编程模型的方式公开资源。  在基本资源服务示例中，公开了一个客户集合资源，从而可以创建、检索、更新和删除集合中的客户。  基本资源服务示例仅使用两个本机支持的传入请求格式，即 XML 和 JSON。  
  
 此窗体发布示例中的控制台应用程序利用 HtmlFormProcessing 库中的自定义格式化程序，该格式化程序使用户可以通过使用浏览器从 HTML 窗体发布发送请求来创建客户。  它还添加返回 HTML 页的操作，该页包含要回发到服务的窗体。  此 HTML 页使用预处理的 T4 模板生成，该模板包含一个 .tt 文件和一个自动生成的 .cs 文件。  通过 .tt 文件，开发人员可以采用包含变量和控制结构的模板形式编写响应。  [!INCLUDE[crabout](../../../../includes/crabout-md.md)] T4 的更多信息，请参见[使用文本模板生成项目](http://go.microsoft.com/fwlink/?LinkId=178139)（可能为英文网页）。  
  
#### 运行示例  
  
1.  打开窗体发布示例的解决方案。  在启动 [!INCLUDE[vs_current_long](../../../../includes/vs-current-long-md.md)] 时，必须以管理员身份运行才能成功执行示例。  通过右击 [!INCLUDE[vs_current_long](../../../../includes/vs-current-long-md.md)] 图标并从上下文菜单选择“以管理员身份运行”来完成此操作。  
  
2.  按 Ctrl\+Shift\+B 生成解决方案，然后按 Ctrl\+F5 运行控制台应用程序 FormPost 项目。  
  
3.  将出现控制台窗口，它提供了正在运行的服务的 URI，以及该服务的 HTML 帮助页的 URI。  
  
4.  该示例运行时，客户端将当前活动的状态（是添加客户、更新客户、删除客户还是从服务获取当前客户的列表）写入控制台窗口。  
  
5.  然后，会提示您浏览至客户窗体的 URI。  打开浏览器并浏览至给定 URI。  为客户键入名称和地址，然后单击**“提交”**按钮。  
  
6.  对控制台窗口按任何键以继续运行示例。  
  
7.  当示例完成时，请注意使用浏览器创建的客户包含在最终客户列表中。  
  
8.  按任何键可终止示例。  
  
> [!IMPORTANT]
>  您的计算机上可能已安装这些示例。  在继续操作之前，请先检查以下（默认）目录：  
>   
>  `<安装驱动器>:\WF_WCF_Samples`  
>   
>  如果此目录不存在，请访问[针对 .NET Framework 4 的 Windows Communication Foundation \(WCF\) 和 Windows Workflow Foundation \(WF\) 示例](http://go.microsoft.com/fwlink/?LinkId=150780)（可能为英文网页），下载所有 [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] 和 [!INCLUDE[wf1](../../../../includes/wf1-md.md)] 示例。  此示例位于以下目录：  
>   
>  `<安装驱动器>:\WF_WCF_Samples\WCF\Extensibility\Web\FormPost`