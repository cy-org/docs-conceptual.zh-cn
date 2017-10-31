---
title: "如何：在 Windows 窗体应用程序中响应字体方案更改 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-winforms"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "jsharp"
helpviewer_keywords: 
  - "Windows 窗体, 字体方案更改"
ms.assetid: 4db27702-22e7-43bf-a07d-9a004549853c
caps.latest.revision: 9
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 9
---
# 如何：在 Windows 窗体应用程序中响应字体方案更改
在 Windows 操作系统中，用户可以更改系统级的字体设置，使默认字体显示得更大或更小。  更改这些字体设置对于视力受损的用户尤为关键，因为他们需要屏幕上显示较大的文本才能进行阅读。  每当字体方案发生更改时，可以通过增加或减小窗体以及所有包含文本的大小，来调整 Windows 窗体应用程序以响应这些更改。  如果想让窗体动态适应字号的更改，可以向窗体添加代码。  
  
 通常，Windows 窗体使用的默认字体是 <xref:Microsoft.Win32> 命名空间调用 `GetStockObject(DEFAULT_GUI_FONT)` 所返回的字体。  此调用所返回的字体只在屏幕分辨率发生变化时才会更改。  如下面的过程所示，您的代码必须将默认字体更改为 <xref:System.Drawing.SystemFonts.IconTitleFont%2A>，以响应字号的更改。  
  
### 使用桌面字体和响应字体方案更改  
  
1.  创建窗体，并向该窗体添加您需要的控件。  有关更多信息，请参见[如何：从命令行创建 Windows 窗体应用程序](../../../docs/framework/winforms/how-to-create-a-windows-forms-application-from-the-command-line.md)和[在 Windows 窗体上使用的控件](../../../docs/framework/winforms/controls/controls-to-use-on-windows-forms.md)。  
  
2.  向代码中添加对 <xref:Microsoft.Win32> 命名空间的引用。  
  
     [!code-csharp[WinFormsAutoScaling#2](../../../samples/snippets/csharp/VS_Snippets_Winforms/WinFormsAutoScaling/CS/Form1.cs#2)]
     [!code-vb[WinFormsAutoScaling#2](../../../samples/snippets/visualbasic/VS_Snippets_Winforms/WinFormsAutoScaling/VB/Form1.vb#2)]  
  
3.  将下面的代码添加到窗体的构造函数中，以挂接所需的事件处理程序，并更改窗体使用的默认字体。  
  
     [!code-csharp[WinFormsAutoScaling#3](../../../samples/snippets/csharp/VS_Snippets_Winforms/WinFormsAutoScaling/CS/Form1.cs#3)]
     [!code-vb[WinFormsAutoScaling#3](../../../samples/snippets/visualbasic/VS_Snippets_Winforms/WinFormsAutoScaling/VB/Form1.vb#3)]  
  
4.  实现 <xref:Microsoft.Win32.SystemEvents.UserPreferenceChanged> 事件的处理程序，当 <xref:Microsoft.Win32.UserPreferenceCategory> 类别更改时，该事件将导致窗体自动缩放。  
  
     [!code-csharp[WinFormsAutoScaling#4](../../../samples/snippets/csharp/VS_Snippets_Winforms/WinFormsAutoScaling/CS/Form1.cs#4)]
     [!code-vb[WinFormsAutoScaling#4](../../../samples/snippets/visualbasic/VS_Snippets_Winforms/WinFormsAutoScaling/VB/Form1.vb#4)]  
  
5.  最后，实现 <xref:System.Windows.Forms.Form.FormClosing> 事件的处理程序，该事件分离 <xref:Microsoft.Win32.SystemEvents.UserPreferenceChanged> 事件处理程序。  
  
> [!IMPORTANT]
>  不包括此代码将导致应用程序泄漏内存。  
  
 [!code-csharp[WinFormsAutoScaling#5](../../../samples/snippets/csharp/VS_Snippets_Winforms/WinFormsAutoScaling/CS/Form1.cs#5)]
 [!code-vb[WinFormsAutoScaling#5](../../../samples/snippets/visualbasic/VS_Snippets_Winforms/WinFormsAutoScaling/VB/Form1.vb#5)]  
  
1.  编译并运行代码。  
  
### 手动更改 Windows XP 中的字体方案  
  
1.  在 Windows 窗体应用程序运行期间，右击 Windows 桌面，然后从快捷菜单中选择**“属性”**。  
  
2.  在**“显示属性”**对话框中，单击**“外观”**选项卡。  
  
3.  从**“字号”**下拉列表框中，选择一个新字号。  
  
     您将注意到窗体现在对桌面字体方案的运行时更改做出响应。  当用户在**“普通”**、**“大字体”**和**“特大字体”**之间更改时，窗体将相应地更改字体并缩放。  
  
## 示例  
 [!code-csharp[WinFormsAutoScaling#1](../../../samples/snippets/csharp/VS_Snippets_Winforms/WinFormsAutoScaling/CS/Form1.cs#1)]
 [!code-vb[WinFormsAutoScaling#1](../../../samples/snippets/visualbasic/VS_Snippets_Winforms/WinFormsAutoScaling/VB/Form1.vb#1)]  
  
 此代码示例中的构造函数包含对 `InitializeComponent` 的调用，该组件是您在 Visual Studio 中创建新的 Windows 窗体项目时定义的。  如果通过命令行生成应用程序，请移除此行代码。  
  
## 请参阅  
 <xref:System.Windows.Forms.ContainerControl.PerformAutoScale%2A>   
 [Windows 窗体中的自动缩放](../../../docs/framework/winforms/automatic-scaling-in-windows-forms.md)