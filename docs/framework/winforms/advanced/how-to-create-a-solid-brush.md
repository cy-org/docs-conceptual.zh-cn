---
title: "如何：创建实心画笔 | Microsoft Docs"
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
  - "画笔, 创建实心"
  - "画笔, 示例"
  - "实心画笔"
ms.assetid: 85c3fe7d-fb1d-4591-8a9f-d75b556b90af
caps.latest.revision: 13
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 13
---
# 如何：创建实心画笔
此示例创建一个 <xref:System.Drawing.SolidBrush> 对象，<xref:System.Drawing.Graphics> 对象可以用它来填充形状。  
  
## 示例  
 [!code-cpp[System.Drawing.ConceptualHowTos#1](../../../../samples/snippets/cpp/VS_Snippets_Winforms/System.Drawing.ConceptualHowTos/cpp/form1.cpp#1)]
 [!code-csharp[System.Drawing.ConceptualHowTos#1](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Drawing.ConceptualHowTos/CS/form1.cs#1)]
 [!code-vb[System.Drawing.ConceptualHowTos#1](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Drawing.ConceptualHowTos/VB/form1.vb#1)]  
  
## 可靠编程  
 当使用完那些使用系统资源的对象（如 Brush 对象）后，应该对这些对象调用 <xref:System.IDisposable.Dispose%2A>。  
  
## 请参阅  
 <xref:System.Drawing.SolidBrush>   
 <xref:System.Drawing.Brush>   
 [图形编程入门](../../../../docs/framework/winforms/advanced/getting-started-with-graphics-programming.md)   
 [GDI\+ 中的画笔和实心形状](../../../../docs/framework/winforms/advanced/brushes-and-filled-shapes-in-gdi.md)   
 [使用画笔填充形状](../../../../docs/framework/winforms/advanced/using-a-brush-to-fill-shapes.md)