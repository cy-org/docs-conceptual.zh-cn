---
title: "根据功能列出的 Windows 窗体控件 | Microsoft Docs"
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
  - "控件 [Windows 窗体], 按功能"
  - "Windows 窗体控件, 列表"
  - "Windows 窗体, 按功能分类的控件"
ms.assetid: 5e65a6c3-5d6f-480d-beb8-b28f865f07e3
caps.latest.revision: 15
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 15
---
# 根据功能列出的 Windows 窗体控件
Windows 窗体提供执行许多功能的控件和组件。  下表列出了与一般功能对应的 Windows 窗体控件和组件。  此外，如果提供同一功能的控件有多个，还会指出推荐的控件，并提供关于它所取代的控件的说明。  在随后的一个单独的表中，会将被取代的控件及推荐的替代控件同时列出。  
  
> [!NOTE]
>  下表未列出可以在 Windows 窗体中使用的每一个控件或组件；有关更完整的列表，请参见 [在 Windows 窗体上使用的控件](../../../../docs/framework/winforms/controls/controls-to-use-on-windows-forms.md)  
  
## 按功能列出的推荐控件和组件  
  
|功能|控件|说明|  
|--------|--------|--------|  
|数据显示|<xref:System.Windows.Forms.DataGridView> 控件|<xref:System.Windows.Forms.DataGridView> 控件提供用来显示数据的可自定义表。  使用 <xref:System.Windows.Forms.DataGridView> 类，可以自定义单元格、行、列和边框。 **Note:**  <xref:System.Windows.Forms.DataGridView> 控件提供了 <xref:System.Windows.Forms.DataGrid> 控件中没有的许多基本功能和高级功能。  有关更多信息，请参见[Windows 窗体 DataGridView 控件和 DataGrid 控件之间的区别](../../../../docs/framework/winforms/controls/differences-between-the-windows-forms-datagridview-and-datagrid-controls.md)|  
|数据绑定和定位|<xref:System.Windows.Forms.BindingSource> 组件|通过提供当前项管理、更改通知和其他服务，来简化将窗体上的控件绑定到数据的过程。|  
||<xref:System.Windows.Forms.BindingNavigator> 控件|提供工具栏式的界面来定位和操作窗体上的数据。|  
|文本编辑|<xref:System.Windows.Forms.TextBox> 控件|显示设计时输入的文本，它可由用户在运行时编辑或以编程方式更改。|  
||<xref:System.Windows.Forms.RichTextBox> 控件|使文本能够以纯文本或 RTF 格式显示。|  
||<xref:System.Windows.Forms.MaskedTextBox> 控件|约束用户输入的格式|  
|信息显示（只读）|<xref:System.Windows.Forms.Label> 控件|显示用户无法直接编辑的文本。|  
||<xref:System.Windows.Forms.LinkLabel> 控件|将文本显示为 Web 样式的链接，并在用户单击该特殊文本时触发事件。  该文本通常是到另一个窗口或网站的链接。|  
||<xref:System.Windows.Forms.StatusStrip> 控件|通常在父窗体的底部使用有框架的区域显示有关应用程序的当前状态的信息。|  
||<xref:System.Windows.Forms.ProgressBar> 控件|向用户显示操作的当前进度。|  
|网页显示|<xref:System.Windows.Forms.WebBrowser> 控件|使用户可以在窗体内导航网页。|  
|从列表中选择|<xref:System.Windows.Forms.CheckedListBox> 控件|显示一个可滚动的项列表，每项旁边都有一个复选框。|  
||<xref:System.Windows.Forms.ComboBox> 控件|显示一个下拉式项列表。|  
||<xref:System.Windows.Forms.DomainUpDown> 控件|显示用户可用向上和向下按钮滚动的文本项列表。|  
||<xref:System.Windows.Forms.ListBox> 控件|显示一个文本项和图形项（图标）列表。|  
||<xref:System.Windows.Forms.ListView> 控件|在四个不同视图之一中显示项。  这些视图包括纯文本视图、带有小图标的文本视图、带有大图标的文本视图和详细信息视图。|  
||<xref:System.Windows.Forms.NumericUpDown> 控件|显示用户可用向上和向下按钮滚动的数字列表。|  
||<xref:System.Windows.Forms.TreeView> 控件|显示一个节点对象的分层集合，这些节点对象由带有可选复选框或图标的文本组成。|  
|图形显示|<xref:System.Windows.Forms.PictureBox> 控件|在一个框架中显示图形文件（如位图和图标）。|  
|图形存储|<xref:System.Windows.Forms.ImageList> 控件|充当图像储存库。  <xref:System.Windows.Forms.ImageList> 控件及其包含的图像可以在不同的应用程序中重用。|  
|值的设置|<xref:System.Windows.Forms.CheckBox> 控件|显示一个复选框和一个文本标签。  通常用来设置选项。|  
||<xref:System.Windows.Forms.CheckedListBox> 控件|显示一个可滚动的项列表，每项旁边都有一个复选框。|  
||<xref:System.Windows.Forms.RadioButton> 控件|显示一个可打开或关闭的按钮。|  
||<xref:System.Windows.Forms.TrackBar> 控件|允许用户通过沿标尺移动“滚动块”来设置标尺上的值。|  
|数据的设置|<xref:System.Windows.Forms.DateTimePicker> 控件|显示一个图形日历以允许用户选择日期或时间。|  
||<xref:System.Windows.Forms.MonthCalendar> 控件|显示一个图形日历以允许用户选择日期范围。|  
|对话框|<xref:System.Windows.Forms.ColorDialog> 控件|显示允许用户设置界面元素的颜色的颜色选择器对话框。|  
||<xref:System.Windows.Forms.FontDialog> 控件|显示允许用户设置字体及其特性的对话框。|  
||<xref:System.Windows.Forms.OpenFileDialog> 控件|显示允许用户定位文件和选择文件的对话框。|  
||<xref:System.Windows.Forms.PrintDialog> 控件|显示允许用户选择打印机并设置其特性的对话框。|  
||<xref:System.Windows.Forms.PrintPreviewDialog> 控件|显示一个对话框，该对话框显示 <xref:System.Drawing.Printing.PrintDocument> 组件在打印出来后的外观。|  
||<xref:System.Windows.Forms.FolderBrowserDialog> 控件|显示用来浏览、创建以及最终选择文件夹的对话框|  
||<xref:System.Windows.Forms.SaveFileDialog> 控件|显示允许用户保存文件的对话框。|  
|菜单控件|<xref:System.Windows.Forms.MenuStrip> 控件|创建自定义菜单 **Note:**  <xref:System.Windows.Forms.MenuStrip> 用于取代 <xref:System.Windows.Forms.MainMenu> 控件。|  
||<xref:System.Windows.Forms.ContextMenuStrip> 控件|创建自定义上下文菜单。 **Note:**  <xref:System.Windows.Forms.ContextMenuStrip> 用于取代 <xref:System.Windows.Forms.ContextMenu> 控件。|  
|命令|<xref:System.Windows.Forms.Button> 控件|启动、停止或中断进程。|  
||<xref:System.Windows.Forms.LinkLabel> 控件|将文本显示为 Web 样式的链接，并在用户单击该特殊文本时触发事件。  该文本通常是到另一个窗口或网站的链接。|  
||<xref:System.Windows.Forms.NotifyIcon> 控件|在表示正在后台运行的应用程序的任务栏的状态通知区域中显示一个图标。|  
||<xref:System.Windows.Forms.ToolStrip> 控件|创建工具栏，这些工具栏可以具有与 Microsoft Windows XP、Microsoft Office 或 Microsoft Internet Explorer 类似的外观，也可以具有自定义外观，可以有主题，也可以没有主题，并支持溢出和运行时项重新排序。 **Note:**  <xref:System.Windows.Forms.ToolStrip> 控件的设计目的是为了取代 <xref:System.Windows.Forms.ToolBar> 控件。|  
|用户帮助|<xref:System.Windows.Forms.HelpProvider> 组件|提供控件的弹出帮助或联机帮助。|  
||<xref:System.Windows.Forms.ToolTip> 组件|当用户将指针停留在控件上时，提供一个弹出式窗口来显示该控件的用途的简短说明。|  
|将其他控件分组|<xref:System.Windows.Forms.Panel> 控件|将一组控件分组到未标记、可滚动的框架中。|  
||<xref:System.Windows.Forms.GroupBox> 控件|将一组控件（如单选按钮 \(RadioButton\)）分组到带标记、不可滚动的框架中。|  
||<xref:System.Windows.Forms.TabControl> 控件|提供一个选项卡式页面以有效地组织和访问已分组对象。|  
||<xref:System.Windows.Forms.SplitContainer> 控件|提供用可移动拆分条分隔的两个面板。 **Note:**  <xref:System.Windows.Forms.SplitContainer> 控件的设计目的是为了取代 <xref:System.Windows.Forms.Splitter> 控件。|  
||<xref:System.Windows.Forms.TableLayoutPanel> 控件|表示一个面板，它可以在一个由行和列组成的网格中对其内容进行动态布局。|  
||<xref:System.Windows.Forms.FlowLayoutPanel> 控件|表示一个沿水平或垂直方向动态排放其内容的面板。|  
|音频|<xref:System.Media.SoundPlayer> 控件|播放 .wav 格式的声音文件。  加载声音和播放声音可以异步进行。|  
  
## 按功能列出的被取代控件和组件  
  
|功能|被取代的控件|推荐的替代控件|  
|--------|------------|-------------|  
|数据显示|<xref:System.Windows.Forms.DataGrid>|<xref:System.Windows.Forms.DataGridView>|  
|信息显示（只读控件）|<xref:System.Windows.Forms.StatusBar>|<xref:System.Windows.Forms.StatusStrip>|  
|菜单控件|<xref:System.Windows.Forms.ContextMenu>|<xref:System.Windows.Forms.ContextMenuStrip>|  
||<xref:System.Windows.Forms.MainMenu>|<xref:System.Windows.Forms.MenuStrip>|  
|命令|<xref:System.Windows.Forms.ToolBar>|<xref:System.Windows.Forms.ToolStrip>|  
||<xref:System.Windows.Forms.StatusBar>|<xref:System.Windows.Forms.StatusStrip>|  
|窗体布局|<xref:System.Windows.Forms.Splitter>|<xref:System.Windows.Forms.SplitContainer>|  
  
## 请参阅  
 [在 Windows 窗体上使用的控件](../../../../docs/framework/winforms/controls/controls-to-use-on-windows-forms.md)   
 [使用 .NET Framework 开发自定义 Windows 窗体控件](../../../../docs/framework/winforms/controls/developing-custom-windows-forms-controls.md)