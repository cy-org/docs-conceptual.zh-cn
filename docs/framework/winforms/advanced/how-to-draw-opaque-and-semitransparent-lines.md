---
title: "如何：绘制不透明和半透明的线条 | Microsoft Docs"
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
  - "alpha 混合, 绘制线条"
  - "绘图, 文本行"
  - "文本行, 绘制 alpha 混合的"
  - "透明度, 文本行"
ms.assetid: 8f2508af-f495-4223-b5cc-646cbbb520eb
caps.latest.revision: 18
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 18
---
# 如何：绘制不透明和半透明的线条
绘制线条时，必须将 <xref:System.Drawing.Pen> 对象传递给 <xref:System.Drawing.Graphics> 类的 <xref:System.Drawing.Graphics.DrawLine%2A> 方法。  <xref:System.Drawing.Pen.%23ctor%2A> 构造函数的参数之一是 <xref:System.Drawing.Color> 对象。  若要绘制不透明的线条，请将颜色的 alpha 分量设置为 255。  若要绘制半透明的线条，请将 alpha 分量设置为从 1 到 254 的任何值。  
  
 在背景上绘制半透明的线条时，线条的颜色与背景的颜色混合。  alpha 分量指定线条和背景色混合的方式；alpha 值越接近 0，背景颜色的权重越大，alpha 值越接近 255，线条颜色的权重越大。  
  
## 示例  
 下面的示例绘制一个位图，然后制使用该位图作为背景绘三条线。  第一条线使用值为 255 的 alpha 分量，因此它是不透明的。  第二条和第三条线使用值为 128 的 alpha 分量，因此它们是半透明的；你可透过线条看到背景图像。  设置 <xref:System.Drawing.Graphics.CompositingQuality%2A> 属性的语句会导致第三条线的混合与 gamma 矫正一起完成。  
  
 下图显示以下代码的输出。  
  
 ![不透明和半透明](../../../../docs/framework/winforms/advanced/media/compqualline.png "compqualline")  
  
 [!code-csharp[System.Drawing.AlphaBlending#11](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Drawing.AlphaBlending/CS/Class1.cs#11)]
 [!code-vb[System.Drawing.AlphaBlending#11](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Drawing.AlphaBlending/VB/Class1.vb#11)]  
  
## 编译代码  
 前面的示例专用于 Windows 窗体，它需要 <xref:System.Windows.Forms.PaintEventArgs> `e`，后者是 <xref:System.Windows.Forms.Control.Paint> 事件处理程序的参数。  
  
## 请参阅  
 [Alpha 混合线条和填充](../../../../docs/framework/winforms/advanced/alpha-blending-lines-and-fills.md)   
 [如何：使控件拥有透明背景](../../../../docs/framework/winforms/controls/how-to-give-your-control-a-transparent-background.md)   
 [如何：用不透明和半透明的画笔绘制](../../../../docs/framework/winforms/advanced/how-to-draw-with-opaque-and-semitransparent-brushes.md)