---
title: "如何：对区域使用剪辑 | Microsoft Docs"
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
  - "区域, 剪辑"
  - "区域, 限制绘图图画"
ms.assetid: 43d121b4-e14c-4901-b25c-2d6c25ba4e29
caps.latest.revision: 14
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 14
---
# 如何：对区域使用剪辑
<xref:System.Drawing.Graphics> 类的一个属性是剪辑区域。  所有由给定的 <xref:System.Drawing.Graphics> 对象进行的绘制都限制在 <xref:System.Drawing.Graphics> 对象的剪辑区域中。  可通过调用 <xref:System.Drawing.Graphics.SetClip%2A> 方法设置剪辑区域。  
  
## 示例  
 下面的示例构造由一个多边形组成的路径。  然后，该代码根据该路径构造一个区域。  将该区域传递给 <xref:System.Drawing.Graphics> 对象的 <xref:System.Drawing.Graphics.SetClip%2A> 方法，然后绘制两个字符串。  
  
 下面的插图显示这个经剪辑的字符串。  
  
 ![剪辑](../../../../docs/framework/winforms/advanced/media/clip1.png "clip1")  
  
 [!code-csharp[System.Drawing.MiscLegacyTopics#41](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Drawing.MiscLegacyTopics/CS/Class1.cs#41)]
 [!code-vb[System.Drawing.MiscLegacyTopics#41](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Drawing.MiscLegacyTopics/VB/Class1.vb#41)]  
  
## 编译代码  
 前面的示例是为使用 Windows 窗体而设计的，它需要 <xref:System.Windows.Forms.PaintEventHandler> 的参数 <xref:System.Windows.Forms.PaintEventArgs> `e`。  
  
## 请参阅  
 [GDI\+ 中的区域](../../../../docs/framework/winforms/advanced/regions-in-gdi.md)   
 [使用区域](../../../../docs/framework/winforms/advanced/using-regions.md)