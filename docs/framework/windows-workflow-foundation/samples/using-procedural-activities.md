---
title: "使用过程性活动 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 1c67f739-3878-48ad-806c-b2ce0d6733a0
caps.latest.revision: 11
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 11
---
# 使用过程性活动
此示例使用 <xref:System.Activities.Statements.Sequence>、<xref:System.Activities.Statements.Assign>、<xref:System.Activities.Statements.If>、<xref:System.Activities.Statements.While>、<xref:System.Activities.Statements.Switch%601>、<xref:System.Activities.Statements.TryCatch> 和 <xref:System.Activities.Statements.WriteLine> 活动实现猜谜游戏。猜谜游戏将选择一个随机数，然后玩家必须猜出该数字。当玩家所猜测的数字错误时，工作流会给出一个提示，指示所猜的数字是过大还是过小。如果玩家在 7 次之内猜出该数字，则将为其显示特定的祝贺语。  
  
## 此示例中的自定义活动  
  
### ReadLine  
 从控制台读取一行文本。此活动派生自 <xref:System.Activities.NativeActivity> 类，并创建一个书签，控制台应用程序在读取行时将恢复该书签。  
  
### PromptInt  
 提示用户键入一个数字，然后从控制台窗口读取该数字。此活动派生自 <xref:System.Activities.Activity%601> 并使用 <xref:System.Activities.Statements.WriteLine> 和 `ReadLine` 活动。  
  
##### 使用此示例  
  
1.  使用 [!INCLUDE[vs2010](../../../../includes/vs2010-md.md)]，打开 GuessingGame.sln 解决方案文件。  
  
2.  要生成解决方案，按 Ctrl\+Shift\+B。  
  
3.  若要运行解决方案，请按 Ctrl\+F5。  
  
> [!IMPORTANT]
>  您的计算机上可能已安装这些示例。在继续操作之前，请先检查以下（默认）目录：  
>   
>  `<安装驱动器>:\WF_WCF_Samples`  
>   
>  如果此目录不存在，请访问[针对 .NET Framework 4 的 Windows Communication Foundation \(WCF\) 和 Windows Workflow Foundation \(WF\) 示例](http://go.microsoft.com/fwlink/?LinkId=150780)（可能为英文网页），下载所有 [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] 和 [!INCLUDE[wf1](../../../../includes/wf1-md.md)] 示例。此示例位于以下目录：  
>   
>  `<安装驱动器>：\WF_WCF_Samples\WF\Basic\Built-InActivities\Procedurals`  
  
## 请参阅