---
title: "活动关系验证 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 6f11a34e-ed67-4bce-88ce-7e96bbb4d052
caps.latest.revision: 8
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 8
---
# 活动关系验证
此示例由三种活动组成：`CreateCity`、`CreateState` 和 `CreateCountry` 活动。`CreateCity` 必须在 `CreateState` 活动的内部，`CreateState` 必须在 `CreateCountry` 活动的内部。 此示例出于演示的需要，对 `CreateState` 活动使用代码形式的验证逻辑，而对 `CreateCity` 活动使用 XAML 形式的验证逻辑。这两个约束具有相同的行为。  
  
 [!INCLUDE[netfx_current_long](../../../../includes/netfx-current-long-md.md)] 提供了以下三个帮助器活动，开发人员可使用它们验证各活动之间的关系。  
  
 <xref:System.Activities.Validation.GetParentChain>  
 提供属于当前节点的父级的所有活动的集合  
  
 <xref:System.Activities.Validation.GetChildSubtree>  
 提供属于当前节点的子树（不包括当前节点）的所有活动的集合  
  
 <xref:System.Activities.Validation.GetWorkflowTree>  
 提供当前节点所在的同一树中的所有活动的集合  
  
 在此示例中，<xref:System.Activities.Statements.ForEach%601> 活动用于遍历 <xref:System.Activities.Validation.GetParentChain> 返回的集合。对于集合中的每个元素，都会将其类型与 `CreateCountry` 进行比较（如果验证的是 `CreateCity`，则与 `CreateState` 进行比较），发现匹配项，则会将结果标志设置为 `true`。最后，<xref:System.Activities.Validation.AssertValidation> 用于在结果标志设置为 `false` 时生成验证错误。  
  
### 使用此示例  
  
1.  在 [!INCLUDE[vs2010](../../../../includes/vs2010-md.md)] 中打开 ContainmentValidation.sln 示例解决方案。  
  
2.  生成解决方案。  
  
3.  按 CTRL \+ F5 启动程序。  
  
> [!IMPORTANT]
>  您的计算机上可能已安装这些示例。在继续操作之前，请先检查以下（默认）目录：  
>   
>  `<安装驱动器>:\WF_WCF_Samples`  
>   
>  如果此目录不存在，请访问[针对 .NET Framework 4 的 Windows Communication Foundation \(WCF\) 和 Windows Workflow Foundation \(WF\) 示例](http://go.microsoft.com/fwlink/?LinkId=150780)（可能为英文网页），下载所有 [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] 和 [!INCLUDE[wf1](../../../../includes/wf1-md.md)] 示例。此示例位于以下目录：  
>   
>  `<安装驱动器>:\WF_WCF_Samples\WF\Basic\Validation\ActivityRelationships`  
  
## 请参阅