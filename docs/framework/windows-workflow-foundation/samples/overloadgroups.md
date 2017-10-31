---
title: "OverloadGroups | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: d1d547d2-f5fb-4de3-a959-ee6139a4f1ad
caps.latest.revision: 9
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 9
---
# OverloadGroups
此示例包含 `CreateLocation` 活动，它具有两个有趣的特征：  
  
1.  它具有一些必需的参数和一些可选的参数。  
  
2.  它允许用户选择提供两个不同参数集中的一个。  
  
 使用以下两项功能可以实现上述行为：  
  
-   `[isRequired]` 验证是否已为某个特定活动的属性赋值，如果没有，则它将引发异常。  
  
-   `[OverloadGroup]` 汇集了一组参数，以便活动用户可在两个参数集中选择使用哪一个。用户不能使用同一实例中不同重载组中的参数。  
  
 在设置不同的工作流之后，调用 <xref:System.Activities.Validation.ActivityValidationServices.Validate%2A>，它将返回<xref:System.Activities.Validation.ConstraintViolation> 的 <xref:System.Activities.Validation.ValidationResults> 集合。将 <xref:System.Activities.Validation.ConstraintViolation> 对象输出到控制台。  
  
### 设置、生成和运行示例  
  
1.  在 [!INCLUDE[vs2010](../../../../includes/vs2010-md.md)] 中打开**“OverloadGroups.sln”**示例解决方案。  
  
2.  生成和运行解决方案。  
  
> [!IMPORTANT]
>  您的计算机上可能已安装这些示例。在继续操作之前，请先检查以下（默认）目录：  
>   
>  `<安装驱动器>:\WF_WCF_Samples`  
>   
>  如果此目录不存在，请访问[针对 .NET Framework 4 的 Windows Communication Foundation \(WCF\) 和 Windows Workflow Foundation \(WF\) 示例](http://go.microsoft.com/fwlink/?LinkId=150780)（可能为英文网页），下载所有 [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] 和 [!INCLUDE[wf1](../../../../includes/wf1-md.md)] 示例。此示例位于以下目录：  
>   
>  `<安装驱动器>:\WF_WCF_Samples\WF\Basic\Validation\OverloadGroups`  
  
## 请参阅