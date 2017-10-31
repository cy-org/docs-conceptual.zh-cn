---
title: "GDI+ 中的画笔和实心形状 | Microsoft Docs"
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
  - "画笔, GDI+"
  - "画笔, 渐变"
  - "已填充的形状, GDI+"
  - "GDI+, 画笔"
  - "GDI+, 已填充的形状"
  - "渐变画刷"
  - "形状, GDI+"
ms.assetid: e863e2a7-0294-4130-99b6-f1ea3201e7cd
caps.latest.revision: 15
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 15
---
# GDI+ 中的画笔和实心形状
闭合的形状（例如，矩形或椭圆）由轮廓和内部组成。  使用钢笔绘制出轮廓，并用画笔填充其内部。  [!INCLUDE[ndptecgdiplus](../../../../includes/ndptecgdiplus-md.md)] 提供了几种填充闭合形状内部的画笔类：<xref:System.Drawing.SolidBrush>、<xref:System.Drawing.Drawing2D.HatchBrush>、<xref:System.Drawing.TextureBrush>、<xref:System.Drawing.Drawing2D.LinearGradientBrush> 和 <xref:System.Drawing.Drawing2D.PathGradientBrush>。  所有这些类都是从 <xref:System.Drawing.Brush> 类继承的。  下面的插图显示了用实心画笔填充的矩形和用阴影画笔填充的椭圆。  
  
 ![实心形状](../../../../docs/framework/winforms/advanced/media/aboutgdip02-art17.png "Aboutgdip02\_art17")  
  
## 实心画笔  
 若要填充闭合的形状，需要 <xref:System.Drawing.Graphics> 类的实例和 <xref:System.Drawing.Brush>。  <xref:System.Drawing.Graphics> 类的实例提供方法，如 <xref:System.Drawing.Graphics.FillRectangle%2A> 和 <xref:System.Drawing.Graphics.FillEllipse%2A>，而 <xref:System.Drawing.Brush> 存储填充的特性，如颜色和模式。  <xref:System.Drawing.Brush> 作为参数之一传递给填充方法。  下面的代码示例演示如何用纯红色填充椭圆。  
  
 [!code-csharp[LinesCurvesAndShapes#121](../../../../samples/snippets/csharp/VS_Snippets_Winforms/LinesCurvesAndShapes/CS/Class1.cs#121)]
 [!code-vb[LinesCurvesAndShapes#121](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/LinesCurvesAndShapes/VB/Class1.vb#121)]  
  
> [!NOTE]
>  在前面的示例中，画笔为 <xref:System.Drawing.SolidBrush> 类型，该类型从 <xref:System.Drawing.Brush> 继承。  
  
## 阴影画笔  
 用阴影画笔填充图形时，要指定前景色、背景色和阴影样式。  前景色是阴影的颜色。  
  
 [!code-csharp[LinesCurvesAndShapes#122](../../../../samples/snippets/csharp/VS_Snippets_Winforms/LinesCurvesAndShapes/CS/Class1.cs#122)]
 [!code-vb[LinesCurvesAndShapes#122](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/LinesCurvesAndShapes/VB/Class1.vb#122)]  
  
 [!INCLUDE[ndptecgdiplus](../../../../includes/ndptecgdiplus-md.md)] 提供 50 多种阴影样式；在下面的插图中显示的三种样式为：<xref:System.Drawing.Drawing2D.HatchStyle>、<xref:System.Drawing.Drawing2D.HatchStyle> 和 <xref:System.Drawing.Drawing2D.HatchStyle>。  
  
 ![实心形状](../../../../docs/framework/winforms/advanced/media/aboutgdip02-art18.png "Aboutgdip02\_art18")  
  
## 纹理画笔  
 有了纹理画笔，您就可以用位图中存储的图案来填充图形。  例如，假定下面的图片存储在名为 `MyTexture.bmp` 的磁盘文件中。  
  
 ![实心形状](../../../../docs/framework/winforms/advanced/media/aboutgdip02-art19.png "Aboutgdip02\_Art19")  
  
 下面的代码示例演示了如何通过重复存储在 `MyTexture.bmp` 中的图片来填充椭圆。  
  
 [!code-csharp[LinesCurvesAndShapes#123](../../../../samples/snippets/csharp/VS_Snippets_Winforms/LinesCurvesAndShapes/CS/Class1.cs#123)]
 [!code-vb[LinesCurvesAndShapes#123](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/LinesCurvesAndShapes/VB/Class1.vb#123)]  
  
 下面的插图显示已填充的椭圆。  
  
 ![实心形状](../../../../docs/framework/winforms/advanced/media/aboutgdip02-art20.png "AboutGdip02\_Art20")  
  
## 渐变画笔  
 [!INCLUDE[ndptecgdiplus](../../../../includes/ndptecgdiplus-md.md)] 提供两种渐变画笔：线性和路径。  您可以使用线性渐变画笔来用颜色（在您横向、纵向或斜向移过图形时会逐渐变化的颜色）填充图形。  下面的代码示例演示如何用水平渐变画笔填充一个椭圆，当从椭圆的左边缘向右边缘移动时，画笔颜色会由蓝变为绿。  
  
 [!code-csharp[LinesCurvesAndShapes#124](../../../../samples/snippets/csharp/VS_Snippets_Winforms/LinesCurvesAndShapes/CS/Class1.cs#124)]
 [!code-vb[LinesCurvesAndShapes#124](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/LinesCurvesAndShapes/VB/Class1.vb#124)]  
  
 下面的插图显示已填充的椭圆。  
  
 ![实心形状](../../../../docs/framework/winforms/advanced/media/aboutgdip02-art21.png "AboutGdip02\_Art21")  
  
 路径渐变画笔可配置为当您从图形中心向边缘移动时颜色随之改变。  
  
 ![实心形状](../../../../docs/framework/winforms/advanced/media/aboutgdip02-art22.png "AboutGdip02\_Art22")  
  
 路径渐变画笔非常灵活。  用于填充下面插图中三角形的渐变画笔，颜色从中心由红色开始到顶点逐渐变为三种不同的颜色。  
  
 ![实心形状](../../../../docs/framework/winforms/advanced/media/aboutgdip02-art23.png "AboutGdip02\_Art23")  
  
## 请参阅  
 <xref:System.Drawing.SolidBrush?displayProperty=fullName>   
 <xref:System.Drawing.Drawing2D.HatchBrush?displayProperty=fullName>   
 <xref:System.Drawing.TextureBrush?displayProperty=fullName>   
 <xref:System.Drawing.Drawing2D.LinearGradientBrush?displayProperty=fullName>   
 [直线、曲线和图形](../../../../docs/framework/winforms/advanced/lines-curves-and-shapes.md)   
 [如何：在 Windows 窗体上绘制实心矩形](../../../../docs/framework/winforms/advanced/how-to-draw-a-filled-rectangle-on-a-windows-form.md)   
 [如何：在 Windows 窗体上绘制实心椭圆](../../../../docs/framework/winforms/advanced/how-to-draw-a-filled-ellipse-on-a-windows-form.md)