---
title: "图形界面的结构 | Microsoft Docs"
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
  - "GDI+, 使用托管接口"
  - "图形, 类结构"
ms.assetid: 010a1e46-656b-40a1-8d5d-87aa05ee1243
caps.latest.revision: 11
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 11
---
# 图形界面的结构
[!INCLUDE[ndptecgdiplus](../../../../includes/ndptecgdiplus-md.md)] 的托管类接口包含大约 60 个类、50 个枚举和 8 个结构。  <xref:System.Drawing.Graphics> 类是 [!INCLUDE[ndptecgdiplus](../../../../includes/ndptecgdiplus-md.md)] 功能的核心，它是实际绘制直线、曲线、图形、图像和文本的类。  
  
## 重要的类  
 许多类与 <xref:System.Drawing.Graphics> 类一起使用。  例如，<xref:System.Drawing.Graphics.DrawLine%2A> 方法接收 <xref:System.Drawing.Pen> 对象，该对象中存有所要绘制的线条的特性（颜色、宽度、虚线线型等）。  <xref:System.Drawing.Graphics.FillRectangle%2A> 方法可以接收指向 <xref:System.Drawing.Drawing2D.LinearGradientBrush> 对象的指针，该对象与 <xref:System.Drawing.Graphics> 配合工作以使用一种渐变色填充矩形。  <xref:System.Drawing.Font> 和 <xref:System.Drawing.StringFormat> 对象影响 <xref:System.Drawing.Graphics> 对象绘制文本的方式。  <xref:System.Drawing.Drawing2D.Matrix> 对象存储并操作 <xref:System.Drawing.Graphics> 对象的世界变换，该对象用于旋转、缩放和翻转图像。  
  
 [!INCLUDE[ndptecgdiplus](../../../../includes/ndptecgdiplus-md.md)] 提供了用于组织图形数据的几种结构（例如 <xref:System.Drawing.Rectangle>、<xref:System.Drawing.Point> 和 <xref:System.Drawing.Size>）。  而且，某些类的主要作用是结构化数据类型。  例如，<xref:System.Drawing.Imaging.BitmapData> 类是 <xref:System.Drawing.Bitmap> 类的帮助器，<xref:System.Drawing.Drawing2D.PathData> 类是 <xref:System.Drawing.Drawing2D.GraphicsPath> 类的帮助器。  
  
 [!INCLUDE[ndptecgdiplus](../../../../includes/ndptecgdiplus-md.md)] 定义了几种枚举，它们是相关常量的集合。  例如，<xref:System.Drawing.Drawing2D.LineJoin> 枚举包含元素 <xref:System.Drawing.Drawing2D.LineJoin>、<xref:System.Drawing.Drawing2D.LineJoin> 和 <xref:System.Drawing.Drawing2D.LineJoin>，它们指定可用于连接两个线条的线型。  
  
## 请参阅  
 [图形概述](../../../../docs/framework/winforms/advanced/graphics-overview-windows-forms.md)   
 [关于 GDI\+ 托管代码](../../../../docs/framework/winforms/advanced/about-gdi-managed-code.md)   
 [使用托管图形类](../../../../docs/framework/winforms/advanced/using-managed-graphics-classes.md)