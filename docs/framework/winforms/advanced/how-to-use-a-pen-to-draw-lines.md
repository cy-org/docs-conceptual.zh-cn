---
title: "如何：使用钢笔绘制线条 | Microsoft Docs"
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
  - "文本行, 绘图"
  - "钢笔, 绘制线条"
ms.assetid: 0828c331-a438-4bdd-a4d6-3ef1e59e8795
caps.latest.revision: 16
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 16
---
# 如何：使用钢笔绘制线条
若要绘制线条，需要 <xref:System.Drawing.Graphics> 对象和 <xref:System.Drawing.Pen> 对象。  <xref:System.Drawing.Graphics> 对象提供 <xref:System.Drawing.Graphics.DrawLine%2A> 方法，而 <xref:System.Drawing.Pen> 对象则存储线条的特征，如颜色和宽度。  
  
## 示例  
 下面的示例绘制一条从 \(20, 10\) 到 \(300, 100\) 的直线。  第一条语句使用 <xref:System.Drawing.Pen.%23ctor%2A> 类构造函数创建黑色钢笔。  传递给 <xref:System.Drawing.Pen.%23ctor%2A> 构造函数的参数之一是用 <xref:System.Drawing.Color.FromArgb%2A> 方法创建的 <xref:System.Drawing.Color> 对象。  用于创建 <xref:System.Drawing.Color> 对象的值（255、0、0、0）对应于颜色的 alpha、红色、绿色和蓝色分量。  这些值定义不透明的黑色钢笔。  
  
 [!code-csharp[System.Drawing.UsingAPen#11](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Drawing.UsingAPen/CS/Class1.cs#11)]
 [!code-vb[System.Drawing.UsingAPen#11](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Drawing.UsingAPen/VB/Class1.vb#11)]  
  
## 编译代码  
 前面的示例是为使用 Windows 窗体而设计的，它需要 <xref:System.Windows.Forms.Control.Paint> 事件处理程序的参数 <xref:System.Windows.Forms.PaintEventArgs> `e`。  
  
## 请参阅  
 <xref:System.Drawing.Pen>   
 [使用钢笔绘制线条和形状](../../../../docs/framework/winforms/advanced/using-a-pen-to-draw-lines-and-shapes.md)   
 [GDI\+ 中的笔、直线和矩形](../../../../docs/framework/winforms/advanced/pens-lines-and-rectangles-in-gdi.md)