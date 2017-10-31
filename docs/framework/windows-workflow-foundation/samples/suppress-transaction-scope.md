---
title: "禁止显示事务范围 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 49fb6dd4-30d4-4067-925c-c5de44c8c740
caps.latest.revision: 8
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 8
---
# 禁止显示事务范围
此示例演示如何创作自定义 `SuppressTransactionScope` 活动以禁止环境运行时事务（如果存在的话）。  
  
> [!IMPORTANT]
>  您的计算机上可能已安装这些示例。在继续操作之前，请先检查以下（默认）目录：  
>   
>  `<安装驱动器>:\WF_WCF_Samples`  
>   
>  如果此目录不存在，请访问[针对 .NET Framework 4 的 Windows Communication Foundation \(WCF\) 和 Windows Workflow Foundation \(WF\) 示例](http://go.microsoft.com/fwlink/?LinkId=150780)（可能为英文网页），下载所有 [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] 和 [!INCLUDE[wf1](../../../../includes/wf1-md.md)] 示例。此示例位于以下目录：  
>   
>  `<安装驱动器>:\WF_WCF_Samples\WF\Scenario\Transactions\SuppressTransactionScope`  
  
## 示例详细信息  
 如果在特定方案中不希望出现事务流，则可使用自定义活动防止事务流向其他服务。工作流运行时为禁止 <xref:System.Activities.NativeActivity> 类中的环境事务提供内置支持。不过，要使用这一支持，需要创作此示例中的类似的自定义 <xref:System.Activities.NativeActivity>。  
  
 此方案由三个部分组成。首先，<xref:System.Activities.Statements.TransactionScope> 创建一个成为环境的运行时事务。这可以通过一个输出该事务的本地标识符和分布式标识符的自定义活动来验证。然后，在第二部分开始之前，该事务流到某个远程服务。在第二部分中，工作流进入 `SuppressTransactionScope`，并再次重复输出事务标识符并流动事务的过程。但是，自定义活动不会查找环境事务，并且流动到该服务的消息不会包含该事务。结果，该服务创建一个事务，这意味着，在客户端上输出的分布式 ID 与服务不会匹配。最后一部分发生在 `SuppressTransactionScope` 退出之后，运行时事务再次成为环境，这可以通过发送给该服务的具有与第一条消息的标识符匹配的分布式标识符的另一条消息来验证。  
  
 该活动本身派生自 <xref:System.Activities.NativeActivity>，因为它必须计划一个子级活动，并添加一个执行属性。`SuppressTransactionScope` 具有一个 <xref:System.Activities.RuntimeTransactionHandle> 类型的 <xref:System.Activities.Variable>，必须使用它，而不是使用 <xref:System.Activities.RuntimeTransactionHandle> 类型的实例字段，因为必须初始化句柄。将 `Variable<RuntimeTransactionHandle>` 作为一个实现变量添加到活动的元数据，因为它仅在内部使用。  
  
 执行活动后，它首先检查是否指定了正文，如果已指定，则设置 <xref:System.Activities.RuntimeTransactionHandle> 的 `SuppressTransaction` 属性。设置该属性之后，它即会添加到执行属性中并成为环境。这意味着，作为 `SuppressTransactionScope` 的子级的任何活动均可以查看该属性，因此将强制禁止运行时事务，并导致嵌套的 <xref:System.Activities.Statements.TransactionScope> 引发异常。在将句柄添加到执行属性之后，即会安排运行正文。  
  
#### 使用此示例  
  
1.  在 [!INCLUDE[vs2010](../../../../includes/vs2010-md.md)] 中打开 SuppressTransactionScope.sln 解决方案。  
  
2.  若要生成该解决方案，请按 CTRL\+SHIFT\+B 或从**“生成”**菜单中选择**“生成解决方案”**。  
  
3.  在成功生成之后，右击该解决方案，然后选择**“设置启动项目”**。从对话框中选择**“多启动项目”**，并确保两个项目的操作都设置为**“启动”**。  
  
4.  按 F5，或从**“调试”**菜单中选择**“开始调试”**。或者，可以按 Ctrl\+F5 或从**“调试”**菜单中选择**“开始执行\(不调试\)”**，以便在不调试情况下运行。  
  
    > [!NOTE]
    >  在启动客户端之前，服务器必须正在运行。承载该服务的控制台窗口的输出将指示它启动的时间。  
  
> [!IMPORTANT]
>  您的计算机上可能已安装这些示例。在继续操作之前，请先检查以下（默认）目录：  
>   
>  `<安装驱动器>:\WF_WCF_Samples`  
>   
>  如果此目录不存在，请访问[针对 .NET Framework 4 的 Windows Communication Foundation \(WCF\) 和 Windows Workflow Foundation \(WF\) 示例](http://go.microsoft.com/fwlink/?LinkId=150780)（可能为英文网页），下载所有 [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] 和 [!INCLUDE[wf1](../../../../includes/wf1-md.md)] 示例。此示例位于以下目录：  
>   
>  `<安装驱动器>:\WF_WCF_Samples\WF\Scenario\Transactions\SuppressTransactionScope`  
  
## 请参阅