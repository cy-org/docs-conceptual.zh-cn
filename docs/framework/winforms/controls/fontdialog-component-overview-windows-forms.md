---
title: "FontDialog 组件概述（Windows 窗体） | Microsoft Docs"
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
  - "FontDialog"
dev_langs: 
  - "jsharp"
helpviewer_keywords: 
  - "“字体”对话框"
  - "“字体”对话框, Windows 窗体"
  - "FontDialog 组件 [Windows 窗体], 关于 FontDialog 组件"
ms.assetid: daf46e57-1b4b-4b7a-bad0-b50ca7ba75dc
caps.latest.revision: 10
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 10
---
# FontDialog 组件概述（Windows 窗体）
Windows 窗体 <xref:System.Windows.Forms.FontDialog> 组件是一个预先配置的对话框，该对话框是标准的 Windows**“字体”**对话框，用于公开系统上当前安装的字体。  可在基于 Windows 的应用程序中将其用作简单的字体选择解决方案，而不是配置您自己的对话框。  
  
 默认情况下，该对话框显示字体、字体样式和字体大小的列表框；删除线和下划线等效果的复选框；脚本的下拉列表以及字体外观的示例。  （脚本是指给定字体可用的不同字符脚本，如希伯来语或日语。）若要显示字体对话框，请调用 <xref:System.Windows.Forms.CommonDialog.ShowDialog%2A> 方法。  
  
## 主要属性  
 该组件具有若干可配置其外观的属性。  用于设置对话框选择内容的属性包括 <xref:System.Windows.Forms.FontDialog.Font%2A> 和 <xref:System.Windows.Forms.FontDialog.Color%2A>。  <xref:System.Windows.Forms.FontDialog.Font%2A> 属性设置字体、样式、大小、脚本和效果；如  `Arial, 10pt, style=Italic, Strikeout`。  
  
## 请参阅  
 <xref:System.Windows.Forms.FontDialog>   
 [FontDialog 组件](../../../../docs/framework/winforms/controls/fontdialog-component-windows-forms.md)