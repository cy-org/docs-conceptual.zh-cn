---
title: "外部活动验证 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 49619f59-9819-484a-bcd8-5596308e8551
caps.latest.revision: 6
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 6
---
# 外部活动验证
此示例演示如何向不是由您创作的内置活动添加验证逻辑。验证逻辑包括强制工作流中存在的所有 <xref:System.Activities.Statements.If> 活动已设置其 <xref:System.Activities.Statements.If.Then%2A> 属性或其 <xref:System.Activities.Statements.If.Else%2A> 属性。此外，验证逻辑还包括检查工作流中存在的所有 <xref:System.Activities.Statements.Pick> 活动是否具有多个分支，如果不具有多个分支，则会生成一个警告。  
  
## 示例详细信息  
 此示例使用要验证的每个活动（即 <xref:System.Activities.Statements.If> 活动和 <xref:System.Activities.Statements.Pick> 活动）的实例创建工作流。为每个验证行为创建一个 <xref:System.Activities.Validation.Constraint>。此示例中创建的约束为 `ConstraintError_IfShouldHaveThenOrElse` 和 `ConstraintWarning_PickHasOneBranch`。紧接着，将这些约束添加到 <xref:System.Activities.Validation.ValidationSettings> 实例的 `AdditionalConstraints` 集合中。最后，调用 <xref:System.Activities.Validation.ActivityValidationServices> 的 `static`<xref:System.Activities.Validation.ActivityValidationServices.Validate%2A> 方法以验证工作流中的活动并将验证结果输出到控制台。  
  
> [!NOTE]
>  可以向任何活动添加策略约束。例如，可以向 <xref:System.Activities.Statements.Sequence> 或 <xref:System.Activities.Statements.Parallel> 活动添加策略约束。  
  
#### 使用此示例  
  
1.  使用 [!INCLUDE[vs2010](../../../../includes/vs2010-md.md)] 打开 ExternalActivityValidation.sln 文件。  
  
2.  要生成解决方案，按 Ctrl\+Shift\+B。  
  
3.  若要运行解决方案，请按 Ctrl\+F5。  
  
> [!IMPORTANT]
>  您的计算机上可能已安装这些示例。在继续操作之前，请先检查以下（默认）目录：  
>   
>  `<安装驱动器>:\WF_WCF_Samples`  
>   
>  如果此目录不存在，请访问[针对 .NET Framework 4 的 Windows Communication Foundation \(WCF\) 和 Windows Workflow Foundation \(WF\) 示例](http://go.microsoft.com/fwlink/?LinkId=150780)（可能为英文网页），下载所有 [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] 和 [!INCLUDE[wf1](../../../../includes/wf1-md.md)] 示例。此示例位于以下目录：  
>   
>  `<安装驱动器>:\WF_WCF_Samples\WF\Basic\Validation\ExternalActivityValidation`  
  
## 请参阅