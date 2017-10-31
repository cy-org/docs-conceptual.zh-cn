---
title: "如何：绘制用纹理填充的线条 | Microsoft Docs"
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
  - "绘制线条, 纹理"
  - "绘图, 文本行"
  - "文本行, 纹理"
ms.assetid: dc9118cc-f3c2-42e5-8173-f46d41d18fd5
caps.latest.revision: 12
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 12
---
# 如何：绘制用纹理填充的线条
您可以不用纯色绘制线条，而用纹理绘制线条。  若要绘制带有纹理的直线和曲线，请创建 <xref:System.Drawing.TextureBrush> 对象，并将该 <xref:System.Drawing.TextureBrush> 对象传递给 <xref:System.Drawing.Pen.%23ctor%2A> 构造函数。  与该纹理刷相关联的位图用于平铺平面（不可见），然后当钢笔绘制直线或曲线时，钢笔的笔划揭开平铺纹理的某些像素。  
  
## 示例  
 下面的示例从文件  `Texture1.jpg` 创建 <xref:System.Drawing.Bitmap> 对象。  位图用于构造 <xref:System.Drawing.TextureBrush> 对象，而 <xref:System.Drawing.TextureBrush> 对象用于构造 <xref:System.Drawing.Pen> 对象。  对 <xref:System.Drawing.Graphics.DrawImage%2A> 的调用将绘制该位图，位图的左上角位于 \(0, 0\)。  对 <xref:System.Drawing.Graphics.DrawEllipse%2A> 的调用将使用 <xref:System.Drawing.Pen> 对象绘制带纹理的椭圆。  
  
 下面的插图显示该位图和带纹理的椭圆。  
  
 ![钢笔](../../../../docs/framework/winforms/advanced/media/pens7.png "pens7")  
  
 [!code-csharp[System.Drawing.UsingAPen#61](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Drawing.UsingAPen/CS/Class1.cs#61)]
 [!code-vb[System.Drawing.UsingAPen#61](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Drawing.UsingAPen/VB/Class1.vb#61)]  
  
## 编译代码  
 创建一个 Windows 窗体并处理窗体的 <xref:System.Windows.Forms.Control.Paint> 事件。  将上面的代码粘贴到 <xref:System.Windows.Forms.Control.Paint> 事件处理程序中。  用一个对您的系统有效的图像替换  `Texture.jpg`。  
  
## 请参阅  
 [使用钢笔绘制线条和形状](../../../../docs/framework/winforms/advanced/using-a-pen-to-draw-lines-and-shapes.md)   
 [Windows 窗体中的图形和绘制](../../../../docs/framework/winforms/advanced/graphics-and-drawing-in-windows-forms.md)