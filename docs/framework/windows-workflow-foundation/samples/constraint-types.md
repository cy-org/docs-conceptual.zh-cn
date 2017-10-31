---
title: "约束类型 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: b6b246e6-1130-4698-9625-c5c42abcbfed
caps.latest.revision: 9
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 9
---
# 约束类型
本实例演示将约束应用于工作流的两种不同方法：一种方法是从活动内部应用（生成），另一种方法是从活动外部应用（策略）。在此方案中，某个活动作者（来自于第三方软件公司）想要验证两个参数之间的关系。在此例中，成本应小于或等于价格。这是一个常规的验证生成约束。  
  
 然后，一个店主想要为此常规活动中添加一些验证。对于他而言，他想要让大多数产品的价格为 9.99 美元或者更少。因此，他在 `CreateProduct` 活动之上使用一个策略约束。  
  
 在此示例中：  
  
 活动作者（生成）必须：  
  
-   创建一个约束 \(`PriceGreaterThanCost`\)。这是存放全部验证逻辑的位置。  
  
-   重写 <xref:System.Activities.CodeActivity%601.OnGetConstraints%2A> 并将约束 \(`PriceGreaterThanCost`\) 添加到约束集 <xref:System.Collections.IList> 中。  
  
 工作流作者（策略）必须：  
  
-   使用要验证的活动实例来创建一个工作流 \(`CreateProduct`\)。  
  
-   创建一个约束 \(`MaxPrice`\)。  
  
-   创建一个 <xref:System.Activities.Validation.ValidatorSettings> 实例 \(`validatorSettings`\)，并将约束 \(`MaxPrice`\) 添加到集合 `AdditionalConstraints` 中。在此处，工作流作者可以将策略约束添加到任何活动，例如一个序列或并行活动。  
  
-   调用 <xref:System.Activities.Validation.ActivityValidationServices.Validate%2A>，它将返回 <xref:System.Activities.Validation.ConstraintViolation> 对象的 <xref:System.Activities.Validation.ValidationResults> 的集合。  
  
-   （可选）输出 <xref:System.Activities.Validation.ConstraintViolation> 对象。  
  
### 设置、生成和运行示例  
  
1.  在 [!INCLUDE[vs2010](../../../../includes/vs2010-md.md)] 中打开 ConstraintTypes.sln 示例解决方案。  
  
2.  生成和运行解决方案。  
  
> [!IMPORTANT]
>  您的计算机上可能已安装这些示例。在继续操作之前，请先检查以下（默认）目录：  
>   
>  `<安装驱动器>:\WF_WCF_Samples`  
>   
>  如果此目录不存在，请访问[针对 .NET Framework 4 的 Windows Communication Foundation \(WCF\) 和 Windows Workflow Foundation \(WF\) 示例](http://go.microsoft.com/fwlink/?LinkId=150780)（可能为英文网页），下载所有 [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] 和 [!INCLUDE[wf1](../../../../includes/wf1-md.md)] 示例。此示例位于以下目录：  
>   
>  `<安装驱动器>:\WF_WCF_Samples\WF\Scenario\Validation\ConstraintLibrary`  
  
## 请参阅