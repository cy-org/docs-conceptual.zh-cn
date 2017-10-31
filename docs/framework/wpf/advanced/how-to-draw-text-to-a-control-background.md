---
title: "如何：将文本绘制到控件的背景上 | Microsoft Docs"
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
  - "背景, 将文本绘制到"
  - "控件, 将文本绘制到背景"
  - "绘图, 文本绘制到控件背景"
  - "文本, 绘制到控件背景"
  - "版式, 绘制文本到控件背景"
ms.assetid: 686d8fba-f61c-4974-a871-c635d67a7f69
caps.latest.revision: 10
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 7
---
# 如何：将文本绘制到控件的背景上
可以将文本直接绘制到控件的背景上，方法是将文本字符串转换为 <xref:System.Windows.Media.FormattedText> 对象，然后将该对象绘制到控件的 <xref:System.Windows.Media.DrawingContext> 中。  还可以使用这种方法来绘制到派生自 <xref:System.Windows.Controls.Panel> 的对象（如 <xref:System.Windows.Controls.Canvas> 和 <xref:System.Windows.Controls.StackPanel>）的背景上。  
  
 ![将文本作为背景显示的控件](../../../../docs/framework/wpf/advanced/media/drawtext2background01.png "DrawText2Background01")  
具有自定义文本背景的控件的示例  
  
## 示例  
 若要绘制到某个控件的背景上，请创建一个新的 <xref:System.Windows.Media.DrawingBrush> 对象，并将转换后的文本绘制到该对象的 <xref:System.Windows.Media.DrawingContext> 中。  然后，将新的 <xref:System.Windows.Media.DrawingBrush> 分配给该控件的背景属性。  
  
 下面的代码示例演示如何创建 <xref:System.Windows.Media.FormattedText> 对象，并将其绘制到 <xref:System.Windows.Controls.Label> 和 <xref:System.Windows.Controls.Button> 对象的背景上。  
  
 [!code-csharp[DrawTextToControlBackground#DrawTextToControlBackground1](../../../../samples/snippets/csharp/VS_Snippets_Wpf/DrawTextToControlBackground/CSHARP/Window1.xaml.cs#drawtexttocontrolbackground1)]  
  
## 请参阅  
 <xref:System.Windows.Media.FormattedText>   
 [绘制格式化文本](../../../../docs/framework/wpf/advanced/drawing-formatted-text.md)