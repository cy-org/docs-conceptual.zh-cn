---
title: "图形服务的三个类别 | Microsoft Docs"
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
  - "二维向量图形"
  - "图形, 类别"
  - "图像处理"
  - "版式"
  - "向量图形"
ms.assetid: 068c0ef3-f6ee-4d58-a7b6-eb2531ead408
caps.latest.revision: 14
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 14
---
# 图形服务的三个类别
Windows 窗体中提供的图形分为下面的三大类：  
  
-   二维 \(2\-D\) 矢量图形  
  
-   图像处理  
  
-   版式  
  
## 二维矢量图形  
 二维矢量图形为基元（例如，直线、曲线和图形）；它们由坐标系统上的多组点指定。  例如，直线可通过它的两个端点来指定，而矩形可通过确定其左上角位置的点并给出其宽度和高度的一对数字来指定。  简单路径可由通过直线连接的点的数组来指定。  贝塞尔样条曲线是由四个控制点指定的复杂曲线。  
  
 [!INCLUDE[ndptecgdiplus](../../../../includes/ndptecgdiplus-md.md)] 提供了用于存储基元自身信息的类和结构、用于存储基元绘制方式信息的类以及用于实际绘制的类。  例如，<xref:System.Drawing.Rectangle> 结构存储矩形的位置和尺寸；<xref:System.Drawing.Pen> 类存储有关线条颜色、线条粗细和线型的信息；而 <xref:System.Drawing.Graphics> 类具有用于绘制直线、矩形、路径和其他图形的方法。  还有几种 <xref:System.Drawing.Brush> 类，它们存储有关如何使用颜色或图案来填充封闭图形和路径的信息。  
  
 您可以在元文件中记录表示图形命令序列的矢量图像。  [!INCLUDE[ndptecgdiplus](../../../../includes/ndptecgdiplus-md.md)] 提供了用于记录、显示和保存元文件的 <xref:System.Drawing.Imaging.Metafile> 类。  使用 <xref:System.Drawing.Imaging.MetafileHeader> 和 <xref:System.Drawing.Imaging.MetaHeader> 类可以检查存储在元文件头中的数据。  
  
## 图像处理  
 某些种类的图片很难或者根本无法用矢量图形技术来显示。  例如，工具栏按钮上的图片和显示为图标的图片就难以指定为直线和曲线的集合。  拥挤的棒球运动场的高分辨率数字照片会更难以使用矢量技术来制作。  此类型的图像将以位图的形式存储，位图是由表示屏幕上各个点的颜色的数字阵列。  [!INCLUDE[ndptecgdiplus](../../../../includes/ndptecgdiplus-md.md)] 提供了用于显示、操作和保存位图的 <xref:System.Drawing.Bitmap> 类。  
  
## 版式  
 版式是指以各种字体、大小和样式显示文本。  [!INCLUDE[ndptecgdiplus](../../../../includes/ndptecgdiplus-md.md)] 提供了对这种复杂任务的广泛支持。  [!INCLUDE[ndptecgdiplus](../../../../includes/ndptecgdiplus-md.md)] 中的一个新功能是子像素抗锯齿，它可以使文本在 LCD 屏幕上呈现时显得更平滑。  
  
 另外，Windows 窗体还提供了在其 <xref:System.Windows.Forms.TextRenderer> 类中使用 [!INCLUDE[ndptecgdi](../../../../includes/ndptecgdi-md.md)] 功能绘制文本的选项。  
  
## 请参阅  
 [图形概述](../../../../docs/framework/winforms/advanced/graphics-overview-windows-forms.md)   
 [关于 GDI\+ 托管代码](../../../../docs/framework/winforms/advanced/about-gdi-managed-code.md)   
 [使用托管图形类](../../../../docs/framework/winforms/advanced/using-managed-graphics-classes.md)