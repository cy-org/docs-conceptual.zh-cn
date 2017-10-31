---
title: "如何：绘制贝塞尔样条序列 | Microsoft Docs"
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
  - "贝塞尔曲线样条, 绘制序列"
  - "样条, 绘制贝塞尔"
ms.assetid: 37a0bedb-20c2-4cf0-91fa-a5509e826b30
caps.latest.revision: 9
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 9
---
# 如何：绘制贝塞尔样条序列
可使用 <xref:System.Drawing.Graphics> 类的 <xref:System.Drawing.Graphics.DrawBeziers%2A> 方法绘制相连的贝塞尔样条序列。  
  
## 示例  
 下面的示例绘制一条由两条相连的贝塞尔样条组成的曲线。  第一条贝塞尔样条的终点是第二条贝塞尔样条的起点。  
  
 下面的插图显示相连的样条和这七个点。  
  
 ![贝塞尔样条](../../../../docs/framework/winforms/advanced/media/bezierspline2.png "BezierSpline2")  
  
 [!code-csharp[System.Drawing.ConstructingDrawingCurves#11](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Drawing.ConstructingDrawingCurves/CS/Class1.cs#11)]
 [!code-vb[System.Drawing.ConstructingDrawingCurves#11](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Drawing.ConstructingDrawingCurves/VB/Class1.vb#11)]  
  
## 编译代码  
 前面的示例是为使用 Windows 窗体而设计的，它需要 <xref:System.Windows.Forms.Control.Paint> 事件处理程序的参数 <xref:System.Windows.Forms.PaintEventArgs> `e`。  
  
## 请参阅  
 [Windows 窗体中的图形和绘制](../../../../docs/framework/winforms/advanced/graphics-and-drawing-in-windows-forms.md)   
 [GDI\+ 中的贝塞尔样条](../../../../docs/framework/winforms/advanced/bezier-splines-in-gdi.md)   
 [构造并绘制曲线](../../../../docs/framework/winforms/advanced/constructing-and-drawing-curves.md)