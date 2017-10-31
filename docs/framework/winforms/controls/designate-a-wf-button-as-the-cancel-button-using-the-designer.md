---
title: "如何：使用设计器将 Windows 窗体按钮指定为“取消”按钮 | Microsoft Docs"
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
  - "Button 控件 [Windows 窗体], 指定为取消按钮"
  - "按钮, 取消按钮"
ms.assetid: 30e77d9c-d565-4ab5-a84a-62c043af8822
caps.latest.revision: 13
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 13
---
# 如何：使用设计器将 Windows 窗体按钮指定为“取消”按钮
在任何 Windows 窗体上，您都可以将 <xref:System.Windows.Forms.Button> 控件指定为“取消”按钮。  每当用户按 Esc 键时，即单击“取消”按钮，而不管窗体上的其他哪个控件具有焦点。  通常设计这样的按钮是为了允许用户快速退出操作而无需执行任何动作。  
  
> [!NOTE]
>  显示的对话框和菜单命令可能会与“帮助”中的描述不同，具体取决于您现用的设置或版本。  若要更改设置，请在**“工具”**菜单上选择**“导入和导出设置”**。  有关更多信息，请参见 [Customizing Development Settings in Visual Studio](http://msdn.microsoft.com/zh-cn/22c4debb-4e31-47a8-8f19-16f328d7dcd3)。  
  
### 指定“取消”按钮  
  
1.  选择按钮所驻留的窗体。  
  
2.  在**“属性”**窗口中，将窗体的 <xref:System.Windows.Forms.Form.CancelButton%2A> 属性设置为 <xref:System.Windows.Forms.Button> 控件的名称。  
  
## 请参阅  
 <xref:System.Windows.Forms.Form.CancelButton%2A>   
 [Button 控件概述](../../../../docs/framework/winforms/controls/button-control-overview-windows-forms.md)   
 [选择 Windows 窗体 Button 控件的方法](../../../../docs/framework/winforms/controls/ways-to-select-a-windows-forms-button-control.md)   
 [如何：响应 Windows 窗体按钮的单击](../../../../docs/framework/winforms/controls/how-to-respond-to-windows-forms-button-clicks.md)   
 [如何：使用设计器将 Windows 窗体按钮指定为“接受”按钮](../../../../docs/framework/winforms/controls/designate-a-wf-button-as-the-accept-button-using-the-designer.md)   
 [Button 控件](../../../../docs/framework/winforms/controls/button-control-windows-forms.md)