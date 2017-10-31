---
title: "TextElement 内容模型概述 | Microsoft Docs"
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
  - "文档, 流文档"
  - "流内容元素 [WPF], TextElement 内容模型"
  - "流文档"
  - "TextElement 内容模型"
ms.assetid: d0a7791c-b090-438c-812f-b9d009d83ee9
caps.latest.revision: 11
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 7
---
# TextElement 内容模型概述
本内容模型概述描述了 <xref:System.Windows.Documents.TextElement> 支持的内容。  <xref:System.Windows.Documents.Paragraph> 类是 <xref:System.Windows.Documents.TextElement> 的类型。  内容模型描述哪些对象\/元素可以包含在其他对象\/元素中。  本概述汇总了派生自 <xref:System.Windows.Documents.TextElement> 的对象所使用的内容模型。  有关更多信息，请参见[流文档概述](../../../../docs/framework/wpf/advanced/flow-document-overview.md)。  
  
   
  
<a name="text_element_classes"></a>   
## 内容模型关系图  
 下面的关系图对派生自 <xref:System.Windows.Documents.TextElement> 的类所使用的内容模型，以及其他非 `TextElement` 类如何适应该模型进行了汇总。  
  
 ![示意图：流内容包含架构](../../../../docs/framework/wpf/advanced/media/flow-content-schema.png "Flow\_Content\_Schema")  
  
 如上面的关系图所示，元素可以具有的子元素不一定通过某个类派生自 <xref:System.Windows.Documents.Block> 类还是 <xref:System.Windows.Documents.Inline> 类来确定。  例如，<xref:System.Windows.Documents.Span>（从 <xref:System.Windows.Documents.Inline> 派生的类）只能具有 <xref:System.Windows.Documents.Inline> 子元素，但是 <xref:System.Windows.Documents.Figure>（也是从 <xref:System.Windows.Documents.Inline> 派生的类）只能具有 <xref:System.Windows.Documents.Block> 子元素。  因此，关系图可用于快速地确定哪些元素可以包含在其他元素中。  例如，我们可以使用关系图来确定如何构造 <xref:System.Windows.Controls.RichTextBox> 的流内容。  
  
1.  一个 <xref:System.Windows.Controls.RichTextBox> 必须包含一个 <xref:System.Windows.Documents.FlowDocument>，而后者又必须包含一个派生自 <xref:System.Windows.Documents.Block> 的对象。  下图是上述关系图中的相应一部分。  
  
     ![示意图：RichTextBox 包含规则](../../../../docs/framework/wpf/advanced/media/flow-ovw-schemawalkthrough1.png "Flow\_Ovw\_SchemaWalkThrough1")  
  
     到此为止，标记可能类似于所示内容。  
  
     [!code-xml[FlowOvwSnippets_snip#SchemaWalkThrough1](../../../../samples/snippets/csharp/VS_Snippets_Wpf/FlowOvwSnippets_snip/CS/MiscSnippets.xaml#schemawalkthrough1)]  
  
2.  按照该关系图，存在多个可以从中进行选择的 <xref:System.Windows.Documents.Block> 元素，包括 <xref:System.Windows.Documents.Paragraph>、<xref:System.Windows.Documents.Section>、<xref:System.Windows.Documents.Table>、<xref:System.Windows.Documents.List> 和 <xref:System.Windows.Documents.BlockUIContainer>（请参见上图中从 Block 派生的类）。  假设我们需要一个 <xref:System.Windows.Documents.Table>。  按照上面的关系图，一个 <xref:System.Windows.Documents.Table> 包含一个 <xref:System.Windows.Documents.TableRowGroup>，后者包含多个 <xref:System.Windows.Documents.TableRow> 元素，这些行元素又包含多个 <xref:System.Windows.Documents.TableCell> 元素，而这些单元格元素又包含一个从 <xref:System.Windows.Documents.Block> 派生的对象。  下图是本文档内第一个关系图中与 <xref:System.Windows.Documents.Table> 相对应的一部分。  
  
     ![示意图：表的父&#47;子架构](../../../../docs/framework/wpf/advanced/media/flow-ovw-schemawalkthrough2.png "Flow\_Ovw\_SchemaWalkThrough2")  
  
     下面是相应的标记。  
  
     [!code-xml[FlowOvwSnippets_snip#SchemaWalkThrough2](../../../../samples/snippets/csharp/VS_Snippets_Wpf/FlowOvwSnippets_snip/CS/MiscSnippets.xaml#schemawalkthrough2)]  
  
3.  同样，<xref:System.Windows.Documents.TableCell> 下需要一个或多个 <xref:System.Windows.Documents.Block> 元素。  为简单起见，我们在单元格内部放置一些文本。  可以使用一个带有 <xref:System.Windows.Documents.Run> 元素的 <xref:System.Windows.Documents.Paragraph> 来实现该操作。  下图是本文档内第一个关系图中的一部分，由该图可见，<xref:System.Windows.Documents.Paragraph> 可以包含一个 <xref:System.Windows.Documents.Inline> 元素，而 <xref:System.Windows.Documents.Run>（一个 <xref:System.Windows.Documents.Inline> 元素）只能包含纯文本。  
  
     ![示意图：段落的父&#47;子架构](../../../../docs/framework/wpf/advanced/media/flow-ovw-schemawalkthrough3.png "Flow\_Ovw\_SchemaWalkThrough3")  
  
     ![示意图：运行的父&#47;子架构](../../../../docs/framework/wpf/advanced/media/flow-ovw-schemawalkthrough4.png "Flow\_Ovw\_SchemaWalkThrough4")  
  
 下面是标记中的完整示例。  
  
 [!code-xml[FlowOvwSnippets_snip#SchemaExampleWholePage](../../../../samples/snippets/csharp/VS_Snippets_Wpf/FlowOvwSnippets_snip/CS/SchemaExample.xaml#schemaexamplewholepage)]  
  
<a name="Using_the_Content_Property"></a>   
## 以编程方式处理 TextElement 内容  
 <xref:System.Windows.Documents.TextElement> 的内容由集合组成，因此，可以通过处理这些集合来以编程方式操作 <xref:System.Windows.Documents.TextElement> 对象的内容。  从 <xref:System.Windows.Documents.TextElement> 派生的类可以使用以下三个不同的集合：  
  
-   <xref:System.Windows.Documents.InlineCollection>：表示 <xref:System.Windows.Documents.Inline> 元素的集合。  <xref:System.Windows.Documents.InlineCollection> 定义 <xref:System.Windows.Documents.Paragraph>、<xref:System.Windows.Documents.Span> 和 <xref:System.Windows.Controls.TextBlock> 元素允许使用的子内容。  
  
-   <xref:System.Windows.Documents.BlockCollection>：表示 <xref:System.Windows.Documents.Block> 元素的集合。  <xref:System.Windows.Documents.BlockCollection> 定义 <xref:System.Windows.Documents.FlowDocument>、<xref:System.Windows.Documents.Section>、<xref:System.Windows.Documents.ListItem>、<xref:System.Windows.Documents.TableCell>、<xref:System.Windows.Documents.Floater> 和 <xref:System.Windows.Documents.Figure> 元素允许使用的子内容。  
  
-   <xref:System.Windows.Documents.ListItemCollection>：一个流内容元素，表示有序或无序 <xref:System.Windows.Documents.List> 中的特定内容项。  
  
 可以从这些集合中，分别使用 **Inline**、**Block** 和 **ListItem** 的属性来进行操作（添加或移除项）。  下面的示例演示如何使用 **Inline** 属性来操作 Span 的内容。  
  
> [!NOTE]
>  Table 使用多个集合来操作其内容，但是这里我们不对其进行说明。  有关更多信息，请参见[表概述](../../../../docs/framework/wpf/advanced/table-overview.md)。  
  
 下面的示例创建一个新 <xref:System.Windows.Documents.Span> 对象，然后使用 `Add` 方法添加两个文本运行，作为 <xref:System.Windows.Documents.Span> 的子内容。  
  
 [!code-csharp[SpanSnippets#_SpanInlinesAdd](../../../../samples/snippets/csharp/VS_Snippets_Wpf/SpanSnippets/CSharp/Window1.xaml.cs#_spaninlinesadd)]
 [!code-vb[SpanSnippets#_SpanInlinesAdd](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/SpanSnippets/visualbasic/window1.xaml.vb#_spaninlinesadd)]  
  
 下面的示例创建一个新 <xref:System.Windows.Documents.Run> 元素并将其插入到 <xref:System.Windows.Documents.Span> 的开始位置。  
  
 [!code-csharp[SpanSnippets#_SpanInlinesInsert](../../../../samples/snippets/csharp/VS_Snippets_Wpf/SpanSnippets/CSharp/Window1.xaml.cs#_spaninlinesinsert)]
 [!code-vb[SpanSnippets#_SpanInlinesInsert](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/SpanSnippets/visualbasic/window1.xaml.vb#_spaninlinesinsert)]  
  
 下面的示例删除 <xref:System.Windows.Documents.Span> 中的最后一个 <xref:System.Windows.Documents.Inline> 元素。  
  
 [!code-csharp[SpanSnippets#_SpanInlinesRemoveLast](../../../../samples/snippets/csharp/VS_Snippets_Wpf/SpanSnippets/CSharp/Window1.xaml.cs#_spaninlinesremovelast)]
 [!code-vb[SpanSnippets#_SpanInlinesRemoveLast](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/SpanSnippets/visualbasic/window1.xaml.vb#_spaninlinesremovelast)]  
  
 下面的示例从 <xref:System.Windows.Documents.Span> 中清除所有内容（<xref:System.Windows.Documents.Inline> 元素）。  
  
 [!code-csharp[SpanSnippets#_SpanInlinesClear](../../../../samples/snippets/csharp/VS_Snippets_Wpf/SpanSnippets/CSharp/Window1.xaml.cs#_spaninlinesclear)]
 [!code-vb[SpanSnippets#_SpanInlinesClear](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/SpanSnippets/visualbasic/window1.xaml.vb#_spaninlinesclear)]  
  
<a name="Types_that_Share_this_Content_Model"></a>   
## 共享此内容模型的类型  
 下面的类型继承自 <xref:System.Windows.Documents.TextElement> 类，可以用来显示本概述中描述的内容。  
  
 <xref:System.Windows.Documents.Bold>, <xref:System.Windows.Documents.Figure>, <xref:System.Windows.Documents.Floater>, <xref:System.Windows.Documents.Hyperlink>, <xref:System.Windows.Documents.InlineUIContainer>, <xref:System.Windows.Documents.Italic>, <xref:System.Windows.Documents.LineBreak>, <xref:System.Windows.Documents.List>, <xref:System.Windows.Documents.ListItem>, <xref:System.Windows.Documents.Paragraph>, <xref:System.Windows.Documents.Run>, <xref:System.Windows.Documents.Section>, <xref:System.Windows.Documents.Span>, <xref:System.Windows.Documents.Table>, <xref:System.Windows.Documents.Underline>.  
  
 请注意，此列表中仅包括与 [!INCLUDE[TLA2#tla_winfxsdk](../../../../includes/tla2sharptla-winfxsdk-md.md)] 一起分发的非抽象类型。  可以使用继承自 <xref:System.Windows.Documents.TextElement> 的其他类型。  
  
<a name="Types_that_Can_Contain_ContentControl_Objects"></a>   
## 可包含 TextElement 对象的类型  
 请参见 [WPF 内容模型](../../../../docs/framework/wpf/controls/wpf-content-model.md)。  
  
## 请参阅  
 [通过 Blocks 属性操作 FlowDocument](../../../../docs/framework/wpf/advanced/how-to-manipulate-a-flowdocument-through-the-blocks-property.md)   
 [通过 Blocks 属性操作流内容元素](../../../../docs/framework/wpf/advanced/how-to-manipulate-flow-content-elements-through-the-blocks-property.md)   
 [通过 Blocks 属性操作 FlowDocument](../../../../docs/framework/wpf/advanced/how-to-manipulate-a-flowdocument-through-the-blocks-property.md)   
 [通过 Columns 属性操作表列](../../../../docs/framework/wpf/advanced/how-to-manipulate-table-columns-through-the-columns-property.md)   
 [通过 RowGroups 属性操作表的行组](../../../../docs/framework/wpf/advanced/how-to-manipulate-table-row-groups-through-the-rowgroups-property.md)