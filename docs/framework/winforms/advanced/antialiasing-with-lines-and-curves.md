---
title: "用直线和曲线抗锯齿 | Microsoft Docs"
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
  - "Antialias 处理"
  - "Antialias 处理, 平滑模式"
  - "GDI+, Antialias 处理"
ms.assetid: 810da1a4-c136-4abf-88df-68e49efdd8d4
caps.latest.revision: 16
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 16
---
# 用直线和曲线抗锯齿
当使用 [!INCLUDE[ndptecgdiplus](../../../../includes/ndptecgdiplus-md.md)] 绘制直线时，需要提供直线的起点和终点，但不必提供有关直线上的各个像素的任何信息。  [!INCLUDE[ndptecgdiplus](../../../../includes/ndptecgdiplus-md.md)] 与显示设备驱动程序软件协同工作，确定要启用哪些像素以便在特定显示设备上显示直线。  
  
## 锯齿化  
 请注意从点 \(4，2\) 到点 \(16，10\) 的红色直线。  假定坐标系统的原点位于左上角且度量单位是像素。  另外假定 x 坐标轴指向右边、y 坐标轴指向下边。  下面的插图显示了在多颜色背景下绘制的红线的放大视图。  
  
 ![未抗锯齿的直线](../../../../docs/framework/winforms/advanced/media/aboutgdip02-art33.png "AboutGdip02\_Art33")  
  
 用来呈现直线的红色像素是不透明的。  直线中没有部分透明的像素。  这种呈现类型的直线看上去带有锯齿，有点像楼梯。  这种用楼梯状来表示直线的技术被称为锯齿化；楼梯是理论直线的一个别名。  
  
## 抗锯齿  
 一项更为复杂的呈现直线的技术需要使用部分透明的像素和不透明的像素。  像素被设为纯红色或红色与背景色的混合色（取决于它们和直线的接近程度）。  这种呈现方式被称为抗锯齿，它可以生成视觉上更感平滑的直线。  下面的插图显示了如何混合特定的像素和背景来生成抗锯齿的直线。  
  
 ![消除直线的锯齿](../../../../docs/framework/winforms/advanced/media/aboutgdip02-art34.png "AboutGdip02\_Art34")  
  
 抗锯齿（也称为平滑）也可应用于曲线。  下面的插图显示了平滑椭圆的放大视图。  
  
 ![消除曲线的锯齿](../../../../docs/framework/winforms/advanced/media/aboutgdip02-art35.png "AboutGdip02\_Art35")  
  
 下面的插图显示了实际大小的同一个椭圆，一次没有使用抗锯齿，另一次使用了抗锯齿。  
  
 ![抗锯齿示例](../../../../docs/framework/winforms/advanced/media/aboutgdip02-art36.gif "AboutGdip02\_Art36")  
  
 若要使用“抗锯齿”功能绘制直线和曲线，请创建 <xref:System.Drawing.Graphics> 类的实例，并将其 <xref:System.Drawing.Graphics.SmoothingMode%2A> 属性设置为 <xref:System.Drawing.Drawing2D.SmoothingMode> 或 <xref:System.Drawing.Drawing2D.SmoothingMode>。  然后调用同一 <xref:System.Drawing.Graphics> 类的某个绘制方法。  
  
 [!code-csharp[LinesCurvesAndShapes#81](../../../../samples/snippets/csharp/VS_Snippets_Winforms/LinesCurvesAndShapes/CS/Class1.cs#81)]
 [!code-vb[LinesCurvesAndShapes#81](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/LinesCurvesAndShapes/VB/Class1.vb#81)]  
  
## 请参阅  
 <xref:System.Drawing.Drawing2D.SmoothingMode?displayProperty=fullName>   
 [直线、曲线和图形](../../../../docs/framework/winforms/advanced/lines-curves-and-shapes.md)   
 [如何：对文本使用抗锯齿效果](../../../../docs/framework/winforms/advanced/how-to-use-antialiasing-with-text.md)