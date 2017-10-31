---
title: "如何：显示弹出帮助 | Microsoft Docs"
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
  - "F1 帮助, 在对话框中"
  - "窗体, 显示帮助"
  - "帮助, 添加到对话框"
  - "帮助, 弹出帮助"
  - "HelpProvider 组件 [Windows 窗体]"
  - "有模式对话框, 弹出帮助"
  - "弹出帮助"
  - "Windows 窗体, 显示帮助"
ms.assetid: 218aa81e-e87e-4d67-af05-11627bbdce3b
caps.latest.revision: 16
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 16
---
# 如何：显示弹出帮助
在 Windows 窗体上显示帮助的一种方法就是，通过“帮助”按钮实现，该按钮位于标题栏右侧，可通过 <xref:System.Windows.Forms.Form.HelpButton%2A> 属性访问。  此类型的“帮助”显示非常适用于对话框。  使用 <xref:System.Windows.Forms.Form.ShowDialog%2A> 方法适度显示的对话框在获取外部帮助系统时会遇到问题，因为必须先关闭模型对话框后才能切换到另一个窗口。  此外，如果标题栏中未显示“最小化”按钮或“最大化”按钮，则需要使用“帮助”按钮。  这是一个标准对话框约定，而窗体通常具有“最小化”和“最大化”按钮。  
  
 请注意，你还可以使用 <xref:System.Windows.Forms.HelpProvider> 组件将控件链接到帮助系统中的文件，即使你已实现了弹出帮助。  有关详细信息，请参阅[在 Windows 应用程序中提供帮助](../../../../docs/framework/winforms/advanced/how-to-provide-help-in-a-windows-application.md)。  
  
> [!NOTE]
>  显示的对话框和菜单命令可能会与“帮助”中的描述不同，具体取决于你现用的设置或版本。  若要更改设置，请在**“工具”**菜单上选择**“导入和导出设置”**。  有关详细信息，请参阅 [Customizing Development Settings in Visual Studio](http://msdn.microsoft.com/zh-cn/22c4debb-4e31-47a8-8f19-16f328d7dcd3)。  
  
### 显示弹出帮助  
  
1.  将 [HelpProvider](../../../../docs/framework/winforms/controls/helpprovider-component-windows-forms.md) 组件从工具箱拖到你的窗体。  
  
     它将显示在 Windows 窗体设计器底部的任务栏中。  
  
2.  在“属性”窗口，将 <xref:System.Windows.Forms.Form.HelpButton%2A> 属性设置为 `true`。  这将在窗体的标题栏右侧显示带问号的按钮。  
  
3.  为了显示 <xref:System.Windows.Forms.Form.HelpButton%2A>，必须将窗体的 <xref:System.Windows.Forms.Form.MinimizeBox%2A> 和 <xref:System.Windows.Forms.Form.MaximizeBox%2A> 属性设置为 `false`，将 <xref:System.Windows.Forms.Form.ControlBox%2A> 属性设置为 `true` 以及将 <xref:System.Windows.Forms.Form.FormBorderStyle%2A> 属性设置为下列值之一：<xref:System.Windows.Forms.FormBorderStyle>、<xref:System.Windows.Forms.FormBorderStyle>、<xref:System.Windows.Forms.FormBorderStyle> 或 <xref:System.Windows.Forms.FormBorderStyle>。  
  
4.  选择想在你的窗体上显示帮助的控件，然后在“属性”窗口设置“帮助”字符串。  这是文本字符串，将显示在类似于[工具提示](../../../../docs/framework/winforms/controls/tooltip-component-windows-forms.md)的窗口中。  
  
5.  按 F5。  
  
6.  按标题栏上的“帮助”按钮，然后单击设置帮助字符串的控件。  
  
## 请参阅  
 [使用工具提示的控件帮助](../../../../docs/framework/winforms/advanced/control-help-using-tooltips.md)   
 [在 Windows 窗体中集成用户帮助](../../../../docs/framework/winforms/advanced/integrating-user-help-in-windows-forms.md)   
 [Windows 窗体](../../../../docs/framework/winforms/index.md)