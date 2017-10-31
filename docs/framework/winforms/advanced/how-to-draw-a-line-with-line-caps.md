---
title: "如何：绘制具有线帽的线条 | Microsoft Docs"
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
  - "绘制线条, 线帽"
  - "绘图, 文本行"
  - "文本行, 绘图"
  - "钢笔, 绘制线条"
ms.assetid: eb68c3e1-c400-4886-8a04-76978a429cb6
caps.latest.revision: 16
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 16
---
# 如何：绘制具有线帽的线条
可用形状多样的线帽来绘制线条的起点或终点。  [!INCLUDE[ndptecgdiplus](../../../../includes/ndptecgdiplus-md.md)] 支持多种线帽，如圆形、方形、菱形和箭头。  
  
## 示例  
 您可为线条的起点、线条的终点或虚线的短划线指定线帽，分别称为起始线帽、终止线帽和短划线线帽。  
  
 下面的示例绘制一端为箭头线帽、另一端为圆形线帽的线条。  下面的插图显示产生的线条：  
  
 ![钢笔](../../../../docs/framework/winforms/advanced/media/pens4.png "pens4")  
  
 [!code-csharp[System.Drawing.UsingAPen#71](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Drawing.UsingAPen/CS/Class1.cs#71)]
 [!code-vb[System.Drawing.UsingAPen#71](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Drawing.UsingAPen/VB/Class1.vb#71)]  
  
## 编译代码  
  
-   创建一个 Windows 窗体并处理窗体的 <xref:System.Windows.Forms.Control.Paint> 事件。  将代码示例粘贴到 <xref:System.Windows.Forms.Control.Paint> 事件处理程序中，并传递 `e` 作为 <xref:System.Windows.Forms.PaintEventArgs>。  
  
## 请参阅  
 <xref:System.Drawing.Pen?displayProperty=fullName>   
 <xref:System.Drawing.Drawing2D.LineCap?displayProperty=fullName>   
 [Windows 窗体中的图形和绘制](../../../../docs/framework/winforms/advanced/graphics-and-drawing-in-windows-forms.md)   
 [使用钢笔绘制线条和形状](../../../../docs/framework/winforms/advanced/using-a-pen-to-draw-lines-and-shapes.md)