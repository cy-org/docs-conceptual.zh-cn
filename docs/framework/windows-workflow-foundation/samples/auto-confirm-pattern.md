---
title: "自动确认模式 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 668aec65-78d3-4636-9c7b-deed643a18f9
caps.latest.revision: 6
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 6
---
# 自动确认模式
此示例包含三个用来说明自定义 `AutoConfirmScope` 活动的方案。第一个示例演示一个由四个可补偿活动组成的序列的成功执行，其中的第二个和第三个可补偿活动嵌套到 `AutoConfirmScope` 中。第二个示例演示相同的序列，但在执行第四个 <xref:System.Activities.Statements.CompensableActivity> 之后会发生异常。第三个方案演示相同的序列，但在第二个 <xref:System.Activities.Statements.CompensableActivity> 完成后 `AutoConfirmScope` 中会发生异常。  
  
 此示例演示自动确认模式，在此模式中，在成功完成范围之后立即确认所有的子级可补偿活动。此模式定义所有子级可补偿活动的生存期，在生存期过后，再也无法补偿或确认这些活动。  
  
 此范围包含一个 <xref:System.Activities.Statements.TryCatch>，其中的 <xref:System.Activities.Statements.TryCatch.Try%2A> 是一个内部 <xref:System.Activities.Statements.CompensableActivity>。`AutoConfirmScope` 的用户指定主体是内部 <xref:System.Activities.Statements.CompensableActivity> 的主体。当此内部 <xref:System.Activities.Statements.CompensableActivity> 完成时，它会生成一个 <xref:System.Activities.Statements.CompensationToken> 作为 out 参数。`AutoConfirmScope` 使用 <xref:System.Activities.Statements.TryCatch.Finally%2A> 检查是否已生成此令牌，如果已生成此令牌，则确认内部 <xref:System.Activities.Statements.CompensableActivity>。内部 <xref:System.Activities.Statements.CompensableActivity> 为可能存在于其主体中的任何可补偿活动调用默认补偿。  
  
 第一个方案演示成功执行工作流，并演示在工作流完成并确认第一个和第四个可补偿活动时，已确认第二个和第三个可补偿活动。这将产生 3、2、4 和 1 的确认顺序。  
  
 第二个方案演示完成第四个可补偿活动之后的异常。因为可补偿活动 2 和 3 已经得到确认，所以不影响它们，但要补偿可补偿活动 1 和 4。这将产生确认 3、确认 2、补偿 4 和补偿 1。  
  
 最后一个方案演示未成功执行 `AutoConfirmScope`。在此方案中，在完成第二个 <xref:System.Activities.Statements.CompensableActivity> 之后发生异常。因为未执行第三个和第四个可补偿活动，所以不影响它们。因为此范围未成功完成，所以第二个 <xref:System.Activities.Statements.CompensableActivity> 未得到确认。这将产生先 2 后 1 的补偿顺序。  
  
#### 使用此示例  
  
1.  使用 [!INCLUDE[vs2010](../../../../includes/vs2010-md.md)] 打开 AutoConfirmSample.sln 解决方案文件。  
  
2.  要生成解决方案，按 Ctrl\+Shift\+B。  
  
3.  若要运行解决方案，请按 Ctrl\+F5。  
  
> [!IMPORTANT]
>  您的计算机上可能已安装这些示例。在继续操作之前，请先检查以下（默认）目录：  
>   
>  `<安装驱动器>:\WF_WCF_Samples`  
>   
>  如果此目录不存在，请访问[针对 .NET Framework 4 的 Windows Communication Foundation \(WCF\) 和 Windows Workflow Foundation \(WF\) 示例](http://go.microsoft.com/fwlink/?LinkId=150780)（可能为英文网页），下载所有 [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] 和 [!INCLUDE[wf1](../../../../includes/wf1-md.md)] 示例。此示例位于以下目录。  
>   
>  `<安装驱动器>:\WF_WCF_Samples\WF\Scenario\Compensation\AutoConfirm`  
  
## 请参阅