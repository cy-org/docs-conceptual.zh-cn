---
title: "管理 Graphics 对象的状态 | Microsoft Docs"
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
  - "图形, 剪辑"
  - "图形, 管理状态"
ms.assetid: 6207cad1-7a34-4bd6-bfc1-db823ca7a73e
caps.latest.revision: 14
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 14
---
# 管理 Graphics 对象的状态
<xref:System.Drawing.Graphics> 类是 [!INCLUDE[ndptecgdiplus](../../../../includes/ndptecgdiplus-md.md)] 的核心。  若要进行绘制，请获取 <xref:System.Drawing.Graphics> 对象，设置其属性，并调用其方法（<xref:System.Drawing.Graphics.DrawLine%2A>、<xref:System.Drawing.Graphics.DrawImage%2A> 和 <xref:System.Drawing.Graphics.DrawString%2A> 等）。  
  
 下面的示例调用 <xref:System.Drawing.Graphics> 对象的 <xref:System.Drawing.Graphics.DrawRectangle%2A> 方法。  传递给 <xref:System.Drawing.Graphics.DrawRectangle%2A> 方法的第一个参数是 <xref:System.Drawing.Pen> 对象。  
  
```vb  
Dim graphics As Graphics = e.Graphics  
Dim pen As New Pen(Color.Blue) ' Opaque blue  
graphics.DrawRectangle(pen, 10, 10, 200, 100)  
  
```  
  
```csharp  
Graphics graphics = e.Graphics;  
Pen pen = new Pen(Color.Blue);  // Opaque blue  
graphics.DrawRectangle(pen, 10, 10, 200, 100);  
```  
  
## Graphics 状态  
 <xref:System.Drawing.Graphics> 对象不仅仅提供绘制方法，如 <xref:System.Drawing.Graphics.DrawLine%2A> 和 <xref:System.Drawing.Graphics.DrawRectangle%2A>。  <xref:System.Drawing.Graphics> 对象还维护图形状态，图形状态可划分为以下几类：  
  
-   质量设置  
  
-   变换  
  
-   剪辑区域  
  
### 质量设置  
 <xref:System.Drawing.Graphics> 对象具有几个影响所绘项质量的属性。  例如，可设置 <xref:System.Drawing.Graphics.TextRenderingHint%2A> 属性以指定应用于文本的抗锯齿的类型（如果有的话）。  影响质量的其他属性是 <xref:System.Drawing.Graphics.SmoothingMode%2A>、<xref:System.Drawing.Graphics.CompositingMode%2A>、<xref:System.Drawing.Graphics.CompositingQuality%2A> 和 <xref:System.Drawing.Graphics.InterpolationMode%2A>。  
  
 下面的示例绘制了两个椭圆，一个的平滑模式设置为 <xref:System.Drawing.Drawing2D.SmoothingMode>，另一个的平滑模式设置为 <xref:System.Drawing.Drawing2D.SmoothingMode>：  
  
```vb  
Dim graphics As Graphics = e.Graphics  
Dim pen As New Pen(Color.Blue)  
  
graphics.SmoothingMode = SmoothingMode.AntiAlias  
graphics.DrawEllipse(pen, 0, 0, 200, 100)  
graphics.SmoothingMode = SmoothingMode.HighSpeed  
graphics.DrawEllipse(pen, 0, 150, 200, 100)  
  
```  
  
```csharp  
Graphics graphics = e.Graphics;  
Pen pen = new Pen(Color.Blue);  
  
graphics.SmoothingMode = SmoothingMode.AntiAlias;  
graphics.DrawEllipse(pen, 0, 0, 200, 100);  
graphics.SmoothingMode = SmoothingMode.HighSpeed;  
graphics.DrawEllipse(pen, 0, 150, 200, 100);  
```  
  
### 变换  
 <xref:System.Drawing.Graphics> 对象维护两种应用到由 <xref:System.Drawing.Graphics> 对象绘制的所有项目的变换（世界变换和页变换）。  任何仿射变换都可存储在世界变换中。  仿射变换包括缩放、旋转、反射、扭曲和平移。  页变换可用于缩放和更改单位（例如，像素到英寸）。  有关更多信息，请参见[坐标系统和变换](../../../../docs/framework/winforms/advanced/coordinate-systems-and-transformations.md)。  
  
 下面的示例设置 <xref:System.Drawing.Graphics> 对象的世界变换和页变换。  世界变换被设置为旋转 30 度。  设置页变换，使传递给第二个 <xref:System.Drawing.Graphics.DrawEllipse%2A> 的坐标按毫米计，而不是像素。  该代码对 <xref:System.Drawing.Graphics.DrawEllipse%2A> 方法进行两次相同的调用。  世界变换应用于第一个 <xref:System.Drawing.Graphics.DrawEllipse%2A> 调用，两种变换（世界变换和页变换）都应用于第二个 <xref:System.Drawing.Graphics.DrawEllipse%2A> 调用。  
  
```vb  
Dim graphics As Graphics = e.Graphics  
Dim pen As New Pen(Color.Red)  
  
graphics.ResetTransform()  
graphics.RotateTransform(30) ' world transformation  
graphics.DrawEllipse(pen, 0, 0, 100, 50)  
graphics.PageUnit = GraphicsUnit.Millimeter ' page transformation  
graphics.DrawEllipse(pen, 0, 0, 100, 50)  
  
```  
  
```csharp  
Graphics graphics = e.Graphics;  
Pen pen = new Pen(Color.Red);   
  
graphics.ResetTransform();  
graphics.RotateTransform(30);                    // world transformation  
graphics.DrawEllipse(pen, 0, 0, 100, 50);  
graphics.PageUnit = GraphicsUnit.Millimeter;     // page transformation  
graphics.DrawEllipse(pen, 0, 0, 100, 50);  
```  
  
 下面的插图显示这两个椭圆。  请注意，30 度的旋转是针对坐标系的原点（工作区的左上角）的，而不是椭圆的中心。  还要注意，画笔的宽度 1 对于第一个椭圆来说表示 1 个像素，对于第二个椭圆来说表示 1 毫米。  
  
 ![椭圆形](../../../../docs/framework/winforms/advanced/media/csgraphicsascon1.png "csgraphicsascon1")  
  
### 剪辑区域  
 <xref:System.Drawing.Graphics> 对象维护应用于由 <xref:System.Drawing.Graphics> 对象绘制的所有项目的剪辑区域。  可通过调用 <xref:System.Drawing.Graphics.SetClip%2A> 方法设置剪辑区域。  
  
 下面的示例通过合并两个矩形来创建形状为加号的区域。  该区域被指定为 <xref:System.Drawing.Graphics> 对象的剪辑区域。  然后，该代码绘制两条限制在剪辑区域内部的直线。  
  
```vb  
Dim graphics As Graphics = e.Graphics  
  
' Opaque red, width 5  
Dim pen As New Pen(Color.Red, 5)  
  
' Opaque aqua  
Dim brush As New SolidBrush(Color.FromArgb(255, 180, 255, 255))  
  
' Create a plus-shaped region by forming the union of two rectangles.  
Dim [region] As New [Region](../../../../amples/snippets/visualbasic/VS_Snippets_Wpf/ToolBarOrient_snip/visualbasic/toolbargraphics/new.bmp Rectangle(50, 0, 50, 150))  
[region].Union(New Rectangle(0, 50, 150, 50))  
graphics.FillRegion(brush, [region])  
  
' Set the clipping region.  
graphics.SetClip([region], CombineMode.Replace)  
  
' Draw two clipped lines.  
graphics.DrawLine(pen, 0, 30, 150, 160)  
graphics.DrawLine(pen, 40, 20, 190, 150)  
  
```  
  
```csharp  
Graphics graphics = e.Graphics;  
  
// Opaque red, width 5  
Pen pen = new Pen(Color.Red, 5);    
  
// Opaque aqua  
SolidBrush brush = new SolidBrush(Color.FromArgb(255, 180, 255, 255));    
  
// Create a plus-shaped region by forming the union of two rectangles.  
Region region = new Region(new Rectangle(50, 0, 50, 150));  
region.Union(new Rectangle(0, 50, 150, 50));  
graphics.FillRegion(brush, region);  
  
// Set the clipping region.  
graphics.SetClip(region, CombineMode.Replace);  
  
// Draw two clipped lines.  
graphics.DrawLine(pen, 0, 30, 150, 160);  
graphics.DrawLine(pen, 40, 20, 190, 150);  
```  
  
 下面的插图显示这两条剪辑过的直线。  
  
 ![受限剪辑区域](../../../../docs/framework/winforms/advanced/media/graphicsascon2.png "graphicsascon2")  
  
## 请参阅  
 [Windows 窗体中的图形和绘制](../../../../docs/framework/winforms/advanced/graphics-and-drawing-in-windows-forms.md)   
 [使用嵌套的 Graphics 容器](../../../../docs/framework/winforms/advanced/using-nested-graphics-containers.md)