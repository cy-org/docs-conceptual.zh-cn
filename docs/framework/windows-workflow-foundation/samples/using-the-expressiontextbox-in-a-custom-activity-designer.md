---
title: "在自定义设计器中使用 ExpressionTextBox | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: f82e73e7-a256-4a4d-82b7-c0d62f4ab5e7
caps.latest.revision: 9
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 9
---
# 在自定义设计器中使用 ExpressionTextBox
此示例演示如何在自定义活动设计器中使用 <xref:System.Activities.Presentation.View.ExpressionTextBox>。自定义活动 `MultiAssign` 将两个字符串值分配给两个字符串变量。某些 <xref:System.Activities.Presentation.View.ExpressionTextBox> 控件绑定到 <xref:System.Activities.InArgument>，而某些控件绑定到 <xref:System.Activities.OutArgument>。  
  
## 示例详细信息  
 `ArgumentToExpressionConverter` 是在将表达式绑定到参数时使用的类型转换器。`ConverterParameter` 必须设置为适当的 `In` 或 `Out`。不支持 `InOut`。  
  
 `UseLocationExpression` 特性在 `OutArgument` 上使用，以指定表达式应是一个左值（“左侧值”或“位置值”）表达式。在大多数情况下，左值表达式是有效的 Visual Basic 标识符，用于指示要返回的 `OutArgument` 是变量还是参数名称。  
  
 在此示例中，将 `MaxLines` 特性设置为 1，未设置 `MinLines`。这表示无论用户键入多少文本，<xref:System.Activities.Presentation.View.ExpressionTextBox> 都是大小固定的一行。若要允许 <xref:System.Activities.Presentation.View.ExpressionTextBox> 增大以容纳用户输入，请将 `MaxLines` 设置为大于 `MinLines`。  
  
 ExpressionTextBox 只能绑定到参数，不能绑定到 CLR 属性。  
  
#### 使用此示例  
  
1.  使用 [!INCLUDE[vs2010](../../../../includes/vs2010-md.md)] 打开 ExpressionTextBoxSample.sln 文件。  
  
2.  要生成解决方案，按 Ctrl\+Shift\+B。  
  
#### 运行此示例  
  
1.  向解决方案添加新工作流控制台应用程序。  
  
2.  从新工作流控制台应用程序项目添加对**“ExpressionTextBoxSample”**项目的引用。  
  
3.  生成解决方案。  
  
4.  将**“MultiAssign”**活动从工具箱拖放到工作流中。  
  
> [!IMPORTANT]
>  您的计算机上可能已安装这些示例。在继续操作之前，请先检查以下（默认）目录：  
>   
>  `<安装驱动器>:\WF_WCF_Samples`  
>   
>  如果此目录不存在，请访问[针对 .NET Framework 4 的 Windows Communication Foundation \(WCF\) 和 Windows Workflow Foundation \(WF\) 示例](http://go.microsoft.com/fwlink/?LinkId=150780)（可能为英文网页），下载所有 [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] 和 [!INCLUDE[wf1](../../../../includes/wf1-md.md)] 示例。此示例位于以下目录：  
>   
>  `<安装驱动器>:\WF_WCF_Samples\WF\Basic\CustomActivities\CustomActivityDesigners\ExpressionTextBox`  
  
## 请参阅  
 <xref:System.Activities.Presentation.View.ExpressionTextBox>   
 [使用工作流设计器开发应用程序](../Topic/Developing%20Applications%20with%20the%20Workflow%20Designer.md)