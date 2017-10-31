---
title: "访问 OperationContext | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 4e92efe8-7e79-41f3-b50e-bdc38b9f41f8
caps.latest.revision: 5
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 5
---
# 访问 OperationContext
此示例演示如何将消息传递活动（<xref:System.ServiceModel.Activities.Receive> 和 <xref:System.ServiceModel.Activities.Send>）与自定义范围活动一起使用以访问 <xref:System.ServiceModel.OperationContext.Current%2A> 并附加或检索传出消息或传入消息中的自定义消息头。  
  
## 演示  
 消息传递活动、<xref:System.ServiceModel.Activities.ISendMessageCallback>、<xref:System.ServiceModel.Activities.IReceiveMessageCallback>。  
  
## 讨论  
 此示例演示如何使用消息传递活动中的扩展性点（<xref:System.ServiceModel.Activities.ISendMessageCallback> 和 <xref:System.ServiceModel.Activities.IReceiveMessageCallback>）来访问 <xref:System.ServiceModel.OperationContext.Current%2A>。在工作流运行时中，将回调注册为由消息传递活动在执行后选取的 <xref:System.Activities.IExecutionProperty> 的实现。与该 <xref:System.Activities.IExecutionProperty> 实现处于同一范围内的任何消息传递活动都会受到影响。特别是，此示例使用自定义范围活动来强制实施回调行为。在客户端工作流中使用 <xref:System.ServiceModel.Activities.ISendMessageCallback> 可将工作流的 <xref:System.Activities.WorkflowApplication.Id%2A> 作为传出 <xref:System.ServiceModel.Channels.MessageHeader> 包含。然后，在使用 <xref:System.ServiceModel.Activities.IReceiveMessageCallback> 的服务中选择此标头，并将此标头的值输出到控制台。  
  
#### 设置、生成和运行示例  
  
1.  此示例公开一个使用 HTTP 终结点的工作流服务。若要运行此示例，必须通过以管理员身份运行 Visual Studio 来添加适当的 URL ACL，或在提升的提示符下执行以下命令来添加适当的 ACL。有关详细信息，请参见[配置 HTTP 和 HTTPS](http://go.microsoft.com/fwlink/?LinkId=70353)（可能为英文网页）。确保替换了域和用户名。  
  
    ```  
    netsh http add urlacl url=http://+:8000/ user=%DOMAIN%\%UserName%  
    ```  
  
2.  在添加 URL ACL 后，请使用下列步骤。  
  
    1.  生成解决方案。  
  
    2.  通过右击解决方案并选择**“设置启动项目”**来设置多个启动项目。  
  
    3.  将**“Service”**和**“Client”**（按此顺序）添加为多个启动项目。  
  
    4.  运行该应用程序。客户端控制台显示运行两次的工作流，而服务窗口显示这些工作流的实例 ID。  
  
> [!IMPORTANT]
>  您的计算机上可能已安装这些示例。在继续操作之前，请先检查以下（默认）目录：  
>   
>  `<安装驱动器>:\WF_WCF_Samples`  
>   
>  如果此目录不存在，请访问[针对 .NET Framework 4 的 Windows Communication Foundation \(WCF\) 和 Windows Workflow Foundation \(WF\) 示例](http://go.microsoft.com/fwlink/?LinkId=150780)（可能为英文网页），下载所有 [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] 和 [!INCLUDE[wf1](../../../../includes/wf1-md.md)] 示例。此示例位于以下目录：  
>   
>  `<安装驱动器>:\WF_WCF_Samples\WF\Scenario\Services\Accessing Operation Context`