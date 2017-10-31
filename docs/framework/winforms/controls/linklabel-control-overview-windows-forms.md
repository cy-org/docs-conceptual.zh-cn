---
title: "LinkLabel 控件概述（Windows 窗体） | Microsoft Docs"
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
  - "LinkLabel"
dev_langs: 
  - "jsharp"
helpviewer_keywords: 
  - "Label 控件 [Windows 窗体], 关于 Label 控件"
  - "LinkLabel 控件 [Windows 窗体], 关于 LinkLabel 控件"
  - "链接, LinkLabel 控件"
ms.assetid: 9e248549-10ca-43a3-bb5e-60f583d369f1
caps.latest.revision: 9
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 9
---
# LinkLabel 控件概述（Windows 窗体）
Windows 窗体 <xref:System.Windows.Forms.LinkLabel> 控件使您可以向 Windows 窗体应用程序添加 Web 样式的链接。  一切可以使用 <xref:System.Windows.Forms.Label> 控件的地方，都可以使用 <xref:System.Windows.Forms.LinkLabel> 控件；还可以将文本的一部分设置为指向某个文件、文件夹或网页的链接。  
  
## 使用 LinkLabel 控件可以实现的功能  
 除了具有 <xref:System.Windows.Forms.Label> 控件的所有属性、方法和事件以外，<xref:System.Windows.Forms.LinkLabel> 控件还有针对超链接和链接颜色的属性。  <xref:System.Windows.Forms.LinkLabel.LinkArea%2A> 属性设置激活链接的文本区域。  <xref:System.Windows.Forms.LinkLabel.LinkColor%2A>、<xref:System.Windows.Forms.LinkLabel.VisitedLinkColor%2A> 和 <xref:System.Windows.Forms.LinkLabel.ActiveLinkColor%2A> 属性设置链接的颜色。  <xref:System.Windows.Forms.LinkLabel.LinkClicked> 事件确定选择链接文本后将发生的操作。  
  
 <xref:System.Windows.Forms.LinkLabel> 控件的最简单用法是使用 <xref:System.Windows.Forms.LinkLabel.LinkArea%2A> 属性显示一个链接，但您也可以使用 <xref:System.Windows.Forms.LinkLabel.Links%2A> 属性显示多个超链接。  <xref:System.Windows.Forms.LinkLabel.Links%2A> 属性使您可以访问一个链接集合。  也可以在每个单个 <xref:System.Windows.Forms.LinkLabel.Link> 对象的 <xref:System.Windows.Forms.LinkLabel.Link.LinkData%2A> 属性中指定数据。  <xref:System.Windows.Forms.LinkLabel.Link.LinkData%2A> 属性的值可以用来存储要显示文件的位置或网站的地址。  
  
## 请参阅  
 <xref:System.Windows.Forms.LinkLabel>   
 [Label 控件概述](../../../../docs/framework/winforms/controls/label-control-overview-windows-forms.md)   
 [如何：使用 Windows 窗体 LinkLabel 控件链接到对象或网页](../../../../docs/framework/winforms/controls/link-to-an-object-or-web-page-with-wf-linklabel-control.md)   
 [如何：更改 Windows 窗体 LinkLabel 控件的外观](../../../../docs/framework/winforms/controls/how-to-change-the-appearance-of-the-windows-forms-linklabel-control.md)