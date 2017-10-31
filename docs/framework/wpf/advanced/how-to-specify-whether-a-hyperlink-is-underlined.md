---
title: "如何：指定是否为超链接添加下划线 | Microsoft Docs"
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
  - "类, TextDecoration"
  - "Hyperlink 控件类型"
  - "TextDecoration 类"
ms.assetid: 3996cfe6-1dac-4835-aeb3-c719ce9cfee5
caps.latest.revision: 5
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 5
---
# 如何：指定是否为超链接添加下划线
<xref:System.Windows.Documents.Hyperlink> 对象是一个内联级别的流内容元素，允许您在流内容中承载超链接。  默认情况下，<xref:System.Windows.Documents.Hyperlink> 使用 <xref:System.Windows.TextDecoration> 对象来显示下划线。  实例化 <xref:System.Windows.TextDecoration> 对象可能会大幅降低性能，使用了许多 <xref:System.Windows.Documents.Hyperlink> 对象时尤其如此。  如果您使用大量 <xref:System.Windows.Documents.Hyperlink> 元素，则可能需要考虑仅在触发某个事件（如 <xref:System.Windows.ContentElement.MouseEnter> 事件）时才显示下划线。  
  
 在下面的示例中，“My MSN”（我的 MSN）的下划线是动态的，它仅在触发 <xref:System.Windows.ContentElement.MouseEnter> 事件时才出现。  
  
 ![显示 TextDecoration 的超链接](../../../../docs/framework/wpf/advanced/media/textdecoration03.png "TextDecoration03")  
用 TextDecorations 定义的超链接  
  
## 示例  
 下面的标记示例演示了一个使用和未使用下划线定义的 <xref:System.Windows.Documents.Hyperlink>：  
  
 [!code-xml[Performance#PerformanceSnippet11](../../../../samples/snippets/csharp/VS_Snippets_Wpf/Performance/CSharp/Hyperlink.xaml#performancesnippet11)]  
  
 下面的代码示例演示如何在触发 <xref:System.Windows.ContentElement.MouseEnter> 事件时为 <xref:System.Windows.Documents.Hyperlink> 创建下划线，以及如何在触发 <xref:System.Windows.ContentElement.MouseLeave> 事件时移除下划线。  
  
 [!code-csharp[Performance#PerformanceSnippet15](../../../../samples/snippets/csharp/VS_Snippets_Wpf/Performance/CSharp/Hyperlink.xaml.cs#performancesnippet15)]
 [!code-vb[Performance#PerformanceSnippet15](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/Performance/visualbasic/hyperlink.xaml.vb#performancesnippet15)]  
  
## 请参阅  
 <xref:System.Windows.TextDecoration>   
 <xref:System.Windows.Documents.Hyperlink>   
 [优化 WPF 应用程序性能](../../../../docs/framework/wpf/advanced/optimizing-wpf-application-performance.md)   
 [创建文本修饰](../../../../docs/framework/wpf/advanced/how-to-create-a-text-decoration.md)