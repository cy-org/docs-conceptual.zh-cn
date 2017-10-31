---
title: "双缓冲图形 | Microsoft Docs"
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
  - "双缓冲"
  - "示例 [Windows 窗体], 双缓冲的图形"
  - "闪烁, 使用双缓冲来减少"
  - "图形, 双缓冲的"
ms.assetid: 4f6fef99-0972-436e-9d73-0167e4033f71
caps.latest.revision: 11
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 9
---
# 双缓冲图形
闪烁是图形编程的一个常见问题。  需要多重复杂绘制操作的图形操作会导致呈现的图像闪烁或具有其他不可接受的外观。  为解决这些问题，.NET Framework 提供了对双缓冲的使用。  
  
 双缓冲使用内存缓冲区来解决由多重绘制操作造成的闪烁问题。  当启用双缓冲时，所有绘制操作首先呈现到内存缓冲区，而不是屏幕上的绘图图面。  所有绘制操作完成后，内存缓冲区直接复制到与其关联的绘图图面。  因为在屏幕上只执行一个图形操作，所以消除了由复杂绘制操作造成的图像闪烁。  
  
## 默认双缓冲  
 在应用程序中使用双缓冲的最简便的方法是使用 .NET Framework 为窗体和控件提供的默认双缓冲。  通过将 <xref:System.Windows.Forms.Control.DoubleBuffered%2A> 属性设置为 `true` 或使用 <xref:System.Windows.Forms.Control.SetStyle%2A> 方法可以为 Windows 窗体和所创作的 Windows 控件启用默认双缓冲。  有关更多信息，请参见 [如何：通过对窗体和控件使用双缓冲来减少图形闪烁](../../../../docs/framework/winforms/advanced/how-to-reduce-graphics-flicker-with-double-buffering-for-forms-and-controls.md)。  
  
## 手动管理缓冲的图形  
 对于更多的高级双缓冲情形（如动画或高级内存管理），可以使用 .NET Framework 中的类实现自己的双缓冲逻辑。  负责单独分配和管理图形缓冲区的类是 <xref:System.Drawing.BufferedGraphicsContext> 类。  每个应用程序域都有自己的默认 <xref:System.Drawing.BufferedGraphicsContext> 实例来管理此应用程序的所有默认双缓冲。  大多数情况下，每个应用程序只有一个应用程序域，所以每个应用程序通常只有一个默认 <xref:System.Drawing.BufferedGraphicsContext>。  默认 <xref:System.Drawing.BufferedGraphicsContext> 实例由 <xref:System.Drawing.BufferedGraphicsManager> 类管理。  通过调用 [BufferedGraphicsManager.Current 属性](frlrfSystemDrawingBufferedGraphicsManagerClassCurrentTopic)可以检索对默认 <xref:System.Drawing.BufferedGraphicsContext> 实例的引用。  还可以创建一个专用的 <xref:System.Drawing.BufferedGraphicsContext> 实例以提高图形密集型应用程序的性能。  有关如何创建 <xref:System.Drawing.BufferedGraphicsContext> 实例的信息，请参见 [如何：手动管理缓冲图形](../../../../docs/framework/winforms/advanced/how-to-manually-manage-buffered-graphics.md)。  
  
## 手动显示缓冲的图形  
 通过调用 [BufferedGraphicsContext.Allocate 方法](frlrfSystemDrawingBufferedGraphicsContextClassAllocateTopic)（该方法返回 <xref:System.Drawing.BufferedGraphics> 类的实例），可以使用 <xref:System.Drawing.BufferedGraphicsContext> 类的实例创建图形缓冲区。  <xref:System.Drawing.BufferedGraphics> 对象管理与呈现图面（如窗体或控件）关联的内存缓冲区。  
  
 <xref:System.Drawing.BufferedGraphics> 类在实例化后将图形呈现到内存的图形缓冲区中。  通过 [BufferedGraphics.Graphics 属性](frlrfSystemDrawingBufferedGraphicsClassGraphicsTopic)可以在内存缓冲区中呈现图形，该属性公开了一个直接表示内存缓冲区的 <xref:System.Drawing.Graphics> 对象。  可以绘制到此 <xref:System.Drawing.Graphics> 对象，这与绘制到表示绘图图面的 <xref:System.Drawing.Graphics> 对象一样。  所有图形绘制到缓冲区后，可以使用 [BufferedGraphics.Render 方法](frlrfSystemDrawingBufferedGraphicsClassRenderTopic)将缓冲区的内容复制到屏幕上的绘图图面。  
  
 有关使用 <xref:System.Drawing.BufferedGraphics> 类的更多信息，请参见[手动呈现缓冲的图形](../../../../docs/framework/winforms/advanced/how-to-manually-render-buffered-graphics.md)。  有关呈现图形的更多信息，请参见 [Windows 窗体中的图形和绘制](../../../../docs/framework/winforms/advanced/graphics-and-drawing-in-windows-forms.md)  
  
## 请参阅  
 <xref:System.Drawing.BufferedGraphics>   
 <xref:System.Drawing.BufferedGraphicsContext>   
 <xref:System.Drawing.BufferedGraphicsManager>   
 [如何：手动呈现缓冲图形](../../../../docs/framework/winforms/advanced/how-to-manually-render-buffered-graphics.md)   
 [如何：通过对窗体和控件使用双缓冲来减少图形闪烁](../../../../docs/framework/winforms/advanced/how-to-reduce-graphics-flicker-with-double-buffering-for-forms-and-controls.md)   
 [如何：手动管理缓冲图形](../../../../docs/framework/winforms/advanced/how-to-manually-manage-buffered-graphics.md)   
 [Windows 窗体中的图形和绘制](../../../../docs/framework/winforms/advanced/graphics-and-drawing-in-windows-forms.md)