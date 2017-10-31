---
title: "基本 TransactionScope | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 1e22b76a-76de-43b4-9be7-7a86ed3d5a44
caps.latest.revision: 13
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 13
---
# 基本 TransactionScope
此示例包含四个演示如何嵌套 <xref:System.Activities.Statements.TransactionScope> 实例的方案。第一个方案演示如何嵌套作者不了解其构造的第三方活动。第二个和第三个方案演示如何遵循超时限制，最后一个方案演示 <xref:System.Activities.Statements.TransactionScope.AbortInstanceOnTransactionFailure%2A> 设置。  
  
## TransactionScopeActivity 的嵌套  
 第一个方案的工作流由一个包含两个 <xref:System.Activities.Statements.WriteLine> 活动和一个 <xref:System.Activities.Statements.TransactionScope> 的序列组成。<xref:System.Activities.Statements.TransactionScope> 的正文是一个包含两个以上的 <xref:System.Activities.Statements.WriteLine> 活动、一个可打印事务的本地标识符的自定义活动和一个第三方活动的序列。第三方活动 `TransactionScopeTest` 包含一个 <xref:System.Activities.Statements.TransactionScope>，但工作流作者无法了解它。此方案演示了可以嵌套 <xref:System.Activities.Statements.TransactionScope> 活动。  
  
## 超时  
 第二个方案的工作流和第一个方案的工作流几乎完全相同。`TransactionScopeTest` 已替换为 <xref:System.Activities.Statements.TransactionScope>。<xref:System.Activities.Statements.TransactionScope> 的正文是 5 秒延迟，事务的超时配置为 2 秒。外部 <xref:System.Activities.Statements.TransactionScope> 的超时设置为 10 秒。请注意，此方案将遵循范围中的最小超时限制，事务将会超时。  
  
 第三个方案的工作流几乎和前两个方案的工作流完全相同。延迟活动已从内部 <xref:System.Activities.Statements.TransactionScope> 的正文中移动到序列中紧随其后的外部 <xref:System.Activities.Statements.TransactionScope> 的正文。事务仍然会超时，不过，由于不再应用内部 <xref:System.Activities.Statements.TransactionScope> 的 2 秒超时值，事务会在 10 秒后超时（当超过外部 <xref:System.Activities.Statements.TransactionScope> 超时值时）。  
  
## 事务失败时中止  
 此工作流与第三个方案类似，只是超时值已替换为 <xref:System.Activities.Statements.TransactionScope.AbortInstanceOnTransactionFailure%2A> 属性。请注意，设置的所有内部子级的标志必须与外部 <xref:System.Activities.Statements.TransactionScope> 匹配。在此方案中，这些标志不匹配，因此，在工作流打开时会引发异常。  
  
#### 运行示例  
  
1.  在 [!INCLUDE[vs2010](../../../../includes/vs2010-md.md)] 中打开 BasicTransactionScopeSample.sln 解决方案。  
  
2.  若要生成该解决方案，请按 CTRL\+SHIFT\+B 或从**“生成”**菜单中选择**“生成解决方案”**。  
  
3.  成功生成之后，按 F5 或从**“调试”**菜单中选择**“开始调试”**。或者，可以按 Ctrl\+F5 或从**“调试”**菜单中选择**“开始执行\(不调试\)”**，以便在不调试情况下运行。  
  
> [!IMPORTANT]
>  您的计算机上可能已安装这些示例。在继续操作之前，请先检查以下（默认）目录：  
>   
>  `<安装驱动器>:\WF_WCF_Samples`  
>   
>  如果此目录不存在，请访问[针对 .NET Framework 4 的 Windows Communication Foundation \(WCF\) 和 Windows Workflow Foundation \(WF\) 示例](http://go.microsoft.com/fwlink/?LinkId=150780)（可能为英文网页），下载所有 [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] 和 [!INCLUDE[wf1](../../../../includes/wf1-md.md)] 示例。此示例位于以下目录：  
>   
>  `<安装驱动器>:\WF_WCF_Samples\WF\Basic\Transactions\BasicTransactionScope`  
  
## 请参阅