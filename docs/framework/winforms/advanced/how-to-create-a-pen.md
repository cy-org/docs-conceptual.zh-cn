---
title: "如何：创建钢笔 | Microsoft Docs"
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
  - "图形, 创建画笔"
  - "Pen 对象"
  - "钢笔, 创建"
ms.assetid: 7fbea8b7-7ac1-4413-9c17-733a850381e3
caps.latest.revision: 12
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 12
---
# 如何：创建钢笔
此示例创建一个 <xref:System.Drawing.Pen> 对象。  
  
## 示例  
 [!code-cpp[System.Drawing.ConceptualHowTos#3](../../../../samples/snippets/cpp/VS_Snippets_Winforms/System.Drawing.ConceptualHowTos/cpp/form1.cpp#3)]
 [!code-csharp[System.Drawing.ConceptualHowTos#3](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Drawing.ConceptualHowTos/CS/form1.cs#3)]
 [!code-vb[System.Drawing.ConceptualHowTos#3](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Drawing.ConceptualHowTos/VB/form1.vb#3)]  
  
## 可靠编程  
 当使用完需要消耗系统资源的对象（如 <xref:System.Drawing.Pen> 对象）后，应对其调用 <xref:System.Drawing.Pen.Dispose%2A>。  
  
## 请参阅  
 <xref:System.Drawing.Pen>   
 [图形编程入门](../../../../docs/framework/winforms/advanced/getting-started-with-graphics-programming.md)   
 [GDI\+ 中的笔、直线和矩形](../../../../docs/framework/winforms/advanced/pens-lines-and-rectangles-in-gdi.md)