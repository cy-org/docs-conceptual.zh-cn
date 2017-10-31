---
title: "WPF 中的双向功能概述 | Microsoft Docs"
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
  - "双向功能"
  - "FlowDirection 属性"
  - "FlowDocument 属性"
  - "Span 元素"
ms.assetid: fd850e25-7dba-408c-b521-8873e51dc968
caps.latest.revision: 22
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 18
---
# WPF 中的双向功能概述
与其他任何开发平台不同的是，[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 具有许多支持快速开发双向内容（例如，同一文档中混合了从左到右和从右到左的数据）的功能。  同时，[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 也为需要双向功能的用户（如阿拉伯语和希伯来语用户）带来了绝佳的体验。  
  
 以下各部分结合一些示例阐释如何获得双向内容的最佳显示效果，并对许多双向功能进行了说明。  其中多数示例使用的是 [!INCLUDE[TLA#tla_titlexaml](../../../../includes/tlasharptla-titlexaml-md.md)]，但您可以轻松地将这些概念应用于 [!INCLUDE[TLA#tla_cshrp](../../../../includes/tlasharptla-cshrp-md.md)] 或 [!INCLUDE[TLA#tla_visualb](../../../../includes/tlasharptla-visualb-md.md)] 代码中。  
  
   
  
<a name="FlowDirection"></a>   
## FlowDirection  
 <xref:System.Windows.FrameworkElement.FlowDirection%2A> 是在 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 应用程序中定义内容流方向的基本属性。  此属性可设置为以下两个枚举值之一：<xref:System.Windows.FlowDirection> 和 <xref:System.Windows.FlowDirection>。  此属性可用于从 <xref:System.Windows.FrameworkElement> 继承的所有 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 元素。  
  
 下面几个示例设置 <xref:System.Windows.Controls.TextBox> 元素的流方向。  
  
 **从左到右的流方向**  
  
 [!code-xml[LTRRTL#LTR](../../../../samples/snippets/csharp/VS_Snippets_Wpf/LTRRTL/CS/Pane1.xaml#ltr)]  
  
 **从右到左的流方向**  
  
 [!code-xml[LTRRTL#RTL](../../../../samples/snippets/csharp/VS_Snippets_Wpf/LTRRTL/CS/Pane1.xaml#rtl)]  
  
 下图显示了如何呈现上述代码。  
  
 **阐释 FlowDirection 的图形**  
  
 ![TextBlock 对齐](../../../../docs/framework/wpf/advanced/media/lefttorightrighttoleft.png "LefttoRightRighttoLeft")  
  
 [!INCLUDE[TLA#tla_ui](../../../../includes/tlasharptla-ui-md.md)] 树中的元素将从其容器中继承 <xref:System.Windows.FrameworkElement.FlowDirection%2A>。  在下面的示例中，<xref:System.Windows.Controls.TextBlock> 位于 <xref:System.Windows.Controls.Grid> 中，而后者位于 <xref:System.Windows.Window> 中。  为 <xref:System.Windows.Window> 设置 <xref:System.Windows.FrameworkElement.FlowDirection%2A> 属性意味着同时也会为 <xref:System.Windows.Controls.Grid> 和 <xref:System.Windows.Controls.TextBlock> 设置该属性。  
  
 下面的示例演示如何设置 <xref:System.Windows.FrameworkElement.FlowDirection%2A>。  
  
 [!code-xml[FlowDirection#FlowDirection](../../../../samples/snippets/csharp/VS_Snippets_Wpf/FlowDirection/CS/Window1.xaml#flowdirection)]  
  
 顶级 <xref:System.Windows.Window> 具有 <xref:System.Windows.FlowDirection> <xref:System.Windows.FlowDirection> 属性，因此它所包含的所有元素也都继承同一 <xref:System.Windows.FrameworkElement.FlowDirection%2A>。  对于要重写指定 <xref:System.Windows.FrameworkElement.FlowDirection%2A> 的元素，它必须添加显式方向更改，如上一示例中的第二个 <xref:System.Windows.Controls.TextBlock>，该控件将更改为 <xref:System.Windows.FlowDirection>。  如果没有定义 <xref:System.Windows.FrameworkElement.FlowDirection%2A>，则会应用默认的 <xref:System.Windows.FlowDirection>。  
  
 下图显示了上一示例的输出。  
  
 **阐释显式分配了 FlowDirection 的图形**  
  
 ![流方向图](../../../../docs/framework/wpf/advanced/media/flowdir.png "FlowDir")  
  
<a name="FlowDocument"></a>   
## FlowDocument  
 许多开发平台（如 [!INCLUDE[TLA#tla_html](../../../../includes/tlasharptla-html-md.md)]、[!INCLUDE[TLA#tla_win32](../../../../includes/tlasharptla-win32-md.md)] 和 Java）都特意支持双向内容开发。  诸如 [!INCLUDE[TLA#tla_html](../../../../includes/tlasharptla-html-md.md)] 的标记语言为内容编写器提供了在任意所需方向显示文本时必需的标记，如 [!INCLUDE[TLA#tla_html](../../../../includes/tlasharptla-html-md.md)] 4.0 标记、采用“rtl”或“ltr”作为值的“dir”等。  此标记与 <xref:System.Windows.FrameworkElement.FlowDirection%2A> 属性类似，但 <xref:System.Windows.FrameworkElement.FlowDirection%2A> 属性使用了一种更高级的方法来设置文本内容的布局，并可用于除文本以外的内容。  
  
 在 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 中，<xref:System.Windows.Documents.FlowDocument> 是一种多功能 [!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)] 元素，可承载文本、表、图像和其他元素的组合。  以下各部分中的示例将使用此元素。  
  
 可以使用多种方法将文本添加到 <xref:System.Windows.Documents.FlowDocument> 中。  其中一种简单方法就是使用 <xref:System.Windows.Documents.Paragraph>，它是用于对文本等内容进行分组的块级元素。  为了将文本添加到内联级元素，这些示例使用了 <xref:System.Windows.Documents.Span> 和 <xref:System.Windows.Documents.Run>。  <xref:System.Windows.Documents.Span> 是用于对其他内联元素进行分组的内联级流内容元素，而 <xref:System.Windows.Documents.Run> 是用于包含一系列无格式文本的内联级流内容元素。  <xref:System.Windows.Documents.Span> 可包含多个 <xref:System.Windows.Documents.Run> 元素。  
  
 第一个文档示例包含的文档具有很多个网络共享名；例如 `\\server1\folder\file.ext`。  无论此网络链接是包含在阿拉伯语文档还是英语文档中，您始终希望用相同的方式显示它。  下图显示了阿拉伯语 <xref:System.Windows.FlowDirection> 文档中的该链接。  
  
 **阐释如何使用 Span 元素的图形**  
  
 ![从右向左显示的文档](../../../../docs/framework/wpf/advanced/media/flowdocument.png "FlowDocument")  
  
 由于文本是 <xref:System.Windows.FlowDirection>，因此所有特殊字符（如“\\”）都按从右到左的顺序分隔文本。  这会导致无法按正确顺序显示该链接。若要解决此问题，必须嵌入文本以保留单独的按 <xref:System.Windows.FlowDirection> 流动的 <xref:System.Windows.Documents.Run>。  除了为每种语言提供单独的 <xref:System.Windows.Documents.Run> 之外，还可使用一种更好的方法来解决此问题，就是将不常用的英语文本嵌入到较大的阿拉伯语 <xref:System.Windows.Documents.Span> 中。  
  
 下图阐释了这一点。  
  
 **阐释如何使用 Span 元素中嵌入的 Run 元素的图形**  
  
 ![XamlPad 屏幕快照](../../../../docs/framework/wpf/advanced/media/runspan.png "RunSpan")  
  
 下面的示例演示如何在文档中使用 <xref:System.Windows.Documents.Run> 和 <xref:System.Windows.Documents.Span> 元素。  
  
 [!code-xml[RunSpan#RunSpan](../../../../samples/snippets/csharp/VS_Snippets_Wpf/RunSpan/CS/Window1.xaml#runspan)]  
  
<a name="SpanElements"></a>   
## Span 元素  
 <xref:System.Windows.Documents.Span> 元素用作具有不同流方向的文本之间的边界分隔符。  即使具有相同流方向的 <xref:System.Windows.Documents.Span> 元素被视为具有不同的双向范围（这意味着 <xref:System.Windows.Documents.Span> 元素按容器的 <xref:System.Windows.FlowDirection> 排序），也只有 <xref:System.Windows.Documents.Span> 元素中的内容才遵循 <xref:System.Windows.Documents.Span> 的 <xref:System.Windows.FlowDirection>。  
  
 下图显示了若干 <xref:System.Windows.Controls.TextBlock> 元素的流方向。  
  
 **阐释若干 TextBlock 元素中的 FlowDirection 的图形**  
  
 ![具有不同流方向的文本块](../../../../docs/framework/wpf/advanced/media/span.png "Span")  
  
 下面的示例演示如何使用 <xref:System.Windows.Documents.Span> 和 <xref:System.Windows.Documents.Run> 元素生成上图中显示的结果。  
  
 [!code-xml[Span#Span](../../../../samples/snippets/csharp/VS_Snippets_Wpf/Span/CS/Window1.xaml#span)]  
  
 在该示例的 <xref:System.Windows.Controls.TextBlock> 元素中，<xref:System.Windows.Documents.Span> 元素按父级的 <xref:System.Windows.FlowDirection> 进行布局，而每个 <xref:System.Windows.Documents.Span> 元素中的文本则按其自己的 <xref:System.Windows.FlowDirection> 流动。  这适用于拉丁语和阿拉伯语，也适用于任何其他语言。  
  
### 添加 xml:lang  
 下图显示了另一个示例，此示例使用数字和算术表达式，如 `"200.0+21.4=221.4"`。  请注意，此示例仅设置了 <xref:System.Windows.FlowDirection>。  
  
 **仅使用 FlowDirection 显示数字的图形**  
  
 ![从右向左显示的数字](../../../../docs/framework/wpf/advanced/media/langattribute.png "LangAttribute")  
  
 此应用程序的用户会对输出感到失望，因为即使 <xref:System.Windows.FlowDirection> 正确，这些数字的形状也不同于正常的阿拉伯数字。  
  
 XAML 元素可包含 [!INCLUDE[TLA#tla_xml](../../../../includes/tlasharptla-xml-md.md)] 特性（`xml:lang`），该特性指定每个元素的语言。  XAML 还支持 [!INCLUDE[TLA2#tla_xml](../../../../includes/tla2sharptla-xml-md.md)] 语言原则，供子元素使用应用于树中父元素的 `xml:lang` 值。  在上一示例中，由于没有为 <xref:System.Windows.Documents.Run> 元素或其任何顶级元素定义语言，因此使用了默认语言 `xml:lang`，即 XML 中的 `en-US`。  [!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)] 的内部数字形状算法用相应的语言（在此示例中为英语）选择数字。  若要正确呈现阿拉伯数字，需要设置 `xml:lang`。  
  
 下图显示了添加了 `xml:lang` 的示例。  
  
 **阐释如何使用 xml:lang 特性的图形**  
  
 ![从右向左显示的阿拉伯数字](../../../../docs/framework/wpf/advanced/media/langattribute2.png "LangAttribute2")  
  
 下面的示例将 `xml:lang` 添加到应用程序中。  
  
 [!code-xml[LangAttribute#LangAttribute](../../../../samples/snippets/csharp/VS_Snippets_Wpf/LangAttribute/CS/Window1.xaml#langattribute)]  
  
 请注意，许多语言根据目标区域会有不同的 `xml:lang` 值；例如，`"ar-SA"` 和 `"ar-EG"` 表示阿拉伯语的两个变体。  上面几个示例阐释需要同时定义 `xml:lang` 和 <xref:System.Windows.FlowDirection> 值。  
  
<a name="FlowDirectionNontext"></a>   
## 针对非文本元素使用 FlowDirection  
 <xref:System.Windows.FlowDirection> 不仅定义文本在文本元素中流动的方式，而且还定义了几乎所有其他 [!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)] 元素的流方向。  下图显示了一个 <xref:System.Windows.Controls.ToolBar>，该控件可使用水平 <xref:System.Windows.Media.LinearGradientBrush> 绘制其背景。  
  
 **显示使用从左到右渐变的工具栏的图形**  
  
 ![渐变屏幕快照](../../../../docs/framework/wpf/advanced/media/gradient.png "Gradient")  
  
 在将 <xref:System.Windows.FlowDirection> 设置为 <xref:System.Windows.FlowDirection> 后，不仅 <xref:System.Windows.Controls.ToolBar> 按钮是从右到左排列的，甚至 <xref:System.Windows.Media.LinearGradientBrush> 也将其偏移量重新调整为从右到左流动。  
  
 下图显示了重新调整 <xref:System.Windows.Media.LinearGradientBrush> 后的结果。  
  
 **显示使用从右到左渐变的工具栏的图形**  
  
 ![从右向左显示的渐变](../../../../docs/framework/wpf/advanced/media/gradient2-wpf.png "Gradient2\_WPF")  
  
 下面的示例绘制一个 <xref:System.Windows.FlowDirection> <xref:System.Windows.Controls.ToolBar>。  （若要从左到右绘制它，请移除 <xref:System.Windows.Controls.ToolBar> 上的 <xref:System.Windows.FlowDirection> 特性。）  
  
 [!code-xml[Gradient#Gradient](../../../../samples/snippets/csharp/VS_Snippets_Wpf/Gradient/CS/Window1.xaml#gradient)]  
  
<a name="FlowDirectionExceptions"></a>   
### FlowDirection 异常  
 在有些情况下，<xref:System.Windows.FlowDirection> 可能会发生意外行为。  本部分介绍了其中的两种异常。  
  
 **Image**  
  
 <xref:System.Windows.Controls.Image> 表示显示图像的控件。  在 [!INCLUDE[TLA#tla_titlexaml](../../../../includes/tlasharptla-titlexaml-md.md)] 中，该控件可与 <xref:System.Windows.Controls.Image.Source%2A> 属性一起使用，而该属性定义要显示的 <xref:System.Windows.Controls.Image> 的[!INCLUDE[TLA#tla_uri](../../../../includes/tlasharptla-uri-md.md)]。  
  
 与其他 [!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)] 元素不同，<xref:System.Windows.Controls.Image> 不从容器继承 <xref:System.Windows.FlowDirection>。  但如果将 <xref:System.Windows.FlowDirection> 显式设置为 <xref:System.Windows.FlowDirection>，则会以水平翻转的方式显示 <xref:System.Windows.Controls.Image>。  这可作为一种便捷功能提供给双向内容的开发人员，因为在某些情况下，水平翻转图像会达到所需的效果。  
  
 下图显示了一个翻转的 <xref:System.Windows.Controls.Image>。  
  
 **阐释翻转图像的图形**  
  
 ![XamlPad 屏幕快照](../../../../docs/framework/wpf/advanced/media/image.png "Image")  
  
 下面的示例演示 <xref:System.Windows.Controls.Image> 无法从包含它的 <xref:System.Windows.Controls.StackPanel> 中继承 <xref:System.Windows.FlowDirection>。  **注意** 若要运行此示例，C:\\ 驱动器上必须存在一个名为 **ms\_logo.jpg** 的文件。  
  
 [!code-xml[Image#Image](../../../../samples/snippets/csharp/VS_Snippets_Wpf/Image/CS/Window1.xaml#image)]  
  
 **注意** 下载文件中包含 **ms\_logo.jpg** 文件。  此代码假定 .jpg 文件不在您的项目中，而是位于 C:\\ 驱动器下的某个位置。  您必须将项目文件中的 .jpg 文件复制到 C:\\ 驱动器下，或者更改代码以查找项目中的文件。  为此，需要将 `Source="file://c:/ms_logo.jpg"` 更改为 `Source="ms_logo.jpg"`。  
  
 **Path**  
  
 除了 <xref:System.Windows.Controls.Image> 之外，还有一个值得关注的元素 <xref:System.Windows.Shapes.Path>。  Path 是一个对象，可用于绘制一系列相互连接的直线和曲线。  就其 <xref:System.Windows.FlowDirection> 而言，它的行为方式与 <xref:System.Windows.Controls.Image> 类似；例如，它的 <xref:System.Windows.FlowDirection> <xref:System.Windows.FlowDirection> 是它的 <xref:System.Windows.FlowDirection> 图像的水平镜像。  但与 <xref:System.Windows.Controls.Image> 不同的是，<xref:System.Windows.Shapes.Path> 从容器继承其 <xref:System.Windows.FlowDirection>，因此用户无需显式指定它。  
  
 下面的示例使用 3 个线条绘制简单箭头。  第一个箭头从 <xref:System.Windows.Controls.StackPanel> 继承 <xref:System.Windows.FlowDirection> 流方向，以便从右侧的根处测量其起点和终点。  具有显式 <xref:System.Windows.FlowDirection> <xref:System.Windows.FlowDirection> 的第二个箭头也从右侧开头。  但第三个箭头的起始根位于左侧。  有关绘制的更多信息，请参见 <xref:System.Windows.Media.LineGeometry> 和 <xref:System.Windows.Media.GeometryGroup>。  
  
 [!code-xml[Paths#Paths](../../../../samples/snippets/csharp/VS_Snippets_Wpf/Paths/CS/Window1.xaml#paths)]  
  
 下图显示了上一示例的输出。  
  
 **阐释使用 Path 元素绘制的箭头的图形**  
  
 ![路径](../../../../docs/framework/wpf/advanced/media/paths.png "Paths")  
  
 <xref:System.Windows.Controls.Image> 和 <xref:System.Windows.Shapes.Path> 这两个示例演示 [!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)] 如何使用 <xref:System.Windows.FlowDirection>。  除了在容器中按特定方向对 [!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)] 元素进行布局之外，<xref:System.Windows.FlowDirection> 还可用于 <xref:System.Windows.Controls.InkPresenter>（在图面上呈现墨迹）、<xref:System.Windows.Media.LinearGradientBrush>、<xref:System.Windows.Media.RadialGradientBrush> 之类的元素。  每当模拟从左到右行为的内容需要从右到左行为（反之亦然）时，[!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)] 就会提供该功能。  
  
<a name="NumberSubstitution"></a>   
## 数字替换  
 一直以来，[!INCLUDE[TLA#tla_mswin](../../../../includes/tlasharptla-mswin-md.md)] 始终通过以下方式支持数字替换：允许对相同数字使用不同区域性形状的表示形式，但同时使这些数字的内部存储形式在不同区域设置之间保持统一；例如，数字虽然以其常见的十六进制值（如 0x40、0x41）存储，但却根据所选的语言进行显示。  
  
 这使应用程序无需将数值从一种语言转换为另一种语言就可对它们进行处理；例如，用户可以在本地化的阿拉伯文 [!INCLUDE[TLA#tla_mswin](../../../../includes/tlasharptla-mswin-md.md)] 中打开 [!INCLUDE[TLA#tla_xl](../../../../includes/tlasharptla-xl-md.md)] 电子表格，并会看到阿拉伯文形状的数字；而在 [!INCLUDE[TLA#tla_mswin](../../../../includes/tlasharptla-mswin-md.md)] 的欧洲版本中打开它，则会看到相同数字的欧洲表示形式。  这对其他符号（如逗号分隔符和百分比符号）来说也是必需的，因为在同一文档中它们通常随数字一起出现。  
  
 [!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)] 沿承了这一传统，并为此功能提供了进一步支持，以允许更多的用户对使用替换的时间和方式进行控制。  虽然此功能适用于任何语言，但它对双向内容尤其有用；由于应用程序可能会在各种区域性下运行，因此针对特定语言来设置数字形状通常是应用程序开发人员所面临的难题。  
  
 <xref:System.Windows.Media.NumberSubstitution.Substitution%2A> 依赖项属性是用来控制在 [!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)] 中如何执行数字替换的核心属性。  <xref:System.Windows.Media.NumberSubstitution> 类指定文本中数字的显示方式，  它有三个定义其行为的公共属性。  下面概括了其中的每个属性。  
  
 **CultureSource：**  
  
 此属性指定确定数字区域性的方式。  它采用以下三个 <xref:System.Windows.Media.NumberCultureSource> 枚举值之一。  
  
-   Override：数字区域性是 <xref:System.Windows.Media.NumberSubstitution.CultureOverride%2A> 属性的区域性。  
  
-   Text：数字区域性是文本运行的区域性。  在标记中，它将为 `xml:lang` 或其别名 `Language` 属性（<xref:System.Windows.FrameworkElement.Language%2A> 或 <xref:System.Windows.FrameworkContentElement.Language%2A>）。  此外，它是派生自 <xref:System.Windows.FrameworkContentElement> 的类的默认属性。  这样的类包括 <xref:System.Windows.Documents.Paragraph?displayProperty=fullName>、<xref:System.Windows.Documents.Table?displayProperty=fullName>、<xref:System.Windows.Documents.TableCell?displayProperty=fullName> 等。  
  
-   User：数字区域性是当前线程的区域性。  此属性是 <xref:System.Windows.FrameworkElement> 的所有子类（如 <xref:System.Windows.Controls.Page>、<xref:System.Windows.Window> 和 <xref:System.Windows.Controls.TextBlock>）的默认属性。  
  
 **CultureOverride**：  
  
 仅当 <xref:System.Windows.Media.NumberSubstitution.CultureSource%2A> 属性设置为 <xref:System.Windows.Media.NumberCultureSource> 时，才使用 <xref:System.Windows.Media.NumberSubstitution.CultureOverride%2A> 属性；否则后一种属性会被忽略。  该属性指定数字区域性。  默认值为 `null`，它将被解释为 en\-US。  
  
 **Substitution**：  
  
 此属性指定要执行的数字替换的类型。  它采用下列 <xref:System.Windows.Media.NumberSubstitutionMethod> 枚举值之一。  
  
-   <xref:System.Windows.Media.NumberSubstitutionMethod>：根据数字区域性的 <xref:System.Globalization.NumberFormatInfo.DigitSubstitution%2A?displayProperty=fullName> 属性确定替换方法。  这是默认值。  
  
-   <xref:System.Windows.Media.NumberSubstitutionMethod>：如果数字区域性为阿拉伯语或波斯语区域性，它将指定数字取决于上下文。  
  
-   <xref:System.Windows.Media.NumberSubstitutionMethod>：数字始终呈现为欧洲数字。  
  
-   <xref:System.Windows.Media.NumberSubstitutionMethod>：使用数字区域性的民族数字（由区域性的 <xref:System.Globalization.CultureInfo.NumberFormat%2A> 指定）呈现数字。  
  
-   <xref:System.Windows.Media.NumberSubstitutionMethod>：使用数字区域性的传统数字呈现数字。  对于大多数区域性，其效果与 <xref:System.Windows.Media.NumberSubstitutionMethod> 相同。  但是，<xref:System.Windows.Media.NumberSubstitutionMethod> 对某些阿拉伯语区域性会产生拉丁数字，而此值对所有阿拉伯语区域性产生阿拉伯数字。  
  
 这些值对双向内容开发人员意味着什么呢？  在多数情况下，开发人员可能仅需要定义 <xref:System.Windows.FlowDirection> 以及每个文本 [!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)] 元素的语言（例如，`Language="ar-SA"`），而 <xref:System.Windows.Media.NumberSubstitution> 逻辑将负责根据正确的 [!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)] 显示这些数字。  下面的示例演示如何在阿拉伯文版本的 [!INCLUDE[TLA#tla_mswin](../../../../includes/tlasharptla-mswin-md.md)] 中运行的 [!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)] 应用程序内使用阿拉伯数字和英文数字。  
  
 [!code-xml[Numbers#Numbers](../../../../samples/snippets/csharp/VS_Snippets_Wpf/Numbers/CS/Window1.xaml#numbers)]  
  
 下图显示了在阿拉伯语版本的 [!INCLUDE[TLA#tla_mswin](../../../../includes/tlasharptla-mswin-md.md)] 中运行时上一示例的输出。  
  
 **演示所显示的阿拉伯数字和英文数字的图形**  
  
 ![具有数字的 XamlPad 屏幕快照](../../../../docs/framework/wpf/advanced/media/numbers.png "Numbers")  
  
 在此示例中，<xref:System.Windows.FlowDirection> 十分重要，因为将 <xref:System.Windows.FlowDirection> 改为设置成 <xref:System.Windows.FlowDirection> 时会产生欧洲数字。  以下各部分讨论了如何在整个文档内统一显示数字。  如果此示例未在 Windows 的阿拉伯文版本中运行，则所有数字都会显示为欧洲数字。  
  
 **定义替换规则**  
  
 在实际的应用程序中，可能需要以编程方式设置 Language。  例如，希望将 `xml:lang` 特性设置为与系统的 [!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)] 所使用的特性相同，或者可能根据应用程序状态更改 Language。  
  
 如果要根据应用程序的状态进行更改，请使用 [!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)] 所提供的其他功能。  
  
 首先，设置应用程序组件的 `NumberSubstitution.CultureSource="Text"`。  使用此设置可确保对于将 "User" 用作默认值的文本元素（如 <xref:System.Windows.Controls.TextBlock>），设置不会来自 [!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)]。  
  
 例如：  
  
||  
|-|  
|`<TextBlock`<br /><br /> `Name="text1" NumberSubstitution.CultureSource="Text">`<br /><br /> `1234+5679=6913`<br /><br /> `</TextBlock>`|  
  
 在相应的 [!INCLUDE[TLA2#tla_lhcshrp](../../../../includes/tla2sharptla-lhcshrp-md.md)] 代码中，设置 `Language` 属性；例如，将该属性设置为 `"ar-SA"`。  
  
||  
|-|  
|`text1.Language =`<br /><br /> `System.Windows.Markup.XmlLanguage.GetLanguage("ar-SA");`|  
  
 如果需要将 `Language` 属性设置为当前用户的 [!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)] 语言，请使用以下代码。  
  
||  
|-|  
|`text1.Language =`<br /><br /> `System.Windows.Markup.XmlLanguage.GetLanguage(`<br /><br /> `System.Globalization.CultureInfo.CurrentUICulture.IetfLanguageTag);`|  
  
 <xref:System.Globalization.CultureInfo.CurrentCulture%2A> 表示当前线程在运行时所使用的当前区域性。  
  
 最后一个 [!INCLUDE[TLA#tla_titlexaml](../../../../includes/tlasharptla-titlexaml-md.md)] 示例应与下面的示例类似。  
  
 [!code-xml[Numbers2#Numbers2](../../../../samples/snippets/csharp/VS_Snippets_Wpf/Numbers2/CS/Window1.xaml#numbers2)]  
  
 最后一个 [!INCLUDE[TLA#tla_cshrp](../../../../includes/tlasharptla-cshrp-md.md)] 示例应与以下类似。  
  
 [!code-csharp[NumbersCSharp#NumbersCSharp](../../../../samples/snippets/csharp/VS_Snippets_Wpf/NumbersCSharp/CSharp/Window1.xaml.cs#numberscsharp)]  
  
 下图针对任一编程语言显示了窗口的外观。  
  
 **显示阿拉伯数字的图形**  
  
 ![阿拉伯数字](../../../../docs/framework/wpf/advanced/media/numbers2.png "Numbers2")  
  
 **使用 Substitution 属性**  
  
 数字替换在 [!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)] 中的工作方式取决于文本元素的 Language 及其 <xref:System.Windows.FlowDirection>。  如果 <xref:System.Windows.FlowDirection> 为从左到右，则会呈现欧洲数字。  但如果数字的前面为阿拉伯语文本或者具有设置为 "ar" 的 Language，并且 <xref:System.Windows.FlowDirection> 为 <xref:System.Windows.FlowDirection>，则会改为呈现阿拉伯数字。  
  
 但在某些情况下，可能需要创建统一的应用；例如，对所有用户呈现欧洲数字。  或者，在具有特定 <xref:System.Windows.Style> 的 <xref:System.Windows.Documents.Table> 单元格中呈现阿拉伯数字。  执行此操作的一种简单方法是使用 <xref:System.Windows.Media.NumberSubstitution.Substitution%2A> 属性。  
  
 在下面的示例中，第一个 <xref:System.Windows.Controls.TextBlock> 没有设置 <xref:System.Windows.Media.NumberSubstitution.Substitution%2A> 属性，因此算法会正常显示阿拉伯数字。  但在第二个 <xref:System.Windows.Controls.TextBlock> 中，Substitution 设置为 European，这会重写呈现阿拉伯数字的默认 Substitution，并且会显示欧洲数字。  
  
 [!code-xml[Numbers3#Numbers3](../../../../samples/snippets/csharp/VS_Snippets_Wpf/Numbers3/CS/Window1.xaml#numbers3)]