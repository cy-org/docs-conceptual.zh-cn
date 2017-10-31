---
title: "优化性能：文本 | Microsoft Docs"
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
  - "呈现文本"
  - "超链接"
  - "格式化文本 [WPF]"
  - "文本性能"
  - "标志符号"
ms.assetid: 66b1b9a7-8618-48db-b616-c57ea4327b98
caps.latest.revision: 10
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 9
---
# 优化性能：文本
[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]包括对文本内容通过使用功能丰富的演示文稿的支持[!INCLUDE[TLA#tla_ui](../../../../includes/tlasharptla-ui-md.md)]控件。 通常可以将三个层中的文本呈现︰  
  
1.  使用<xref:System.Windows.Documents.Glyphs>和<xref:System.Windows.Media.GlyphRun>直接对象。  
  
2.  使用<xref:System.Windows.Media.FormattedText>对象。  
  
3.  使用高级别控件，如<xref:System.Windows.Controls.TextBlock>和<xref:System.Windows.Documents.FlowDocument>对象。  
  
 本主题提供的文本呈现性能的建议。  
  
   
  
<a name="Glyph_Level"></a>   
## <a name="rendering-text-at-the-glyph-level"></a>呈现标志符号级别的文本  
 [!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)]提供高级的文本支持，包括具有直接访问权限的标志符号级别标记<xref:System.Windows.Documents.Glyphs>的用户想要截获并保存在格式化后的文本。 这些功能提供关键支持的不同文本呈现要求在每个以下方案。  
  
-   屏幕上显示的固定格式文档。  
  
-   打印方案。  
  
    -   [!INCLUDE[TLA#tla_xaml](../../../../includes/tlasharptla-xaml-md.md)]作为设备的打印机语言。  
  
    -   [!INCLUDE[TLA#tla_mxdw](../../../../includes/tlasharptla-mxdw-md.md)]。  
  
    -   以前的打印机驱动程序，从输出[!INCLUDE[TLA#tla_win32](../../../../includes/tlasharptla-win32-md.md)]为固定格式的应用程序。  
  
    -   打印后台处理格式。  
  
-   固定格式的文档表示形式，包括以前版本的客户端[!INCLUDE[TLA#tla_mswin](../../../../includes/tlasharptla-mswin-md.md)]和其他计算设备。  
  
> [!NOTE]
>  <xref:System.Windows.Documents.Glyphs>和<xref:System.Windows.Media.GlyphRun>旨在用于固定格式的文档演示文稿和打印方案。 [!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)]为常规布局提供了几个元素和[!INCLUDE[TLA#tla_ui](../../../../includes/tlasharptla-ui-md.md)]方案如<xref:System.Windows.Controls.Label>和<xref:System.Windows.Controls.TextBlock>。 有关详细信息布局和[!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)]方案，请参阅[WPF 中的版式](../../../../docs/framework/wpf/advanced/typography-in-wpf.md)。  
  
 下面的示例演示如何定义属性<xref:System.Windows.Documents.Glyphs>对象在[!INCLUDE[TLA#tla_xaml](../../../../includes/tlasharptla-xaml-md.md)]。 <xref:System.Windows.Documents.Glyphs>对象表示的输出<xref:System.Windows.Media.GlyphRun>中[!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)]。 这些示例假定︰ 宋体、 Courier New 和 Times New Roman 字体安装在**C:\WINDOWS\Fonts**本地计算机上的文件夹。  
  
 [!code-xml[GlyphsOvwSample1#1](../../../../samples/snippets/csharp/VS_Snippets_Wpf/GlyphsOvwSample1/CS/default.xaml#1)]  
  
### <a name="using-drawglyphrun"></a>使用 DrawGlyphRun  
 如果具有自定义控件，并且您想要呈现标志符号，请使用<xref:System.Windows.Media.DrawingContext.DrawGlyphRun%2A>方法。  
  
 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]此外提供了自定义设置文本格式使用较低级别服务<xref:System.Windows.Media.FormattedText>对象。 在呈现文本的最有效方法[!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)]是通过生成文本的内容的标志符号级别使用<xref:System.Windows.Documents.Glyphs>和<xref:System.Windows.Media.GlyphRun>。 但是，这一高效率的成本是易于使用丰富的文本格式，这些是内置的功能丧失的[!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)]控件，如<xref:System.Windows.Controls.TextBlock>和<xref:System.Windows.Documents.FlowDocument>。  
  
<a name="FormattedText_Object"></a>   
## <a name="formattedtext-object"></a>FormattedText 对象  
 <xref:System.Windows.Media.FormattedText>对象，您可以绘制多行文本，在其中的文本中的每个字符可以单独设置格式。 有关详细信息，请参阅[绘图格式的文本](../../../../docs/framework/wpf/advanced/drawing-formatted-text.md)。  
  
 若要创建带格式的文本，请调用<xref:System.Windows.Media.FormattedText.%23ctor%2A>构造函数来创建<xref:System.Windows.Media.FormattedText>对象。 一旦您已经创建初始格式化的文本字符串，您可以应用范围的格式样式。 如果您的应用程序想要实现其自己的布局，则<xref:System.Windows.Media.FormattedText>对象是更好的选择，比使用一个控件，如<xref:System.Windows.Controls.TextBlock>。 有关详细信息<xref:System.Windows.Media.FormattedText>对象，请参阅[绘图格式的文本](../../../../docs/framework/wpf/advanced/drawing-formatted-text.md)。  
  
 <xref:System.Windows.Media.FormattedText>对象提供低级别的文本格式设置功能。 可以将多个格式设置样式应用到一个或多个字符。 例如，您可以调用<xref:System.Windows.Media.FormattedText.SetFontSize%2A>和<xref:System.Windows.Media.FormattedText.SetForegroundBrush%2A>方法来更改文本中的前五个字符的格式。  
  
 下面的代码示例创建<xref:System.Windows.Media.FormattedText>对象并将其呈现。  
  
 [!code-csharp[formattedtextsnippets#FormattedTextSnippets1](../../../../samples/snippets/csharp/VS_Snippets_Wpf/FormattedTextSnippets/CSharp/Window1.xaml.cs#formattedtextsnippets1)]
 [!code-vb[formattedtextsnippets#FormattedTextSnippets1](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/FormattedTextSnippets/visualbasic/window1.xaml.vb#formattedtextsnippets1)]  
  
<a name="FlowDocument_TextBlock_Label"></a>   
## <a name="flowdocument-textblock-and-label-controls"></a>FlowDocument、 TextBlock 和标签控件  
 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]包括多个控件的文本绘制到屏幕。 每个控件面向不同的方案，并具有自己的功能和限制的列表。  
  
### <a name="flowdocument-impacts-performance-more-than-textblock-or-label"></a>FlowDocument 对性能的影响多个 TextBlock 或标签  
 一般情况下， <xref:System.Windows.Controls.TextBlock>有限的文本支持是必需的如中的简短句子时，应使用元素[!INCLUDE[TLA#tla_ui](../../../../includes/tlasharptla-ui-md.md)]。 <xref:System.Windows.Controls.Label>时需要极少的文字支持时，可以使用。 <xref:System.Windows.Documents.FlowDocument>元素是可重流动支持丰富的内容，显示的文档容器，因此，具有比使用较好的性能效果<xref:System.Windows.Controls.TextBlock>或<xref:System.Windows.Controls.Label>控件。  
  
 有关详细信息<xref:System.Windows.Documents.FlowDocument>，请参阅[流文档概述](../../../../docs/framework/wpf/advanced/flow-document-overview.md)。  
  
### <a name="avoid-using-textblock-in-flowdocument"></a>应避免在 FlowDocument 使用 TextBlock  
 <xref:System.Windows.Controls.TextBlock>元素派生自<xref:System.Windows.UIElement>。 <xref:System.Windows.Documents.Run>元素派生自<xref:System.Windows.Documents.TextElement>，这是比使用成本较低<xref:System.Windows.UIElement>的派生的对象。 如果可能，请使用<xref:System.Windows.Documents.Run>而不是<xref:System.Windows.Controls.TextBlock>用于显示文本中的内容<xref:System.Windows.Documents.FlowDocument>。  
  
 下面的标记示例阐释了两种方法中设置文本内容<xref:System.Windows.Documents.FlowDocument>:  
  
 [!code-xml[Performance#PerformanceSnippet13](../../../../samples/snippets/csharp/VS_Snippets_Wpf/Performance/CSharp/FlowDocument.xaml#performancesnippet13)]  
  
### <a name="avoid-using-run-to-set-text-properties"></a>避免使用运行来设置文本属性  
 一般情况下，使用<xref:System.Windows.Documents.Run>内<xref:System.Windows.Controls.TextBlock>是更好的性能比不使用显式密集型<xref:System.Windows.Documents.Run>根本对象。 如果您使用<xref:System.Windows.Documents.Run>以便设置文本属性，请设置这些属性直接在上<xref:System.Windows.Controls.TextBlock>相反。  
  
 下面的标记示例阐释了这两种方式的 text 属性，在这种情况下，设置<xref:System.Windows.Controls.TextBlock.FontWeight%2A>属性︰  
  
 [!code-xml[Performance#PerformanceSnippet12](../../../../samples/snippets/csharp/VS_Snippets_Wpf/Performance/CSharp/Window1.xaml#performancesnippet12)]  
  
 下表显示了显示 1000 个成本<xref:System.Windows.Controls.TextBlock>对象显式超时和没有显式<xref:System.Windows.Documents.Run>。  
  
|**TextBlock 类型**|**创建时间 （毫秒）**|**呈现时间 （毫秒）**|  
|------------------------|------------------------------|----------------------------|  
|运行设置文本属性|146|540|  
|TextBlock 设置文本属性|43|453|  
  
### <a name="avoid-databinding-to-the-labelcontent-property"></a>避免对 Label.Content 属性进行数据绑定  
 假设您有<xref:System.Windows.Controls.Label>从经常更新的对象<xref:System.String>源。 当数据绑定<xref:System.Windows.Controls.Label>元素的<xref:System.Windows.Controls.ContentControl.Content%2A>属性设置为<xref:System.String>源对象时，您可能会遇到性能不佳。 每次源<xref:System.String>更新时，旧<xref:System.String>对象是放弃，并且一个新<xref:System.String>重新创建，因为<xref:System.String>对象是不可变的不能对其进行修改。 而这又会导致<xref:System.Windows.Controls.ContentPresenter>的<xref:System.Windows.Controls.Label>对象放弃其旧内容，并重新生成新的内容，以显示新<xref:System.String>。  
  
 此问题的解决方案很简单。 如果<xref:System.Windows.Controls.Label>未设置为一个自定义<xref:System.Windows.Controls.ContentControl.ContentTemplate%2A>值时，请替换<xref:System.Windows.Controls.Label>与<xref:System.Windows.Controls.TextBlock>和数据绑定其<xref:System.Windows.Controls.TextBlock.Text%2A>属性设置为源字符串。  
  
|**数据绑定属性**|**更新时间 （毫秒）**|  
|-----------------------------|----------------------------|  
|Label.Content|835|  
|TextBlock.Text|242|  
  
<a name="Hyperlink"></a>   
## <a name="hyperlink"></a>超链接  
 <xref:System.Windows.Documents.Hyperlink>对象为内联级别的流内容元素，它允许您承载在流内容中的超链接。  
  
### <a name="combine-hyperlinks-in-one-textblock-object"></a>组合中一个 TextBlock 对象的超链接  
 您可以优化使用多个<xref:System.Windows.Documents.Hyperlink>按在同一个分组元素<xref:System.Windows.Controls.TextBlock>。 这可帮助您在您的应用程序中创建的对象的数量降至最低。 例如，你可能想要显示多个超链接，如下所示︰  
  
 MSN 主页 |我 MSN  
  
 下面的标记示例显示了多个<xref:System.Windows.Controls.TextBlock>元素用来显示这些超链接︰  
  
 [!code-xml[Performance#PerformanceSnippet9](../../../../samples/snippets/csharp/VS_Snippets_Wpf/Performance/CSharp/Hyperlink.xaml#performancesnippet9)]  
  
 下面的标记示例显示了更高效的方法显示的超链接，这一次，使用单个<xref:System.Windows.Controls.TextBlock>:  
  
 [!code-xml[Performance#PerformanceSnippet10](../../../../samples/snippets/csharp/VS_Snippets_Wpf/Performance/CSharp/Hyperlink.xaml#performancesnippet10)]  
  
### <a name="showing-underlines-on-hyperlinks-only-on-mouseenter-events"></a>仅在 MouseEnter 事件上的超链接显示下划线  
 一个<xref:System.Windows.TextDecoration>对象是可以添加到文本的视觉装饰; 但是，它可以是实例化大幅降低性能。 如果进行了充分利用<xref:System.Windows.Documents.Hyperlink>元素，请考虑仅在触发某个事件，如时显示下划线<xref:System.Windows.ContentElement.MouseEnter>事件。 有关详细信息，请参阅[指定是否为超链接添加下划线](../../../../docs/framework/wpf/advanced/how-to-specify-whether-a-hyperlink-is-underlined.md)。  
  
 ![显示 Textdecoration 的超链接](../../../../docs/framework/wpf/advanced/media/textdecoration03.png "TextDecoration03")  
超链接出现在 MouseEnter  
  
 下面的标记的示例演示<xref:System.Windows.Documents.Hyperlink>使用和未使用下划线定义︰  
  
 [!code-xml[Performance#PerformanceSnippet11](../../../../samples/snippets/csharp/VS_Snippets_Wpf/Performance/CSharp/Hyperlink.xaml#performancesnippet11)]  
  
 下表显示了显示 1000 个的性能开销<xref:System.Windows.Documents.Hyperlink>带以及不带下划线的元素。  
  
|**超链接**|**创建时间 （毫秒）**|**呈现时间 （毫秒）**|  
|-------------------|------------------------------|----------------------------|  
|带有下划线|289|1130|  
|未下划线|299|776|  
  
<a name="Text_Formatting_Features"></a>   
## <a name="text-formatting-features"></a>文本格式设置功能  
 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]提供了丰富文本格式的服务，如自动断字。 这些服务可能会影响应用程序的性能，应仅在需要时使用。  
  
### <a name="avoid-unnecessary-use-of-hyphenation"></a>避免不必要地使用断字  
 自动断字功能查找行的文本，连字符断点，并允许附加断点位置中的行<xref:System.Windows.Controls.TextBlock>和<xref:System.Windows.Documents.FlowDocument>对象。 默认情况下，这些对象中禁用自动断字功能。 可以通过将该对象的 IsHyphenationEnabled 属性设置为启用此功能`true`。 但是，启用此功能会导致[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]启动[!INCLUDE[TLA#tla_com](../../../../includes/tlasharptla-com-md.md)]互操作性，可能会影响应用程序的性能。 建议，除非您需要它，并使用自动断字功能。  
  
### <a name="use-figures-carefully"></a>谨慎使用图形  
 一个<xref:System.Windows.Documents.Figure>元素代表可以是绝对定位在某一页内容的流内容的一部分。 在某些情况下，<xref:System.Windows.Documents.Figure>可能会导致整个页后，可以自动重新设置格式的如果其位置与已布局的内容相冲突。 通过组合在一起不需要重新格式化的可能性降到最低<xref:System.Windows.Documents.Figure>旁边对方，或者将它们声明中固定的页大小的情况下的内容的顶部附近的元素。  
  
### <a name="optimal-paragraph"></a>最佳段落  
 最佳段落功能的<xref:System.Windows.Documents.FlowDocument>对象段落的布局，以便尽可能均匀地分布空白区域。 默认情况下，最佳段落功能被禁用。 可以通过将对象设置启用此功能<xref:System.Windows.Documents.FlowDocument.IsOptimalParagraphEnabled%2A>属性设置为`true`。 但是，启用此功能会影响应用程序的性能。 建议您不要使用最佳段落功能，除非您需要它。  
  
## <a name="see-also"></a>另请参阅  
 [优化 WPF 应用程序性能](../../../../docs/framework/wpf/advanced/optimizing-wpf-application-performance.md)   
 [规划应用程序性能](../../../../docs/framework/wpf/advanced/planning-for-application-performance.md)   
 [利用硬件](../../../../docs/framework/wpf/advanced/optimizing-performance-taking-advantage-of-hardware.md)   
 [布局和设计](../../../../docs/framework/wpf/advanced/optimizing-performance-layout-and-design.md)   
 [二维图形和图像处理](../../../../docs/framework/wpf/advanced/optimizing-performance-2d-graphics-and-imaging.md)   
 [对象行为](../../../../docs/framework/wpf/advanced/optimizing-performance-object-behavior.md)   
 [应用程序资源](../../../../docs/framework/wpf/advanced/optimizing-performance-application-resources.md)   
 [数据绑定](../../../../docs/framework/wpf/advanced/optimizing-performance-data-binding.md)   
 [其他性能建议](../../../../docs/framework/wpf/advanced/optimizing-performance-other-recommendations.md)