---
title: "如何：清除自定义控件上的墨迹 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-wpf"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "自定义控件, 清除墨迹"
  - "墨迹, 在自定义控件上清除"
ms.assetid: d88c50f9-b4d8-4962-a28b-67d6a15a5fe0
caps.latest.revision: 4
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 4
---
# 如何：清除自定义控件上的墨迹
<xref:System.Windows.Ink.IncrementalStrokeHitTester> 决定了当前绘制的笔画是否与另一笔画相交。  这对于创建能够使用户清除部分笔画的控件非常有用，将 <xref:System.Windows.Controls.InkCanvas.EditingMode%2A> 设置为 <xref:System.Windows.Controls.InkCanvasEditingMode> 后，用户可以在 <xref:System.Windows.Controls.InkCanvas> 上使用这种方法。  
  
## 示例  
 下面的示例创建了一个使用户能够清除部分笔画的自定义控件。  此示例创建了一个在初始化后包含墨迹的控件。  若要创建收集墨迹的控件，请参见[创建墨迹输入控件](../../../../docs/framework/wpf/advanced/creating-an-ink-input-control.md)。  
  
 [!code-csharp[HowToEraseInk#1](../../../../samples/snippets/csharp/VS_Snippets_Wpf/HowToEraseInk/CSharp/InkEraser.cs#1)]
 [!code-vb[HowToEraseInk#1](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/HowToEraseInk/VisualBasic/InkEraser.vb#1)]