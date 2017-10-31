---
title: "GDI+ 中的区域 | Microsoft Docs"
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
  - "绘图, 区域"
  - "GDI+, 区域"
  - "区域"
ms.assetid: 52184f9b-16dd-4bbd-85be-029112644ceb
caps.latest.revision: 15
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 15
---
# GDI+ 中的区域
区域是输出设备显示区域的一部分。  区域可以是简单的（单个矩形）或复杂的（多边形和闭合曲线的组合）。  下面的插图显示了两个区域：一个利用矩形构造，另一个利用路径构造。  
  
 ![区域](../../../../docs/framework/winforms/advanced/media/aboutgdip02-art27.png "AboutGdip02\_Art27")  
  
## 使用区域  
 区域常用于剪辑和命中检测。  剪辑需要将绘制限制到显示区域的一个特定区域，通常是需要更新的部分。  命中检测需要通过检查来确定按下鼠标按钮时光标是否在屏幕的特定区域中。  
  
 您可以从矩形或路径中构造区域。  您也可以通过合并现有的区域来创建复杂区域。  <xref:System.Drawing.Region> 类提供以下区域合并方法：<xref:System.Drawing.Region.Intersect%2A>、<xref:System.Drawing.Region.Union%2A>、<xref:System.Drawing.Region.Xor%2A>、<xref:System.Drawing.Region.Exclude%2A> 和 <xref:System.Drawing.Region.Complement%2A>。  
  
 两个区域的交集是同时属于两个区域的所有点的集合。  并集是属于一个或另一个或两个区域的所有点的集合。  区域的补集是不在该区域的所有点的集合。  下面的插图显示了前面插图中两个区域的交集和并集。  
  
 ![区域](../../../../docs/framework/winforms/advanced/media/aboutgdip02-art28.gif "AboutGdip02\_Art28")  
  
 适用于一对区域的 <xref:System.Drawing.Region.Xor%2A> 方法可生成一个区域，其中包含属于一个区域或另一个区域但不同时属于两个区域的所有点。  适用于一对区域的 <xref:System.Drawing.Region.Exclude%2A> 方法可生成一个区域，其中包含属于第一个区域而不属于第二个区域的所有点。  下面的插图显示了通过将 <xref:System.Drawing.Region.Xor%2A> 和 <xref:System.Drawing.Region.Exclude%2A> 方法应用于本主题开始处的两个区域而产生的区域。  
  
 ![区域](../../../../docs/framework/winforms/advanced/media/aboutgdip02-art29.png "AboutGdip02\_Art29")  
  
 若要填充区域，需要有 <xref:System.Drawing.Graphics> 对象、<xref:System.Drawing.Brush> 对象和 <xref:System.Drawing.Region> 对象。  <xref:System.Drawing.Graphics> 对象提供 <xref:System.Drawing.Graphics.FillRegion%2A> 方法，<xref:System.Drawing.Brush> 对象存储填充的特性，如颜色或图案。  下面的示例用纯色填充区域。  
  
 [!code-csharp[LinesCurvesAndShapes#61](../../../../samples/snippets/csharp/VS_Snippets_Winforms/LinesCurvesAndShapes/CS/Class1.cs#61)]
 [!code-vb[LinesCurvesAndShapes#61](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/LinesCurvesAndShapes/VB/Class1.vb#61)]  
  
## 请参阅  
 <xref:System.Drawing.Region?displayProperty=fullName>   
 [直线、曲线和图形](../../../../docs/framework/winforms/advanced/lines-curves-and-shapes.md)   
 [使用区域](../../../../docs/framework/winforms/advanced/using-regions.md)