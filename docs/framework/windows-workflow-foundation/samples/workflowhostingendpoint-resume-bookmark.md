---
title: "WorkflowHostingEndpoint 恢复书签 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: a708064f-50b0-4751-b44e-d5410d08d451
caps.latest.revision: 6
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 6
---
# WorkflowHostingEndpoint 恢复书签
此示例演示如何将 <xref:System.ServiceModel.Activities.WorkflowHostingEndpoint> 与 <xref:System.ServiceModel.Activities.WorkflowServiceHost> 一起使用创建工作流实例。  
  
## 演示  
 <xref:System.ServiceModel.Activities.WorkflowHostingEndpoint>,<xref:System.ServiceModel.Activities.WorkflowServiceHost>  
  
## 讨论  
 使用 <xref:System.ServiceModel.Activities.WorkflowServiceHost>，此示例使用 <xref:System.ServiceModel.Activities.WorkflowHostingEndpoint> 创建承载的工作流实例。<xref:System.ServiceModel.Activities.WorkflowHostingEndpoint> 是可用于以下方案的 <xref:System.ServiceModel.Activities.WorkflowServiceHost> 的扩展点：  
  
-   创建新的工作流实例。  
  
-   恢复 <xref:System.ServiceModel.Activities.WorkflowServiceHost> 中承载的工作流实例上的书签。  
  
 所包含的示例终结点将公开一个协定，该协定提供用于创建工作流并返回实例 ID 或使用特定 ID 创建实例的操作。示例控制台应用程序使用一个基本工作流定义创建 <xref:System.ServiceModel.Activities.WorkflowServiceHost> 实例，并将 `CreationEndpoint` 添加到主机。然后它对所添加的终结点调用 `Create` 操作以创建新的工作流实例。  
  
#### 设置、生成和运行示例  
  
1.  生成解决方案。  
  
2.  运行该应用程序。当创建工作流实例时，`CreationEndpoint` 控制台会显示一条消息，其中包含该工作流实例 ID。成功恢复书签时，工作流将输出消息“Hello World\!”。  
  
> [!IMPORTANT]
>  您的计算机上可能已安装这些示例。在继续操作之前，请先检查以下（默认）目录：  
>   
>  `<安装驱动器>:\WF_WCF_Samples`  
>   
>  如果此目录不存在，请访问[针对 .NET Framework 4 的 Windows Communication Foundation \(WCF\) 和 Windows Workflow Foundation \(WF\) 示例](http://go.microsoft.com/fwlink/?LinkId=150780)（可能为英文网页），下载所有 [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] 和 [!INCLUDE[wf1](../../../../includes/wf1-md.md)] 示例。此示例位于以下目录：  
>   
>  `<安装驱动器>:\WF_WCF_Samples\WF\Basic\Execution\ResumeBookmarkEndpoint`