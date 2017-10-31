---
title: "Windows 窗体中的事件顺序 | Microsoft Docs"
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
  - "应用程序关闭事件的顺序"
  - "应用程序启动事件的顺序"
  - "事件 [Windows 窗体], 顺序"
  - "焦点事件顺序"
  - "序列, 事件的"
  - "验证事件, 顺序"
ms.assetid: e81db09b-4453-437f-b78a-62d7cd5c9829
caps.latest.revision: 15
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 15
---
# Windows 窗体中的事件顺序
对于依次处理其中每个事件的开发人员，Windows 窗体应用程序中引发事件的顺序非常具有吸引力。  当出现需要谨慎处理事件的情况时（例如，在重绘窗体的某些部件时），有必要了解运行时引发事件的确切顺序。  本主题提供了应用程序和控件的生存期中几个重要阶段中的事件顺序的详细信息。  有关鼠标输入事件顺序的特定详细信息，请参阅 [Windows 窗体中的鼠标事件](../../../docs/framework/winforms/mouse-events-in-windows-forms.md)。  有关 Windows 窗体中的事件概述，请参阅[事件概述](../../../docs/framework/winforms/events-overview-windows-forms.md)。  有关事件处理程序组成部分的详细信息，请参阅[事件处理程序概述](../../../docs/framework/winforms/event-handlers-overview-windows-forms.md)。  
  
## 应用程序启动和关闭事件  
 <xref:System.Windows.Forms.Form> 和 <xref:System.Windows.Forms.Control> 类公开一组与应用程序启动和关闭相关的事件。  Windows 窗体应用程序启动时，主窗体的启动事件将按照以下顺序引发：  
  
-   <xref:System.Windows.Forms.Control.HandleCreated?displayProperty=fullName>  
  
-   <xref:System.Windows.Forms.Control.BindingContextChanged?displayProperty=fullName>  
  
-   <xref:System.Windows.Forms.Form.Load?displayProperty=fullName>  
  
-   <xref:System.Windows.Forms.Control.VisibleChanged?displayProperty=fullName>  
  
-   <xref:System.Windows.Forms.Form.Activated?displayProperty=fullName>  
  
-   <xref:System.Windows.Forms.Form.Shown?displayProperty=fullName>  
  
 应用程序关闭时，主窗体的关闭事件将按照以下顺序引发：  
  
-   <xref:System.Windows.Forms.Form.Closing?displayProperty=fullName>  
  
-   <xref:System.Windows.Forms.Form.FormClosing?displayProperty=fullName>  
  
-   <xref:System.Windows.Forms.Form.Closed?displayProperty=fullName>  
  
-   <xref:System.Windows.Forms.Form.FormClosed?displayProperty=fullName>  
  
-   <xref:System.Windows.Forms.Form.Deactivate?displayProperty=fullName>  
  
 在主窗体关闭事件后，将引发 <xref:System.Windows.Forms.Application> 类的 <xref:System.Windows.Forms.Application.ApplicationExit> 事件。  
  
> [!NOTE]
>  Visual Basic 2005 包括其他应用程序事件，例如 <xref:Microsoft.VisualBasic.ApplicationServices.WindowsFormsApplicationBase.Startup?displayProperty=fullName> 和 <xref:Microsoft.VisualBasic.ApplicationServices.WindowsFormsApplicationBase.Shutdown?displayProperty=fullName>。  
  
## 焦点和验证事件  
 当通过使用键盘（TAB、SHIFT\+TAB 等），通过调用 <xref:System.Windows.Forms.Control.Select%2A> 或 <xref:System.Windows.Forms.Control.SelectNextControl%2A> 方法，或通过将 <xref:System.Windows.Forms.ContainerControl.ActiveControl%2A> 属性设置为当前窗体来更改焦点时，<xref:System.Windows.Forms.Control> 类的焦点事件将按以下顺序发生：  
  
-   <xref:System.Windows.Forms.Control.Enter>  
  
-   <xref:System.Windows.Forms.Control.GotFocus>  
  
-   <xref:System.Windows.Forms.Control.Leave>  
  
-   <xref:System.Windows.Forms.Control.Validating>  
  
-   <xref:System.Windows.Forms.Control.Validated>  
  
-   <xref:System.Windows.Forms.Control.LostFocus>  
  
 当通过使用鼠标或调用 <xref:System.Windows.Forms.Control.Focus%2A> 方法更改焦点时，<xref:System.Windows.Forms.Control> 类的焦点事件将按以下顺序发生：  
  
-   <xref:System.Windows.Forms.Control.Enter>  
  
-   <xref:System.Windows.Forms.Control.GotFocus>  
  
-   <xref:System.Windows.Forms.Control.LostFocus>  
  
-   <xref:System.Windows.Forms.Control.Leave>  
  
-   <xref:System.Windows.Forms.Control.Validating>  
  
-   <xref:System.Windows.Forms.Control.Validated>  
  
## 请参阅  
 [在 Windows 窗体中创建事件处理程序](../../../docs/framework/winforms/creating-event-handlers-in-windows-forms.md)