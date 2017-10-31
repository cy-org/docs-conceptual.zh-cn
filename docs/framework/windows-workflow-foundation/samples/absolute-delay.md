---
title: "绝对延迟 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: b483139a-39bb-4560-8003-8969a8fc2cd1
caps.latest.revision: 3
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 3
---
# 绝对延迟
此示例的主要方案是，通过在工作流应用程序中使用持久性计时器延迟到指定的 <xref:System.DateTime>。这不同于使用内置 <xref:System.Activities.Statements.Delay> 活动，因为后者只允许延迟一段给定的 <xref:Sysem.TimeSpan>（或分钟数\/秒数）。  
  
 您可能希望在某些实际方案中进行此区分，这些方案包括：  
  
1.  您希望将邮件发送时间延迟 30 秒以确保您未犯任何错误。  
  
2.  您正在加班，并希望所有邮件延迟到正常工作时间（如上午 8 点）。  
  
## 演示  
  
1.  用于实现绝对延迟的 <xref:System.Activities.Statements.DurableTimerExtension>  
  
2.  将 <xref:System.Activities.WorkflowApplication> 用于持久性计时器来设置持久性  
  
3.  在使用扩展点时使用 <xref:System.Activities.NativeActivity%601>  
  
4.  在 SendEmail 活动中使用 <xref:System.Activities.CodeActivity%601>  
  
5.  <xref:System.Activities.Statements.Delay>  
  
6.  仅 XAML 工作流  
  
 此示例演示如何创建一个自定义活动，该活动接受 <xref:System.DateTime> 并使用持久性计时器来注册延迟持续时间。在使用持久性计时器时，您必须使用 <xref:System.Activities.NativeActivity> 创建书签，因为您需要将此书签注册到计时器扩展。在此示例中，当持久性计时器过期时，将调用 `OnTimerExpired` 方法。请务必在 <xref:System.Activities.NativeActivity%601.CacheMetadata%2A> 事件中添加计时器扩展，以确保为运行时提供此信息。另一个实现细节是，您需要实现逻辑以将 <xref:System.DateTime> 转换为 <xref:Sysem.TimeSpan>，因为持久性计时器只接受 <xref:System.DateTime>。  
  
> [!NOTE]
>  将 <xref:System.DateTime> 转换为 <xref:Sysem.TimeSpan> 会损失少量精度。  
  
 此示例还演示如何为 <xref:System.Activities.WorkflowApplication> 启用持久性。在此特定示例中，我们将使用持久性计时器，在该计时器中，工作流数据将在等待计时器过期的空闲时间内卸载到持久性数据库中。此实现还可用于其他持久性操作。此示例演示如何使用 SQL Server 设置持久性连接字符串以及如何创建实例存储以便为工作流实例保留数据。提供了有关如何在引发使工作流实例可运行的事件后恢复工作流的逻辑。  
  
 在执行此示例时，您将看到内置延迟开始和完成的时间，而后者会导致发送电子邮件。从这里开始，AbsoluteDelay 活动将暂停直到指定的 <xref:System.DateTime>（如果 <xref:System.DateTime> 已过期，则为 0 秒），而后者会在过期后发送电子邮件。这将显示内置 <xref:System.Activities.Statements.Delay> 功能与使用 AbsoluteDelay 活动的两种不同用例。  
  
#### 设置、生成和运行示例  
  
1.  请确保在您的计算机上已经安装了 SQL Server Express（或更高版本）。  
  
2.  在 [!INCLUDE[vs2010](../../../../includes/vs2010-md.md)] 命令提示符处运行 setup.cmd（位于 WF\/Basic\/Services\/AbsoluteDelay\/CS 中）以创建 AbsoluteDelaySampleDB 数据库、持久性架构和持久性逻辑。  
  
3.  在 [!INCLUDE[vs2010](../../../../includes/vs2010-md.md)] 中打开解决方案。  
  
4.  在 Delay 活动中指定持续时间。  
  
5.  在 AbsoluteDelay 活动中指定 ExpirationTime。  
  
6.  更新 SendMail 活动中的 SendMailTo、SendMailFrom、SendMailSubject、SendMailBody 和 SmtpHost 字段。  
  
    > [!NOTE]
    >  如果未输入有效 SMTP 主机，则应用程序将引发 SMTP 异常。  
  
7.  通过选择**“生成”**，再选择**“生成解决方案”**来生成解决方案。  
  
8.  按 F5 运行解决方案。  
  
> [!IMPORTANT]
>  您的计算机上可能已安装这些示例。在继续操作之前，请先检查以下（默认）目录：  
>   
>  `<安装驱动器>:\WF_WCF_Samples`  
>   
>  如果此目录不存在，请访问[针对 .NET Framework 4 的 Windows Communication Foundation \(WCF\) 和 Windows Workflow Foundation \(WF\) 示例](http://go.microsoft.com/fwlink/?LinkId=150780)（可能为英文网页），下载所有 [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] 和 [!INCLUDE[wf1](../../../../includes/wf1-md.md)] 示例。此示例位于以下目录：  
>   
>  `<安装驱动器>:\WF_WCF_Samples\WF\Basic\Services\AbsoluteDelay`