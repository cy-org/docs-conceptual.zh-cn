---
title: "流文档概述 | Microsoft Docs"
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
  - "内容架构"
  - "文档, 流文档"
  - "流内容元素 [WPF], 流文档"
  - "流文档"
ms.assetid: ef236a50-d44f-43c8-ba7c-82b0c733c0b7
caps.latest.revision: 39
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 29
---
# 流文档概述
流文档旨在优化查看和可读性。  流文档根据运行时变量（例如，窗口大小、设备分辨率和可选的用户首选项）来动态调整和重新排列文档内容，而不是设置为一个预定义的布局。  此外，流文档还提供一些高级文档功能，例如，分页和分栏。  本主题概述了流文档及其创建方式。  
  
   
  
<a name="what_is_a_flow_document"></a>   
## 什么是流文档？  
 流文档旨在根据窗口大小、设备分辨率和其他环境变量来“调整内容的流动”。  此外，流文档还具有很多内置功能，包括搜索、能够优化可读性的查看模式以及更改字体大小和外观的功能。  当文档首先看重易于阅读时，最适合使用流文档。  相反，固定文档旨在提供静态表示形式。  当源内容的高保真至关重要时，固定文档非常有用。  有关不同类型文档的更多信息，请参见 [WPF 中的文档](../../../../docs/framework/wpf/advanced/documents-in-wpf.md)。  
  
 下图演示在多个不同大小的窗口中查看同一个示例流文档的情况。  随着显示区域的变化，内容将调整流动，从而最好地利用可用空间。  
  
 ![流文档内容调整](../../../../docs/framework/wpf/advanced/media/edocs-flowdocument.png "eDocs\_FlowDocument")  
  
 如上图所示，流内容可以包括很多个组成部分，包括段落、列表、图像等等。  这些组成部分对应于标记中的元素和程序代码中的对象。  稍后，我们将在本概述的[“与流相关的类”](#flow_related_classes)一节中详细介绍这些类。  现在，我们提供一个简单的代码示例，其中创建了一个流文档，该文档由一个包含一些粗体文本的段落和一个列表组成。  
  
 [!code-xml[FlowOvwSnippets_snip#SimpleFlowExampleWholePage](../../../../samples/snippets/csharp/VS_Snippets_Wpf/FlowOvwSnippets_snip/CS/SimpleFlowExample.xaml#simpleflowexamplewholepage)]  
  
 [!code-csharp[FlowOvwSnippets_procedural_snip#SimpleFlowCodeOnlyExampleWholePage](../../../../samples/snippets/csharp/VS_Snippets_Wpf/FlowOvwSnippets_procedural_snip/CSharp/SimpleFlowExample.cs#simpleflowcodeonlyexamplewholepage)]
 [!code-vb[FlowOvwSnippets_procedural_snip#SimpleFlowCodeOnlyExampleWholePage](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/FlowOvwSnippets_procedural_snip/VisualBasic/SimpleFlowExample.vb#simpleflowcodeonlyexamplewholepage)]  
  
 下图显示了此代码段。  
  
 ![屏幕快照：呈现的 FlowDocument 示例](../../../../docs/framework/wpf/advanced/media/flow-ovw-first-example.png "Flow\_Ovw\_First\_Example")  
  
 在此示例中，<xref:System.Windows.Controls.FlowDocumentReader> 控件用于承载流内容。  有关流内容承载控件的更多信息，请参见[流文档类型](#flow_document_types)。  <xref:System.Windows.Documents.Paragraph>、<xref:System.Windows.Documents.List>、<xref:System.Windows.Documents.ListItem> 和 <xref:System.Windows.Documents.Bold> 元素用于根据它们在标记中的顺序来控制内容格式。  例如，<xref:System.Windows.Documents.Bold> 元素只涵盖该段落中的一部分文本，因此，只有这一部分文本是粗体。  如果您使用过 HTML，那么这对于您来说应该很熟悉。  
  
 正如上图中突出显示的那样，流文档中有多个内置功能：  
  
-   搜索：使用户可以对整个文档执行全文搜索。  
  
-   查看模式：用户可以选择他们喜欢的查看模式，包括单页（一次一页）查看模式、一次两页（书本阅读格式）查看模式和连续滚动（无界限）查看模式。  有关这些查看模式的更多信息，请参见 <xref:System.Windows.Controls.FlowDocumentReaderViewingMode>。  
  
-   页面导航控件：如果文档的查看模式使用页面，则页面导航控件包括一个用于跳转到下一页（下箭头）或上一页（上箭头）的按钮，以及显示当前页码和总页数的指示器。  也可以使用键盘上的箭头键来实现翻页的操作。  
  
-   缩放：缩放控件使用户可以通过单击加号或减号按钮来相应地增大或减小缩放级别。  缩放控件还包括一个用于调整缩放级别的滑块。  有关更多信息，请参见 <xref:System.Windows.Controls.FlowDocumentReader.Zoom%2A>。  
  
 这些功能可以根据用于承载流内容的控件进行修改。  下一节将介绍各种控件。  
  
<a name="flow_document_types"></a>   
## 流文档类型  
 流文档内容的显示和外观依赖于用于承载流内容的对象。  有四个控件可以为查看流内容提供支持：<xref:System.Windows.Controls.FlowDocumentReader>、<xref:System.Windows.Controls.FlowDocumentPageViewer>、<xref:System.Windows.Controls.RichTextBox> 和 <xref:System.Windows.Controls.FlowDocumentScrollViewer>。  下面简要介绍了这些控件。  
  
 **注意：**需要使用 <xref:System.Windows.Documents.FlowDocument> 来直接承载流内容，因此所有这些查看控件都使用一个 <xref:System.Windows.Documents.FlowDocument> 来启用流内容承载。  
  
### FlowDocumentReader  
 <xref:System.Windows.Controls.FlowDocumentReader> 包含一些功能，使用户能够动态地在各种查看模式之间进行选择，这些查看模式包括单页（一次一页）查看模式、一次两页（书本阅读格式）查看模式和连续滚动（无界限）查看模式。  有关这些查看模式的更多信息，请参见 <xref:System.Windows.Controls.FlowDocumentReaderViewingMode>。  如果您不需要在不同查看模式之间动态切换的功能，则可以使用 <xref:System.Windows.Controls.FlowDocumentPageViewer> 和 <xref:System.Windows.Controls.FlowDocumentScrollViewer>，它们提供了固定使用特定查看模式的轻量级流内容查看器。  
  
### FlowDocumentPageViewer 和 FlowDocumentScrollViewer  
 <xref:System.Windows.Controls.FlowDocumentPageViewer> 以一次一页的查看模式显示内容，而 <xref:System.Windows.Controls.FlowDocumentScrollViewer> 以连续滚动模式显示内容。  <xref:System.Windows.Controls.FlowDocumentPageViewer> 和 <xref:System.Windows.Controls.FlowDocumentScrollViewer> 都固定使用特定查看模式。  与 <xref:System.Windows.Controls.FlowDocumentReader> 相比，后者包含一些功能，使用户能够动态地在各种查看模式（由 <xref:System.Windows.Controls.FlowDocumentReaderViewingMode> 枚举提供）之间进行选择，但代价是需要消耗比 <xref:System.Windows.Controls.FlowDocumentPageViewer> 或 <xref:System.Windows.Controls.FlowDocumentScrollViewer> 更多的资源。  
  
 默认情况下，总是显示垂直滚动条，而水平滚动条则在需要时显示。  <xref:System.Windows.Controls.FlowDocumentScrollViewer> 的默认 UI 不包括工具栏；不过，可以使用 <xref:System.Windows.Controls.FlowDocumentScrollViewer.IsToolBarVisible%2A> 属性来启用内置工具栏。  
  
### RichTextBox  
 若要允许用户编辑流内容，请使用 <xref:System.Windows.Controls.RichTextBox>。  例如，如果您希望创建一个编辑器，其中允许用户处理表、斜体和粗体格式等，则应该使用 <xref:System.Windows.Controls.RichTextBox>。  有关更多信息，请参见[RichTextBox 概述](../../../../docs/framework/wpf/controls/richtextbox-overview.md)。  
  
 **注意：** <xref:System.Windows.Controls.RichTextBox> 内部的流内容的行为并不与其他控件中包含的流内容完全相同。  例如，在 <xref:System.Windows.Controls.RichTextBox> 中不分栏，因此没有自动调整大小行为。  另外，在 <xref:System.Windows.Controls.RichTextBox> 中不能使用通常内置在流内容中的功能，例如搜索、查看模式、页面导航和缩放。  
  
<a name="creating_flow_content"></a>   
## 创建流内容  
 流内容可能很复杂并包含各种元素，包括文本、图像、表甚至像控件这样的 <xref:System.Windows.UIElement> 派生类。  若要了解如何创建复杂流内容，掌握下列知识点是非常关键的：  
  
-   **与流相关的类**：流内容中使用的每个类都有特定用途。  此外，流类之间的层次关系可帮助您了解它们的使用方式。  例如，从 <xref:System.Windows.Documents.Block> 类派生的类用于包含其他对象，而从 <xref:System.Windows.Documents.Inline> 派生的类包含所显示的对象。  
  
-   **内容架构**：流文档可能需要大量嵌套元素。  内容架构指定了元素之间可能存在的父\/子关系。  
  
 以下各节将详细介绍上述每个方面。  
  
<a name="flow_related_classes"></a>   
## 与流相关的类  
 下图演示最常与流内容一起使用的对象：  
  
 ![示意图：流内容元素类层次结构](../../../../docs/framework/wpf/advanced/media/flow-class-hierarchy.png "Flow\_Class\_Hierarchy")  
  
 根据流内容的用途，可以分为两个重要类别：  
  
1.  **Block 派生类**：也称为“Block 内容元素”，或简称为“Block 元素”。  继承自 <xref:System.Windows.Documents.Block> 的元素可用于将元素分组到一个公用父级下，或将公用特性应用于某个组。  
  
2.  **Inline 派生类**：也称为“Inline 内容元素”，或简称为“Inline 元素”。  继承自 <xref:System.Windows.Documents.Inline> 的元素包含在一个 Block 元素中，或者包含在另一个 Inline 元素中。  Inline 元素通常用作在屏幕上呈现的内容的直接容器。  例如，一个 <xref:System.Windows.Documents.Paragraph>（Block 元素）可包含一个 <xref:System.Windows.Documents.Run>（Inline 元素），而 <xref:System.Windows.Documents.Run> 实际包含在屏幕上呈现的文本。  
  
 下面简要介绍了这两个类别中的每个类。  
  
### Block 派生类  
 **Paragraph**  
  
 <xref:System.Windows.Documents.Paragraph> 通常用于将内容分组到一个段落中。  Paragraph 的最简单且最常见的用途是创建文本段落。  
  
 [!code-xml[FlowOvwSnippets_snip#ParagraphExampleWholePage](../../../../samples/snippets/csharp/VS_Snippets_Wpf/FlowOvwSnippets_snip/CS/ParagraphExample.xaml#paragraphexamplewholepage)]  
  
 [!code-csharp[FlowOvwSnippets_procedural_snip#ParagraphCodeOnlyExampleWholePage](../../../../samples/snippets/csharp/VS_Snippets_Wpf/FlowOvwSnippets_procedural_snip/CSharp/ParagraphExample.cs#paragraphcodeonlyexamplewholepage)]
 [!code-vb[FlowOvwSnippets_procedural_snip#ParagraphCodeOnlyExampleWholePage](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/FlowOvwSnippets_procedural_snip/VisualBasic/ParagraphExample.vb#paragraphcodeonlyexamplewholepage)]  
  
 不过，也可以包含其他 Inline 派生元素，如下所示。  
  
 **节**  
  
 <xref:System.Windows.Documents.Section> 只用于包含其他 <xref:System.Windows.Documents.Block> 派生元素。  它不会向其中包含的元素应用任何默认格式。  不过，在 <xref:System.Windows.Documents.Section> 上设置的任何属性值都适用于其子元素。  使用节能够以编程方式循环访问其子级的集合。  <xref:System.Windows.Documents.Section> 的使用方式类似于 HTML 中的 \<DIV\> 标记。  
  
 在下面的示例中，在一个 <xref:System.Windows.Documents.Section> 下定义了三个段落。  该节具有 <xref:System.Windows.Documents.TextElement.Background%2A> 属性值 Red，因此段落的背景色也是红色。  
  
 [!code-xml[FlowOvwSnippets_snip#SectionExampleWholePage](../../../../samples/snippets/csharp/VS_Snippets_Wpf/FlowOvwSnippets_snip/CS/SectionExample.xaml#sectionexamplewholepage)]  
  
 [!code-csharp[FlowOvwSnippets_procedural_snip#SectionCodeOnlyExampleWholePage](../../../../samples/snippets/csharp/VS_Snippets_Wpf/FlowOvwSnippets_procedural_snip/CSharp/SectionExample.cs#sectioncodeonlyexamplewholepage)]
 [!code-vb[FlowOvwSnippets_procedural_snip#SectionCodeOnlyExampleWholePage](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/FlowOvwSnippets_procedural_snip/VisualBasic/SectionExample.vb#sectioncodeonlyexamplewholepage)]  
  
 **BlockUIContainer**  
  
 <xref:System.Windows.Documents.BlockUIContainer> 使 <xref:System.Windows.UIElement> 元素（即  <xref:System.Windows.Controls.Button>）能够嵌入到区块派生的流内容中。  <xref:System.Windows.Documents.InlineUIContainer>（参见下文）用于在内联派生的流内容中嵌入 <xref:System.Windows.UIElement> 元素。  <xref:System.Windows.Documents.BlockUIContainer> 和 <xref:System.Windows.Documents.InlineUIContainer> 很重要，因为除非 <xref:System.Windows.UIElement> 包含在这两个元素之一内部，否则没有其他办法在流内容中使用它。  
  
 下面的示例演示如何使用 <xref:System.Windows.Documents.BlockUIContainer> 元素在流内容中承载 <xref:System.Windows.UIElement> 对象。  
  
 [!code-xml[SpanSnippets#_BlockUIXAML](../../../../samples/snippets/csharp/VS_Snippets_Wpf/SpanSnippets/CSharp/Window1.xaml#_blockuixaml)]  
  
 下图显示了此示例的呈现效果。  
  
 ![屏幕快照：嵌入在流内容中的 UIElement](../../../../docs/framework/wpf/advanced/media/blockuicontainer.png "BlockUIContainer")  
  
 **列表**  
  
 <xref:System.Windows.Documents.List> 用于创建项目符号列表或编号列表。  将 <xref:System.Windows.Documents.List.MarkerStyle%2A> 属性设置为 <xref:System.Windows.TextMarkerStyle> 枚举值可确定列表的样式。  下面的示例演示如何创建一个简单的列表。  
  
 [!code-xml[FlowOvwSnippets_snip#ListExampleWholePage](../../../../samples/snippets/csharp/VS_Snippets_Wpf/FlowOvwSnippets_snip/CS/ListExample.xaml#listexamplewholepage)]  
  
 [!code-csharp[FlowOvwSnippets_procedural_snip#ListCodeOnlyExampleWholePage](../../../../samples/snippets/csharp/VS_Snippets_Wpf/FlowOvwSnippets_procedural_snip/CSharp/ListExample.cs#listcodeonlyexamplewholepage)]
 [!code-vb[FlowOvwSnippets_procedural_snip#ListCodeOnlyExampleWholePage](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/FlowOvwSnippets_procedural_snip/VisualBasic/ListExample.vb#listcodeonlyexamplewholepage)]  
  
 **注意：** <xref:System.Windows.Documents.List> 是唯一一个使用 <xref:System.Windows.Documents.ListItemCollection> 来管理子元素的流元素。  
  
 **表**  
  
 <xref:System.Windows.Documents.Table> 用于创建表。  <xref:System.Windows.Documents.Table> 与 <xref:System.Windows.Controls.Grid> 元素类似，但是前者具有更多功能，因此需要更大的资源开销。  因为 <xref:System.Windows.Controls.Grid> 是一个 <xref:System.Windows.UIElement>，所以除非它包含在 <xref:System.Windows.Documents.BlockUIContainer> 或 <xref:System.Windows.Documents.InlineUIContainer> 中，否则不能在流内容中使用。  有关 <xref:System.Windows.Documents.Table> 的更多信息，请参见 [表概述](../../../../docs/framework/wpf/advanced/table-overview.md)：  
  
### Inline 派生类  
 **Run**  
  
 <xref:System.Windows.Documents.Run> 用于包含无格式文本。  在流内容中，您可能期望广泛使用 <xref:System.Windows.Documents.Run> 对象。  但是，在标记中，无需显式使用 <xref:System.Windows.Documents.Run> 元素。  在使用代码创建或操作流文档时，需要使用 <xref:System.Windows.Documents.Run>。  例如，在下面的标记中，第一个 <xref:System.Windows.Documents.Paragraph> 显式指定了 <xref:System.Windows.Documents.Run> 元素，而第二个却没有。  这两个段落生成相同的输出。  
  
 [!code-xml[FlowOvwSnippets_snip#RunExample1](../../../../samples/snippets/csharp/VS_Snippets_Wpf/FlowOvwSnippets_snip/CS/RunSnippetsExample.xaml#runexample1)]  
  
 **注意：**从 [!INCLUDE[net_v40_short](../../../../includes/net-v40-short-md.md)] 开始，<xref:System.Windows.Documents.Run> 对象的 <xref:System.Windows.Documents.Run.Text%2A>属性为依赖项属性。  您可以将 <xref:System.Windows.Documents.Run.Text%2A> 属性绑定到数据源，例如 <xref:System.Windows.Controls.TextBlock>。  <xref:System.Windows.Documents.Run.Text%2A> 属性完全支持单向绑定。  <xref:System.Windows.Documents.Run.Text%2A> 属性还支持双向绑定（<xref:System.Windows.Controls.RichTextBox> 除外）。  有关示例，请参见<xref:System.Windows.Documents.Run.Text%2A?displayProperty=fullName>。  
  
 **Span**  
  
 <xref:System.Windows.Documents.Span> 将其他内联内容元素组织到一起。  对于 <xref:System.Windows.Documents.Span> 元素中的内容，不应用任何继承呈现。  但是，从 <xref:System.Windows.Documents.Span> 继承的元素（包括 <xref:System.Windows.Documents.Hyperlink>、<xref:System.Windows.Documents.Bold>、<xref:System.Windows.Documents.Italic> 和 <xref:System.Windows.Documents.Underline>）确实会向文本应用格式。  
  
 下面是 <xref:System.Windows.Documents.Span> 的一个示例，它用于包含内联内容，包括文本、一个 <xref:System.Windows.Documents.Bold> 元素和一个 <xref:System.Windows.Controls.Button>。  
  
 [!code-xml[FlowOvwSnippets_snip#SpanExampleWholePage](../../../../samples/snippets/csharp/VS_Snippets_Wpf/FlowOvwSnippets_snip/CS/SpanExample.xaml#spanexamplewholepage)]  
  
 下面的屏幕快照显示了此示例的呈现效果。  
  
 ![屏幕快照：呈现的 Span 示例](../../../../docs/framework/wpf/advanced/media/flow-spanexample.png "Flow\_SpanExample")  
  
 **InlineUIContainer**  
  
 <xref:System.Windows.Documents.InlineUIContainer> 使 <xref:System.Windows.UIElement> 元素（即  像 <xref:System.Windows.Controls.Button> 这样的控件）能够嵌入到 <xref:System.Windows.Documents.Inline> 内容元素中。  此元素是与上面介绍的 <xref:System.Windows.Documents.BlockUIContainer> 等效的 Inline 元素。  下面的示例使用 <xref:System.Windows.Documents.InlineUIContainer> 将一个 <xref:System.Windows.Controls.Button> 以内联方式插入到 <xref:System.Windows.Documents.Paragraph> 中。  
  
 [!code-xml[FlowOvwSnippets_snip#InlineUIContainerExampleWholePage](../../../../samples/snippets/csharp/VS_Snippets_Wpf/FlowOvwSnippets_snip/CS/InlineUIContainerExample.xaml#inlineuicontainerexamplewholepage)]  
  
 [!code-csharp[FlowOvwSnippets_procedural_snip#InlineUIContainerCodeOnlyExampleWholePage](../../../../samples/snippets/csharp/VS_Snippets_Wpf/FlowOvwSnippets_procedural_snip/CSharp/InlineUIContainerExample.cs#inlineuicontainercodeonlyexamplewholepage)]
 [!code-vb[FlowOvwSnippets_procedural_snip#InlineUIContainerCodeOnlyExampleWholePage](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/FlowOvwSnippets_procedural_snip/VisualBasic/InlineUIContainerExample.vb#inlineuicontainercodeonlyexamplewholepage)]  
  
 **注意：**不需要在标记中显式使用 <xref:System.Windows.Documents.InlineUIContainer>。  如果将其省略，编译代码时仍将创建一个 <xref:System.Windows.Documents.InlineUIContainer>。  
  
 **Figure 和 Floater**  
  
 通过 <xref:System.Windows.Documents.Figure> 和 <xref:System.Windows.Documents.Floater>，可以使用定位属性在流文档中嵌入内容，这些定位属性可独立于主内容流进行自定义。  <xref:System.Windows.Documents.Figure> 或 <xref:System.Windows.Documents.Floater> 元素通常用于突出显示或强调内容的某些部分，承载主内容流中的支持图像或其他内容，或者用于插入松散相关的内容（如广告）。  
  
 下面的示例演示如何将一个 <xref:System.Windows.Documents.Figure> 嵌入到文本段落中。  
  
 [!code-xml[FlowOvwSnippets_snip#FigureExampleWholePage](../../../../samples/snippets/csharp/VS_Snippets_Wpf/FlowOvwSnippets_snip/CS/FigureExample.xaml#figureexamplewholepage)]  
  
 [!code-csharp[FlowOvwSnippets_procedural_snip#FigureCodeOnlyExampleWholePage](../../../../samples/snippets/csharp/VS_Snippets_Wpf/FlowOvwSnippets_procedural_snip/CSharp/FigureExample.cs#figurecodeonlyexamplewholepage)]
 [!code-vb[FlowOvwSnippets_procedural_snip#FigureCodeOnlyExampleWholePage](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/FlowOvwSnippets_procedural_snip/VisualBasic/FigureExample.vb#figurecodeonlyexamplewholepage)]  
  
 下图显示了此示例的呈现效果。  
  
 ![屏幕快照：图示例](../../../../docs/framework/wpf/advanced/media/flow-ovw-figure-example.png "Flow\_Ovw\_Figure\_Example")  
  
 <xref:System.Windows.Documents.Figure> 和 <xref:System.Windows.Documents.Floater> 在多个方面存在差异，并且用于不同的方案。  
  
 **Figure：**  
  
-   可定位：可以设置其水平和垂直定位点，以便相对于页面、内容、栏或段落进行停靠。  还可以使用其 <xref:System.Windows.Documents.Figure.HorizontalOffset%2A> 和 <xref:System.Windows.Documents.Figure.VerticalOffset%2A> 属性指定任意偏移量。  
  
-   可将其大小调整为栏大小的几倍：可以将 <xref:System.Windows.Documents.Figure> 的高度和宽度设置为页面、内容或栏的高度或宽度的倍数。  请注意，对于页面和内容，倍数不能大于 1。  例如，可以将 <xref:System.Windows.Documents.Figure> 的宽度设置为“页面的 0.5 倍”、“内容的 0.25 倍”或“栏的 2 倍”。  还可以将高度和宽度设置为绝对像素值。  
  
-   不分页：如果 <xref:System.Windows.Documents.Figure> 中的内容无法容纳在 <xref:System.Windows.Documents.Figure> 内部，它会呈现能够容纳的内容部分，而其余内容将丢失  
  
 **Floater：**  
  
-   无法定位，可在能够为其提供空间的任何位置呈现。  不能设置偏移量或锚定 <xref:System.Windows.Documents.Floater>。  
  
-   不能将其大小设置为栏大小的几倍：默认情况下，<xref:System.Windows.Documents.Floater> 的大小为一个栏大小。  它有一个可设置为绝对像素值的 <xref:System.Windows.Documents.Floater.Width%2A> 属性，但是如果此值大于一个栏宽，则将其忽略并将浮动对象的大小设置为一个栏大小。  可以通过设置正确的像素宽度将其大小设置为小于一个栏宽，但设置大小与栏无关，因此“0.5 倍栏宽”并不是 <xref:System.Windows.Documents.Floater> 宽度的有效表达。  <xref:System.Windows.Documents.Floater> 没有高度属性，无法设置其高度；其高度取决于内容  
  
-   <xref:System.Windows.Documents.Floater> 分页：如果指定宽度的内容超出了一个栏的高度，则浮动对象会断开并显示到下一栏、下一页中等等。  
  
 <xref:System.Windows.Documents.Figure> 适合放置希望控制其大小和定位的独立内容，并且可以确信内容将适合指定的大小。  <xref:System.Windows.Documents.Floater> 适合放置流动更加自由的内容，其流动方式与主页内容类似，但与主页内容相分离。  
  
 **LineBreak**  
  
 <xref:System.Windows.Documents.LineBreak> 导致在流内容中发生换行。  下面的示例说明 <xref:System.Windows.Documents.LineBreak> 的用法。  
  
 [!code-xml[FlowOvwSnippets_snip#LineBreakExampleWholePage](../../../../samples/snippets/csharp/VS_Snippets_Wpf/FlowOvwSnippets_snip/CS/LineBreakExample.xaml#linebreakexamplewholepage)]  
  
 下面的屏幕快照显示了此示例的呈现效果。  
  
 ![屏幕快照：LineBreak 示例](../../../../docs/framework/wpf/advanced/media/flow-ovw-linebreakexample.png "Flow\_Ovw\_LineBreakExample")  
  
### 流集合元素  
 在上面的多个示例中，<xref:System.Windows.Documents.BlockCollection> 和 <xref:System.Windows.Documents.InlineCollection> 用于以编程方式构造流内容。  例如，若要向 <xref:System.Windows.Documents.Paragraph> 中添加元素，可以使用以下语法：  
  
 `…`  
  
 `myParagraph.Inlines.Add(new Run("Some text"));`  
  
 `…`  
  
 该语法向 <xref:System.Windows.Documents.Paragraph> 的 <xref:System.Windows.Documents.InlineCollection> 中添加一个 <xref:System.Windows.Documents.Run>。  这与标记中的 <xref:System.Windows.Documents.Paragraph> 内部包含的隐式 <xref:System.Windows.Documents.Run> 相同。  
  
 `…`  
  
 `<Paragraph>`  
  
 `Some Text`  
  
 `</Paragraph>`  
  
 `…`  
  
 作为使用 <xref:System.Windows.Documents.BlockCollection> 的示例，下面的示例创建了一个新的 <xref:System.Windows.Documents.Section>，然后使用 **Add** 方法将一个新的 <xref:System.Windows.Documents.Paragraph> 添加到 <xref:System.Windows.Documents.Section> 内容中。  
  
 [!code-csharp[FlowDocumentSnippets#_SectionBlocksAdd](../../../../samples/snippets/csharp/VS_Snippets_Wpf/FlowDocumentSnippets/CSharp/Window1.xaml.cs#_sectionblocksadd)]
 [!code-vb[FlowDocumentSnippets#_SectionBlocksAdd](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/FlowDocumentSnippets/visualbasic/window1.xaml.vb#_sectionblocksadd)]  
  
 除了向流集合中添加项以外，还可以移除项。  下面的示例删除 <xref:System.Windows.Documents.Span> 中的最后一个 <xref:System.Windows.Documents.Inline> 元素。  
  
 [!code-csharp[SpanSnippets#_SpanInlinesRemoveLast](../../../../samples/snippets/csharp/VS_Snippets_Wpf/SpanSnippets/CSharp/Window1.xaml.cs#_spaninlinesremovelast)]
 [!code-vb[SpanSnippets#_SpanInlinesRemoveLast](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/SpanSnippets/visualbasic/window1.xaml.vb#_spaninlinesremovelast)]  
  
 下面的示例从 <xref:System.Windows.Documents.Span> 中清除所有内容（<xref:System.Windows.Documents.Inline> 元素）。  
  
 [!code-csharp[SpanSnippets#_SpanInlinesClear](../../../../samples/snippets/csharp/VS_Snippets_Wpf/SpanSnippets/CSharp/Window1.xaml.cs#_spaninlinesclear)]
 [!code-vb[SpanSnippets#_SpanInlinesClear](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/SpanSnippets/visualbasic/window1.xaml.vb#_spaninlinesclear)]  
  
 在以编程方式使用流内容时，可能会广泛使用这些集合。  
  
 流元素是使用 <xref:System.Windows.Documents.InlineCollection>（内联）还是 <xref:System.Windows.Documents.BlockCollection>（块）来包含其子元素取决于父级可以包含的子元素的类型（<xref:System.Windows.Documents.Block> 或 <xref:System.Windows.Documents.Inline>）。  下一节中的内容架构中概述了流内容元素的包容规则。  
  
 **注意：**还有第三种类型的集合可用于流内容，即 <xref:System.Windows.Documents.ListItemCollection>，但此集合仅用于 <xref:System.Windows.Documents.List>。  此外，还有几个集合可用于 <xref:System.Windows.Documents.Table>。  有关更多信息，请参见[表概述](../../../../docs/framework/wpf/advanced/table-overview.md)。  
  
<a name="content_schema"></a>   
## 内容架构  
 不同流内容元素的数量是如此之多，因此了解某个元素可包含的子元素的类型是非常困难的。  下面的关系图概述了流元素的包容规则。  箭头表示可能存在的父\/子关系。  
  
 ![示意图：流内容包含架构](../../../../docs/framework/wpf/advanced/media/flow-content-schema.png "Flow\_Content\_Schema")  
  
 如上面的关系图所示，元素可以具有的子元素不一定通过该元素是 <xref:System.Windows.Documents.Block> 元素还是 <xref:System.Windows.Documents.Inline> 元素来确定。  例如，<xref:System.Windows.Documents.Span>（一个 <xref:System.Windows.Documents.Inline> 元素）只能具有 <xref:System.Windows.Documents.Inline> 子元素，而 <xref:System.Windows.Documents.Figure>（也是 <xref:System.Windows.Documents.Inline> 元素）只能具有 <xref:System.Windows.Documents.Block> 子元素。  因此，关系图可用于快速地确定哪些元素可以包含在其他元素中。  例如，我们可以使用关系图来确定如何构造 <xref:System.Windows.Controls.RichTextBox> 的流内容。  
  
 **1.**一个 <xref:System.Windows.Controls.RichTextBox> 必须包含一个 <xref:System.Windows.Documents.FlowDocument>，而后者又必须包含一个派生自 <xref:System.Windows.Documents.Block> 的对象。  下面是上述关系图中的对应部分。  
  
 ![示意图：RichTextBox 包含规则](../../../../docs/framework/wpf/advanced/media/flow-ovw-schemawalkthrough1.png "Flow\_Ovw\_SchemaWalkThrough1")  
  
 到此为止，标记可能类似于所示内容。  
  
 [!code-xml[FlowOvwSnippets_snip#SchemaWalkThrough1](../../../../samples/snippets/csharp/VS_Snippets_Wpf/FlowOvwSnippets_snip/CS/MiscSnippets.xaml#schemawalkthrough1)]  
  
 **2.**按照该关系图，存在多个可以从中进行选择的 <xref:System.Windows.Documents.Block> 元素，包括 <xref:System.Windows.Documents.Paragraph>、<xref:System.Windows.Documents.Section>、<xref:System.Windows.Documents.Table>、<xref:System.Windows.Documents.List> 和 <xref:System.Windows.Documents.BlockUIContainer>（请参见上面的 Block 派生类）。  假设我们需要一个 <xref:System.Windows.Documents.Table>。  按照上面的关系图，一个 <xref:System.Windows.Documents.Table> 包含一个 <xref:System.Windows.Documents.TableRowGroup>，后者包含 <xref:System.Windows.Documents.TableRow> 元素，这些元素又包含 <xref:System.Windows.Documents.TableCell> 元素，而这些元素包含一个 <xref:System.Windows.Documents.Block> 派生对象。  下面是取自上述关系图中的 <xref:System.Windows.Documents.Table> 的对应部分。  
  
 ![示意图：表的父&#47;子架构](../../../../docs/framework/wpf/advanced/media/flow-ovw-schemawalkthrough2.png "Flow\_Ovw\_SchemaWalkThrough2")  
  
 下面是对应的标记。  
  
 [!code-xml[FlowOvwSnippets_snip#SchemaWalkThrough2](../../../../samples/snippets/csharp/VS_Snippets_Wpf/FlowOvwSnippets_snip/CS/MiscSnippets.xaml#schemawalkthrough2)]  
  
 **3.**同样，<xref:System.Windows.Documents.TableCell> 下需要一个或多个 <xref:System.Windows.Documents.Block> 元素。  为简单起见，我们在单元格内部放置一些文本。  可以使用一个带有 <xref:System.Windows.Documents.Run> 元素的 <xref:System.Windows.Documents.Paragraph> 来实现该操作。  下面是该关系图中的对应部分，它显示 <xref:System.Windows.Documents.Paragraph> 可以包含一个 <xref:System.Windows.Documents.Inline> 元素，而 <xref:System.Windows.Documents.Run>（一个 <xref:System.Windows.Documents.Inline> 元素）只能包含纯文本。  
  
 ![示意图：段落的父&#47;子架构](../../../../docs/framework/wpf/advanced/media/flow-ovw-schemawalkthrough3.png "Flow\_Ovw\_SchemaWalkThrough3")  
  
 ![示意图：运行的父&#47;子架构](../../../../docs/framework/wpf/advanced/media/flow-ovw-schemawalkthrough4.png "Flow\_Ovw\_SchemaWalkThrough4")  
  
 下面是标记中的完整示例。  
  
 [!code-xml[FlowOvwSnippets_snip#SchemaExampleWholePage](../../../../samples/snippets/csharp/VS_Snippets_Wpf/FlowOvwSnippets_snip/CS/SchemaExample.xaml#schemaexamplewholepage)]  
  
<a name="customizing_text"></a>   
## 自定义文本  
 通常，文本是流文档中最普遍的内容类型。  尽管上面介绍的对象可用于控制文本呈现方式的大多数方面，但还有其他一些自定义文本的方法。本节将对此进行介绍。  
  
### 文本修饰  
 使用文本修饰，可以向文本应用下划线、上划线、基线和删除线效果（请参见下图）。  这些修饰是使用 <xref:System.Windows.Documents.Inline.TextDecorations%2A> 属性添加的，该属性由很多对象公开，其中包括 <xref:System.Windows.Documents.Inline>、<xref:System.Windows.Documents.Paragraph>、<xref:System.Windows.Controls.TextBlock> 和 <xref:System.Windows.Controls.TextBox>。  
  
 下面的示例演示如何设置 <xref:System.Windows.Documents.Paragraph> 的 <xref:System.Windows.Documents.Paragraph.TextDecorations%2A> 属性。  
  
 [!code-xml[InlineSnippets#_Paragraph_TextDecXAML](../../../../samples/snippets/csharp/VS_Snippets_Wpf/InlineSnippets/CSharp/Window1.xaml#_paragraph_textdecxaml)]  
  
 [!code-csharp[InlineSnippets#_Paragraph_TextDec](../../../../samples/snippets/csharp/VS_Snippets_Wpf/InlineSnippets/CSharp/Window1.xaml.cs#_paragraph_textdec)]
 [!code-vb[InlineSnippets#_Paragraph_TextDec](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/InlineSnippets/visualbasic/window1.xaml.vb#_paragraph_textdec)]  
  
 下图显示了此示例的呈现效果。  
  
 ![屏幕快照：具有默认删除线效果的文本](../../../../docs/framework/wpf/advanced/media/inline-textdec-strike.png "Inline\_TextDec\_Strike")  
  
 下面的各图分别显示了**上划线**、**基线**和**下划线**修饰的呈现效果。  
  
 ![屏幕快照：上划线 TextDecorator](../../../../docs/framework/wpf/advanced/media/inline-textdec-over.png "Inline\_TextDec\_Over")  
  
 ![屏幕快照：文本上的默认基线效果](../../../../docs/framework/wpf/advanced/media/inline-textdec-base.png "Inline\_TextDec\_Base")  
  
 ![屏幕快照：具有默认下划线效果的文本](../../../../docs/framework/wpf/advanced/media/inline-textdec-under.png "Inline\_TextDec\_Under")  
  
### 版式  
 <xref:System.Windows.Documents.TextElement.Typography%2A> 属性由大多数与流相关的内容公开，其中包括 <xref:System.Windows.Documents.TextElement>、<xref:System.Windows.Documents.FlowDocument>、<xref:System.Windows.Controls.TextBlock> 和 <xref:System.Windows.Controls.TextBox>。  此属性用于控制文本的版式特征\/变体（即  小型大写字母或大型大写字母、设置上标和下标等）。  
  
 下面的示例演示如何设置 <xref:System.Windows.Documents.TextElement.Typography%2A> 特性，其中使用 <xref:System.Windows.Documents.Paragraph> 作为示例元素。  
  
 [!code-xml[TextElementSnippets#_TextElement_TypogXAML](../../../../samples/snippets/csharp/VS_Snippets_Wpf/TextElementSnippets/CSharp/Window1.xaml#_textelement_typogxaml)]  
  
 下图显示了此示例的呈现效果。  
  
 ![屏幕快照：改变版式的文本](../../../../docs/framework/wpf/advanced/media/textelement-typog.png "TextElement\_Typog")  
  
 作为对比，下图显示了一个具有默认版式属性的类似示例的呈现效果。  
  
 ![屏幕快照：改变版式的文本](../../../../docs/framework/wpf/advanced/media/textelement-typog-default.png "TextElement\_Typog\_Default")  
  
 下面的示例演示如何以编程方式设置 <xref:System.Windows.Controls.TextBox.Typography%2A> 属性。  
  
 [!code-csharp[TextElementSnippets#_TextElement_Typog](../../../../samples/snippets/csharp/VS_Snippets_Wpf/TextElementSnippets/CSharp/Window1.xaml.cs#_textelement_typog)]
 [!code-vb[TextElementSnippets#_TextElement_Typog](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/TextElementSnippets/visualbasic/window1.xaml.vb#_textelement_typog)]  
  
 有关版式的更多信息，请参见 [WPF 中的版式](../../../../docs/framework/wpf/advanced/typography-in-wpf.md)。  
  
## 请参阅  
 [Text](../../../../docs/framework/wpf/advanced/optimizing-performance-text.md)   
 [WPF 中的版式](../../../../docs/framework/wpf/advanced/typography-in-wpf.md)   
 [帮助主题](../../../../docs/framework/wpf/advanced/flow-content-elements-how-to-topics.md)   
 [TextElement 内容模型概述](../../../../docs/framework/wpf/advanced/textelement-content-model-overview.md)   
 [RichTextBox 概述](../../../../docs/framework/wpf/controls/richtextbox-overview.md)   
 [WPF 中的文档](../../../../docs/framework/wpf/advanced/documents-in-wpf.md)   
 [表概述](../../../../docs/framework/wpf/advanced/table-overview.md)   
 [批注概述](../../../../docs/framework/wpf/advanced/annotations-overview.md)