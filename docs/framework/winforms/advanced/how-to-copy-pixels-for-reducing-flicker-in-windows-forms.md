---
title: "如何：在 Windows 窗体中复制像素以减少闪烁 | Microsoft Docs"
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
  - "位块传送"
  - "位块传送"
  - "闪烁"
  - "闪烁, 在 Windows 窗体中减少"
  - "图形, 复制"
  - "图形, 减少闪烁"
  - "像素, 复制"
ms.assetid: 33b76910-13a3-4521-be98-5c097341ae3b
caps.latest.revision: 13
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 13
---
# 如何：在 Windows 窗体中复制像素以减少闪烁
在使一个简单图形产生动画效果时，用户有时可能会遇到闪烁或其他不需要的视觉效果。  限制出现此问题的一种方法是对该图形使用“bitblt”进程。  Bitblt 是颜色数据从像素原始矩形到像素目标矩形的“位块转换”。  
  
 在 Windows 窗体中，bitblt 是通过使用 <xref:System.Drawing.Graphics> 类的 <xref:System.Drawing.Graphics.CopyFromScreen%2A> 方法实现的。  您可以在该方法的参数中指定源和目标（根据点）、要复制的区域大小和用于绘制新形状的图形对象。  
  
 在下面的示例中，使用 <xref:System.Windows.Forms.Control.Paint> 事件处理程序在窗体上绘制了一个形状。  然后，使用 <xref:System.Drawing.Graphics.CopyFromScreen%2A> 方法复制了该形状。  
  
> [!NOTE]
>  将窗体的 <xref:System.Windows.Forms.Control.DoubleBuffered%2A> 属性设置为 `true` 将使 <xref:System.Windows.Forms.Control.Paint> 事件中基于图形的代码被双缓冲。  但在使用下面的代码时不会有任何明显的性能提升，这一点在使用更加复杂的图形操作代码时必须记住。  
  
## 示例  
  
```vb  
Private Sub Form1_Paint(ByVal sender As Object, ByVal e As _  
    System.Windows.Forms.PaintEventArgs) Handles MyBase.Paint  
    ' Draw a circle with a bar on top.  
        e.Graphics.FillEllipse(Brushes.DarkBlue, New Rectangle _  
             (10, 10, 60, 60))  
        e.Graphics.FillRectangle(Brushes.Khaki, New Rectangle _  
             (20, 30, 60, 10))  
    ' Copy the graphic to a new location.  
        e.Graphics.CopyFromScreen(New Point(10, 10), New Point _  
             (100, 100), New Size(70, 70))  
End Sub  
  
```  
  
```csharp  
private void Form1_Paint(System.Object sender,  
    System.Windows.Forms.PaintEventArgs e)  
        {  
        e.Graphics.FillEllipse(Brushes.DarkBlue, new  
            Rectangle(10,10,60,60));  
        e.Graphics.FillRectangle(Brushes.Khaki, new  
            Rectangle(20,30,60,10));  
        e.Graphics.CopyFromScreen(new Point(10, 10), new Point(100, 100),   
            new Size(70, 70));  
}  
```  
  
## 编译代码  
 上面的代码在窗体的 <xref:System.Windows.Forms.Control.Paint> 事件处理程序中运行，从而在重新绘制窗体时仍然会保持图形。  同样地，不要在 <xref:System.Windows.Forms.Form.Load> 事件处理程序中调用图形相关的方法，因为如果窗体大小经过调整或被其他窗体遮盖后，已绘制的内容将不会重新绘制。  
  
## 请参阅  
 <xref:System.Drawing.CopyPixelOperation>   
 <xref:System.Drawing.Graphics.FillRectangle%2A?displayProperty=fullName>   
 <xref:System.Windows.Forms.Control.OnPaint%2A?displayProperty=fullName>   
 [Windows 窗体中的图形和绘制](../../../../docs/framework/winforms/advanced/graphics-and-drawing-in-windows-forms.md)   
 [使用钢笔绘制线条和形状](../../../../docs/framework/winforms/advanced/using-a-pen-to-draw-lines-and-shapes.md)