---
title: "如何：手动呈现缓冲图形 | Microsoft Docs"
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
  - "BufferedGraphics 类"
  - "闪烁, 通过手动呈现图形来减少"
  - "图形 [Windows 窗体], 呈现"
ms.assetid: 5192295e-bd8e-45f7-8bd6-5c4f6bd21e61
caps.latest.revision: 10
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 10
---
# 如何：手动呈现缓冲图形
如果你正在管理自己的缓冲图形，你将需要能创建和程序图形缓冲区。  你可以通过调用 <xref:System.Drawing.BufferedGraphicsContext.Allocate%2A> 方法，在屏幕上创建与绘图图面相关联的 <xref:System.Drawing.BufferedGraphics> 类的实例。  此方法会创建一个与特定呈现图面（如表格或控件）关联的 <xref:System.Drawing.BufferedGraphics> 实例。  在创建 <xref:System.Drawing.BufferedGraphics> 实例后，可以通过 <xref:System.Drawing.BufferedGraphics.Graphics%2A> 属性，将图形绘制到它表示的缓冲区内。  执行所有图形操作之后，可以通过调用 <xref:System.Drawing.BufferedGraphics.Render%2A> 方法将缓冲区的内容复制到屏幕。  
  
> [!NOTE]
>  如果执行自己的呈现，内存消耗将会增加，但可能只是略微增加。  
  
### 手动显示缓冲图形  
  
1.  获取对 <xref:System.Drawing.BufferedGraphicsContext> 类的实例的引用。  有关详细信息，请参阅 [如何：手动管理缓冲图形](../../../../docs/framework/winforms/advanced/how-to-manually-manage-buffered-graphics.md)。  
  
2.  如下列代码示例所示，通过调用 <xref:System.Drawing.BufferedGraphicsContext.Allocate%2A> 方法，创建 <xref:System.Drawing.BufferedGraphics> 类的实例。  
  
     [!code-csharp[System.Windows.Forms.LegacyBufferedGraphics#21](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.LegacyBufferedGraphics/CS/Class1.cs#21)]
     [!code-vb[System.Windows.Forms.LegacyBufferedGraphics#21](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.LegacyBufferedGraphics/VB/Class1.vb#21)]  
  
3.  通过设置 <xref:System.Drawing.BufferedGraphics.Graphics%2A> 属性将图形绘制到图形缓冲区内。  例如：  
  
     [!code-csharp[System.Windows.Forms.LegacyBufferedGraphics#22](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.LegacyBufferedGraphics/CS/Class1.cs#22)]
     [!code-vb[System.Windows.Forms.LegacyBufferedGraphics#22](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.LegacyBufferedGraphics/VB/Class1.vb#22)]  
  
4.  当你已完成所有对图形缓冲区的绘制操作时，调用 <xref:System.Drawing.BufferedGraphics.Render%2A> 方法将缓冲区呈现到与该缓冲区关联的绘图图面或指定的绘图图面，如下列代码示例所示。  
  
     [!code-csharp[System.Windows.Forms.LegacyBufferedGraphics#23](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.LegacyBufferedGraphics/CS/Class1.cs#23)]
     [!code-vb[System.Windows.Forms.LegacyBufferedGraphics#23](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.LegacyBufferedGraphics/VB/Class1.vb#23)]  
  
5.  在完成图形呈现后，调用 <xref:System.Drawing.BufferedGraphics> 实例上的 `Dispose` 方法释放系统资源。  
  
     [!code-csharp[System.Windows.Forms.LegacyBufferedGraphics#24](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.LegacyBufferedGraphics/CS/Class1.cs#24)]
     [!code-vb[System.Windows.Forms.LegacyBufferedGraphics#24](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.LegacyBufferedGraphics/VB/Class1.vb#24)]  
  
## 请参阅  
 <xref:System.Drawing.BufferedGraphicsContext>   
 <xref:System.Drawing.BufferedGraphics>   
 [双缓冲图形](../../../../docs/framework/winforms/advanced/double-buffered-graphics.md)   
 [如何：手动管理缓冲图形](../../../../docs/framework/winforms/advanced/how-to-manually-manage-buffered-graphics.md)