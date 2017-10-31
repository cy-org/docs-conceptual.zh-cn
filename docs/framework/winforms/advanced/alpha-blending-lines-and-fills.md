---
title: "Alpha 混合线条和填充 | Microsoft Docs"
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
  - "alpha 混合"
  - "alpha 混合, 使用填充"
  - "alpha 混合, 使用线条"
  - "示例 [Windows 窗体], alpha 混合"
  - "填充, alpha 混合"
  - "文本行, 添加透明度"
  - "文本行, alpha 混合"
  - "形状, 添加透明度"
ms.assetid: 5440f48c-3ac9-44c3-b170-c1c110bdbab8
caps.latest.revision: 13
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 13
---
# Alpha 混合线条和填充
在 [!INCLUDE[ndptecgdiplus](../../../../includes/ndptecgdiplus-md.md)] 中，颜色为 32 位值：alpha、红色、绿色和蓝色各 8 位。  alpha 值指示颜色的透明度，即颜色与背景色的混合程度。  Alpha 值的范围是 0 到 255，其中 0 表示完全透明的颜色，255 表示完全不透明的颜色。  
  
 Alpha 混合是源颜色数据和背景颜色数据之间逐个像素的混合。  给定源颜色的三个分量（红色、绿色和蓝色）都按照以下公式与背景颜色的相应分量混合：  
  
 显示颜色 \= 源颜色 × alpha \/ 255 \+ 背景颜色 × \(255 \- alpha\) \/ 255  
  
 例如，假设源颜色的红色分量是 150，背景颜色的红色分量是 100。  如果 alpha 值是 200，则结果颜色的红色分量按以下公式计算：  
  
 150 × 200 \/ 255 \+ 100 × \(255 – 200\) \/ 255 \= 139  
  
## 本节内容  
 [如何：绘制不透明和半透明的线条](../../../../docs/framework/winforms/advanced/how-to-draw-opaque-and-semitransparent-lines.md)  
 演示如何绘制 alpha 混合线条。  
  
 [如何：用不透明和半透明的画笔绘制](../../../../docs/framework/winforms/advanced/how-to-draw-with-opaque-and-semitransparent-brushes.md)  
 解释如何使用画笔进行 alpha 混合。  
  
 [如何：使用复合模式控制 Alpha 混合](../../../../docs/framework/winforms/advanced/how-to-use-compositing-mode-to-control-alpha-blending.md)  
 描述如何使用 <xref:System.Drawing.Drawing2D.CompositingMode> 控制 alpha 混合。  
  
 [如何：使用颜色矩阵设置图像中的 Alpha 值](../../../../docs/framework/winforms/advanced/how-to-use-a-color-matrix-to-set-alpha-values-in-images.md)  
 解释如何使用 <xref:System.Drawing.Imaging.ColorMatrix> 对象控制 alpha 混合。