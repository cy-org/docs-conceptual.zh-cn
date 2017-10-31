---
title: "如何：创建特定形状的 Windows 窗体 | Microsoft Docs"
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
  - "窗体, 更改形状"
  - "窗体, 环形"
  - "窗体, 自定义形状"
  - "窗体, 非矩形"
  - "窗体, 圆角"
  - "有形状的窗体"
  - "Windows 窗体, 环形"
  - "Windows 窗体, 自定义形状"
  - "Windows 窗体, 非矩形形状"
  - "Windows 窗体, 圆角"
  - "Windows 窗体, 特定形状的"
ms.assetid: 6e6041e0-8e67-4487-b1e9-e410dbd1ef6c
caps.latest.revision: 8
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 8
---
# 如何：创建特定形状的 Windows 窗体
此示例向窗体提供随该窗体一起调整大小的椭圆形状。  
  
## 示例  
 [!code-cpp[System.Drawing.ConceptualHowTos#10](../../../../samples/snippets/cpp/VS_Snippets_Winforms/System.Drawing.ConceptualHowTos/cpp/form1.cpp#10)]
 [!code-csharp[System.Drawing.ConceptualHowTos#10](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Drawing.ConceptualHowTos/CS/form1.cs#10)]
 [!code-vb[System.Drawing.ConceptualHowTos#10](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Drawing.ConceptualHowTos/VB/form1.vb#10)]  
  
## 编译代码  
 此示例需要：  
  
-   对 <xref:System.Windows.Forms> 和 <xref:System.Drawing> 命名空间的引用。  
  
 该示例重写 <xref:System.Windows.Forms.Control.OnPaint%2A> 方法以更改窗体的形状。  若要使用此代码，请将方法声明以及绘图代码复制到该方法中。  
  
## 请参阅  
 <xref:System.Windows.Forms.Control.OnPaint%2A>   
 <xref:System.Drawing.Region>   
 <xref:System.Drawing>   
 <xref:System.Drawing.Drawing2D.GraphicsPath.AddEllipse%2A>   
 <xref:System.Windows.Forms.Control.Region%2A>   
 [图形编程入门](../../../../docs/framework/winforms/advanced/getting-started-with-graphics-programming.md)