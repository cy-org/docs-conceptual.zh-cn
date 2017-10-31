---
title: "调试工作流 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: b23b4814-ebb1-4c51-b7a9-469f4da7a96d
caps.latest.revision: 8
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 8
---
# 调试工作流
[!INCLUDE[netfx_current_long](../../../includes/netfx-current-long-md.md)]提供多个用于从开发环境调试运行的工作流的选项。  可以在设计器、XAML 和代码中调试工作流。  
  
## 在工作流设计器中调试  
 在工作流设计器中，可以通过突出显示活动并按**“F9”**或通过使用活动的上下文菜单在活动上设置断点。  然后，当工作流宿主在调试模式下运行时将中断工作流的执行。  在下面的屏幕快照中，工作流执行在断点处暂停。  [!INCLUDE[crdefault](../../../includes/crdefault-md.md)][使用工作流设计器调试工作流](../Topic/Debugging%20Workflows%20with%20the%20Workflow%20Designer.md)。  
  
## 在 XAML 中调试  
 如果在设计器中某个工作流已在断点处暂停，则还可以在 XAML 中调试该工作流。  若要在 XAML 中查看执行点，请在工作流执行暂停时在工作流设计器中选择**“XAML 视图”**。  通过从解决方案资源管理器重新打开工作流可以将调试切换回设计器。  [!INCLUDE[crdefault](../../../includes/crdefault-md.md)][如何：使用工作流设计器调试 XAML](../Topic/How%20to:%20Debug%20XAML%20with%20the%20Workflow%20Designer.md)。  
  
## 在代码中调试  
 也可以在 [!INCLUDE[netfx_current_short](../../../includes/netfx-current-short-md.md)] 中使用代码断点，其使用方式与在其他命令性应用程序中相同。  单击代码窗格的左侧空白处可创建一个代码断点，或者按**“F9”**在光标位置处放置一个断点。  
  
## 附加到工作流过程  
 工作流调试还支持使用 Visual Studio 的基础结构附加到某个过程。  这使工作流创作者能够调试在另一个宿主环境（如 Internet 信息服务 \(IIS\) 7.0）中运行的工作流。  
  
## 远程调试  
 [!INCLUDE[wf](../../../includes/wf-md.md)] 远程调试的作用方式与其他 [!INCLUDE[vs_current_short](../../../includes/vs-current-short-md.md)] 组件的远程调试相同。  有关使用远程调试的信息，请参见[如何启用远程调试](http://go.microsoft.com/fwlink/?LinkId=196257)（可能为英文网页）。  
  
> [!NOTE]
>  如果工作流应用程序针对 x86 体系结构并位于运行 64 位操作系统的计算机上，远程调试将无法工作，除非在远程计算机上安装了 [!INCLUDE[vs_current_short](../../../includes/vs-current-short-md.md)] 或将工作流应用程序的目标更改为**“任意 CPU”**。  
  
## 扩展工作流调试服务  
 工作流调试器服务现在以公共方式使用，可以使用该服务创建自定义应用程序，如在重新承载的设计器中进行监视、模拟和调试。  [!INCLUDE[crdefault](../../../includes/crdefault-md.md)] <xref:System.Activities.Presentation.Debug.DebuggerService> 主题。