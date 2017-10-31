---
title: "WorkflowApplication ReadLine 主机 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: f7b362be-cb42-40d7-b9ef-cfc4aed2455b
caps.latest.revision: 14
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 14
---
# WorkflowApplication ReadLine 主机
此示例是一个泛型 ReadLine 主机。可以使用包含的 `ReadLine` 活动（或是从通过字符串恢复的书签获取数据的其他类似活动）来加载和运行任何工作流。`WriteLine` 活动的输出或写入 <xref:System.Activities.Statements.WriteLine.TextWriter%2A> 扩展的任何内容会定向到主机窗口。当某个实例处于空闲状态时，该实例的可用书签会出现在一个组合框中。选择书签、输入某些文本和按恢复书签按钮都会继续执行工作流。也可以取消、中止或终止选择的工作流。默认情况下持久性处于启用状态 \- 您可以关闭主机，然后将其重新打开，实例列表会被那些存储在数据库中的实例所填充。跟踪可用于将 <xref:System.Activities.WorkflowApplication> 级别事件输出到主机（可以选择在活动级别添加详细跟踪）。  
  
## 示例详细信息  
 此主机有两层：视图和实例管理器。视图由 `HostView` 和 `WorkflowApplicationInfo` 类组成。此主机的常规模式针对 `HostView` 类，以便基于 `WorkflowApplicationInfo` 对象向用户显示可用选项，这些对象与其所表示的实例保持合理同步。实例管理器层由 `WorkflowApplicationManager` 类（所有主机通信的核心）和 `WorkflowDefinitionExtension` 类（保留实例与用于启动实例的程序定义之间的关系，以及一些其他类）。`HostView` 调用控制 `WorkflowApplicationManager` 上的操作。这些调用通常是异步的，以维持具有响应能力的用户界面。这些异步调用完成时，`WorkflowApplicationManager` 通过一个定义完善的界面 \(`IHostView`\) 回调到视图层中。`HostView` 类通常将这些调用从 `WorkflowApplicationManager` 类调度到用户界面线程。将向由 `HostView` 类提供的线程安全 <xref:System.Activities.Statements.WriteLine.TextWriter%2A> 对象写入文本。不只是用户界面生成事件。例如，当 <xref:System.Activities.WorkflowApplication> 对象转为 `Idle`、`Complete` 或 `Aborted` 时，也会向 `WorkflowApplicationManager` 发出信号。`WorkflowApplicationManager` 类通过将清理或更新工作调度到主机来脱离事件线程。  
  
 通过 `WorkflowDefinitionExtension` 类可帮助对用于启动 <xref:System.Activities.WorkflowApplication> 的文件进行记录。该类实现 <xref:System.Activities.Persistence.PersistenceIOParticipant> 接口以参与持久性并将路径保留至工作流定义。  
  
 `WorkflowApplicationManager.Load` 方法使用存储的路径来实例化加载未完成 <xref:System.Activities.WorkflowApplication> 对象所需的工作流程序。  
  
#### 设置、生成和运行示例  
  
1.  此示例要求安装 SQL Express。[!INCLUDE[vs2010](../../../../includes/vs2010-md.md)] 附带有 SQL Express。  
  
2.  打开 Visual Studio 2010 命令提示符。  
  
3.  导航到示例目录 \(\\WF\\Basic\\Execution\\ControllingWorkflowApplications\)，然后运行 CreateInstanceStore.cmd。  
  
4.  CreateInstanceStore.cmd 脚本尝试在 SQL Server 2008 Express 的默认实例上创建数据库。如果要在不同的实例上安装数据库，请修改脚本。  
  
5.  编译 WorkflowApplicationReadLineHost 项目，然后从命令行运行该项目。  
  
6.  一旦运行，便可以选择关闭或打开持久性。另外，也可以选择打开或关闭详细活动跟踪。  
  
7.  按**“运行”**按钮旁的省略号按钮可浏览在 XAML 文件中定义的工作流  
  
     SampleWorkflows 文件夹下面有两个示例。parallel1.xaml 示例进入空闲状态。  
  
8.  选择了一个示例后，按**“运行”**按钮。  
  
9. 当工作流进入空闲状态时，**“书签”**组合框会填充有可用书签。  
  
10. 此时的选项可用于恢复书签以及取消、中止或终止工作流。也可以关闭主机然后重新启动。如果持久性保留为打开，则会在关机时卸载实例，并在启动时重新加载。  
  
     若要恢复书签，请选择所需的书签，在组合框旁的文本框中键入一个值，然后按**“恢复书签”\[Resume Bookmark\]**。  
  
#### 删除实例存储区数据库  
  
1.  打开 Visual Studio 2010 命令提示符。  
  
2.  导航到示例目录 \(\\WF\\Basic\\Execution\\ControllingWorkflowApplications\)，然后运行 RemoveInstanceStore.cmd。  
  
> [!IMPORTANT]
>  您的计算机上可能已安装这些示例。在继续操作之前，请先检查以下（默认）目录：  
>   
>  `<安装驱动器>:\WF_WCF_Samples`  
>   
>  如果此目录不存在，请访问[针对 .NET Framework 4 的 Windows Communication Foundation \(WCF\) 和 Windows Workflow Foundation \(WF\) 示例](http://go.microsoft.com/fwlink/?LinkId=150780)（可能为英文网页），下载所有 [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] 和 [!INCLUDE[wf1](../../../../includes/wf1-md.md)] 示例。此示例位于以下目录：  
>   
>  `<安装驱动器>:\WF_WCF_Samples\WF\Basic\Execution\ControllingWorkflowApplications`  
  
## 请参阅