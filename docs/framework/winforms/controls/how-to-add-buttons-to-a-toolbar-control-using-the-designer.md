---
title: "如何：使用设计器向 ToolBar 控件添加按钮 | Microsoft Docs"
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
  - "示例 [Windows 窗体], 工具栏"
  - "ToolBar 控件 [Windows 窗体], 添加按钮"
  - "ToolBar 控件 [Windows 窗体], 添加下拉菜单"
  - "ToolBar 控件 [Windows 窗体], 添加分隔符"
  - "工具栏 [Windows 窗体], 添加按钮"
ms.assetid: d9ce3040-3e21-4e2d-80ae-b430982b2db8
caps.latest.revision: 8
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 8
---
# 如何：使用设计器向 ToolBar 控件添加按钮
> [!NOTE]
>  <xref:System.Windows.Forms.ToolStrip> 控件取代了 <xref:System.Windows.Forms.ToolBar> 控件并添加了功能；但是，可以选择保留 <xref:System.Windows.Forms.ToolBar> 控件以实现向后兼容并供将来使用。  
  
 <xref:System.Windows.Forms.ToolBar> 控件中添加的按钮是该控件的必要组成部分。  使用这些按钮可以很容易地访问菜单命令；或者也可以将它们放在应用程序用户界面的另一个区域，向用户公开菜单结构中不可用的命令。  
  
 下面的过程需要一个**“Windows 应用程序”**项目，该项目拥有一个包含 <xref:System.Windows.Forms.ToolBar> 控件的窗体。  有关设置此类项目的信息，请参见[How to: Create a Windows Application Project](http://msdn.microsoft.com/zh-cn/b2f93fed-c635-4705-8d0e-cf079a264efa)和[如何：向 Windows 窗体添加控件](../../../../docs/framework/winforms/controls/how-to-add-controls-to-windows-forms.md)。  
  
> [!NOTE]
>  显示的对话框和菜单命令可能会与“帮助”中的描述不同，具体取决于您现用的设置或版本。  若要更改设置，请在**“工具”**菜单上选择**“导入和导出设置”**。  有关更多信息，请参见 [Customizing Development Settings in Visual Studio](http://msdn.microsoft.com/zh-cn/22c4debb-4e31-47a8-8f19-16f328d7dcd3)。  
  
### 在设计时添加按钮  
  
1.  选择 <xref:System.Windows.Forms.ToolBar> 控件。  
  
2.  在**“属性”**窗口中，单击 <xref:System.Windows.Forms.ToolBar.Buttons%2A> 属性以选择该属性，然后单击**“省略号”**\(![VisualStudioEllipsesButton 屏幕快照](../../../../docs/framework/winforms/media/vbellipsesbutton.png "vbEllipsesButton")\) 按钮以打开**“ToolBarButton 集合编辑器”**。  
  
3.  使用**“添加”**和**“移除”**按钮分别向 <xref:System.Windows.Forms.ToolBar> 控件中添加按钮和从中移除按钮。  
  
4.  在编辑器右侧窗格中出现的**“属性”**窗口中配置各个按钮的属性。  下表显示需要考虑的一些重要属性。  
  
    |属性|说明|  
    |--------|--------|  
    |<xref:System.Windows.Forms.ToolBarButton.DropDownMenu%2A>|设置要在下拉工具栏按钮中显示的菜单。  工具栏按钮的 <xref:System.Windows.Forms.ToolBarButton.Style%2A> 属性必须设置为 <xref:System.Windows.Forms.ToolBarButtonStyle>。  该属性将 <xref:System.Windows.Forms.ContextMenu> 类的一个实例作为引用。|  
    |<xref:System.Windows.Forms.ToolBarButton.PartialPush%2A>|设置切换样式的按钮是否为部分下压。  工具栏按钮的 <xref:System.Windows.Forms.ToolBarButton.Style%2A> 属性必须设置为 <xref:System.Windows.Forms.ToolBarButtonStyle>。|  
    |<xref:System.Windows.Forms.ToolBarButton.Pushed%2A>|设置切换样式的工具栏按钮当前是否处于下压状态。  工具栏按钮的 <xref:System.Windows.Forms.ToolBarButton.Style%2A> 属性必须设置为 <xref:System.Windows.Forms.ToolBarButtonStyle> 或 <xref:System.Windows.Forms.ToolBarButtonStyle>。|  
    |<xref:System.Windows.Forms.ToolBarButton.Style%2A>|设置工具栏按钮的样式。  必须是 <xref:System.Windows.Forms.ToolBarButtonStyle> 枚举中的值之一。|  
    |<xref:System.Windows.Forms.ToolBarButton.Text%2A>|按钮显示的文本字符串。|  
    |<xref:System.Windows.Forms.ToolBarButton.ToolTipText%2A>|显示为按钮的工具提示的文本。|  
  
5.  单击**“确定”**可关闭对话框并创建您指定的面板。  
  
## 请参阅  
 <xref:System.Windows.Forms.ToolBar>   
 [如何：定义工具栏按钮的图标](../../../../docs/framework/winforms/controls/how-to-define-an-icon-for-a-toolbar-button.md)   
 [如何：触发工具栏按钮的菜单事件](../../../../docs/framework/winforms/controls/how-to-trigger-menu-events-for-toolbar-buttons.md)   
 [ToolBar 控件概述](../../../../docs/framework/winforms/controls/toolbar-control-overview-windows-forms.md)   
 [ToolBar 控件](../../../../docs/framework/winforms/controls/toolbar-control-windows-forms.md)