---
title: "如何：创建文本修饰 | Microsoft Docs"
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
  - "基线类型"
  - "字体, 基线"
  - "字体, 上划线"
  - "字体, 删除线"
  - "字体, 下划线"
  - "上划线类型"
  - "删除线类型"
  - "文本, 修饰"
  - "版式, 文本修饰"
  - "下划线类型"
ms.assetid: cf3cb4e7-782a-4be7-b2d4-e0935e21e4e0
caps.latest.revision: 9
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 9
---
# 如何：创建文本修饰
<xref:System.Windows.TextDecoration> 对象是可以添加到文本的视觉装饰。  有四种类型的文本修饰：下划线、基线、删除线和上划线。  下面的示例演示了文本修饰相对于文本的位置。  
  
 ![文本修饰位置示意图](../../../../docs/framework/wpf/advanced/media/textdecoration01.png "TextDecoration01")  
文本修饰类型示例  
  
 若要为文本添加文本修饰，请创建一个 <xref:System.Windows.TextDecoration> 对象并修改其属性。  可以使用 <xref:System.Windows.TextDecoration.Location%2A> 属性来指定文本修饰的显示位置（如下划线）。  可以使用 <xref:System.Windows.TextDecoration.Pen%2A> 属性来指定文本修饰的外观（如实心或渐变颜色）。  如果您没有为 <xref:System.Windows.TextDecoration.Pen%2A> 属性指定值，则在默认情况下文本修饰的颜色将与文本的颜色相同。  在定义了 <xref:System.Windows.TextDecoration> 对象之后，请将它添加到所需文本对象的 <xref:System.Windows.TextDecorations> 集合中。  
  
 下面的示例演示用线性渐变画笔和虚线钢笔设计的文本修饰。  
  
 ![采用线性渐变下划线的文本修饰](../../../../docs/framework/wpf/advanced/media/textdecoration02.png "TextDecoration02")  
用线性渐变画笔和虚线笔设计的下划线示例  
  
 <xref:System.Windows.Documents.Hyperlink> 对象是一个内联级别的流内容元素，允许您在流内容中承载超链接。  默认情况下，<xref:System.Windows.Documents.Hyperlink> 使用 <xref:System.Windows.TextDecoration> 对象来显示下划线。  实例化 <xref:System.Windows.TextDecoration> 对象可能会大幅降低性能，使用了许多 <xref:System.Windows.Documents.Hyperlink> 对象时尤其如此。  如果您使用大量 <xref:System.Windows.Documents.Hyperlink> 元素，则可能需要考虑仅在触发某个事件（如 <xref:System.Windows.ContentElement.MouseEnter> 事件）时才显示下划线。  
  
 在下面的示例中，“My MSN”（我的 MSN）的下划线是动态的，它仅在触发 <xref:System.Windows.ContentElement.MouseEnter> 事件时才出现。  
  
 ![显示 TextDecoration 的超链接](../../../../docs/framework/wpf/advanced/media/textdecoration03.png "TextDecoration03")  
用 TextDecorations 定义的超链接  
  
 有关更多信息，请参见[指定是否为超链接添加下划线](../../../../docs/framework/wpf/advanced/how-to-specify-whether-a-hyperlink-is-underlined.md)。  
  
## 示例  
 在下面的代码示例中，下划线文本修饰使用默认的字体值。  
  
 [!code-csharp[TextDecorationSnippets#TextDecorationSnippets1](../../../../samples/snippets/csharp/VS_Snippets_Wpf/TextDecorationSnippets/CSharp/Window1.xaml.cs#textdecorationsnippets1)]
 [!code-vb[TextDecorationSnippets#TextDecorationSnippets1](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/TextDecorationSnippets/visualbasic/window1.xaml.vb#textdecorationsnippets1)]
 [!code-xml[TextDecorationSnippets#TextDecorationSnippets1](../../../../samples/snippets/csharp/VS_Snippets_Wpf/TextDecorationSnippets/CSharp/Window1.xaml#textdecorationsnippets1)]  
  
 下面的代码示例将使用钢笔的纯色画笔来创建下划线文本修饰。  
  
 [!code-csharp[TextDecorationSnippets#TextDecorationSnippets2](../../../../samples/snippets/csharp/VS_Snippets_Wpf/TextDecorationSnippets/CSharp/Window1.xaml.cs#textdecorationsnippets2)]
 [!code-vb[TextDecorationSnippets#TextDecorationSnippets2](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/TextDecorationSnippets/visualbasic/window1.xaml.vb#textdecorationsnippets2)]
 [!code-xml[TextDecorationSnippets#TextDecorationSnippets2](../../../../samples/snippets/csharp/VS_Snippets_Wpf/TextDecorationSnippets/CSharp/Window1.xaml#textdecorationsnippets2)]  
  
 下面的代码示例使用虚线钢笔的线性渐变画笔创建一个下划线文本修饰。  
  
 [!code-csharp[TextDecorationSnippets#TextDecorationSnippets3](../../../../samples/snippets/csharp/VS_Snippets_Wpf/TextDecorationSnippets/CSharp/Window1.xaml.cs#textdecorationsnippets3)]
 [!code-vb[TextDecorationSnippets#TextDecorationSnippets3](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/TextDecorationSnippets/visualbasic/window1.xaml.vb#textdecorationsnippets3)]
 [!code-xml[TextDecorationSnippets#TextDecorationSnippets3](../../../../samples/snippets/csharp/VS_Snippets_Wpf/TextDecorationSnippets/CSharp/Window1.xaml#textdecorationsnippets3)]  
  
## 请参阅  
 <xref:System.Windows.TextDecoration>   
 <xref:System.Windows.Documents.Hyperlink>   
 [指定是否为超链接添加下划线](../../../../docs/framework/wpf/advanced/how-to-specify-whether-a-hyperlink-is-underlined.md)