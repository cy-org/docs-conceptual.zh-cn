---
title: "演练：向窗体提供标准菜单项 | Microsoft Docs"
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
  - "菜单项, 标准"
  - "StatusStrip 控件 [Windows 窗体]"
  - "工具栏 [Windows 窗体], 演练"
  - "ToolStrip 控件 [Windows 窗体]"
ms.assetid: dac37d98-589e-4d6d-9673-6437e8943122
caps.latest.revision: 7
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 7
---
# 演练：向窗体提供标准菜单项
可以通过 <xref:System.Windows.Forms.MenuStrip> 控件为窗体提供标准菜单。  
  
 此演练演示如何使用 <xref:System.Windows.Forms.MenuStrip> 控件创建标准菜单。  窗体还将在用户选择菜单项时作出响应。  本演练演示了以下任务：  
  
-   创建 Windows 窗体项目。  
  
-   创建标准菜单。  
  
-   创建 <xref:System.Windows.Forms.StatusStrip> 控件。  
  
-   处理菜单项的选择。  
  
 完成以上步骤后，您将得到一个包含标准菜单的窗体，该窗体在一个 <xref:System.Windows.Forms.StatusStrip> 控件中显示菜单项的选择情况。  
  
 若要将本主题中的代码作为一个单独的清单进行复制，请参见[如何：向窗体提供标准菜单项](../../../../docs/framework/winforms/controls/how-to-provide-standard-menu-items-to-a-form.md)。  
  
> [!NOTE]
>  显示的对话框和菜单命令可能会与“帮助”中的描述不同，具体取决于您现用的设置或版本。  若要更改设置，请在**“工具”**菜单上选择**“导入和导出设置”**。  有关更多信息，请参见 [Customizing Development Settings in Visual Studio](http://msdn.microsoft.com/zh-cn/22c4debb-4e31-47a8-8f19-16f328d7dcd3)。  
  
## 系统必备  
 若要完成本演练，您需要：  
  
-   足以在安装了 [!INCLUDE[vsprvs](../../../../includes/vsprvs-md.md)] 的计算机上创建和运行 Windows 窗体应用程序项目的权限。  
  
## 创建项目  
 第一步是创建项目并设置窗体。  
  
#### 创建项目  
  
1.  创建一个名为“StandardMenuForm”的 Windows 应用程序项目。  
  
     有关更多信息，请参见[How to: Create a Windows Application Project](http://msdn.microsoft.com/zh-cn/b2f93fed-c635-4705-8d0e-cf079a264efa)。  
  
2.  在 Windows 窗体设计器中，选择该窗体。  
  
## 创建标准菜单  
 Windows 窗体设计器能够自动以标准菜单项填充 <xref:System.Windows.Forms.MenuStrip> 控件。  
  
#### 创建标准菜单  
  
1.  从**“工具箱”**中将一个 <xref:System.Windows.Forms.MenuStrip> 控件拖动到窗体上。  
  
2.  单击 <xref:System.Windows.Forms.MenuStrip> 控件的智能标记标志符号 \(![智能标记标志符号](../../../../docs/framework/winforms/controls/media/vs-winformsmttagglyph.png "VS\_WinFormSmtTagGlyph")\)，然后选择**“插入标准项”**。  
  
     <xref:System.Windows.Forms.MenuStrip> 控件会用标准菜单项进行填充。  
  
3.  单击**“文件”**菜单项以查看其默认菜单项和对应的图标。  
  
## 创建 StatusStrip 控件  
 使用 <xref:System.Windows.Forms.StatusStrip> 控件显示 Windows 窗体应用程序的状态。  在本示例中，用户选择的菜单项显示于 <xref:System.Windows.Forms.StatusStrip> 控件中。  
  
#### 创建 StatusStrip 控件  
  
1.  从**“工具箱”**中将一个 <xref:System.Windows.Forms.StatusStrip> 控件拖动到窗体上。  
  
     <xref:System.Windows.Forms.StatusStrip> 控件自动停靠于窗体的底部。  
  
2.  单击 <xref:System.Windows.Forms.StatusStrip> 控件的下拉按钮并选择**“StatusLabel”**，将一个 <xref:System.Windows.Forms.ToolStripStatusLabel> 控件添加到 <xref:System.Windows.Forms.StatusStrip> 控件中。  
  
## 处理项的选择  
 处理 <xref:System.Windows.Forms.ToolStripDropDownItem.DropDownItemClicked> 事件以在用户选择菜单项时作出响应。  
  
#### 处理菜单项的选择  
  
1.  单击在“创建标准菜单”一节中创建的**“文件”**菜单项。  
  
2.  在**“属性”**窗口中，单击**“事件”**。  
  
3.  双击 <xref:System.Windows.Forms.ToolStripDropDownItem.DropDownItemClicked> 事件。  
  
     Windows 窗体设计器为 <xref:System.Windows.Forms.ToolStripDropDownItem.DropDownItemClicked> 事件生成一个事件处理程序。  
  
4.  将下面的代码插入到事件处理程序中。  
  
     [!code-csharp[System.Windows.Forms.ToolStrip.StandardMenu#3](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.ToolStrip.StandardMenu/CS/Form1.cs#3)]
     [!code-vb[System.Windows.Forms.ToolStrip.StandardMenu#3](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.ToolStrip.StandardMenu/VB/Form1.vb#3)]  
  
5.  将 `UpdateStatus` 实用工具方法的定义插入到窗体中。  
  
     [!code-csharp[System.Windows.Forms.ToolStrip.StandardMenu#2](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.ToolStrip.StandardMenu/CS/Form1.cs#2)]
     [!code-vb[System.Windows.Forms.ToolStrip.StandardMenu#2](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.ToolStrip.StandardMenu/VB/Form1.vb#2)]  
  
## 检查点  
  
#### 测试窗体  
  
1.  按 F5 编译并运行窗体。  
  
2.  单击**“文件”**菜单项以打开该菜单。  
  
3.  在**“文件”**菜单上，单击其中一个菜单项以选择该项。  
  
     <xref:System.Windows.Forms.StatusStrip> 控件显示了已选择的项。  
  
## 后续步骤  
 在此演练中，您创建了一个包含标准菜单的窗体。  <xref:System.Windows.Forms.ToolStrip> 系列控件有很多其他用途：  
  
-   使用 <xref:System.Windows.Forms.ContextMenuStrip> 来创建控件的快捷菜单。  有关更多信息，请参见 [ContextMenu 组件概述](../../../../docs/framework/winforms/controls/contextmenu-component-overview-windows-forms.md)。  
  
-   创建包含停靠的 <xref:System.Windows.Forms.ToolStrip> 控件的多文档界面 \(MDI\) 窗体。  有关更多信息，请参见[演练：创建具有菜单合并功能和 ToolStrip 控件的 MDI 窗体](../../../../docs/framework/winforms/controls/walkthrough-creating-an-mdi-form-with-menu-merging-and-toolstrip-controls.md)。  
  
-   赋予 <xref:System.Windows.Forms.ToolStrip> 控件专业的外观。  有关更多信息，请参见 [如何：为应用程序设置 ToolStrip 呈现程序](../../../../docs/framework/winforms/controls/how-to-set-the-toolstrip-renderer-for-an-application.md)。  
  
## 请参阅  
 <xref:System.Windows.Forms.MenuStrip>   
 <xref:System.Windows.Forms.ToolStrip>   
 <xref:System.Windows.Forms.StatusStrip>   
 [MenuStrip 控件](../../../../docs/framework/winforms/controls/menustrip-control-windows-forms.md)