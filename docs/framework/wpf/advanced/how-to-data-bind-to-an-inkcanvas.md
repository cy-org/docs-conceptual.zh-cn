---
title: "如何：将数据绑定到 InkCanvas | Microsoft Docs"
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
  - "InkCanvas，将数据绑定到"
  - "将数据绑定，到 InkCanvas"
ms.assetid: 8d6b4d9e-ea7f-4412-ba83-3feccec5a515
caps.latest.revision: 4
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 4
---
# 如何：将数据绑定到 InkCanvas
## <a name="example"></a>示例  
 下面的示例演示如何将绑定<xref:System.Windows.Controls.InkCanvas.Strokes%2A>属性<xref:System.Windows.Controls.InkCanvas>到另一个<xref:System.Windows.Controls.InkCanvas>。  
  
 [!code-xml[InkCanvasBindingSnippet#2](../../../../samples/snippets/csharp/VS_Snippets_Wpf/InkCanvasBindingSnippet/CS/Window2.xaml#2)]  
  
 下面的示例演示如何将绑定<xref:System.Windows.Controls.InkCanvas.DefaultDrawingAttributes%2A>属性设置为数据源。  
  
 [!code-xml[InkCanvasBindingSnippet#3](../../../../samples/snippets/csharp/VS_Snippets_Wpf/InkCanvasBindingSnippet/CS/Window2.xaml#3)]  
[!code-xml[InkCanvasBindingSnippet#4](../../../../samples/snippets/csharp/VS_Snippets_Wpf/InkCanvasBindingSnippet/CS/Window2.xaml#4)]  
  
 下面的示例声明了两个<xref:System.Windows.Controls.InkCanvas>对象在 XAML 中，并建立这些和其他数据源之间的数据绑定。  第一个<xref:System.Windows.Controls.InkCanvas>，称为`ic`，绑定到两个数据源。  <xref:System.Windows.Controls.InkCanvas.EditingMode%2A>和<xref:System.Windows.Controls.InkCanvas.DefaultDrawingAttributes%2A>属性`ic`绑定到<xref:System.Windows.Controls.ListBox>对象，后者又绑定到 XAML 中定义的数组。  <xref:System.Windows.Controls.InkCanvas.EditingMode%2A>， <xref:System.Windows.Controls.InkCanvas.DefaultDrawingAttributes%2A>，和<xref:System.Windows.Controls.InkCanvas.Strokes%2A>第二个属性<xref:System.Windows.Controls.InkCanvas>绑定到第一个<xref:System.Windows.Controls.InkCanvas>， `ic`。  
  
 [!code-xml[InkCanvasBindingSnippet#1](../../../../samples/snippets/csharp/VS_Snippets_Wpf/InkCanvasBindingSnippet/CS/Window1.xaml#1)]