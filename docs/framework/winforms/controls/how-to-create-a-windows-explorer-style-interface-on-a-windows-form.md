---
title: "如何：在 Windows 窗体上创建 Windows 资源管理器样式的界面 | Microsoft Docs"
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
  - "窗体, Windows 资源管理器类型"
  - "SplitContainer 控件 [Windows 窗体], 资源管理器样式界面"
  - "Windows Explorer, 使用 Windows 窗体创建"
ms.assetid: 9a3d5f4f-5dda-4350-9ad5-57ce5976dc47
caps.latest.revision: 15
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 15
---
# 如何：在 Windows 窗体上创建 Windows 资源管理器样式的界面
由于用户对于 Windows 资源管理器已经比较熟悉，因此它是应用程序用户界面的通用选择。  
  
 从本质上讲，Windows 资源管理器是在不同面板上的 <xref:System.Windows.Forms.TreeView> 控件和 <xref:System.Windows.Forms.ListView> 控件。  这些面板是通过拆分器来调整大小的。  这种控件排列对于显示和浏览信息非常有用。  
  
 下面的步骤显示如何在类似于 Windows 资源管理器的窗体中排列控件。  在这些步骤中，并没有显示如何添加 Windows 资源管理器应用程序的文件浏览功能。  
  
> [!NOTE]
>  显示的对话框和菜单命令可能会与“帮助”中的描述不同，具体取决于您现用的设置或版本。  若要更改设置，请在**“工具”**菜单上选择**“导入和导出设置”**。  有关更多信息，请参见 [Customizing Development Settings in Visual Studio](http://msdn.microsoft.com/zh-cn/22c4debb-4e31-47a8-8f19-16f328d7dcd3)。  
  
### 创建 Windows 资源管理器样式的 Windows 窗体  
  
1.  创建新的“Windows 应用程序”项目。  有关详细信息，请参见[How to: Create a Windows Application Project](http://msdn.microsoft.com/zh-cn/b2f93fed-c635-4705-8d0e-cf079a264efa)。  
  
2.  从**“工具箱”**中：  
  
    1.  将 <xref:System.Windows.Forms.SplitContainer> 控件拖到窗体上。  
  
    2.  将 <xref:System.Windows.Forms.TreeView> 控件拖到 **SplitterPanel1**（<xref:System.Windows.Forms.SplitContainer> 控件的面板，标记为 **Panel1**）中。  
  
    3.  将 <xref:System.Windows.Forms.ListView> 控件拖到 **SplitterPanel2**（<xref:System.Windows.Forms.SplitContainer> 控件的面板，标记为 **Panel2**）中。  
  
3.  通过按住 Ctrl 键并依次单击所有三个控件进行全选。  在选择 <xref:System.Windows.Forms.SplitContainer> 控件时，可单击拆分条，而不单击面板。  
  
    > [!NOTE]
    >  请不要使用**“编辑”**菜单上的**“全选”**命令。  如果这样做，在下一步中所需的属性将不会显示在**“属性”**窗口中。  
  
4.  在**“属性”**窗口中，将 <xref:System.Windows.Forms.SplitContainer.Dock%2A> 属性设置为 <xref:System.Windows.Forms.DockStyle>。  
  
5.  按 F5 运行该应用程序。  
  
     窗体显示由两部分组成的用户界面，这类似于 Windows 资源管理器的用户界面。  
  
    > [!NOTE]
    >  在拖动拆分器时，面板会调整它们自身的大小。  
  
## 请参阅  
 <xref:System.Windows.Forms.SplitContainer>   
 [如何：用 Windows 窗体创建多窗格用户界面](../../../../docs/framework/winforms/controls/how-to-create-a-multipane-user-interface-with-windows-forms.md)   
 [如何：定义拆分窗口中的大小调整和定位行为](../../../../docs/framework/winforms/controls/how-to-define-resize-and-positioning-behavior-in-a-split-window.md)   
 [如何：水平拆分窗口](../../../../docs/framework/winforms/controls/how-to-split-a-window-horizontally.md)   
 [SplitContainer 控件](../../../../docs/framework/winforms/controls/splitcontainer-control-windows-forms.md)