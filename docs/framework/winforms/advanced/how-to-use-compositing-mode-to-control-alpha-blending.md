---
title: "如何：使用复合模式控制 Alpha 混合 | Microsoft Docs"
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
  - "alpha 混合, 复合"
  - "颜色, 混合"
  - "颜色, 控制透明度"
ms.assetid: f331df2d-b395-4b0a-95be-24fec8c9bbb5
caps.latest.revision: 14
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 14
---
# 如何：使用复合模式控制 Alpha 混合
有时可能希望创建具有以下特征的离屏位图：  
  
-   颜色的 alpha 值小于 255。  
  
-   在创建位图时颜色之间不进行 alpha 混合。  
  
-   在显示完成的位图时，在显示设备上，位图中的颜色与背景色进行 alpha 混合。  
  
 若要创建这样的位图，请构造一个空白的 <xref:System.Drawing.Bitmap> 对象，然后基于该位图构造 <xref:System.Drawing.Graphics> 对象。  将 <xref:System.Drawing.Graphics> 对象的复合模式设置为 <xref:System.Drawing.Drawing2D.CompositingMode?displayProperty=fullName>。  
  
## 示例  
 下面的示例创建一个基于 <xref:System.Drawing.Bitmap> 对象的 <xref:System.Drawing.Graphics> 对象。  该代码使用 <xref:System.Drawing.Graphics> 对象和两个半透明画笔 \(alpha \= 160\) 在该位图上绘画。  该代码使用半透明画笔填充红色椭圆和绿色椭圆。  绿色椭圆与红色椭圆重叠，但是绿色并不与红色混合，这是因为 <xref:System.Drawing.Graphics> 对象的复合模式已设置为 <xref:System.Drawing.Drawing2D.CompositingMode>。  
  
 该代码在屏幕上绘制该位图两次：一次是在白色背景上，一次是在多色背景上。  位图中属于两个椭圆的像素的 alpha 分量的值是 160，因此这些椭圆与屏幕上的背景色相混合。  
  
 下面的插图显示代码示例的输出。  请注意，这些椭圆与背景相混合，但椭圆之间不进行混合。  
  
 ![源副本](../../../../docs/framework/winforms/advanced/media/sourcecopy.png "sourcecopy")  
  
 代码示例包含这条语句：  
  
 [!code-csharp[System.Drawing.AlphaBlending#41](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Drawing.AlphaBlending/CS/Class1.cs#41)]
 [!code-vb[System.Drawing.AlphaBlending#41](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Drawing.AlphaBlending/VB/Class1.vb#41)]  
  
 如果您希望这些椭圆除了与背景相混合外，椭圆之间也相互混合，请将上述语句更改为如下语句：  
  
 [!code-csharp[System.Drawing.AlphaBlending#42](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Drawing.AlphaBlending/CS/Class1.cs#42)]
 [!code-vb[System.Drawing.AlphaBlending#42](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Drawing.AlphaBlending/VB/Class1.vb#42)]  
  
 下面的插图显示修改后的代码的输出。  
  
 ![源覆盖](../../../../docs/framework/winforms/advanced/media/sourceover.png "sourceover")  
  
 [!code-csharp[System.Drawing.AlphaBlending#43](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Drawing.AlphaBlending/CS/Class1.cs#43)]
 [!code-vb[System.Drawing.AlphaBlending#43](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Drawing.AlphaBlending/VB/Class1.vb#43)]  
  
## 编译代码  
 前面的示例是为使用 Windows 窗体而设计的，它需要 <xref:System.Windows.Forms.PaintEventHandler> 的参数 <xref:System.Windows.Forms.PaintEventArgs> `e`。  
  
## 请参阅  
 <xref:System.Drawing.Color.FromArgb%2A>   
 [Alpha 混合线条和填充](../../../../docs/framework/winforms/advanced/alpha-blending-lines-and-fills.md)