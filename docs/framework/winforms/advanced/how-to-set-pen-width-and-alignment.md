---
title: "如何：设置钢笔的宽度和对齐方式 | Microsoft Docs"
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
  - "钢笔, 设置对齐方式"
  - "钢笔, 设置宽度"
ms.assetid: a202af36-4d31-4401-a126-b232f51db581
caps.latest.revision: 16
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 16
---
# 如何：设置钢笔的宽度和对齐方式
在创建 <xref:System.Drawing.Pen> 时，可将笔的宽度作为参数之一提供给构造函数。  还可用 <xref:System.Drawing.Pen> 类的 <xref:System.Drawing.Pen.Width%2A> 属性更改笔的宽度。  
  
 理论线条的宽度为 0。  当绘制一条 1 个像素宽的线条时，像素以理论线条为中心线分布。  如果绘制的线条宽度大于 1 个像素，则这些像素要么以理论线条为中心线分布，要么出现在理论线条的一侧。  可设置 <xref:System.Drawing.Pen> 的笔对齐方式属性，以确定用该笔绘制的像素相对于理论线条如何定位。  
  
 在下面的代码示例中显示的值 <xref:System.Drawing.Drawing2D.PenAlignment>、<xref:System.Drawing.Drawing2D.PenAlignment> 和 <xref:System.Drawing.Drawing2D.PenAlignment> 为 <xref:System.Drawing.Drawing2D.PenAlignment> 枚举的成员。  
  
 下面的代码示例绘制一段线条两次：一次用宽度为 1 的黑色钢笔，一次用宽度为 10 的绿色钢笔。  
  
### 改变钢笔的宽度  
  
-   将 <xref:System.Drawing.Pen.Alignment%2A> 属性的值设置为 <xref:System.Drawing.Drawing2D.PenAlignment>（默认值），以指定用绿色钢笔绘制的像素以理论线条为中心线分布。  下面的插图显示结果线条。  
  
     ![钢笔](../../../../docs/framework/winforms/advanced/media/pens1a.png "pens1A")  
  
     下面的代码示例绘制一个矩形两次：一次用宽度为 1 的黑色钢笔，一次用宽度为 10 的绿色钢笔。  
  
     [!code-csharp[System.Drawing.UsingAPen#41](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Drawing.UsingAPen/CS/Class1.cs#41)]
     [!code-vb[System.Drawing.UsingAPen#41](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Drawing.UsingAPen/VB/Class1.vb#41)]  
  
### 更改钢笔的对齐方式  
  
-   将 <xref:System.Drawing.Pen.Alignment%2A> 属性的值设置为 <xref:System.Drawing.Drawing2D.PenAlignment>，以指定用绿色钢笔绘制的像素以矩形边界为中心分布。  
  
     下面的插图显示结果矩形。  
  
     ![钢笔](../../../../docs/framework/winforms/advanced/media/pens2.png "pens2")  
  
     [!code-csharp[System.Drawing.UsingAPen#42](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Drawing.UsingAPen/CS/Class1.cs#42)]
     [!code-vb[System.Drawing.UsingAPen#42](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Drawing.UsingAPen/VB/Class1.vb#42)]  
  
### 创建嵌入钢笔  
  
-   可通过将上述代码示例中的第三条语句修改为以下语句来更改绿色钢笔的对齐方式：  
  
     [!code-csharp[System.Drawing.UsingAPen#43](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Drawing.UsingAPen/CS/Class1.cs#43)]
     [!code-vb[System.Drawing.UsingAPen#43](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Drawing.UsingAPen/VB/Class1.vb#43)]  
  
     现在，绿色宽线条中的像素出现在矩形的内侧，如下面的插图所示。  
  
     ![钢笔](../../../../docs/framework/winforms/advanced/media/pens3.png "pens3")  
  
## 请参阅  
 [使用钢笔绘制线条和形状](../../../../docs/framework/winforms/advanced/using-a-pen-to-draw-lines-and-shapes.md)   
 [Windows 窗体中的图形和绘制](../../../../docs/framework/winforms/advanced/graphics-and-drawing-in-windows-forms.md)