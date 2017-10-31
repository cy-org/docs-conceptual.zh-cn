---
title: "基本活动组合 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: c283a1a7-1245-4ecd-8072-206c1b4ca379
caps.latest.revision: 9
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 9
---
# 基本活动组合
此示例演示如何编写自定义活动和系统提供的活动来生成更多自定义活动。  
  
 使用 Survey 活动的工作流安排包含一系列问题的调查，然后输出接收到的响应。  
  
## 示例详细信息  
 此示例使用三个自定义活动。`ReadLine` 是一个简单的 <xref:System.Activities.NativeActivity>\<字符串 \>，它计划时创建了 <xref:System.Activities.Bookmark>，然后通过收回的 <xref:System.Activities.Bookmark> 设置 `Return`<xref:System.Activities.OutArgument%601>的值。`Prompt` 是 <xref:System.Activities.Activity%601>\< 字符串 \>这需要 <xref:System.Activities.InArgument%601>\<字符串 \> 名为 `Text` 和响应中的返回用户  `Result`<xref:System.Activities.OutArgument%601>\< 字符串 \>。`Prompt` 活动使用作为 .NET Framework 的一部分提供的 <xref:System.Activities.Statements.Sequence> 和 <xref:System.Activities.Statements.WriteLine> 活动，并且该活动还集成了自定义 `ReadLine` 活动以获取用户输入。最后一个自定义活动为 `Survey` 活动。它是一个 <xref:System.Activities.Activity>\<ICollection\<string\>\>。此活动接受一个名为 `Questions` 的 <xref:System.Activities.InArgument%601>\<IEnumerable\<string\>\>，并使用响应填充 `Result` out 参数。`Survey` 活动使用 .NET Framework 中的 <xref:System.Activities.Statements.ForEach>、<xref:System.Activities.Statements.Sequence> 和 <xref:System.Activities.Statements.AddToCollection%601>，并使用 `Prompt` 活动询问调查问题并获取响应。  
  
#### 设置、生成和运行示例  
  
1.  在 [!INCLUDE[vs2010](../../../../includes/vs2010-md.md)] 中打开**“BasicActivityComposition.sln”**示例解决方案。  
  
2.  生成和运行解决方案。  
  
> [!IMPORTANT]
>  您的计算机上可能已安装这些示例。在继续操作之前，请先检查以下（默认）目录：  
>   
>  `<安装驱动器>:\WF_WCF_Samples`  
>   
>  如果此目录不存在，请访问[针对 .NET Framework 4 的 Windows Communication Foundation \(WCF\) 和 Windows Workflow Foundation \(WF\) 示例](http://go.microsoft.com/fwlink/?LinkId=150780)（可能为英文网页），下载所有 [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] 和 [!INCLUDE[wf1](../../../../includes/wf1-md.md)] 示例。此示例位于以下目录：  
>   
>  `<安装驱动器>:\WF_WCF_Samples\WF\Basic\CustomActivities\Composite\ActivityComposition`  
  
## 请参阅