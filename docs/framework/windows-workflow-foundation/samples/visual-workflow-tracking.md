---
title: "可视工作流跟踪 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 0143448f-2044-40a0-8a3d-941f6d12468b
caps.latest.revision: 10
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 10
---
# 可视工作流跟踪
此示例演示如何使用 [!INCLUDE[netfx_current_short](../../../../includes/netfx-current-short-md.md)] 提供的调试功能编写可视工作流跟踪应用程序。  
  
## 示例详细信息  
 该应用程序执行简单的流程图工作流（已在 Workflow.xaml 中定义）并重新承载工作流设计器以显示当前正在执行的工作流。在执行工作流时，显示的当前正在执行的活动将带有一个黄色边框和调试箭头。此外，工作流生成的跟踪记录也会显示在应用程序窗口中。有关 [!INCLUDE[crabout](../../../../includes/crabout-md.md)] 工作流跟踪，请参见 [工作流跟踪](../../../../docs/framework/windows-workflow-foundation//workflow-tracking-and-tracing.md)。有关重新承载工作流设计器的 [!INCLUDE[crabout](../../../../includes/crabout-md.md)]，请参见 [重新承载工作流设计器](../../../../docs/framework/windows-workflow-foundation//rehosting-the-workflow-designer.md)。  
  
 工作流模拟器利用两个字典来执行工作。一个字典包含当前正在执行的活动对象与实例化活动时使用的 XAML 行号之间的映射。另一个字典包含活动实例 ID 与活动对象之间的映射。在使用自定义跟踪配置文件发出跟踪记录时，应用程序将确定当前正在执行的活动的实例 ID，并将其映射回用于对其进行实例化的 XAML 文件。然后指示重新承载的工作流设计器在设计图面上突出显示该活动，并将同一方法用作工作流调试器，具体而言，在该活动周围绘制黄色边框并沿设计器的左侧显示一个黄色箭头。  
  
#### 使用此示例  
  
1.  从 [!INCLUDE[vs2010](../../../../includes/vs2010-md.md)] 中的示例目录中打开 WorkflowSimulator.sln 文件。  
  
2.  按 Ctrl\+Shift\+B 生成解决方案。  
  
3.  按 Ctrl\+F5 运行示例。这将在重新承载的工作流设计器窗口中显示 Workflow.xaml 文件。  
  
4.  单击**“文件”**菜单，并选择**“运行工作流...”**。  
  
5.  请注意，将突出显示当前正在执行的活动（如前所述），并将在应用程序窗口的右侧显示跟踪记录。  
  
6.  在完成工作流后，可以单击任一跟踪记录以检查该记录对应的活动。  
  
> [!IMPORTANT]
>  您的计算机上可能已安装这些示例。在继续操作之前，请先检查以下（默认）目录：  
>   
>  `<安装驱动器>:\WF_WCF_Samples`  
>   
>  如果此目录不存在，请访问[针对 .NET Framework 4 的 Windows Communication Foundation \(WCF\) 和 Windows Workflow Foundation \(WF\) 示例](http://go.microsoft.com/fwlink/?LinkId=150780)（可能为英文网页），下载所有 [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] 和 [!INCLUDE[wf1](../../../../includes/wf1-md.md)] 示例。此示例位于以下目录：  
>   
>  `<安装驱动器>:\WF_WCF_Samples\WF\Application\VisualWorkflowTracking`  
  
## 请参阅