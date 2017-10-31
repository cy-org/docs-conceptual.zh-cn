---
title: "如何：绘制单个贝塞尔样条 | Microsoft Docs"
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
  - "贝塞尔曲线样条, 绘图"
  - "绘图, 贝塞尔曲线样条"
ms.assetid: f4f3fe30-f0a6-4743-ac91-11310cebea9f
caps.latest.revision: 15
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 15
---
# 如何：绘制单个贝塞尔样条
用四个点定义一条贝塞尔样条：一个起点、两个控制点和一个终点。  
  
## 示例  
 下面的示例绘制了一条起点为 \(10, 100\)、终点为 \(200, 100\) 的贝塞尔样条。  两个控制点分别为 \(100, 10\) 和 \(150, 150\)。  
  
 下面的插图显示产生的贝塞尔样条及其起点、控制点和终点。  该插图还显示样条的凸包，凸包是通过将这四个点用直线相连而形成的多边形。  
  
 ![贝塞尔样条](../../../../docs/framework/winforms/advanced/media/bezierspline1.png "BezierSpline1")  
  
 [!code-csharp[System.Drawing.ConstructingDrawingCurves#31](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Drawing.ConstructingDrawingCurves/CS/Class1.cs#31)]
 [!code-vb[System.Drawing.ConstructingDrawingCurves#31](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Drawing.ConstructingDrawingCurves/VB/Class1.vb#31)]  
  
## 编译代码  
 前面的示例是为使用 Windows 窗体而设计的，它需要 <xref:System.Windows.Forms.Control.Paint> 事件处理程序的参数 <xref:System.Windows.Forms.PaintEventArgs> `e`。  
  
## 请参阅  
 <xref:System.Drawing.Graphics.DrawBezier%2A>   
 [GDI\+ 中的贝塞尔样条](../../../../docs/framework/winforms/advanced/bezier-splines-in-gdi.md)   
 [如何：绘制贝塞尔样条序列](../../../../docs/framework/winforms/advanced/how-to-draw-a-sequence-of-bezier-splines.md)