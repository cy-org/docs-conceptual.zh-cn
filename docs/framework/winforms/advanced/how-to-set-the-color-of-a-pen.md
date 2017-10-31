---
title: "如何：设置钢笔颜色 | Microsoft Docs"
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
  - "彩色钢笔"
  - "钢笔, 设置颜色"
ms.assetid: a9df06f9-a6d5-4d9b-a2d1-583943540775
caps.latest.revision: 13
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 13
---
# 如何：设置钢笔颜色
此示例更改预先存在的 <xref:System.Drawing.Pen> 对象的颜色。  
  
## 示例  
 [!code-cpp[System.Drawing.ConceptualHowTos#9](../../../../samples/snippets/cpp/VS_Snippets_Winforms/System.Drawing.ConceptualHowTos/cpp/form1.cpp#9)]
 [!code-csharp[System.Drawing.ConceptualHowTos#9](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Drawing.ConceptualHowTos/CS/form1.cs#9)]
 [!code-vb[System.Drawing.ConceptualHowTos#9](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Drawing.ConceptualHowTos/VB/form1.vb#9)]  
  
## 编译代码  
 此示例需要：  
  
-   名为 `myPen` 的 <xref:System.Drawing.Pen> 对象。  
  
## 可靠编程  
 应在使用完需要消耗系统资源的对象（例如 <xref:System.Drawing.Pen> 对象）后，对其调用 <xref:System.Drawing.Pen.Dispose%2A>。  
  
## 请参阅  
 <xref:System.Drawing.Pen>   
 [图形编程入门](../../../../docs/framework/winforms/advanced/getting-started-with-graphics-programming.md)   
 [如何：创建钢笔](../../../../docs/framework/winforms/advanced/how-to-create-a-pen.md)   
 [使用钢笔绘制线条和形状](../../../../docs/framework/winforms/advanced/using-a-pen-to-draw-lines-and-shapes.md)   
 [GDI\+ 中的笔、直线和矩形](../../../../docs/framework/winforms/advanced/pens-lines-and-rectangles-in-gdi.md)