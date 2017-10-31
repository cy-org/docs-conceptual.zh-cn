---
title: "高级文本格式设置 | Microsoft Docs"
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
  - "格式设置 [WPF]"
  - "文本 [WPF]"
  - "版式, 设置文本格式"
ms.assetid: f0a7986e-f5b2-485c-a27d-f8e922022212
caps.latest.revision: 16
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 12
---
# 高级文本格式设置
[!INCLUDE[TLA#tla_wpf](../../../../includes/tlasharptla-wpf-md.md)] 提供了一组稳定可靠的 [!INCLUDE[TLA#tla_api#plural](../../../../includes/tlasharptla-apisharpplural-md.md)]，用于在应用程序中加入文本。  布局和[!INCLUDE[TLA#tla_ui](../../../../includes/tlasharptla-ui-md.md)] [!INCLUDE[TLA2#tla_api#plural](../../../../includes/tla2sharptla-apisharpplural-md.md)]（如 <xref:System.Windows.Controls.TextBlock>）为文本呈现提供了最常见的通用元素。  绘图 [!INCLUDE[TLA2#tla_api#plural](../../../../includes/tla2sharptla-apisharpplural-md.md)]（如 <xref:System.Windows.Media.GlyphRunDrawing> 和 <xref:System.Windows.Media.FormattedText>）提供一种方法，可在绘图中加入已设置了格式的文本。  在最高级别，[!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] 提供了一个可扩展的文本格式引擎，用于控制文本呈现的各个方面，如文本存储管理、文本运行格式管理和嵌入对象管理。  
  
 本主题介绍 [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] 文本格式，  重点介绍客户端实现和 [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] 文本格式引擎的使用上。  
  
> [!NOTE]
>  本文档中的所有代码示例都可以在 [Advanced Text Formatting Sample](http://go.microsoft.com/fwlink/?LinkID=159965)（高级文本格式设置示例）中找到。  
  
   
  
<a name="prereq"></a>   
## 必备组件  
 本主题假定您熟悉较高级别的用于呈现文本的 [!INCLUDE[TLA2#tla_api#plural](../../../../includes/tla2sharptla-apisharpplural-md.md)]。  大部分用户方案都不需要本主题中所讨论的高级文本格式 [!INCLUDE[TLA2#tla_api#plural](../../../../includes/tla2sharptla-apisharpplural-md.md)]。  有关不同文本 [!INCLUDE[TLA2#tla_api#plural](../../../../includes/tla2sharptla-apisharpplural-md.md)] 的介绍，请参见 [WPF 中的文档](../../../../docs/framework/wpf/advanced/documents-in-wpf.md)。  
  
<a name="section1"></a>   
## 高级文本格式  
 [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] 中的文本布局和 [!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)] 控件提供了格式设置属性，通过这些属性，您可以轻松地在应用程序中加入已设置了格式的文本。  这些控件将公开许多用于处理文本呈现（包括字样、大小和颜色）的属性。  在一般情况下，这些控件可以处理应用程序中的大部分文本呈现。  但是，某些高级方案要求控制文本存储和文本呈现。  为此，[!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] 提供了一个可扩展的文本格式引擎。  
  
 在 [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] 中找到的高级文本格式功能包括文本格式引擎、文本存储、文本运行和格式设置属性。  文本格式引擎 <xref:System.Windows.Media.TextFormatting.TextFormatter> 可创建用于呈现的文本行。  这是通过初始化行格式设置过程并调用文本格式设置程序的 <xref:System.Windows.Media.TextFormatting.TextFormatter.FormatLine%2A> 而实现的。  文本格式设置程序通过调用文本存储的 <xref:System.Windows.Media.TextFormatting.TextSource.GetTextRun%2A> 方法而从该存储中检索文本运行。  然后，文本格式设置程序将 <xref:System.Windows.Media.TextFormatting.TextRun> 对象转换成 <xref:System.Windows.Media.TextFormatting.TextLine> 对象，并提供给应用程序进行检查或显示。  
  
<a name="section2"></a>   
## 使用文本格式设置程序  
 <xref:System.Windows.Media.TextFormatting.TextFormatter> 是一种 [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] 文本格式引擎，用于提供文本行格式设置和换行服务。  文本格式设置程序可以处理各种文本字符格式和段落样式，并提供对国际文本布局的支持。  
  
 与传统文本 [!INCLUDE[TLA#tla_api](../../../../includes/tlasharptla-api-md.md)] 不同的是，<xref:System.Windows.Media.TextFormatting.TextFormatter> 通过一组回调方法来与文本布局客户端交互。  它要求客户端在 <xref:System.Windows.Media.TextFormatting.TextSource> 类的实现中提供这些方法。  下面的关系图说明了客户端应用程序和 <xref:System.Windows.Media.TextFormatting.TextFormatter> 之间的文本布局交互。  
  
 ![文本布局客户端和 TextFormatter 示意图](../../../../docs/framework/wpf/advanced/media/textformatter01.png "TextFormatter01")  
应用程序和 TextFormatter 之间的交互  
  
 文本格式设置程序用于从文本存储中检索已设置了格式的文本行（即 <xref:System.Windows.Media.TextFormatting.TextSource> 的实现）。  这是通过首先使用 <xref:System.Windows.Media.TextFormatting.TextFormatter.Create%2A> 方法创建文本格式设置程序实例来完成的。  此方法将创建一个文本格式设置程序实例，并设置最大行高值和行宽值。  一旦创建文本格式设置程序实例，即可通过调用 <xref:System.Windows.Media.TextFormatting.TextFormatter.FormatLine%2A> 方法来启动行创建过程。  <xref:System.Windows.Media.TextFormatting.TextFormatter> 将回调文本源以便检索构成行的文本运行的文本和格式设置参数。  
  
 下面的示例演示文本存储的格式设置过程。  <xref:System.Windows.Media.TextFormatting.TextFormatter> 对象用于从文本存储中检索文本行，然后设置该文本行的格式以便在 <xref:System.Windows.Media.DrawingContext> 中绘制。  
  
 [!code-csharp[TextFormatterExample#100](../../../../samples/snippets/csharp/VS_Snippets_Wpf/TextFormatterExample/CSharp/Window1.xaml.cs#100)]
 [!code-vb[TextFormatterExample#100](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/TextFormatterExample/VisualBasic/Window1.xaml.vb#100)]  
  
<a name="section3"></a>   
## 实现客户端文本存储  
 扩展文本格式引擎时，需要实现和管理文本存储的各个方面。  该任务不是无关紧要的。  文本存储负责跟踪文本运行属性、段落属性、嵌入对象和其他类似内容。  另外，它还为文本格式设置程序提供了单独的 <xref:System.Windows.Media.TextFormatting.TextRun> 对象，以供文本格式设置程序创建 <xref:System.Windows.Media.TextFormatting.TextLine> 对象。  
  
 若要处理文本存储的虚拟化，文本存储必须派生自<xref:System.Windows.Media.TextFormatting.TextSource>。  <xref:System.Windows.Media.TextFormatting.TextSource> 定义了文本格式设置程序用来从文本存储中检索文本运行的方法。  <xref:System.Windows.Media.TextFormatting.TextSource.GetTextRun%2A> 即文本格式设置程序用于检索行格式设置中使用的文本运行的方法。  文本格式设置程序将重复调用 <xref:System.Windows.Media.TextFormatting.TextSource.GetTextRun%2A>，直到满足以下条件之一：  
  
-   返回 <xref:System.Windows.Media.TextFormatting.TextEndOfLine> 或某个子类。  
  
-   文本运行的累积宽度超出在创建文本格式设置程序的调用或调用文本格式设置程序的 <xref:System.Windows.Media.TextFormatting.TextFormatter.FormatLine%2A> 方法中指定的最大行宽。  
  
-   返回 [!INCLUDE[TLA#tla_unicode](../../../../includes/tlasharptla-unicode-md.md)] 换行序列，如“CF”、“LF”或“CRLF”。  
  
<a name="section4"></a>   
## 提供文本运行  
 文本格式设置过程的核心是文本格式设置程序和文本存储之间的交互。  <xref:System.Windows.Media.TextFormatting.TextSource> 的实现为文本格式设置程序提供了用于设置文本运行格式的 <xref:System.Windows.Media.TextFormatting.TextRun> 对象和属性。  此交互是通过文本格式设置程序调用的 <xref:System.Windows.Media.TextFormatting.TextSource.GetTextRun%2A> 方法来处理的。  
  
 下表显示了某些预定义的 <xref:System.Windows.Media.TextFormatting.TextRun> 对象。  
  
|TextRun 类型|用法|  
|----------------|--------|  
|<xref:System.Windows.Media.TextFormatting.TextCharacters>|专用文本运行，用于将字符标志符号的表示形式传回给文本格式设置程序。|  
|<xref:System.Windows.Media.TextFormatting.TextEmbeddedObject>|专用文本运行，用于提供其中的度量、命中测试以及绘制将作为整体执行的内容，如文本中的按钮或图像。|  
|<xref:System.Windows.Media.TextFormatting.TextEndOfLine>|专用文本运行，用于对行尾进行标记。|  
|<xref:System.Windows.Media.TextFormatting.TextEndOfParagraph>|专用文本运行，用于对段落尾部进行标记。|  
|<xref:System.Windows.Media.TextFormatting.TextEndOfSegment>|专用文本运行，用于对节尾进行标记，以便结束受前一次 <xref:System.Windows.Media.TextFormatting.TextModifier> 运行影响的范围。|  
|<xref:System.Windows.Media.TextFormatting.TextHidden>|专用文本运行，用于对一系列隐藏字符进行标记。|  
|<xref:System.Windows.Media.TextFormatting.TextModifier>|专用文本运行，用于在其范围内修改文本运行属性。  该范围可扩展到下一个匹配的 <xref:System.Windows.Media.TextFormatting.TextEndOfSegment> 文本运行或下一个 <xref:System.Windows.Media.TextFormatting.TextEndOfParagraph>。|  
  
 任何预定义的 <xref:System.Windows.Media.TextFormatting.TextRun> 对象都可以创建子类。  这样，文本源便可以为文本格式设置程序提供包含自定义数据的文本运行。  
  
 下面的示例演示了 <xref:System.Windows.Media.TextFormatting.TextSource.GetTextRun%2A> 方法。  此文本存储将 <xref:System.Windows.Media.TextFormatting.TextRun> 对象返回到文本格式设置程序以便处理。  
  
 [!code-csharp[TextFormatterExample#101](../../../../samples/snippets/csharp/VS_Snippets_Wpf/TextFormatterExample/CSharp/CustomTextSource.cs#101)]
 [!code-vb[TextFormatterExample#101](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/TextFormatterExample/VisualBasic/CustomTextSource.vb#101)]  
  
> [!NOTE]
>  在此示例中，文本存储为所有文本提供了相同的文本属性。  高级文本存储需要实现各自的范围管理，以便单个字符具有不同的属性。  
  
<a name="section5"></a>   
## 指定格式设置属性  
 <xref:System.Windows.Media.TextFormatting.TextRun> 对象是使用文本存储提供的属性设置格式的。  这些属性包括分为两种类型：<xref:System.Windows.Media.TextFormatting.TextParagraphProperties> 和 <xref:System.Windows.Media.TextFormatting.TextRunProperties>。  <xref:System.Windows.Media.TextFormatting.TextParagraphProperties> 可处理涉及段落的属性，如 <xref:System.Windows.TextAlignment> 和 <xref:System.Windows.FlowDirection>。  <xref:System.Windows.Media.TextFormatting.TextRunProperties> 是一系列属性（如前景画笔、<xref:System.Windows.Media.Typeface> 和字号），这些属性对段落中的每个文本运行可能会有所不同。  若要实现自定义段落和自定义文本运行属性类型，应用程序必须创建分别派生自 <xref:System.Windows.Media.TextFormatting.TextParagraphProperties> 和 <xref:System.Windows.Media.TextFormatting.TextRunProperties> 的类。  
  
## 请参阅  
 [WPF 中的版式](../../../../docs/framework/wpf/advanced/typography-in-wpf.md)   
 [WPF 中的文档](../../../../docs/framework/wpf/advanced/documents-in-wpf.md)