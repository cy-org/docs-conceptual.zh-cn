---
title: "如何：手动管理缓冲图形 | Microsoft Docs"
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
  - "BufferedGraphicsContext 类"
  - "闪烁, 通过手动管理图形来减少"
  - "图形, 管理缓冲的"
ms.assetid: 4c2a90ee-bbbe-4ff6-9170-1b06c195c918
caps.latest.revision: 8
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 8
---
# 如何：手动管理缓冲图形
对于更高级的双缓存情形，可以使用 [!INCLUDE[dnprdnshort](../../../../includes/dnprdnshort-md.md)] 类实现自己的双缓存逻辑。  负责单独分配和管理图形缓冲区的类是 <xref:System.Drawing.BufferedGraphicsContext> 类。  每个应用程序都有自己的默认 <xref:System.Drawing.BufferedGraphicsContext> 来管理此应用程序的所有默认双缓冲。  提供调用 <xref:System.Drawing.BufferedGraphicsManager.Current%2A> 可以检索对此实例的引用。  
  
### 获得对默认 BufferedGraphicsContext 的引用  
  
-   设置 <xref:System.Drawing.BufferedGraphicsManager.Current%2A> 属性，如下面的代码示例所示。  
  
     [!code-csharp[System.Windows.Forms.LegacyBufferedGraphics#11](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.LegacyBufferedGraphics/CS/Class1.cs#11)]
     [!code-vb[System.Windows.Forms.LegacyBufferedGraphics#11](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.LegacyBufferedGraphics/VB/Class1.vb#11)]  
  
    > [!NOTE]
    >  对于从 <xref:System.Drawing.BufferedGraphicsManager> 类获得的 <xref:System.Drawing.BufferedGraphicsContext> 引用，不需要调用 `Dispose` 方法。  <xref:System.Drawing.BufferedGraphicsManager> 负责处理默认 <xref:System.Drawing.BufferedGraphicsContext> 实例的所有内存分配和分发。  
  
     对于图形密集型应用程序（如动画），有时可通过使用专用的 <xref:System.Drawing.BufferedGraphicsContext>（而不是 <xref:System.Drawing.BufferedGraphicsManager> 提供的 <xref:System.Drawing.BufferedGraphicsContext>）来提高性能。  这样，您可以单独创建并管理图形缓冲区，尽管该应用程序会占用更多内存，但可以避免因管理其他所有与应用程序关联的缓冲图形而导致的性能开销。  
  
### 创建专用的 BufferedGraphicsContext  
  
-   声明并创建 <xref:System.Drawing.BufferedGraphicsContext> 类的新实例，如下面的代码示例所示。  
  
     [!code-csharp[System.Windows.Forms.LegacyBufferedGraphics#12](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.LegacyBufferedGraphics/CS/Class1.cs#12)]
     [!code-vb[System.Windows.Forms.LegacyBufferedGraphics#12](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.LegacyBufferedGraphics/VB/Class1.vb#12)]  
  
## 请参阅  
 <xref:System.Drawing.BufferedGraphicsContext>   
 [双缓冲图形](../../../../docs/framework/winforms/advanced/double-buffered-graphics.md)   
 [如何：手动呈现缓冲图形](../../../../docs/framework/winforms/advanced/how-to-manually-render-buffered-graphics.md)