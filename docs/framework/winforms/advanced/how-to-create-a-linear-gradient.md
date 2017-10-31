---
title: "如何：创建线性渐变 | Microsoft Docs"
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
  - "颜色, 创建线性渐变"
  - "渐变"
  - "渐变, 创建线性"
  - "线性渐变, 创建"
ms.assetid: 6c88e1cc-1217-4399-ac12-cb37592b9f01
caps.latest.revision: 17
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 17
---
# 如何：创建线性渐变
[!INCLUDE[ndptecgdiplus](../../../../includes/ndptecgdiplus-md.md)] 提供水平、垂直和对角线方向线性渐变。  在默认情况下，线性渐变中的颜色均匀地变化。  当然，也可自定义线性渐变，使颜色非均匀变化。  
  
 下面的示例使用水平线性渐变画笔填充线条、椭圆和矩形。  
  
 <xref:System.Drawing.Drawing2D.LinearGradientBrush.%23ctor%2A> 构造函数接收四个参数：两个点和两种颜色。  第一个点 \(0, 10\) 与第一种颜色（红色）相关联，第二个点 \(200, 10\) 与第二种颜色（蓝色）相关联。  正如您所期望的那样，从 \(0, 10\) 绘制到 \(200, 10\) 的线条的颜色从红色逐渐变成蓝色。  
  
 点 \(50, 10\) 和点 \(200, 10\) 中的 10 无关紧要。  重要的是这两个点的第二个坐标相同——它们之间的连线是水平的。  当水平坐标从 0 移到 200 时，椭圆和矩形也逐渐从红色变成蓝色。  
  
 下面的插图显示线条、椭圆和矩形。  请注意，当水平坐标增加到 200 以上时，颜色渐变重复其自身。  
  
 ![线性渐变](../../../../docs/framework/winforms/advanced/media/cslineargradient1.png "cslineargradient1")  
  
### 使用水平线性渐变  
  
-   将不透明红和不透明蓝分别作为第三和第四个参数传递。  
  
     [!code-csharp[System.Drawing.UsingaGradientBrush#21](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Drawing.UsingaGradientBrush/CS/Class1.cs#21)]
     [!code-vb[System.Drawing.UsingaGradientBrush#21](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Drawing.UsingaGradientBrush/VB/Class1.vb#21)]  
  
 在上面的示例中，当您从水平坐标 0 移到水平坐标 200 时，颜色分量成线性变化。  例如，如果某个点的第一个坐标位于 0 和 200 的正中间，则其蓝色分量将是 0 和 255 正中间的值。  
  
 [!INCLUDE[ndptecgdiplus](../../../../includes/ndptecgdiplus-md.md)] 可用于调整颜色从渐变的一个边缘到另一个边缘变化的方式。  假设您希望按照下表创建从黑色变到红色的渐变画笔。  
  
|水平坐标|RGB 组件|  
|----------|------------|  
|0|\(0, 0, 0\)|  
|40|\(128, 0, 0\)|  
|200|\(255, 0, 0\)|  
  
 请注意，当水平坐标才达到 0 到 200 之间的 20% 时，红色分量已达到一半亮度。  
  
 下面的示例设置 <xref:System.Drawing.Drawing2D.LinearGradientBrush> 对象的 <xref:System.Drawing.Drawing2D.LinearGradientBrush.Blend%2A> 属性，以便使三个相对亮度与三个相对位置相关联。  正如上表所示，相对亮度 0.5 与相对位置 0.2 相关联。  该代码用渐变画笔填充椭圆和矩形。  
  
 下面的插图显示所得到的椭圆和矩形。  
  
 ![线性渐变](../../../../docs/framework/winforms/advanced/media/cslineargradient2.png "cslineargradient2")  
  
### 自定义线性渐变  
  
-   将不透明黑和不透明红分别作为第三和第四个参数传递。  
  
     [!code-csharp[System.Drawing.UsingaGradientBrush#22](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Drawing.UsingaGradientBrush/CS/Class1.cs#22)]
     [!code-vb[System.Drawing.UsingaGradientBrush#22](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Drawing.UsingaGradientBrush/VB/Class1.vb#22)]  
  
 在上面的示例中，渐变的方向是水平的；即，当沿着水平线移动时，颜色逐渐变化。  还可以定义垂直渐变和对角线渐变。  
  
 下面的示例将点 \(0, 0\) 和点 \(200, 100\) 传递给 <xref:System.Drawing.Drawing2D.LinearGradientBrush.%23ctor%2A> 构造函数。  蓝色与 \(0, 0\) 相关联，绿色与 \(200, 100\) 相关联。  用线性渐变画笔填充线条（画笔的宽度为 10）和椭圆。  
  
 下面的插图显示该线条和椭圆。  请注意，当沿着任何与穿过 \(0, 0\) 和 \(200, 100\) 的直线平行的直线移动时，椭圆中的颜色逐渐变化。  
  
 ![线性渐变](../../../../docs/framework/winforms/advanced/media/cslineargradient3.png "cslineargradient3")  
  
### 创建对角线性渐变  
  
-   将不透明蓝和不透明绿分别作为第三和第四个参数传递。  
  
     [!code-csharp[System.Drawing.UsingaGradientBrush#23](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Drawing.UsingaGradientBrush/CS/Class1.cs#23)]
     [!code-vb[System.Drawing.UsingaGradientBrush#23](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Drawing.UsingaGradientBrush/VB/Class1.vb#23)]  
  
## 请参阅  
 [使用渐变画笔填充形状](../../../../docs/framework/winforms/advanced/using-a-gradient-brush-to-fill-shapes.md)   
 [Windows 窗体中的图形和绘制](../../../../docs/framework/winforms/advanced/graphics-and-drawing-in-windows-forms.md)