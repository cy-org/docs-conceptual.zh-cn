---
title: "如何：使用设计器定义工具栏按钮的图标 | Microsoft Docs"
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
  - "按钮 [Windows 窗体], 图像"
  - "示例 [Windows 窗体], 工具栏"
  - "图标 [Windows 窗体], 工具栏按钮"
  - "图像 [Windows 窗体], 工具栏按钮"
  - "ToolBar 控件 [Windows 窗体], 向按钮添加图标"
  - "工具栏 [Windows 窗体], 向按钮添加图标"
ms.assetid: d848f38e-67f2-49d4-8e88-01c845c06c02
caps.latest.revision: 7
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 7
---
# 如何：使用设计器定义工具栏按钮的图标
> [!NOTE]
>  <xref:System.Windows.Forms.ToolStrip> 控件取代了 <xref:System.Windows.Forms.ToolBar> 控件并添加了功能；但是，可以选择保留 <xref:System.Windows.Forms.ToolBar> 控件以实现向后兼容并供将来使用。  
  
 <xref:System.Windows.Forms.ToolBar> 按钮能自身中显示图标，以便用户识别。  这可以通过向 <xref:System.Windows.Forms.ImageList> 组件添加图像并将该组件与 <xref:System.Windows.Forms.ToolBar> 控件相关联来实现。  
  
 下面的过程需要一个**“Windows 应用程序”**项目，该项目要有一个包含 <xref:System.Windows.Forms.ToolBar> 控件和 <xref:System.Windows.Forms.ImageList> 组件的窗体。  有关设置此类项目的信息，请参见[How to: Create a Windows Application Project](http://msdn.microsoft.com/zh-cn/b2f93fed-c635-4705-8d0e-cf079a264efa)和[如何：向 Windows 窗体添加控件](../../../../docs/framework/winforms/controls/how-to-add-controls-to-windows-forms.md)。  
  
> [!NOTE]
>  显示的对话框和菜单命令可能会与“帮助”中的描述不同，具体取决于您现用的设置或版本。  若要更改设置，请在**“工具”**菜单上选择**“导入和导出设置”**。  有关更多信息，请参见 [Customizing Development Settings in Visual Studio](http://msdn.microsoft.com/zh-cn/22c4debb-4e31-47a8-8f19-16f328d7dcd3)。  
  
### 在设计时设置工具栏按钮的图标  
  
1.  向 <xref:System.Windows.Forms.ImageList> 组件添加图像。  有关更多信息，请参见 [如何：使用设计器添加或移除 ImageList 图像](../../../../docs/framework/winforms/controls/how-to-add-or-remove-imagelist-images-with-the-designer.md)。  
  
2.  选择窗体上的 <xref:System.Windows.Forms.ToolBar> 控件。  
  
3.  在**“属性”**窗口中，将 <xref:System.Windows.Forms.ToolBar> 控件的 <xref:System.Windows.Forms.ToolBar.ImageList%2A> 属性设置为 <xref:System.Windows.Forms.ImageList> 组件。  
  
4.  单击 <xref:System.Windows.Forms.ToolBar> 控件的 <xref:System.Windows.Forms.ToolBar.Buttons%2A> 属性以选择该属性，然后单击省略号 \(![VisualStudioEllipsesButton 屏幕快照](../../../../docs/framework/winforms/media/vbellipsesbutton.png "vbEllipsesButton")\) 按钮以打开**“ToolBarButton 集合编辑器”**。  
  
5.  使用**“添加”**按钮向 <xref:System.Windows.Forms.ToolBar> 控件添加按钮。  
  
6.  在**“ToolBarButton 集合编辑器”**右侧窗格中出现的**“属性”**窗口中，将每个工具栏按钮的 <xref:System.Windows.Forms.ToolBarButton.ImageIndex%2A> 属性设置为列表中的值之一，该值是从您添加到 <xref:System.Windows.Forms.ImageList> 组件中的图像中提取的。  
  
## 请参阅  
 <xref:System.Windows.Forms.ToolBar>   
 [如何：触发工具栏按钮的菜单事件](../../../../docs/framework/winforms/controls/how-to-trigger-menu-events-for-toolbar-buttons.md)   
 [ToolBar 控件](../../../../docs/framework/winforms/controls/toolbar-control-windows-forms.md)   
 [ImageList 组件](../../../../docs/framework/winforms/controls/imagelist-component-windows-forms.md)