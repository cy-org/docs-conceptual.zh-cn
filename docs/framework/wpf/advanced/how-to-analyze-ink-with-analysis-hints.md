---
title: "如何：通过分析提示来分析墨迹 | Microsoft Docs"
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
  - "AnalysisHintNode 对象"
  - "分析墨迹"
  - "墨迹, AnalysisHintNode 对象"
  - "墨迹, 分析"
ms.assetid: d4421ed4-77f5-4640-829e-9f1de50b2ff2
caps.latest.revision: 4
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 4
---
# 如何：通过分析提示来分析墨迹
<xref:System.Windows.Ink.AnalysisHintNode> 为其所附加到的 <xref:System.Windows.Ink.InkAnalyzer> 提供提示。  提示适用于 <xref:System.Windows.Ink.AnalysisHintNode> 的 <xref:System.Windows.Ink.ContextNode.Location%2A> 属性指定的区域，并向墨迹分析器提供额外的上下文以提高识别的准确性。  <xref:System.Windows.Ink.InkAnalyzer> 在分析从提示区域中获得的墨迹时将应用此上下文信息。  
  
## 示例  
 下面的示例是一个在接受墨迹输入的窗体上使用多个 <xref:System.Windows.Ink.AnalysisHintNode> 对象的应用程序。  此应用程序使用 <xref:System.Windows.Ink.AnalysisHintNode.Factoid%2A> 属性为窗体上的每一项提供上下文信息。  此应用程序使用背景分析来分析墨迹并在用户停止添加墨迹五秒钟后清除窗体上的所有墨迹。  
  
 [!code-xml[HowToAnalyzeInk#1](../../../../samples/snippets/csharp/VS_Snippets_Wpf/HowToAnalyzeInk/CSharp/FormAnalyzer.xaml#1)]  
  
 [!code-csharp[HowToAnalyzeInk#2](../../../../samples/snippets/csharp/VS_Snippets_Wpf/HowToAnalyzeInk/CSharp/FormAnalyzer.xaml.cs#2)]
 [!code-vb[HowToAnalyzeInk#2](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/HowToAnalyzeInk/VisualBasic/FormAnalyzer.xaml.vb#2)]