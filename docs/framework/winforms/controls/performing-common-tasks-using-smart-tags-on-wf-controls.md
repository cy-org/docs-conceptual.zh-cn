---
title: "演练：使用 Windows 窗体控件上的智能标记执行常规任务 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-winforms"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "jsharp"
helpviewer_keywords: 
  - "设计器操作"
  - "DesignerAction 对象模型"
  - "智能标记"
ms.assetid: cac337e6-00f6-4584-80f4-75728f5ea113
caps.latest.revision: 15
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 15
---
# 演练：使用 Windows 窗体控件上的智能标记执行常规任务
在为 Windows 窗体应用程序构造窗体和控件时，要重复执行许多任务。  以下是您将遇到的一些通常要执行的任务：  
  
-   在 <xref:System.Windows.Forms.TabControl> 上添加或移除选项卡。  
  
-   将控件停靠到其父控件。  
  
-   更改 <xref:System.Windows.Forms.SplitContainer> 控件的方向。  
  
 为了加快开发速度，许多控件提供了智能标记。这些智能标记是区分上下文的菜单，允许您在设计时以一个操作即可执行此类常规任务。  这些任务称作“智能标记谓词”。  
  
 在设计器中，附加到一个控件实例上的智能标记在其生命周期内始终保持可用。  
  
 本演练涉及以下任务：  
  
-   创建 Windows 窗体项目  
  
-   使用智能标记  
  
-   启用和禁用智能标  
  
 完成本演练后，您将对这些重要的布局功能所扮演的角色有所了解。  
  
> [!NOTE]
>  显示的对话框和菜单命令可能会与“帮助”中的描述不同，具体取决于您现用的设置或版本。  若要更改设置，请在**“工具”**菜单上选择**“导入和导出设置”**。  有关更多信息，请参见 [Customizing Development Settings in Visual Studio](http://msdn.microsoft.com/zh-cn/22c4debb-4e31-47a8-8f19-16f328d7dcd3)。  
  
## 创建项目  
 第一步是创建项目并设置窗体。  
  
#### 创建项目  
  
1.  创建名为“SmartTagsExample”的基于 Windows 的应用程序项目。  有关详细信息，请参见[How to: Create a Windows Application Project](http://msdn.microsoft.com/zh-cn/b2f93fed-c635-4705-8d0e-cf079a264efa)。  
  
2.  在**“Windows 窗体设计器”**中选择窗体。  
  
## 使用智能标记  
 在设计时，智能标记在提供这些智能标记的控件上始终可用。  
  
#### 使用智能标记  
  
1.  从**“工具箱”**中将一个 <xref:System.Windows.Forms.TabControl> 拖到窗体上。  注意显示在 <xref:System.Windows.Forms.TabControl> 旁边的智能标记标志符号 \(![智能标记标志符号](../../../../docs/framework/winforms/controls/media/vs-winformsmttagglyph.png "VS\_WinFormSmtTagGlyph")\)。  
  
2.  单击智能标记标志符号。  在标志符号旁显示的快捷菜单上选择**“添加选项卡”**项。  可看到 <xref:System.Windows.Forms.TabControl> 上添加了一个新的选项卡页。  
  
3.  从**“工具箱”**中将一个 <xref:System.Windows.Forms.TableLayoutPanel> 控件拖到窗体上。  
  
4.  单击智能标记标志符号。  在标志符号旁显示的快捷菜单上选择**“添加列”**项。  可看到 <xref:System.Windows.Forms.TableLayoutPanel> 控件上添加了一个新列。  
  
5.  从**“工具箱”**中将一个 <xref:System.Windows.Forms.SplitContainer> 控件拖到窗体上。  
  
6.  单击智能标记标志符号。  在标志符号旁显示的快捷菜单上选择**“水平拆分器方向”**项。  可看到 <xref:System.Windows.Forms.SplitContainer> 控件的拆分栏现在处于水平方向。  
  
## 请参阅  
 <xref:System.Windows.Forms.TextBox>   
 <xref:System.Windows.Forms.TabControl>   
 <xref:System.Windows.Forms.SplitContainer>   
 <xref:System.ComponentModel.Design.DesignerActionList>   
 [Walkthrough: Adding Smart Tags to a Windows Forms Component](../Topic/Walkthrough:%20Adding%20Smart%20Tags%20to%20a%20Windows%20Forms%20Component.md)