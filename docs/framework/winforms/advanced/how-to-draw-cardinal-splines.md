---
title: "如何：绘制基数样条曲线 | Microsoft Docs"
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
  - "基本样条, 绘图"
  - "绘图, 基本样条"
  - "图形, 基本样条"
ms.assetid: a4a41e80-4461-4b47-b6bd-2c5e68881994
caps.latest.revision: 13
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 13
---
# 如何：绘制基数样条曲线
基数样条是平滑通过一组给定点的曲线。  若要绘制基数样条曲线，请创建 <xref:System.Drawing.Graphics> 对象并将一组点的地址传递给 <xref:System.Drawing.Graphics.DrawCurve%2A> 方法。  
  
### 绘制钟形基数样条曲线  
  
-   下面的示例绘制了一条通过五个指定点的钟形基数样条曲线。  下面的插图显示该曲线和五个点。  
  
 [!code-csharp[System.Drawing.ConstructingDrawingCurves#21](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Drawing.ConstructingDrawingCurves/CS/Class1.cs#21)]
 [!code-vb[System.Drawing.ConstructingDrawingCurves#21](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Drawing.ConstructingDrawingCurves/VB/Class1.vb#21)]  
  
### 绘制闭合的基数样条曲线  
  
-   使用 <xref:System.Drawing.Graphics> 类的 <xref:System.Drawing.Graphics.DrawClosedCurve%2A> 方法可绘制闭合的基数样条曲线。  在闭合的基数样条曲线中，曲线连续通过系列中最后一个点，并与系列中的第一个点连接。  下面的示例绘制了一条通过六个指定点的闭合的基数样条曲线。  下面的插图显示闭合的样条曲线和六个点。  
  
 ![基数样条](../../../../docs/framework/winforms/advanced/media/cardinalspline1a.png "CardinalSpline1A")  
  
 [!code-csharp[System.Drawing.ConstructingDrawingCurves#22](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Drawing.ConstructingDrawingCurves/CS/Class1.cs#22)]
 [!code-vb[System.Drawing.ConstructingDrawingCurves#22](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Drawing.ConstructingDrawingCurves/VB/Class1.vb#22)]  
  
### 更改基数样条曲线的弯曲方式  
  
-   通过将张力参数传递给 <xref:System.Drawing.Graphics.DrawCurve%2A> 方法，可更改基数样条曲线的弯曲方式。  下面的示例绘制了三条通过同一组点的基数样条曲线。  下面的插图显示三条样条曲线及其张力值。  请注意，当张力为 0 时，这些点由一条直线连接。  
  
 ![基数样条](../../../../docs/framework/winforms/advanced/media/cardinalspline2.png "CardinalSpline2")  
  
 [!code-csharp[System.Drawing.ConstructingDrawingCurves#23](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Drawing.ConstructingDrawingCurves/CS/Class1.cs#23)]
 [!code-vb[System.Drawing.ConstructingDrawingCurves#23](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Drawing.ConstructingDrawingCurves/VB/Class1.vb#23)]  
  
## 编译代码  
 前面的示例是为使用 Windows 窗体而设计的，它们需要 <xref:System.Windows.Forms.Control.Paint> 事件处理程序的参数 <xref:System.Windows.Forms.PaintEventArgs> `e`。  
  
## 请参阅  
 [直线、曲线和图形](../../../../docs/framework/winforms/advanced/lines-curves-and-shapes.md)   
 [构造并绘制曲线](../../../../docs/framework/winforms/advanced/constructing-and-drawing-curves.md)