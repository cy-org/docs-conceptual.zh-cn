---
title: "LINQ 消息查询相关性 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: b746872e-57b1-4514-b337-53398a0e0deb
caps.latest.revision: 6
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 6
---
# LINQ 消息查询相关性
此示例演示如何使用一个与系统提供的 <xref:System.ServiceModel.XPathMessageQuery> 相对的自定义 <xref:System.ServiceModel.Dispatcher.MessageQuery> 实现，执行基于内容的相关性。  
  
## 演示  
 自定义 <xref:System.ServiceModel.Dispatcher.MessageQuery>，基于内容的相关性。  
  
## 讨论  
 此示例演示如何出于相关性的目的从 <xref:System.ServiceModel.Dispatcher.MessageQuery> 基类进行扩展。自定义实现 `LinqMessageQuery` 允许用户提供一个 XName 以使用 XLinq 在消息中查找。此查询检索的数据用于构成相关性键，以将消息调度到相应的工作流实例。  
  
#### 设置、生成和运行示例  
  
1.  此示例使用 HTTP 终结点公开一个工作流服务。若要运行此示例，必须通过以管理员身份运行 Visual Studio 来添加适当的 URL ACL，或在提升的提示符下执行以下命令来添加适当的 ACL。有关详细信息，请参见[配置 HTTP 和 HTTPS](http://go.microsoft.com/fwlink/?LinkId=70353)（可能为英文网页）。确保替换了域和用户名。  
  
    ```  
    netsh http add urlacl url=http://+:8000/ user=%DOMAIN%\%UserName%  
    ```  
  
2.  在添加 URL ACL 后，请使用下列步骤。  
  
    1.  生成解决方案。  
  
    2.  通过右击解决方案并选择**“设置启动项目”**来设置多个启动项目。将**“Service”**和**“Client”**（按此顺序）添加为多个启动项目。  
  
    3.  运行该应用程序。客户端控制台演示工作流如何发送订单、接收订购单 ID 以及随后确认订单。服务窗口将显示正在处理的请求。  
  
> [!IMPORTANT]
>  您的计算机上可能已安装这些示例。在继续操作之前，请先检查以下（默认）目录：  
>   
>  `<安装驱动器>:\WF_WCF_Samples`  
>   
>  如果此目录不存在，请访问[针对 .NET Framework 4 的 Windows Communication Foundation \(WCF\) 和 Windows Workflow Foundation \(WF\) 示例](http://go.microsoft.com/fwlink/?LinkId=150780)（可能为英文网页），下载所有 [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] 和 [!INCLUDE[wf1](../../../../includes/wf1-md.md)] 示例。此示例位于以下目录：  
>   
>  `<安装驱动器>:\WF_WCF_Samples\WF\Scenario\Services\LinqMessageQueryCorrelation`