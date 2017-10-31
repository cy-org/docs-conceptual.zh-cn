---
title: "HelpProvider 组件概述（Windows 窗体） | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-winforms"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "HelpProvider"
dev_langs: 
  - "jsharp"
helpviewer_keywords: 
  - "对话框, 区分上下文的帮助"
  - "F1 帮助, 添加到 Windows 窗体"
  - "帮助, 添加到 Windows 应用程序"
  - "HelpProvider 组件 [Windows 窗体], 关于 HelpProvider 组件"
  - "Windows 窗体, 区分上下文的帮助"
ms.assetid: 6b10c2cc-c577-4cb5-9669-e37b33416af9
caps.latest.revision: 7
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 7
---
# HelpProvider 组件概述（Windows 窗体）
Windows 窗体 [HelpProvider](../../../../docs/framework/winforms/controls/helpprovider-component-windows-forms.md)组件用于将 HTML 帮助 1.x 帮助文件（.htm 文件或由 HTML Help Workshop 产生的 .chm 文件）与 Windows 应用程序相关联。  可以通过多种方式提供帮助：  
  
-   为 Windows 窗体中的控件提供区分上下文的帮助。  
  
-   为特定对话框或对话框中的特定控件提供区分上下文的帮助。  
  
-   打开帮助文件到特定部分，如目录、索引或搜索功能的主页。  
  
## 使用帮助提供程序  
 在 Windows 窗体中添加 <xref:System.Windows.Forms.HelpProvider> 组件可以使该窗体中的其他控件公开 <xref:System.Windows.Forms.HelpProvider> 组件的 Help 属性。  这样您就可以提供有关 Windows 窗体控件的帮助。  可以使用 <xref:System.Windows.Forms.HelpProvider.HelpNamespace%2A> 属性将帮助文件与 <xref:System.Windows.Forms.HelpProvider> 组件相关联。  通过调用 <xref:System.Windows.Forms.HelpProvider.SetHelpNavigator%2A> 并提供指定控件的 <xref:System.Windows.Forms.HelpNavigator> 枚举值来指定提供的帮助类型。  通过调用 <xref:System.Windows.Forms.HelpProvider.SetHelpKeyword%2A> 方法为帮助提供关键字或主题。  
  
 也可以使用 <xref:System.Windows.Forms.HelpProvider.SetHelpString%2A> 方法将特定的帮助字符串与另一个控件相关联。  当控件有焦点且用户按 F1 键时，在弹出式窗口中显示使用上述方法与该控件关联的字符串。  
  
 如果尚未设置 <xref:System.Windows.Forms.HelpProvider.HelpNamespace%2A>，则必须使用 <xref:System.Windows.Forms.HelpProvider.SetHelpString%2A> 提供帮助文本。  如果同时设置了 <xref:System.Windows.Forms.HelpProvider.HelpNamespace%2A> 和帮助字符串，则基于 <xref:System.Windows.Forms.HelpProvider.HelpNamespace%2A> 的帮助优先。  
  
> [!NOTE]
>  如果在 <xref:System.Windows.Forms.HelpProvider> 控件的 <xref:System.Windows.Forms.Help.ShowHelp%2A> 方法或 <xref:System.Windows.Forms.HelpProvider.HelpNamespace%2A> 属性中指定了帮助文件的路径，则使用相对路径时可能会遇到问题。  因此，一定要使用绝对文件路径来指定帮助文件。  
  
## 请参阅  
 [Windows 窗体应用程序中的帮助系统](../../../../docs/framework/winforms/advanced/help-systems-in-windows-forms-applications.md)