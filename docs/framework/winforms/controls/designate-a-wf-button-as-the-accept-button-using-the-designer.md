---
title: "如何：使用设计器将 Windows 窗体按钮指定为“接受”按钮 | Microsoft Docs"
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
  - "Windows 窗体上的“接受”按钮"
  - "Button 控件 [Windows 窗体], 指定为默认值"
  - "按钮, Windows 窗体上的默认按钮"
  - "Windows 窗体控件, 窗体上的默认按钮"
ms.assetid: a1da0590-755f-49f2-aca7-609fac6351bf
caps.latest.revision: 13
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 13
---
# 如何：使用设计器将 Windows 窗体按钮指定为“接受”按钮
在任何 Windows 窗体上都可以将某个 <xref:System.Windows.Forms.Button> 控件指定为“接受”按钮（也称作默认按钮）。  每当用户按 Enter 键时，即单击默认按钮，而不管窗体上其他哪个控件具有焦点。  但当具有焦点的控件为以下情形时存在例外：为另一个按钮，此时，将单击具有焦点的那个按钮；为多行文本框；为捕获了 Enter 键的自定义控件。  
  
> [!NOTE]
>  显示的对话框和菜单命令可能会与“帮助”中的描述不同，具体取决于您现用的设置或版本。  若要更改设置，请在**“工具”**菜单上选择**“导入和导出设置”**。  有关更多信息，请参见 [Customizing Development Settings in Visual Studio](http://msdn.microsoft.com/zh-cn/22c4debb-4e31-47a8-8f19-16f328d7dcd3)。  
  
### 指定“接受”按钮  
  
1.  选择按钮所驻留的窗体。  
  
2.  在**“属性”**窗口中，将窗体的 <xref:System.Windows.Forms.Form.AcceptButton%2A> 属性设置为 <xref:System.Windows.Forms.Button> 控件的名称。  
  
## 请参阅  
 <xref:System.Windows.Forms.Form.AcceptButton%2A>   
 [Button 控件概述](../../../../docs/framework/winforms/controls/button-control-overview-windows-forms.md)   
 [选择 Windows 窗体 Button 控件的方法](../../../../docs/framework/winforms/controls/ways-to-select-a-windows-forms-button-control.md)   
 [如何：响应 Windows 窗体按钮的单击](../../../../docs/framework/winforms/controls/how-to-respond-to-windows-forms-button-clicks.md)   
 [如何：使用设计器将 Windows 窗体按钮指定为“取消”按钮](../../../../docs/framework/winforms/controls/designate-a-wf-button-as-the-cancel-button-using-the-designer.md)   
 [Button 控件](../../../../docs/framework/winforms/controls/button-control-windows-forms.md)