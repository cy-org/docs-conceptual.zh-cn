---
title: "Windows 窗体应用程序中的用户输入 | Microsoft Docs"
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
  - "Windows 窗体, 用户输入"
ms.assetid: 9d61fa96-70f7-4754-885a-49a4a6316bdb
caps.latest.revision: 7
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 7
---
# Windows 窗体应用程序中的用户输入
在 Windows 窗体中，用户输入以 Windows 消息的形式发送到应用程序。  一系列可重写的方法在应用程序、窗体和控件级处理这些消息。  当这些方法接收到鼠标和键盘消息时，将引发相应的事件，可以处理这些事件来获取关于鼠标或键盘输入的信息。  在许多情况下，Windows 窗体应用程序可以仅仅通过处理这些事件来处理所有用户输入。  在其他情况下，应用程序可能需要重写处理消息的某个方法，以便在特定消息被应用程序、窗体或控件接收前截获它。  
  
## 鼠标和键盘事件  
 所有 Windows 窗体控件都继承一组与鼠标和键盘输入有关的事件。  例如，控件可以处理 <xref:System.Windows.Forms.Control.KeyPress> 事件来确定所按键的字符代码，也可以处理 <xref:System.Windows.Forms.Control.MouseClick> 事件来确定鼠标单击的位置。  有关鼠标和键盘事件的更多信息，请参见 [使用键盘事件](../../../docs/framework/winforms/using-keyboard-events.md) 和 [Windows 窗体中的鼠标事件](../../../docs/framework/winforms/mouse-events-in-windows-forms.md)。  
  
## 处理用户输入消息的方法  
 窗体和控件可以访问 <xref:System.Windows.Forms.IMessageFilter> 界面和一组可重写的方法，这些方法处理消息队列中不同位置的 Windows 消息。  这些方法都有 <xref:System.Windows.Forms.Message> 参数，该参数封装 Windows 消息的低级别详细信息。  可以实现或重写这些方法，以检查消息，然后或者使用该消息，或者将消息传递到消息队列中的下一个使用者。  下表列出了处理 Windows 窗体中的所有 Windows 消息的方法。  
  
|方法|注释|  
|--------|--------|  
|<xref:System.Windows.Forms.IMessageFilter.PreFilterMessage%2A>|此方法在应用程序级截获排队的（也称为已发送的）Windows 消息。|  
|<xref:System.Windows.Forms.Control.PreProcessMessage%2A>|此方法在 Windows 消息处理前在窗体和控件级截获它们。|  
|<xref:System.Windows.Forms.Control.WndProc%2A>|此方法在窗体和控件级处理 Windows 消息。|  
|<xref:System.Windows.Forms.Control.DefWndProc%2A>|此方法在窗体和控件级执行 Windows 消息的默认处理。  这提供了窗口的最小功能。|  
|<xref:System.Windows.Forms.Control.OnNotifyMessage%2A>|此方法在消息处理后在窗体和控件级截获它们。  若要调用此方法，必须设置 <xref:System.Windows.Forms.ControlStyles> 样式位。|  
  
 键盘和鼠标消息也可以被另外一组可重写的、特定于这些消息类型的方法处理。  有关更多信息，请参见 [键盘输入工作原理](../../../docs/framework/winforms/how-keyboard-input-works.md) 和 [Windows 窗体中鼠标输入的工作原理](../../../docs/framework/winforms/how-mouse-input-works-in-windows-forms.md)。  
  
## 请参阅  
 [Windows 窗体中的用户输入](../../../docs/framework/winforms/user-input-in-windows-forms.md)   
 [Windows 窗体应用程序中的键盘输入](../../../docs/framework/winforms/keyboard-input-in-a-windows-forms-application.md)   
 [Windows 窗体应用程序中的鼠标输入](../../../docs/framework/winforms/mouse-input-in-a-windows-forms-application.md)