---
title: "使用 TryCatch 在 Flowchart 活动中进行错误处理 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 50922964-bfe0-4ba8-9422-0e7220d514fd
caps.latest.revision: 12
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 12
---
# 使用 TryCatch 在 Flowchart 活动中进行错误处理
此示例演示如何在复杂控制流活动中使用 <xref:System.Activities.Statements.TryCatch> 活动。  
  
 在此示例中，将促销代码和孩子数量作为变量传递到 <xref:System.Activities.Statements.Flowchart> 活动，该活动将根据与促销代码相对应的公式计算折扣。此示例分为命令性代码版本和工作流设计器版本。  
  
 下表详细描述了 `CreateFlowchartWithFaults` 活动的变量。  
  
|参数|说明|  
|--------|--------|  
|promoCode|促销代码。类型：String<br /><br /> 可能的值，括号中带有说明：<br /><br /> -   Single（单身）<br />-   MNK（已婚但没有孩子。）<br />-   MWK（已婚并且有孩子。）|  
|numKids|孩子数量。类型：int|  
  
 `CreateFlowchartWithFaults` 活动使用 <xref:System.Activities.Statements.FlowSwitch%601> 活动，后者根据 `promoCode` 参数进行切换并使用以下公式计算折扣。  
  
|`promoCode` 的值|折扣 \(%\)|  
|--------------------|--------------|  
|Single|10|  
|MNK|15|  
|MWK|15 \+ \(1 – 1\/`numberOfKids`\)\*10 **Note:**  此计算可能会引发 <xref:System.DivideByZeroException>。因此，将折扣计算包装在 <xref:System.Activities.Statements.TryCatch> 活动中，该活动可捕获 <xref:System.DivideByZeroException> 异常并将折扣设置为零。|  
  
#### 使用此示例  
  
1.  使用 [!INCLUDE[vs2010](../../../../includes/vs2010-md.md)] 打开 FlowchartWithFaultHandling.sln 解决方案文件。  
  
2.  要生成解决方案，按 Ctrl\+Shift\+B。  
  
3.  若要运行解决方案，请按 F5。  
  
> [!IMPORTANT]
>  您的计算机上可能已安装这些示例。在继续操作之前，请先检查以下（默认）目录。  
>   
>  `<安装驱动器>:\WF_WCF_Samples`  
>   
>  如果此目录不存在，请访问[针对 .NET Framework 4 的 Windows Communication Foundation \(WCF\) 和 Windows Workflow Foundation \(WF\) 示例](http://go.microsoft.com/fwlink/?LinkId=150780)（可能为英文网页），下载所有 [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] 和 [!INCLUDE[wf1](../../../../includes/wf1-md.md)] 示例。此示例位于以下目录：  
>   
>  `<安装驱动器>:\WF_WCF_Samples\WF\Basic\Built-InActivities\FlowChartWithFaultHandling`  
  
## 请参阅  
 [流程图工作流](../../../../docs/framework/windows-workflow-foundation//flowchart-workflows.md)   
 [异常](../../../../docs/framework/windows-workflow-foundation//exceptions.md)