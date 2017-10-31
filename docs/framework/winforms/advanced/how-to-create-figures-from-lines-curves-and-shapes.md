---
title: "如何：使用线条、曲线和形状创建图形 | Microsoft Docs"
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
  - "图形, 用线条创建"
  - "图形, 用形状创建"
ms.assetid: 82fd56c7-b443-4765-9b7c-62ce030656ec
caps.latest.revision: 14
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 14
---
# 如何：使用线条、曲线和形状创建图形
若要创建图形，请构造 <xref:System.Drawing.Drawing2D.GraphicsPath>，然后调用诸如 <xref:System.Drawing.Drawing2D.GraphicsPath.AddLine%2A> 和 <xref:System.Drawing.Drawing2D.GraphicsPath.AddCurve%2A> 的方法，向路径中添加基元。  
  
## 示例  
 下面的代码示例创建具有图形的路径：  
  
-   第一个示例创建具有单一图形的路径。  该图形由一段弧组成。  该弧的扫描角为 \-180 度，此角度在默认的坐标系中是按逆时针方向旋转的。  
  
-   第二个示例创建具有两个图形的路径。  第一个图形是一段弧，后跟一条直线。  第二个图形是一条直线，后跟一条曲线，再后面又是一条直线。  第一个图形的左边是敞开的；第二个图形是闭合的。  
  
 [!code-csharp[System.Drawing.ConstructingDrawingPaths#21](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Drawing.ConstructingDrawingPaths/CS/Class1.cs#21)]
 [!code-vb[System.Drawing.ConstructingDrawingPaths#21](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Drawing.ConstructingDrawingPaths/VB/Class1.vb#21)]  
  
 [!code-csharp[System.Drawing.ConstructingDrawingPaths#22](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Drawing.ConstructingDrawingPaths/CS/Class1.cs#22)]
 [!code-vb[System.Drawing.ConstructingDrawingPaths#22](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Drawing.ConstructingDrawingPaths/VB/Class1.vb#22)]  
  
## 编译代码  
 前面的示例是为使用 Windows 窗体而设计的，它们需要 <xref:System.Windows.Forms.Control.Paint> 事件处理程序的参数 <xref:System.Windows.Forms.PaintEventArgs> `e`。  
  
## 请参阅  
 <xref:System.Drawing.Drawing2D.GraphicsPath>   
 [构造并绘制轨迹](../../../../docs/framework/winforms/advanced/constructing-and-drawing-paths.md)   
 [使用钢笔绘制线条和形状](../../../../docs/framework/winforms/advanced/using-a-pen-to-draw-lines-and-shapes.md)