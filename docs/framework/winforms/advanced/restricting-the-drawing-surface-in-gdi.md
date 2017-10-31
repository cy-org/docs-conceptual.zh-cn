---
title: "在 GDI+ 中限制绘制图面 | Microsoft Docs"
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
  - "剪辑, 使用 GDI+"
  - "GDI+, 剪辑"
  - "GDI+, 限制绘图图画"
ms.assetid: 8b5f71d9-d2f0-4540-9c41-740f90fd4c26
caps.latest.revision: 14
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 14
---
# 在 GDI+ 中限制绘制图面
剪辑需要把绘制限制到一个特定的矩形或区域。  下面的插图显示了剪辑到心形区域的字符串“Hello”。  
  
 ![受限绘制图面](../../../../docs/framework/winforms/advanced/media/aboutgdip02-art30.png "AboutGdip02\_Art30")  
  
## 使用区域进行剪辑  
 区域可从路径构造，路径可包含字符串的轮廓，因此您可以剪辑空心效果的文字。  下面的插图显示了剪辑到文本字符串内部的一组同心椭圆。  
  
 ![受限绘制图面](../../../../docs/framework/winforms/advanced/media/aboutgdip02-art31.png "AboutGdip02\_Art31")  
  
 若要利用剪辑进行绘制，请创建 <xref:System.Drawing.Graphics> 对象，设置其 <xref:System.Drawing.Graphics.Clip%2A> 属性，然后调用同一 <xref:System.Drawing.Graphics> 对象的绘制方法：  
  
 [!code-csharp[LinesCurvesAndShapes#91](../../../../samples/snippets/csharp/VS_Snippets_Winforms/LinesCurvesAndShapes/CS/Class1.cs#91)]
 [!code-vb[LinesCurvesAndShapes#91](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/LinesCurvesAndShapes/VB/Class1.vb#91)]  
  
## 请参阅  
 <xref:System.Drawing.Graphics?displayProperty=fullName>   
 <xref:System.Drawing.Region?displayProperty=fullName>   
 [直线、曲线和图形](../../../../docs/framework/winforms/advanced/lines-curves-and-shapes.md)   
 [使用区域](../../../../docs/framework/winforms/advanced/using-regions.md)