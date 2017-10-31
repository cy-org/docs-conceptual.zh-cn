---
title: "如何：在 Windows 窗体上绘制线条 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-winforms"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "Graphics.DrawLine"
dev_langs: 
  - "jsharp"
helpviewer_keywords: 
  - "绘制线条"
  - "绘图, 文本行"
  - "示例 [Windows 窗体], 在窗体上绘制线条"
  - "文本行, 绘图"
ms.assetid: 55c1dbeb-75d0-430c-9814-a24b8971ad8c
caps.latest.revision: 13
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 13
---
# 如何：在 Windows 窗体上绘制线条
此示例在窗体上绘制线条。  通常，当您在窗体上进行绘制时，您使用 <xref:System.Windows.Forms.PaintEventArgs> 的 <xref:System.Windows.Forms.PaintEventArgs.Graphics%2A> 属性处理窗体的 <xref:System.Windows.Forms.Control.Paint> 事件和执行绘制，如此示例所示  
  
## 示例  
 [!code-csharp[System.Drawing.UsingAPen#11](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Drawing.UsingAPen/CS/Class1.cs#11)]
 [!code-vb[System.Drawing.UsingAPen#11](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Drawing.UsingAPen/VB/Class1.vb#11)]  
  
## 编译代码  
 前面的示例是为使用 Windows 窗体而设计的，它需要 <xref:System.Windows.Forms.Control.Paint> 事件处理程序的参数 <xref:System.Windows.Forms.PaintEventArgs> `e`。  
  
## 可靠编程  
 应始终对消耗系统资源的任何对象（如 <xref:System.Drawing.Pen> 对象）调用 <xref:System.IDisposable.Dispose%2A>。  
  
## 请参阅  
 <xref:System.Drawing.Graphics.DrawLine%2A>   
 <xref:System.Windows.Forms.Control.OnPaint%2A>   
 [图形编程入门](../../../../docs/framework/winforms/advanced/getting-started-with-graphics-programming.md)   
 [使用钢笔绘制线条和形状](../../../../docs/framework/winforms/advanced/using-a-pen-to-draw-lines-and-shapes.md)   
 [Windows 窗体中的图形和绘制](../../../../docs/framework/winforms/advanced/graphics-and-drawing-in-windows-forms.md)