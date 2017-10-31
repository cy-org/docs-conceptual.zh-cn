---
title: "带规则的 IfElse | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: c4ad9bb2-9037-413a-8b14-59ed7b927a9e
caps.latest.revision: 8
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 8
---
# 带规则的 IfElse
此示例演示如何将规则条件用于 <xref:System.Workflow.Activities.IfElseActivity> 活动。  
  
 示例从宿主中传入一个 `OrderValue` 参数。该参数的值用在 <xref:System.Workflow.Activities.IfElseActivity> 活动第一个分支上的规则条件中。如果值小于 10,000，则执行第一个批处理，而且第一个批处理中的 <xref:System.Workflow.Activities.CodeActivity> 活动打印 **Get Manager Approval** 到控制台。如果值大于 10,000，则执行第二个批处理中的 <xref:System.Workflow.Activities.CodeActivity> 活动并打印 **Get VP Approval**。  
  
### 生成示例  
  
1.  在 [!INCLUDE[vs2010](../../../../includes/vs2010-md.md)] 中打开解决方案。  
  
2.  按 Ctrl\+Shift\+B 生成解决方案。  
  
3.  按 Ctrl\+F5 不进行调试运行解决方案。  
  
### 运行示例  
  
-   在 SDK 命令提示窗口中，运行 IfElseWithRules\\bin\\debug 文件夹（对于该示例的 Visual Basic 版本为 IfElseWithRules\\bin 文件夹）中的 .exe 文件，该文件夹位于该示例的主文件夹下。  
  
> [!IMPORTANT]
>  您的计算机上可能已安装这些示例。在继续操作之前，请先检查以下（默认）目录：  
>   
>  `<安装驱动器>:\WF_WCF_Samples`  
>   
>  如果此目录不存在，请访问[针对 .NET Framework 4 的 Windows Communication Foundation \(WCF\) 和 Windows Workflow Foundation \(WF\) 示例](http://go.microsoft.com/fwlink/?LinkId=150780)（可能为英文网页），下载所有 [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] 和 [!INCLUDE[wf1](../../../../includes/wf1-md.md)] 示例。此示例位于以下目录：  
>   
>  `<安装驱动器>:\WF_WCF_Samples\WF\Basic\Rules\IfElseWithRules`  
  
## 请参阅  
 <xref:System.Workflow.Activities.Rules>   
 <xref:System.Workflow.Activities.IfElseActivity>   
 <xref:System.Workflow.Activities.CodeActivity>   
 <xref:System.Workflow.Activities.Rules.RuleDefinitions>