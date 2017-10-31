---
title: "如何：将曲线路径展平为直线 | Microsoft Docs"
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
  - "曲线, 修整"
  - "绘图, 让曲线变平"
  - "Flatten 方法"
  - "图形, 修整曲线为直线"
  - "GraphicsPath 对象"
  - "路径, 修整"
ms.assetid: e654b8de-25f4-4735-9208-42e4514a589c
caps.latest.revision: 14
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 14
---
# 如何：将曲线路径展平为直线
<xref:System.Drawing.Drawing2D.GraphicsPath> 对象存储一系列直线和贝塞尔样条。  可以将多种类型的曲线（椭圆、弧形和基数样条）添加到路径，但在存储到路径之前，各种曲线都被转换为贝塞尔样条。  拉平路径的操作包含将路径中的每个贝塞尔样条转化为一系列直线。  下面的插图显示了路径（拉平之前和拉平之后）。  
  
 ![直线和曲线](../../../../docs/framework/winforms/advanced/media/aboutgdip02-art32a.png "AboutGdip02\_Art32A")  
  
### 拉平路径  
  
-   调用 <xref:System.Drawing.Drawing2D.GraphicsPath> 对象的 <xref:System.Drawing.Drawing2D.GraphicsPath.Flatten%2A> 方法。  <xref:System.Drawing.Drawing2D.GraphicsPath.Flatten%2A> 方法接收拉平参数，该参数指定拉平的路径和原始路径之间的最大距离。  
  
## 请参阅  
 <xref:System.Drawing.Drawing2D.GraphicsPath?displayProperty=fullName>   
 [直线、曲线和图形](../../../../docs/framework/winforms/advanced/lines-curves-and-shapes.md)   
 [构造并绘制轨迹](../../../../docs/framework/winforms/advanced/constructing-and-drawing-paths.md)