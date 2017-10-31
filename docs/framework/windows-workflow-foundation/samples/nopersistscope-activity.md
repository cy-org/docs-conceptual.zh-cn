---
title: "NoPersistScope 活动 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 9a0baeb7-a05c-4fac-b905-252758cb71bb
caps.latest.revision: 10
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 10
---
# NoPersistScope 活动
此示例演示如何操作工作流中的不可序列化且可释放的状态。工作流不会尝试保留不可序列化的状态是很重要的，在工作流中使用过可释放的对象之后清除它们也是很重要的。  
  
## 演示  
 `NoPersistScope` 自定义活动和设计器。  
  
## 使用 NoPersistZone 活动  
 当示例工作流运行时，一个称为 `CreateTextWriter` 的自定义活动将创建一个 <xref:System.IO.TextWriter> 类型的对象，并将它保存到工作流变量中。 <xref:System.IO.TextWriter> 是 <xref:System.IDisposable> 对象。此 <xref:System.IO.TextWriter> 被配置为写入到运行示例的目录中的一个名为“out.txt”的文件，<xref:System.Activities.Statements.WriteLine> 活动将会使用它，因为它可以在控制台中回显您键入的任何文本。  
  
 回显逻辑在 `NoPersistScope` 活动（此活动的代码也是此示例的一部分）中运行，用于防止工作流持久化。如果您在控制台中键入 `unload`，则主机会尝试保存工作流实例，但此操作会因为工作流保留在 `NoPersistScope` 中而超时。工作流在使用完 <xref:System.IO.TextWriter> 对象之后，还会利用一个名为 `Dispose` 的自定义活动来释放该对象。将 `Dispose` 活动放在声明 <xref:System.IO.TextWriter> 变量的 <xref:System.Activities.Statements.TryCatch> 活动的 <xref:System.Activities.Statements.TryCatch.Finally%2A> 块中，以确保：即使在执行 Try 块期间应发生异常，也会运行它。  
  
 您可以键入 `exit`，以完成工作流实例并退出程序。  
  
#### 运行示例  
  
1.  在 [!INCLUDE[vs2010](../../../../includes/vs2010-md.md)] 中打开 NoPersistZone.sln 解决方案。  
  
2.  若要生成该解决方案，请按 CTRL\+SHIFT\+B 或从**“生成”**菜单中选择**“生成解决方案”**。  
  
3.  在生成成功之后，请按 F5 或者从**“调试”**菜单中选择**“启动调试”**，或者，可以按 Ctrl\+F5 或从**“调试”**菜单中选择**“开始执行\(不调试\)”**以便运行程序而不进行调试。  
  
#### 清理（可选）  
  
1.  若要移除 SQL 实例存储，请运行 Cleanup.cmd。  
  
> [!IMPORTANT]
>  您的计算机上可能已安装这些示例。在继续操作之前，请先检查以下（默认）目录：  
>   
>  `<安装驱动器>:\WF_WCF_Samples`  
>   
>  如果此目录不存在，请访问[针对 .NET Framework 4 的 Windows Communication Foundation \(WCF\) 和 Windows Workflow Foundation \(WF\) 示例](http://go.microsoft.com/fwlink/?LinkId=150780)（可能为英文网页），下载所有 [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] 和 [!INCLUDE[wf1](../../../../includes/wf1-md.md)] 示例。此示例位于以下目录：  
>   
>  `<安装驱动器>:\WF_WCF_Samples\WF\Scenario\ActivityLibrary\NoPersistScope`  
  
## 请参阅