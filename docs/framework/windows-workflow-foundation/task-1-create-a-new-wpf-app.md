---
title: "任务 1：创建一个新的 Windows Presentation Foundation 应用程序 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 270eaeba-9492-4532-af9f-403ce5c9935b
caps.latest.revision: 14
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 14
---
# 任务 1：创建一个新的 Windows Presentation Foundation 应用程序
在此任务中，您将使用 WPF 应用程序 Visual Studio 模板创建一个空 [!INCLUDE[avalon1](../../../includes/avalon1-md.md)] 应用程序，并添加对相应 [!INCLUDE[netfx_current_short](../../../includes/netfx-current-short-md.md)] 工作流程序集的引用。  
  
### 创建 WPF 应用程序项目  
  
1.  打开 [!INCLUDE[vs_current_short](../../../includes/vs-current-short-md.md)]，在**“文件”**菜单上指向**“新建”**，然后单击**“项目”**。  
  
2.  在**“新建项目”**对话框中，在该框左侧的**“已安装的模板”**窗格中，选择**“Visual C\#”**或**“Visual Basic”**。如果未出现您所需的语言，请在**“其他语言”**下查找。  
  
3.  在**“已安装的模板”**窗格中，选择**“Windows”**。  
  
4.  在上窗格的下拉列表框中，确认已选定（默认值）**“.NET Framework 4”**，然后选择**“WPF 应用程序”**。  
  
5.  将项目名称设置为窗口底部的 **HostingApplication**。  
  
6.  将解决方案名称设置为 **RehostingTheDesigner**。  
  
7.  单击**“确定”**创建应用程序项目。[!INCLUDE[vs_current_short](../../../includes/vs-current-short-md.md)] 为您创建基本的 WPF UI 并含有相应的 XAML 和代码隐藏文件。  
  
8.  添加对 **WorkflowModel** 程序集的引用。为此，请在**“解决方案资源管理器”**中，右击**“HostingApplication”**项目并选择**“添加引用”**。  
  
9. 在**“添加引用”**对话框中，单击**“.NET”**选项卡，按住 Ctrl 键并选择下列程序集，然后单击**“确定”**：  
  
    -   System.Activities  
  
    -   System.Activities.Presentation  
  
    -   System.Activities.Core.Presentation  
  
10. 单击**“确定”**。  
  
11. 请参见[任务 2：承载工作流设计器](../../../docs/framework/windows-workflow-foundation//task-2-host-the-workflow-designer.md)，了解如何承载工作流设计器设计画布。  
  
## 请参阅  
 [重新承载工作流设计器](../../../docs/framework/windows-workflow-foundation//rehosting-the-workflow-designer.md)   
 [任务 2：承载工作流设计器](../../../docs/framework/windows-workflow-foundation//task-2-host-the-workflow-designer.md)