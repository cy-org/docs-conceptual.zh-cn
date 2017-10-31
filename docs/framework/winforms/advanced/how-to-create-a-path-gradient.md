---
title: "如何：创建路径渐变 | Microsoft Docs"
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
  - "渐变, 创建路径"
  - "图形路径, 创建渐变"
  - "路径渐变, 创建"
ms.assetid: 1948e834-e104-481c-b71d-d8aa9e4d106e
caps.latest.revision: 19
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 19
---
# 如何：创建路径渐变
<xref:System.Drawing.Drawing2D.PathGradientBrush> 类使您可以自定义用渐变色填充形状的方式。  例如，可为轨迹的中心指定一种颜色；为轨迹的边界指定另一种颜色。  还可为轨迹边界上的七个点分别指定颜色。  
  
> [!NOTE]
>  在 [!INCLUDE[ndptecgdiplus](../../../../includes/ndptecgdiplus-md.md)] 中，路径是由 <xref:System.Drawing.Drawing2D.GraphicsPath> 对象维护的一系列线条和曲线。  有关 [!INCLUDE[ndptecgdiplus](../../../../includes/ndptecgdiplus-md.md)] 路径的更多信息，请参见[GDI\+ 中的图形路径](../../../../docs/framework/winforms/advanced/graphics-paths-in-gdi.md)和[构造并绘制轨迹](../../../../docs/framework/winforms/advanced/constructing-and-drawing-paths.md)。  
  
### 使用路径渐变填充椭圆  
  
-   下面的示例用路径渐变画笔填充椭圆。  中心的颜色设置为蓝色；边界的颜色设置为浅绿色。  下面的插图显示已填充的椭圆。  
  
     ![渐变路径](../../../../docs/framework/winforms/advanced/media/pathgradient1.png "pathgradient1")  
  
     默认情况下，路径渐变画笔不会延伸到路径边界以外。  如果您使用路径渐变画笔来填充延伸到路径边界以外的图形，则无法填充路径以外的屏幕区域。  
  
     下图演示在将以下代码中的 <xref:System.Drawing.Graphics.FillEllipse%2A> 调用更改为 `e.Graphics.FillRectangle(pthGrBrush, 0, 10, 200, 40)` 后所出现的情况。  
  
     ![渐变路径](../../../../docs/framework/winforms/advanced/media/pathgradient2.png "pathgradient2")  
  
     [!code-csharp[System.Drawing.UsingaGradientBrush#11](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Drawing.UsingaGradientBrush/CS/Class1.cs#11)]
     [!code-vb[System.Drawing.UsingaGradientBrush#11](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Drawing.UsingaGradientBrush/VB/Class1.vb#11)]  
  
     前面的代码示例旨在用于 Windows 窗体，它需要 <xref:System.Windows.Forms.PaintEventHandler> 的参数 <xref:System.Windows.Forms.PaintEventArgs> e。  
  
### 在边界上指定点  
  
-   下面的示例由星形轨迹构造路径渐变画笔。  该代码设置 <xref:System.Drawing.Drawing2D.PathGradientBrush.CenterColor%2A> 属性，它将星形中心的颜色设置为红色。  然后，该代码设置 <xref:System.Drawing.Drawing2D.PathGradientBrush.SurroundColors%2A> 属性，以便在 `points` 数组中的各个点处指定不同的颜色（存储在 `colors` 数组中）。  最后一个代码语句用路径渐变画笔填充星形轨迹。  
  
     [!code-csharp[System.Drawing.UsingaGradientBrush#12](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Drawing.UsingaGradientBrush/CS/Class1.cs#12)]
     [!code-vb[System.Drawing.UsingaGradientBrush#12](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Drawing.UsingaGradientBrush/VB/Class1.vb#12)]  
  
-   下面的示例在代码中不使用 <xref:System.Drawing.Drawing2D.GraphicsPath> 对象而绘制一个路径渐变。  在该示例中，特定的 <xref:System.Drawing.Drawing2D.PathGradientBrush.%23ctor%2A> 构造函数接收一系列点，但是不需要 <xref:System.Drawing.Drawing2D.GraphicsPath> 对象。  同时，请注意，<xref:System.Drawing.Drawing2D.PathGradientBrush> 用于填充矩形而不是填充路径。  矩形比用于定义画笔的闭合轨迹大，因此矩形的某些部分未由画笔涂色。  下面的插图显示该矩形（虚线）以及该矩形被路径渐变画笔涂色的那部分。  
  
     ![渐变](../../../../docs/framework/winforms/advanced/media/gradient4.png "gradient4")  
  
     [!code-csharp[System.Drawing.UsingaGradientBrush#13](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Drawing.UsingaGradientBrush/CS/Class1.cs#13)]
     [!code-vb[System.Drawing.UsingaGradientBrush#13](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Drawing.UsingaGradientBrush/VB/Class1.vb#13)]  
  
### 自定义路径渐变  
  
-   自定义路径渐变画笔的一种方法就是设置它的 <xref:System.Drawing.Drawing2D.PathGradientBrush.FocusScales%2A> 属性。  聚焦缩放指定位于主轨迹内部的内部轨迹。  中心颜色显示在内部轨迹中的任何地方，而不是只显示在中心点。  
  
     下面的示例根据椭圆轨迹创建路径渐变画笔。  该代码将边界颜色设置为蓝色，将中心颜色设置为浅绿色，然后使用路径渐变画笔填充椭圆轨迹。  
  
     接着，该代码设置路径渐变画笔的聚焦缩放。  x 聚焦缩放被设置为 0.3，y 聚焦缩放被设置为 0.8。  该代码调用 <xref:System.Drawing.Graphics> 对象的 <xref:System.Drawing.Graphics.TranslateTransform%2A> 方法，以便后来对 <xref:System.Drawing.Graphics.FillPath%2A> 的调用填充位于第一个椭圆右侧的椭圆。  
  
     若要观看聚焦缩放的效果，请设想一个与主椭圆共用一个中心的小椭圆。  小（内部）椭圆是由主椭圆在水平方向上缩小 0.3 倍，在垂直方向上缩小 0.8 倍（围绕其中心）得到的。  当从外部椭圆的边界移到内部椭圆的边界时，颜色逐渐从蓝色变成浅绿色。  当从内部椭圆的边界移到共用中心时，颜色保持浅绿色。  
  
     下面的插图显示以下代码的输出。  左边的椭圆只在中心点上为浅绿色。  右边的椭圆在内部轨迹内部的任何地方都为浅绿色。  
  
 ![渐变](../../../../docs/framework/winforms/advanced/media/focusscales1nogamma.png "focusscales1NoGamma")  
  
 [!code-csharp[System.Drawing.UsingaGradientBrush#14](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Drawing.UsingaGradientBrush/CS/Class1.cs#14)]
 [!code-vb[System.Drawing.UsingaGradientBrush#14](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Drawing.UsingaGradientBrush/VB/Class1.vb#14)]  
  
### 使用插值自定义  
  
-   自定义路径渐变画笔的另一种方法是指定插值颜色数组和插值位置数组。  
  
     下面的示例基于三角形创建路径渐变画笔。  该代码设置路径渐变画笔的 <xref:System.Drawing.Drawing2D.PathGradientBrush.InterpolationColors%2A> 属性，以便指定插值颜色数组（深绿色，浅绿色，蓝色）和插值位置数组 \(0, 0.25, 1\)。  当从三角形的边界移到中心点时，颜色将从深绿色逐渐变成浅绿色，然后从浅绿色变成蓝色。  深绿色到浅绿色的转变发生在深绿色到蓝色转变的距离的 25% 处。  
  
     下面的插图显示用自定义路径渐变画笔填充的三角形。  
  
     [!code-csharp[System.Drawing.UsingaGradientBrush#15](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Drawing.UsingaGradientBrush/CS/Class1.cs#15)]
     [!code-vb[System.Drawing.UsingaGradientBrush#15](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Drawing.UsingaGradientBrush/VB/Class1.vb#15)]  
  
### 设置中心点  
  
-   在默认情况下，路径渐变画笔的中心点位于用来构造梯度刷的轨迹的形心。  可通过设置 <xref:System.Drawing.Drawing2D.PathGradientBrush> 类的 <xref:System.Drawing.Drawing2D.PathGradientBrush.CenterPoint%2A> 属性更改中心点的位置。  
  
     下面的示例基于椭圆来创建路径渐变画笔。  椭圆的中心位于 \(70, 35\)，但是路径渐变画笔的中心点设置在 \(120, 40\)。  
  
     [!code-csharp[System.Drawing.UsingaGradientBrush#16](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Drawing.UsingaGradientBrush/CS/Class1.cs#16)]
     [!code-vb[System.Drawing.UsingaGradientBrush#16](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Drawing.UsingaGradientBrush/VB/Class1.vb#16)]  
  
     下面的插图显示实心椭圆和路径渐变画笔的中心点。  
  
     ![渐变路径](../../../../docs/framework/winforms/advanced/media/pathgradient5.png "pathgradient5")  
  
-   可将路径渐变画笔的中心点设置在用于构造梯度刷的轨迹外部的某个位置。  下面的示例通过替换调用来设置以上代码中的 <xref:System.Drawing.Drawing2D.PathGradientBrush.CenterPoint%2A> 属性。  
  
     [!code-csharp[System.Drawing.UsingaGradientBrush#17](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Drawing.UsingaGradientBrush/CS/Class1.cs#17)]
     [!code-vb[System.Drawing.UsingaGradientBrush#17](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Drawing.UsingaGradientBrush/VB/Class1.vb#17)]  
  
     下面的插图显示更改后的输出。  
  
     ![渐变路径](../../../../docs/framework/winforms/advanced/media/pathgradient6.png "pathgradient6")  
  
     在上面的插图中，椭圆最右边的那些点不是纯蓝色（尽管它们非常接近）。  渐变中颜色的定位就好像是填充到颜色为纯蓝色 \(0, 0, 255\) 的点 \(145, 35\)。  但是，由于路径渐变画笔只在其轨迹内部涂色，所以并未填充到点 \(145, 35\)。  
  
## 编译代码  
 前面的示例是为使用 Windows 窗体而设计的，它们需要 <xref:System.Windows.Forms.Control.Paint> 事件处理程序的参数 <xref:System.Windows.Forms.PaintEventArgs> `e`。  
  
## 请参阅  
 [使用渐变画笔填充形状](../../../../docs/framework/winforms/advanced/using-a-gradient-brush-to-fill-shapes.md)