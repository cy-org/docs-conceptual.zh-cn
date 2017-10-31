---
title: "工作流管理终结点示例 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 3ac6e08f-c43d-4bb7-83c3-e3890a4dac03
caps.latest.revision: 10
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 10
---
# 工作流管理终结点示例
此示例演示如何使用工作流控制终结点以本地方式和远程方式创建和运行工作流。  此示例演示如何承载一个控制终结点并编写调用此控制终结点的客户端，以创建和运行工作流的实例。  工作流不是服务。  
  
 在示例的服务端，使用 WorkflowServiceHost 承载工作流并且添加 WorkflowControlEndpoint，以便客户端可以执行控制操作（暂停、开始等）。  还添加用户定义的 CreationEndpoint，以允许创建工作流。  然后，该服务使用这些终结点在挂起状态中开始工作流，并且继续工作流。  客户端执行相同的操作，但这些操作来自客户端代码。  [!INCLUDE[crabout](../../../../includes/crabout-md.md)]这些接口的更多信息，请参见[工作流控制终结点](../../../../docs/framework/wcf/feature-details/workflow-control-endpoint.md)和[如何：在 IIS 中承载非服务工作流](../../../../docs/framework/wcf/feature-details/how-to-host-a-non-service-workflow-in-iis.md)。  
  
#### 运行示例  
  
1.  使用管理员权限运行 [!INCLUDE[vs2010](../../../../includes/vs2010-md.md)]。  
  
2.  在 [!INCLUDE[vs2010](../../../../includes/vs2010-md.md)] 中打开 ManagementEndpoint.sln 解决方案。  
  
3.  若要生成该解决方案，请按 CTRL\+SHIFT\+B 或从**“生成”**菜单中选择**“生成解决方案”**。  
  
4.  启动 ManagementEndpoint.exe 应用程序。  
  
5.  启动 Client.exe 应用程序。  
  
> [!IMPORTANT]
>  您的计算机上可能已安装这些示例。  在继续操作之前，请先检查以下（默认）目录：  
>   
>  `<安装驱动器>:\WF_WCF_Samples`  
>   
>  如果此目录不存在，请访问[针对 .NET Framework 4 的 Windows Communication Foundation \(WCF\) 和 Windows Workflow Foundation \(WF\) 示例](http://go.microsoft.com/fwlink/?LinkId=150780)（可能为英文网页），下载所有 [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] 和 [!INCLUDE[wf1](../../../../includes/wf1-md.md)] 示例。  此示例位于以下目录：  
>   
>  `<安装驱动器>:\WF_WCF_Samples\WF\Basic\Execution\ManagementEndpoint`  
  
## 请参阅