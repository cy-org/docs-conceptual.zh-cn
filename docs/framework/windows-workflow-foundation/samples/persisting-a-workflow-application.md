---
title: "持久保存工作流应用程序 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: abcff14c-f047-4195-ba26-d27f4a82c24e
caps.latest.revision: 15
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 15
---
# 持久保存工作流应用程序
此示例演示如何运行 <xref:System.Activities.WorkflowApplication>，在其空闲时进行卸载，然后在需要继续执行时重新加载它。  
  
## 示例详细信息  
 <xref:System.Activities.WorkflowApplication> 用于承载单个工作流实例，该实例提供一个简单接口并支持若干更加通用的承载方案。其中一种方案是由持久性帮助实现的长时间运行工作流。可通过以下方式来执行持久性承载控件：对 <xref:System.Activities.WorkflowApplication> 调用一个持久性操作；或者，处理一个 <xref:System.Activities.WorkflowApplication> 事件并指示  <xref:System.Activities.WorkflowApplication> 应持久。  
  
 实例工作流具有一个用于提示用户输入其名称的 <xref:System.Activities.Statements.WriteLine> 活动，一个用于通过恢复 <xref:System.Activities.Bookmark> 接收用户名作为输入的 `ReadLine` 活动，以及另一个用于向用户回显问候语的 <xref:System.Activities.Statements.WriteLine>。当工作流等待输入时，这将为持久性提供一个天然点。这通常称为 <xref:System.Workflow.Runtime.Tracking.TrackingWorkflowEvent> 点。每当工作流程序可以持久化，等待书签恢复以及无需执行其他工作时，<xref:System.Activities.WorkflowApplication> 将引发 <xref:System.Workflow.Runtime.Tracking.TrackingWorkflowEvent> 事件。在此示例的工作流中，上面所提及的点在 `ReadLine` 活动开始执行后立即出现。  
  
 设置 <xref:System.Activities.WorkflowApplication> 以使用<xref:System.Runtime.Persistence.InstanceStore> 执行持久化。此示例使用 <xref:System.Activities.DurableInstancing.SqlWorkflowInstanceStore>。在 <xref:System.Activities.WorkflowApplication> 运行之前，必须将 <xref:System.Runtime.Persistence.InstanceStore> 分配给 <xref:System.Activities.WorkflowApplication.InstanceStore%2A> 属性。  
  
 此示例为 <xref:System.Activities.WorkflowApplication.PersistableIdle%2A> 事件添加一个处理程序。此事件的处理程序指示 <xref:System.Activities.WorkflowApplication> 应通过返回 <xref:System.Activities.PersistableIdleAction> 来执行的工作。当 <xref:System.Activities.PersistableIdleAction> 返回时，将卸载 <xref:System.Activities.WorkflowApplication>。  
  
 此示例然后接受用户的输入，并将持久化工作流加载到新的 <xref:System.Activities.WorkflowApplication> 中。这可通过以下步骤来完成：先创建一个新 <xref:System.Activities.WorkflowApplication>，重新创建 <xref:System.Runtime.Persistence.InstanceStore>，将已完成和已卸载的事件与该实例相关联，然后使用目标工作流实例的标识符调用 <xref:System.Activities.WorkflowApplication.Load%2A>。在获取该实例之后，将恢复 `ReadLine` 活动中的书签。工作流从 `ReadLine` 活动内继续执行，并运行直至完成。当工作流完成并卸载时，将最后一次调试 <xref:System.Runtime.Persistence.InstanceStore> 来删除工作流。  
  
#### 使用此示例  
  
1.  打开 [!INCLUDE[vs2010](../../../../includes/vs2010-md.md)] 命令提示符。  
  
     此示例要求随 [!INCLUDE[vs2010](../../../../includes/vs2010-md.md)] 一起默认安装的 SQL Server Express。  
  
2.  导航到示例目录 \(\\WF\\Basic\\Persistence\\InstancePersistence\\CS\) 然后运行 CreateInstanceStore.cmd.  
  
    > [!CAUTION]
    >  CreateInstanceStore.cmd 脚本尝试在 SQL Server 2008 Express 的默认实例上创建数据库。如果要在不同的实例上安装数据库，请修改脚本。  
  
3.  使用 [!INCLUDE[vs2010](../../../../includes/vs2010-md.md)]，打开 Persistence.sln 解决方案文件，并按 CTRL\+SHIFT\+B 生成它。  
  
    > [!CAUTION]
    >  如果在 SQL Server 的非默认实例上安装了数据库，请在生成解决方案之前更新代码中的连接字符串。  
  
4.  通过在[!INCLUDE[fileExplorer](../../../../includes/fileexplorer-md.md)]中导航到项目的 bin 目录 \(\\WF\\Basic\\Persistence\\InstancePersistence\\bin\\Debug\)，然后右击 Workflow.exe 并选择**“以管理员身份运行”**，从而使用管理员权限运行此示例。  
  
#### 删除实例存储区数据库  
  
1.  打开 [!INCLUDE[vs2010](../../../../includes/vs2010-md.md)] 命令提示符。  
  
2.  导航到此示例目录并运行 RemoveInstanceStore.cmd。  
  
> [!IMPORTANT]
>  您的计算机上可能已安装这些示例。在继续操作之前，请先检查以下（默认）目录。  
>   
>  `<安装驱动器>:\WF_WCF_Samples`  
>   
>  如果此目录不存在，请访问[针对 .NET Framework 4 的 Windows Communication Foundation \(WCF\) 和 Windows Workflow Foundation \(WF\) 示例](http://go.microsoft.com/fwlink/?LinkId=150780)（可能为英文网页），下载所有 [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] 和 [!INCLUDE[wf1](../../../../includes/wf1-md.md)] 示例。此示例位于以下目录：  
>   
>  `<安装驱动器>:\WF_WCF_Samples\WF\Basic\Persistence\InstancePersistence`  
  
## 请参阅  
 [AppFabric 承载和持久性示例](http://go.microsoft.com/fwlink/?LinkId=193961)