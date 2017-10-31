---
title: "WPF 中的版式 | Microsoft Docs"
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
  - "版式, 关于版式"
ms.assetid: 06cbf17b-6eff-4fe5-949d-2dd533e4e1f4
caps.latest.revision: 27
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 26
---
# WPF 中的版式
本主题介绍 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 的主要版式功能。  这些功能包括改进的文本呈现质量和性能、[!INCLUDE[TLA#tla_opentype](../../../../includes/tlasharptla-opentype-md.md)] 版式支持、增强的国际文本、增强的字体支持和新的文本应用程序编程接口 \(API\)。  
  
   
  
<a name="Improved_Quality_and_Performance_of_Text"></a>   
## 改进的文本质量和性能  
 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 中的文字通过 [!INCLUDE[TLA#tla_ct](../../../../includes/tlasharptla-ct-md.md)] 技术呈现，该技术增强了文字的清晰度和可读性。  [!INCLUDE[TLA2#tla_ct](../../../../includes/tla2sharptla-ct-md.md)] 是由 [!INCLUDE[TLA#tla_ms](../../../../includes/tlasharptla-ms-md.md)] 开发的一种软件技术，可以改善文字在现有 LCD（液晶显示器，如便携式计算机屏幕、Pocket PC 屏幕和平板显示器）上的可读性。  [!INCLUDE[TLA2#tla_ct](../../../../includes/tla2sharptla-ct-md.md)] 使用亚像素呈现技术，通过使字符对齐到像素的小数倍，以更高的保真度显示文字的真实形状。  额外的分辨率增加了文本显示中细节的清晰度，使其更便于长时间阅读。  [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 中 [!INCLUDE[TLA2#tla_ct](../../../../includes/tla2sharptla-ct-md.md)] 的另一个改进是可以朝 Y 轴方向抗锯齿，使文本字符中的平缓曲线的顶端和底端变得平滑。  有关 [!INCLUDE[TLA2#tla_ct](../../../../includes/tla2sharptla-ct-md.md)] 功能的详细信息，请参见 [ClearType 概述](../../../../docs/framework/wpf/advanced/cleartype-overview.md)。  
  
 ![采用 ClearType y 向抗锯齿的文本](../../../../docs/framework/wpf/advanced/media/typographyinwpf02.png "TypographyInWPF02")  
使用 ClearType Y 轴方向抗锯齿的文本  
  
 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 中的整个文本呈现管道可以是硬件加速管道，但前提是计算机满足所需硬件的最低要求。  不能使用硬件执行的呈现会退回到软件呈现。  硬件加速会影响文本呈现管道的所有阶段 \- 从存储单个标志符号、将标志符号组成标志符号运行、应用效果，到向最终显示输出应用 [!INCLUDE[TLA2#tla_ct](../../../../includes/tla2sharptla-ct-md.md)] 混合算法。  有关硬件加速的更多信息，请参见[图形呈现层](../../../../docs/framework/wpf/advanced/graphics-rendering-tiers.md)。  
  
 ![文本呈现管线示意图](../../../../docs/framework/wpf/advanced/media/typographyinwpf01.png "TypographyInWPF01")  
文本呈现管道的关系图  
  
 另外，动画文本（无论是按字符还是按标志符号进行动画处理）利用由 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 启用的图形硬件功能  来生成平滑的文本动画。  
  
<a name="Rich_Typography"></a>   
## 丰富的版式  
 [!INCLUDE[TLA2#tla_opentype](../../../../includes/tla2sharptla-opentype-md.md)] 字体格式是 [!INCLUDE[TLA#tla_truetype](../../../../includes/tlasharptla-truetype-md.md)] 字体格式的扩展。  [!INCLUDE[TLA2#tla_opentype](../../../../includes/tla2sharptla-opentype-md.md)] 字体格式由 [!INCLUDE[TLA#tla_ms](../../../../includes/tlasharptla-ms-md.md)] 和 Adobe 共同开发，它提供了多种高级版式功能。  <xref:System.Windows.Documents.Typography> 对象公开了 [!INCLUDE[TLA2#tla_opentype](../../../../includes/tla2sharptla-opentype-md.md)] 字体的许多高级功能，如样式备用项和花体。  [!INCLUDE[TLA2#tla_lhsdk](../../../../includes/tla2sharptla-lhsdk-md.md)] 提供了一组具有丰富特色的 [!INCLUDE[TLA2#tla_opentype](../../../../includes/tla2sharptla-opentype-md.md)] 字体示例，如 Pericles 和 Pescadero 字体。  有关更多信息，请参见[示例 OpenType 字体包](../../../../docs/framework/wpf/advanced/sample-opentype-font-pack.md)。  
  
 Pericles [!INCLUDE[TLA2#tla_opentype](../../../../includes/tla2sharptla-opentype-md.md)] 字体包含其他标志符号，这些标志符号为标准的标志符号集提供样式备用项。  下面的文本显示了备用样式标志符号。  
  
 ![使用 OpenType 样式备用标志符号的文本](../../../../docs/framework/wpf/advanced/media/opentypefont02.png "opentypefont02")  
使用备用 OpenType 样式标志符号的文本  
  
 花体是使用精美修饰艺术的标志符号，通常与书法关联。  下面的文本显示了 Pescadero 字体的标准标志符号和花体标志符号。  
  
 ![使用 OpenType 标准和花体连字的文本](../../../../docs/framework/wpf/advanced/media/opentypefont08.png "opentypefont08")  
使用 OpenType 标准标志符号和 OpenType 花体标志符号的文本  
  
 有关 [!INCLUDE[TLA2#tla_opentype](../../../../includes/tla2sharptla-opentype-md.md)] 功能的详细信息，请参见 [OpenType 字体功能](../../../../docs/framework/wpf/advanced/opentype-font-features.md)。  
  
<a name="Enhanced_International_Text_Support"></a>   
## 增强的国际文本支持  
 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 通过提供下列功能来提供增强的国际文本支持：  
  
-   使用自适应测量功能，在所有书写系统中实现自动行距调整。  
  
-   对国际文本的广泛支持。  有关更多信息，请参见 [WPF 的全球化](../../../../docs/framework/wpf/advanced/globalization-for-wpf.md)。  
  
-   根据不同的语言进行分行、连字和对齐。  
  
<a name="Enhanced_Font_Support"></a>   
## 增强的字体支持  
 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 通过提供下列功能来提供增强的字体支持：  
  
-   所有文本均采用 Unicode。  字体行为和选择不再需要字符集或代码页。  
  
-   字体行为与全局设置（如系统区域设置）无关。  
  
-   独立的 <xref:System.Windows.FontWeight>、<xref:System.Windows.FontStretch> 和 <xref:System.Windows.FontStyle> 类型用于定义 <xref:System.Windows.Media.FontFamily>，  因此其灵活性高于 [!INCLUDE[TLA#tla_win32](../../../../includes/tlasharptla-win32-md.md)] 编程（在这种编程环境中，将使用斜体和粗体的布尔组合来定义字体系列）。  
  
-   在处理书写方向（横向与纵向）时不受字体名称的影响。  
  
-   使用复合字体技术，在可移植 [!INCLUDE[TLA#tla_xml](../../../../includes/tlasharptla-xml-md.md)] 文件中链接和回退字体。  使用复合字体可以构造全面的多语言字体。  复合字体还提供一种可避免显示缺失标志符号的机制。  有关更多信息，请参见 <xref:System.Windows.Media.FontFamily> 类中的备注。  
  
-   使用一组单语言字体，根据复合字体生成国际字体。  在开发多语言字体时，该功能可节省资源成本。  
  
-   在文档中嵌入复合字体，从而能够提供文档可移植性。  有关更多信息，请参见 <xref:System.Windows.Media.FontFamily> 类中的备注。  
  
<a name="New_Text_APIs"></a>   
## 新的文本应用程序编程接口 \(API\)  
 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 提供了多个文本 [!INCLUDE[TLA2#tla_api#plural](../../../../includes/tla2sharptla-apisharpplural-md.md)]，开发人员可以使用它们在其应用程序中包括文本。  这些 [!INCLUDE[TLA2#tla_api#plural](../../../../includes/tla2sharptla-apisharpplural-md.md)] 按以下三个类别进行分组：  
  
-   **布局和用户界面**。  [!INCLUDE[TLA#tla_gui](../../../../includes/tlasharptla-gui-md.md)] 的常见文本控件。  
  
-   **轻量文本绘制**。  允许您直接在对象上绘制文本。  
  
-   **高级文本格式**。  允许您实现自定义文本引擎。  
  
### 布局和用户界面  
 文本 [!INCLUDE[TLA2#tla_api#plural](../../../../includes/tla2sharptla-apisharpplural-md.md)] 是最高级的功能，它提供常见的[!INCLUDE[TLA#tla_ui](../../../../includes/tlasharptla-ui-md.md)] 控件，如 <xref:System.Windows.Controls.Label>、<xref:System.Windows.Controls.TextBlock> 和 <xref:System.Windows.Controls.TextBox>。  这些控件提供应用程序中的基本 [!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)] 元素，并提供一种表示文本和与文本交互的简便方法。  <xref:System.Windows.Controls.RichTextBox> 和 <xref:System.Windows.Controls.PasswordBox> 等控件启用了更高级或更专业的文本处理。  <xref:System.Windows.Documents.TextRange>、<xref:System.Windows.Documents.TextSelection> 和 <xref:System.Windows.Documents.TextPointer> 等类启用了有用的文本操作。  这些 [!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)] 控件提供 <xref:System.Windows.Controls.Control.FontFamily%2A>、<xref:System.Windows.Controls.Control.FontSize%2A> 和 <xref:System.Windows.Controls.Control.FontStyle%2A> 等属性，用于控制呈现文本时使用的字体。  
  
#### 使用位图效果、转换和文本效果  
 通过 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]，可以借助位图效果、转换和文本效果等功能，来创建悦目的文本用法。  下面的示例显示了应用于文本的典型类型的投影效果。  
  
 ![Softness 为 0.25 的文本阴影](../../../../docs/framework/wpf/advanced/media/shadowtext01.png "ShadowText01")  
使用了投影的文本  
  
 下面的示例显示了应用于文本的投影效果和噪音。  
  
 ![有噪音的文本阴影](../../../../docs/framework/wpf/advanced/media/shadowtext04.png "ShadowText04")  
使用了投影和噪音的文本  
  
 下面的示例显示了应用于文本的外部发光效果。  
  
 ![使用 OuterGlowBitmapEffect 的文本阴影](../../../../docs/framework/wpf/advanced/media/shadowtext05.png "ShadowText05")  
使用了外部发光效果的文本  
  
 下面的示例演示应用于文本的模糊效果。  
  
 ![使用 BlurBitmapEffect 的文本阴影](../../../../docs/framework/wpf/advanced/media/shadowtext06.png "ShadowText06")  
使用了模糊效果的文本  
  
 下面的示例演示三行文本，将第一行文本沿着 X 轴放大 150% 得到第二行文本，沿着 Y 轴放大 150% 得到第三行文本。  
  
 ![使用 ScaleTransform 缩放的文本](../../../../docs/framework/wpf/advanced/media/transformedtext02.png "TransformedText02")  
使用 ScaleTransform 的文本  
  
 下面的示例演示沿 X 轴扭曲的文本。  
  
 ![使用 SkewTransform 扭曲的文本](../../../../docs/framework/wpf/advanced/media/transformedtext03.png "TransformedText03")  
使用 SkewTransform 的文本  
  
 <xref:System.Windows.Media.TextEffect> 对象是一个帮助器对象，使用该对象可将文本作为文本字符串中的一组或多组字符进行处理。  下面的示例显示了发生旋转的单个字符。  每个字符都将以 1 秒为间隔单独旋转。  
  
 ![旋转文本的文本效果屏幕快照](../../../../docs/framework/wpf/advanced/media/texteffect01.png "TextEffect01")  
旋转文本效果动画示例  
  
#### 使用流文档  
 除了常见的 [!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)] 控件外，[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 还提供用于呈现文本的布局控件 \- <xref:System.Windows.Documents.FlowDocument> 元素。  <xref:System.Windows.Documents.FlowDocument> 元素与 <xref:System.Windows.Controls.DocumentViewer> 元素结合使用时，可为大量具有不同布局要求的文本提供控件。  布局控件通过其他 [!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)] 控件的 <xref:System.Windows.Documents.Typography> 对象和字体相关属性提供对高级版式的访问。  
  
 下面的示例显示了 <xref:System.Windows.Controls.FlowDocumentReader> 中承载的文本内容，该元素支持搜索、导航、分页和内容缩放。  
  
 ![使用 OpenType 字体示例屏幕快照](../../../../docs/framework/wpf/advanced/media/typographyinwpf-03.png "TypographyInWPF\_03")  
FlowDocumentReader 中承载的文本  
  
 有关更多信息，请参见 [WPF 中的文档](../../../../docs/framework/wpf/advanced/documents-in-wpf.md)。  
  
### 轻量文本绘制  
 您可以通过使用 <xref:System.Windows.Media.DrawingContext> 对象的 <xref:System.Windows.Media.DrawingContext.DrawText%2A> 方法直接在 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 对象上绘制文本。  若要使用此方法，请创建一个 <xref:System.Windows.Media.FormattedText> 对象。  使用该对象可以绘制多行文本，对于多行文本中的每个字符可以单独设置格式。  <xref:System.Windows.Media.FormattedText> 对象的功能包含 Win32 API 中 DrawText 标志的许多功能。  另外，<xref:System.Windows.Media.FormattedText> 对象包含省略号支持（当文本超过其边界时，会显示省略号）之类的功能。  下面的示例显示了应用多种格式的文本，其中第二个和第三个单词应用了线性渐变。  
  
 ![使用 FormattedText 对象显示的文本](../../../../docs/framework/wpf/advanced/media/formattedtext01.png "FormattedText01")  
使用 FormattedText 对象显示的文本  
  
 您可以将带有格式的文本转换为 <xref:System.Windows.Media.Geometry> 对象，这样便可以创建其他类型的悦目文本。  例如，可以基于文本字符串的轮廓创建 <xref:System.Windows.Media.Geometry> 对象。  
  
 ![使用线性渐变画笔的文本轮廓](../../../../docs/framework/wpf/advanced/media/outlinedtext02.png "OutlinedText02")  
使用线性渐变画笔的文本轮廓  
  
 下面的几个示例说明了几种通过修改已转换文本的笔画、填充和高光点来创建悦目效果的方法。  
  
 ![对填充和笔画使用不同颜色的文本](../../../../docs/framework/wpf/advanced/media/outlinedtext03.png "OutlinedText03")  
将笔画和填充设置为不同颜色的示例  
  
 ![笔画应用了图像画笔的文本](../../../../docs/framework/wpf/advanced/media/outlinedtext04.png "OutlinedText04")  
应用于笔画的图像画笔的示例  
  
 ![笔画应用了图像画笔的文本](../../../../docs/framework/wpf/advanced/media/outlinedtext05.png "OutlinedText05")  
应用于笔画和高光点的图像画笔的示例  
  
 有关 <xref:System.Windows.Media.FormattedText> 对象的更多信息，请参见 [绘制格式化文本](../../../../docs/framework/wpf/advanced/drawing-formatted-text.md)。  
  
### 高级文本格式  
 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 是最高级的文本 [!INCLUDE[TLA2#tla_api#plural](../../../../includes/tla2sharptla-apisharpplural-md.md)]，它使您能够通过使用 <xref:System.Windows.Media.TextFormatting> 命名空间中的 <xref:System.Windows.Media.TextFormatting.TextFormatter> 对象和其他类型来创建自定义的文本布局。  使用 <xref:System.Windows.Media.TextFormatting.TextFormatter> 和关联类可以实现自定义的文本布局，以支持您为国际文本定义的字符格式、段落样式、换行规则和其他布局功能。  只有在极少数情况下才需要重写默认情况下实现的 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 文本布局支持。  但是，如果要创建文本编辑控件或应用程序，则可能需要非默认的 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 实现。  
  
 与传统文本 [!INCLUDE[TLA#tla_api](../../../../includes/tlasharptla-api-md.md)] 不同的是，<xref:System.Windows.Media.TextFormatting.TextFormatter> 通过一组回调方法来与文本布局客户端交互。  它要求客户端在 <xref:System.Windows.Media.TextFormatting.TextSource> 类的实现中提供这些方法。  下面的关系图说明了客户端应用程序和 <xref:System.Windows.Media.TextFormatting.TextFormatter> 之间的文本布局交互。  
  
 ![文本布局客户端和 TextFormatter 示意图](../../../../docs/framework/wpf/advanced/media/textformatter01.png "TextFormatter01")  
应用程序和 TextFormatter 之间的交互  
  
 有关创建自定义文本布局的详细信息，请参见[高级文本格式设置](../../../../docs/framework/wpf/advanced/advanced-text-formatting.md)。  
  
## 请参阅  
 <xref:System.Windows.Media.FormattedText>   
 <xref:System.Windows.Media.TextFormatting.TextFormatter>   
 [ClearType 概述](../../../../docs/framework/wpf/advanced/cleartype-overview.md)   
 [OpenType 字体功能](../../../../docs/framework/wpf/advanced/opentype-font-features.md)   
 [绘制格式化文本](../../../../docs/framework/wpf/advanced/drawing-formatted-text.md)   
 [高级文本格式设置](../../../../docs/framework/wpf/advanced/advanced-text-formatting.md)   
 [Text](../../../../docs/framework/wpf/advanced/optimizing-performance-text.md)   
 [Microsoft Typography](http://www.microsoft.com/typography/default.mspx)