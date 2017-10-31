---
title: "如何：创建空心文字 | Microsoft Docs"
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
  - "渐变画笔"
  - "线性渐变画笔"
  - "空心文字"
  - "版式, 线性渐变画笔"
  - "版式, 空心效果"
ms.assetid: 4aa3cf6e-1953-4f26-8230-7c1409e5f28d
caps.latest.revision: 11
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 11
---
# 如何：创建空心文字
在大多数情况下，向 [!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)] 应用程序中的文本字符串添加装饰时，您可以使用离散字符或标志符号集合形式的文本。  例如，可创建线性渐变画笔，并将其应用于 <xref:System.Windows.Controls.TextBox> 对象的 <xref:System.Windows.Controls.Control.Foreground%2A> 属性。  当显示或编辑文本框时，线性渐变画笔将自动应用于文本字符串中的当前字符集。  
  
 ![使用线性渐变画笔显示的文本](../../../../docs/framework/wpf/advanced/media/outlinedtext01.png "OutlinedText01")  
应用于文本框的线性渐变画笔的示例  
  
 但是，您还可以将文本转换为 <xref:System.Windows.Media.Geometry> 对象，这样便可以创建其他类型的可视化多格式文本。  例如，可以基于文本字符串的轮廓创建 <xref:System.Windows.Media.Geometry> 对象。  
  
 ![使用线性渐变画笔的文本轮廓](../../../../docs/framework/wpf/advanced/media/outlinedtext02.png "OutlinedText02")  
应用于文本轮廓几何图形的线性渐变画笔的示例  
  
 将文本转换为 <xref:System.Windows.Media.Geometry> 对象时，它不再是字符的集合 \- 您不能修改文本字符串中的字符。  但是，可以修改已转换文本的笔画和填充属性，以此来影响该文本的外观。  笔画指的是已转换文本的轮廓；填充指的是已转换文本的轮廓的内部区域。  
  
 下面的示例演示几种通过修改已转换文本的笔画和填充来创建视觉效果的方法。  
  
 ![对填充和笔画使用不同颜色的文本](../../../../docs/framework/wpf/advanced/media/outlinedtext03.png "OutlinedText03")  
将笔画和填充设置为不同颜色的示例  
  
 ![笔画应用了图像画笔的文本](../../../../docs/framework/wpf/advanced/media/outlinedtext04.png "OutlinedText04")  
应用于笔画的图像画笔的示例  
  
 还可以修改已转换文本的边界框矩形或高光点。  下面的示例演示一种通过修改已转换文本的笔画和高光点来创建视觉效果的方法。  
  
 ![笔画应用了图像画笔的文本](../../../../docs/framework/wpf/advanced/media/outlinedtext05.png "OutlinedText05")  
应用于笔画和高光点的图像画笔的示例  
  
## 示例  
 将文本转换为 <xref:System.Windows.Media.Geometry> 对象的关键是使用 <xref:System.Windows.Media.FormattedText> 对象。  一旦创建该对象之后，即可使用 <xref:System.Windows.Media.FormattedText.BuildGeometry%2A> 和 <xref:System.Windows.Media.FormattedText.BuildHighlightGeometry%2A> 方法将文本转换为 <xref:System.Windows.Media.Geometry> 对象。  第一个方法返回格式化文本的几何图形；第二个方法返回格式化文本的边界框的几何图形。  下面的代码示例演示如何创建 <xref:System.Windows.Media.FormattedText> 对象以及如何检索格式化文本及其边界框的几何图形。  
  
 [!code-csharp[OutlineTextControlViewer#CreateText](../../../../samples/snippets/csharp/VS_Snippets_Wpf/OutlineTextControlViewer/CSharp/OutlineTextControl.cs#createtext)]
 [!code-vb[OutlineTextControlViewer#CreateText](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/OutlineTextControlViewer/visualbasic/outlinetextcontrol.vb#createtext)]  
  
 要显示检索的 <xref:System.Windows.Media.Geometry> 对象，您需要访问正在显示已转换文本的对象的 <xref:System.Windows.Media.DrawingContext>。  在这些代码示例中，这是通过创建自定义控件对象来执行的，该自定义控件对象从支持用户定义呈现的类派生而来。  
  
 若要显示自定义控件中的 <xref:System.Windows.Media.Geometry> 对象，请重写 <xref:System.Windows.UIElement.OnRender%2A> 方法。  重写后的方法应使用 <xref:System.Windows.Media.DrawingContext.DrawGeometry%2A> 方法来绘制 <xref:System.Windows.Media.Geometry> 对象。  
  
 [!code-csharp[OutlineTextControlViewer#OnRender](../../../../samples/snippets/csharp/VS_Snippets_Wpf/OutlineTextControlViewer/CSharp/OutlineTextControl.cs#onrender)]
 [!code-vb[OutlineTextControlViewer#OnRender](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/OutlineTextControlViewer/visualbasic/outlinetextcontrol.vb#onrender)]  
  
## 请参阅  
 [绘制格式化文本](../../../../docs/framework/wpf/advanced/drawing-formatted-text.md)