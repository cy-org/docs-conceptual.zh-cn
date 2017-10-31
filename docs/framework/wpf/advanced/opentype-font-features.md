---
title: "OpenType 字体功能 | Microsoft Docs"
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
  - "OpenType 字体"
  - "OpenType 字体技术的版式"
  - "OpenType 字体技术"
ms.assetid: 4061a9d1-fe8b-4921-9e17-18ec7d2e3ea2
caps.latest.revision: 38
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 37
---
# OpenType 字体功能
本主题提供的一些主要功能的概述[!INCLUDE[TLA#tla_opentype](../../../../includes/tlasharptla-opentype-md.md)]中的字体技术[!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)]。  
  
   
  
<a name="overview"></a>   
## <a name="opentype-font-format"></a>OpenType 字体格式  
 [!INCLUDE[TLA#tla_opentype](../../../../includes/tlasharptla-opentype-md.md)]字体格式是扩展名为[!INCLUDE[TLA#tla_truetype](../../../../includes/tlasharptla-truetype-md.md)]字体格式，添加对 PostScript 字体数据的支持。 [!INCLUDE[TLA#tla_opentype](../../../../includes/tlasharptla-opentype-md.md)]字体格式由联合开发[!INCLUDE[TLA#tla_ms](../../../../includes/tlasharptla-ms-md.md)]和 Adobe Corporation。 [!INCLUDE[TLA#tla_opentype](../../../../includes/tlasharptla-opentype-md.md)]字体和操作系统服务的支持[!INCLUDE[TLA#tla_opentype](../../../../includes/tlasharptla-opentype-md.md)]字体为用户提供了一种简单方法来安装和使用字体，无论字体包含[!INCLUDE[TLA2#tla_truetype](../../../../includes/tla2sharptla-truetype-md.md)]轮廓或 CFF (PostScript) 轮廓。  
  
 [!INCLUDE[TLA#tla_opentype](../../../../includes/tlasharptla-opentype-md.md)]字体格式可解决以下开发人员挑战︰  
  
-   更广泛的多平台支持。  
  
-   更好地支持国际字符集。  
  
-   更好的保护︰ 字体数据无效。  
  
-   若要使字体分发效率更高的较小文件大小。  
  
-   对高级版式控制更广泛的支持。  
  
> [!NOTE]
>  Windows SDK 包含一组示例[!INCLUDE[TLA#tla_opentype](../../../../includes/tlasharptla-opentype-md.md)]您可以使用的字体[!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)]应用程序。 这些字体提供的大多数功能在本主题的其余部分中所示。 有关详细信息，请参阅[示例 OpenType 字体包](../../../../docs/framework/wpf/advanced/sample-opentype-font-pack.md)。  
  
 请参阅[OpenType 规范](http://go.microsoft.com/fwlink/?LinkId=96731)有关的详细信息[!INCLUDE[TLA#tla_opentype](../../../../includes/tlasharptla-opentype-md.md)]字体格式。  
  
### <a name="advanced-typographic-extensions"></a>高级版式扩展  
 高级版式表格 ([!INCLUDE[TLA#tla_opentype](../../../../includes/tlasharptla-opentype-md.md)]布局表格) 扩展的版本，如果有任何一个功能[!INCLUDE[TLA2#tla_truetype](../../../../includes/tla2sharptla-truetype-md.md)]或 CFF 轮廓。 [!INCLUDE[TLA#tla_opentype](../../../../includes/tlasharptla-opentype-md.md)]布局字体包含扩展的字体的功能，以支持高质量国际版式的其他信息。 大多数[!INCLUDE[TLA#tla_opentype](../../../../includes/tlasharptla-opentype-md.md)]字体公开总数的子集[!INCLUDE[TLA#tla_opentype](../../../../includes/tlasharptla-opentype-md.md)]可用的功能。 [!INCLUDE[TLA#tla_opentype](../../../../includes/tlasharptla-opentype-md.md)]字体提供以下功能。  
  
-   字符和支持连字、 定位格式、 备用项和其他字体替换的标志符号之间的丰富映射。  
  
-   二维定位和字形附件的支持。  
  
-   显式脚本和语言中包含的信息的字体，以便文本处理应用程序可以相应地调整其行为。  
  
 [!INCLUDE[TLA#tla_opentype](../../../../includes/tlasharptla-opentype-md.md)]更详细地介绍布局表["字体文件表"](http://www.microsoft.com/typography/otspec/otff.htm)部分[!INCLUDE[TLA#tla_opentype](../../../../includes/tlasharptla-opentype-md.md)]规范。  
  
 本概述的其余部分介绍的广度和灵活性的直观地关注一些[!INCLUDE[TLA#tla_opentype](../../../../includes/tlasharptla-opentype-md.md)]公开的属性的功能<xref:System.Windows.Documents.Typography>对象。 此对象的详细信息，请参阅[版式类](#typography_class)。  
  
<a name="variants"></a>   
## <a name="variants"></a>变量  
 变体用于呈现不同的版式样式，例如上标和下标。  
  
### <a name="superscripts-and-subscripts"></a>上标和下标  
 <xref:System.Windows.Documents.Typography.Variants%2A>属性允许您设置上标和下标的值[!INCLUDE[TLA#tla_opentype](../../../../includes/tlasharptla-opentype-md.md)]字体。  
  
 下面的文本显示为所使用字体上标。  
  
 ![使用 OpenType 上标的文本](../../../../docs/framework/wpf/advanced/media/opentypefont14.png "opentypefont14")  
使用 OpenType 上标的文本  
  
 下面的标记示例演示如何定义使用的属性的使用字体的上标<xref:System.Windows.Documents.Typography>对象。  
  
 [!code-xml[OpenTypeFontSamples#12](../../../../samples/snippets/csharp/VS_Snippets_Wpf/OpenTypeFontSamples/CS/PageOne.xaml#12)]  
  
 下面的文本显示为所使用字体的下标。  
  
 ![使用 OpenType 下标的文本](../../../../docs/framework/wpf/advanced/media/opentypefont15.png "opentypefont15")  
使用 OpenType 下标的文本  
  
 下面的标记示例演示如何定义使用的属性的使用字体的下标<xref:System.Windows.Documents.Typography>对象。  
  
 [!code-xml[OpenTypeFontSamples#13](../../../../samples/snippets/csharp/VS_Snippets_Wpf/OpenTypeFontSamples/CS/PageOne.xaml#13)]  
  
### <a name="decorative-uses-of-superscripts-and-subscripts"></a>上标和下标的修饰用法  
 您可以使用上标和下标创建混合大小写的文本的修饰效果。 下面的文本显示为所使用字体上标和下标的文本。 请注意首都不会受到影响。  
  
 ![使用 OpenType 上标和下标的文本](../../../../docs/framework/wpf/advanced/media/opentypefont16.png "opentypefont16")  
使用 OpenType 上标和下标的文本  
  
 下面的标记示例演示如何定义上标和下标的字体，使用属性<xref:System.Windows.Documents.Typography>对象。  
  
 [!code-xml[OpenTypeFontSamples#14](../../../../samples/snippets/csharp/VS_Snippets_Wpf/OpenTypeFontSamples/CS/PageOne.xaml#14)]  
  
<a name="capitals"></a>   
## <a name="capitals"></a>大写字母  
 大写字母是一组呈现大写样式的标志符号的文本的版式格式。 通常情况下，当以全大写样式呈现文本时，字母之间的间距可以出现过小，权重和字母过大的比例。 [!INCLUDE[TLA#tla_opentype](../../../../includes/tlasharptla-opentype-md.md)]支持字母大写，包括小型大写字母、 小号大写字母、 标题和大写字母间距的多种样式设置格式。 这些样式设置格式，可以控制大写字母的外观。  
  
 下面的文本显示 Pescadero 字体的样式设置为"SmallCaps"和"AllSmallCaps"的字母后跟的是标准大写字母。 在这种情况下，相同的字体大小适用于所有三个单词。  
  
 ![使用 OpenType 大写字母的文本](../../../../docs/framework/wpf/advanced/media/opentypefont11.png "opentypefont11")  
使用 OpenType 大写字母的文本  
  
 下面的标记示例演示如何定义使用的属性的 Pescadero 字体的大写字母<xref:System.Windows.Documents.Typography>对象。 当使用"SmallCaps"格式时，将忽略任何前导大写字母。  
  
 [!code-xml[OpenTypeFontSamples#9](../../../../samples/snippets/csharp/VS_Snippets_Wpf/OpenTypeFontSamples/CS/PageOne.xaml#9)]  
  
### <a name="titling-capitals"></a>标题大写字母  
 标题大写字母较亮的粗细和比例，旨在提供比普通大写字母更雅致的外观。 标题大写字母通常以较大字体大小用作标题。 下面的文本显示 Pescadero 字体的正常和标题大写字母。 请注意在第二行文本的较大的词干宽度。  
  
 ![使用 OpenType 标题大写字母的文本](../../../../docs/framework/wpf/advanced/media/opentypefont20.png "OpenTypeFont20")  
使用 OpenType 标题大写字母的文本  
  
 下面的标记示例演示如何定义 Pescadero 字体使用的属性的标题大写字母<xref:System.Windows.Documents.Typography>对象。  
  
 [!code-xml[OpenTypeFontSamples#OpenTypeFontSnippet17](../../../../samples/snippets/csharp/VS_Snippets_Wpf/OpenTypeFontSamples/CS/PageOne.xaml#opentypefontsnippet17)]  
  
### <a name="capital-spacing"></a>大写字母间距  
 大写字母间距是一种功能，使您可以在文本中使用全大写字母时提供更多间距。 大写字母形式通常设计为与小写字母混合。 显示美观之间的间距和大写字母和小写字母时可能看起来太紧使用所有字母都大写。 下面的文本显示 Pescadero 字体的普通字母和大写字母间距。  
  
 ![使用 OpenType 大写字母间距的文本](../../../../docs/framework/wpf/advanced/media/opentypefont21.png "OpenTypeFont21")  
使用 OpenType 大写字母间距的文本  
  
 下面的标记示例演示如何定义使用的属性的 Pescadero 字体的大写字母间距<xref:System.Windows.Documents.Typography>对象。  
  
 [!code-xml[OpenTypeFontSamples#OpenTypeFontSnippet18](../../../../samples/snippets/csharp/VS_Snippets_Wpf/OpenTypeFontSamples/CS/PageOne.xaml#opentypefontsnippet18)]  
  
<a name="ligatures"></a>   
## <a name="ligatures"></a>连字  
 连字是为了创建更易读或美观的文本构成的一个标志符号的两个或多个标志符号。 [!INCLUDE[TLA#tla_opentype](../../../../includes/tlasharptla-opentype-md.md)]字体支持连字的四种类型︰  
  
-   **标准连字**。 旨在增强可读性。 标准连字包括"fi"、"fl"和"ff"。  
  
-   **上下文连字**。 旨在通过提供构成连字的字符之间的更好的联接行为来提高可读性。  
  
-   **自由连字**。 设计为装饰，和并非专门设计为便于阅读。  
  
-   **历史连字**。 旨在作为历史记录，以提高可读性并非专门设计。  
  
 下面的文本显示 Pericles 字体的标准连字标志符号。  
  
 ![使用 OpenType 标准连字的文本](../../../../docs/framework/wpf/advanced/media/opentypefont04.png "opentypefont04")  
使用 OpenType 标准连字的文本  
  
 下面的标记示例演示如何定义标准连字的 Pericles 字体使用的属性的标志符号<xref:System.Windows.Documents.Typography>对象。  
  
 [!code-xml[OpenTypeFontSamples#4](../../../../samples/snippets/csharp/VS_Snippets_Wpf/OpenTypeFontSamples/CS/PageOne.xaml#4)]  
  
 下面的文本显示 Pericles 字体的自由连字标志符号。  
  
 ![使用 OpenType 自由连字的文本](../../../../docs/framework/wpf/advanced/media/opentypefont05.png "opentypefont05")  
使用 OpenType 自由连字的文本  
  
 下面的标记示例演示如何定义自由连字的 Pericles 字体使用的属性的标志符号<xref:System.Windows.Documents.Typography>对象。  
  
 [!code-xml[OpenTypeFontSamples#5](../../../../samples/snippets/csharp/VS_Snippets_Wpf/OpenTypeFontSamples/CS/PageOne.xaml#5)]  
  
 默认情况下，[!INCLUDE[TLA#tla_opentype](../../../../includes/tlasharptla-opentype-md.md)]中的字体[!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)]启用标准连字。 例如，如果您使用使用字体，标准连字"fi"、"ff"和"fl"显示为组合的字符标志符号。 请注意，每个标准连字的字符对彼此相连。  
  
 ![使用 OpenType 标准连字的文本](../../../../docs/framework/wpf/advanced/media/opentypefont06.png "opentypefont06")  
使用 OpenType 标准连字的文本  
  
 但是，可以禁用标准连字功能，以便诸如"ff"的标准连字显示为两个单独的标志符号，而不是组合的字符标志符号。  
  
 ![使用已禁用的 OpenType 标准连字的文本](../../../../docs/framework/wpf/advanced/media/opentypefont07.png "opentypefont07")  
使用禁用的 OpenType 标准连字的文本  
  
 下面的标记示例演示如何禁用标准连字的使用的属性的使用字体的标志符号<xref:System.Windows.Documents.Typography>对象。  
  
 [!code-xml[OpenTypeFontSamples#6](../../../../samples/snippets/csharp/VS_Snippets_Wpf/OpenTypeFontSamples/CS/PageOne.xaml#6)]  
  
<a name="swashes"></a>   
## <a name="swashes"></a>连接形式花体  
 花体是修饰性使用精心设计的装饰通常与书法关联的标志符号。 下面的文本显示 Pescadero 字体的标准和花体连字的标志的符号。  
  
 ![使用 opentype 标准和花体连字的文本](../../../../docs/framework/wpf/advanced/media/opentypefont08.png "opentypefont08")  
使用 OpenType 标准和花体连字的文本  
  
 花体通常用作短的说法，例如事件公告中的装饰元素。 下面的文本使用花体强调大写字母的事件的名称。  
  
 ![使用 OpenType 花体的文本](../../../../docs/framework/wpf/advanced/media/opentypefont09.png "opentypefont09")  
使用 OpenType 花体的文本  
  
 下面的标记示例演示如何定义连接形式花体的字体，使用属性<xref:System.Windows.Documents.Typography>对象。  
  
 [!code-xml[OpenTypeFontSamples#7](../../../../samples/snippets/csharp/VS_Snippets_Wpf/OpenTypeFontSamples/CS/PageOne.xaml#7)]  
  
### <a name="contextual-swashes"></a>上下文连接形式花体  
 花体连字标志符号的某些组合可能会导致美观，如相邻字母的重叠下行字母。 使用上下文花体可以使用生成更好的外观的替代花体连字标志符号。 下面的文本应用上下文花体之前和之后显示相同的单词。  
  
 ![使用 OpenType 上下文的连接形式花体的文本](../../../../docs/framework/wpf/advanced/media/opentypefont19.png "OpenTypeFont19")  
使用 OpenType 连接形式花体的文本  
  
 下面的标记示例演示如何定义使用的属性的 Pescadero 字体上下文花体<xref:System.Windows.Documents.Typography>对象。  
  
 [!code-xml[OpenTypeFontSamples#OpenTypeFontSnippet16](../../../../samples/snippets/csharp/VS_Snippets_Wpf/OpenTypeFontSamples/CS/PageOne.xaml#opentypefontsnippet16)]  
  
<a name="alternates"></a>   
## <a name="alternates"></a>备用项  
 替代项是可以替换为标准标志符号的标志符号。 [!INCLUDE[TLA#tla_opentype](../../../../includes/tlasharptla-opentype-md.md)]如下面的示例中使用的 Pericles 字体的字体，可以包含可用于创建不同的文本的外观的备用标志符号。 下面的文本显示 Pericles 字体的标准标志符号。  
  
 ![使用 OpenType 标准标志符号的文本](../../../../docs/framework/wpf/advanced/media/opentypefont01.png "opentypefont01")  
使用 OpenType 标准标志符号的文本  
  
 Pericles[!INCLUDE[TLA#tla_opentype](../../../../includes/tlasharptla-opentype-md.md)]字体包含提供给一组标准的标志符号的样式备用项的其他标志符号。 下面的文本显示样式备用标志符号。  
  
 ![使用 OpenType 样式备用标志符号的文本](../../../../docs/framework/wpf/advanced/media/opentypefont02.png "opentypefont02")  
使用 OpenType 样式备用标志符号的文本  
  
 下面的标记示例演示如何定义使用的属性的 Pericles 字体的样式备用标志符号<xref:System.Windows.Documents.Typography>对象。  
  
 [!code-xml[OpenTypeFontSamples#2](../../../../samples/snippets/csharp/VS_Snippets_Wpf/OpenTypeFontSamples/CS/PageOne.xaml#2)]  
  
 下面的文本显示几个其他样式备用标志符号 Pericles 字体的。  
  
 ![使用 OpenType 样式备用标志符号的文本](../../../../docs/framework/wpf/advanced/media/opentypefont03.png "opentypefont03")  
使用 OpenType 样式备用标志符号的文本  
  
 下面的标记示例演示如何定义这些其他样式备用标志符号。  
  
 [!code-xml[OpenTypeFontSamples#3](../../../../samples/snippets/csharp/VS_Snippets_Wpf/OpenTypeFontSamples/CS/PageOne.xaml#3)]  
  
### <a name="random-contextual-alternates"></a>随机备用连接形式  
 随机备用连接形式提供多种替代标志符号的单个字符。 在实现时与脚本类型的字体，此功能可以通过使用在外观略有差异的随机选择标志符号的一组模拟手写内容。 下面的文本的 Lindsey 字体使用随机备用连接形式。 请注意，字母"a"会稍有不同的外观  
  
 ![使用 OpenType 随机备用连接形式的文本](../../../../docs/framework/wpf/advanced/media/opentypefont23.png "OpenTypeFont23")  
使用 OpenType 随机备用连接形式的文本  
  
 下面的标记示例演示如何定义随机备用连接形式 Lindsey 字体使用的属性的<xref:System.Windows.Documents.Typography>对象。  
  
 [!code-xml[OpenTypeFontSamples#OpenTypeFontSnippet20](../../../../samples/snippets/csharp/VS_Snippets_Wpf/OpenTypeFontSamples/CS/Window1.xaml#opentypefontsnippet20)]  
  
### <a name="historical-forms"></a>历史记录格式  
 历史记录格式是已过去常见的排字约定。 下面的文本显示短语"波士顿，马萨诸塞州"的使用字体使用的标志符号的历史窗体。  
  
 ![使用 OpenType 历史形式的文本](../../../../docs/framework/wpf/advanced/media/opentypefont10.png "opentypefont10")  
使用 OpenType 历史形式的文本  
  
 下面的标记示例演示如何定义使用字体使用的属性的历史记录格式<xref:System.Windows.Documents.Typography>对象。  
  
 [!code-xml[OpenTypeFontSamples#8](../../../../samples/snippets/csharp/VS_Snippets_Wpf/OpenTypeFontSamples/CS/PageOne.xaml#8)]  
  
<a name="numerical_styles"></a>   
## <a name="numerical-styles"></a>数字样式  
 OpenType 字体支持大量可用于在文本中的数字值的功能。  
  
### <a name="fractions"></a>秒的小数部分  
 [!INCLUDE[TLA#tla_opentype](../../../../includes/tlasharptla-opentype-md.md)]字体支持秒的小数部分，包括前面带有斜线和堆积样式。  
  
 下面的文本显示分数使用字体的样式。  
  
 ![文本使用 OpenType 横式分数和竖式分数](../../../../docs/framework/wpf/advanced/media/opentypefont12.png "opentypefont12")  
使用 OpenType 横式分数和竖式分数的文本  
  
 下面的标记示例演示如何定义使用的属性的使用字体的分数样式<xref:System.Windows.Documents.Typography>对象。  
  
 [!code-xml[OpenTypeFontSamples#10](../../../../samples/snippets/csharp/VS_Snippets_Wpf/OpenTypeFontSamples/CS/PageOne.xaml#10)]  
  
### <a name="old-style-numerals"></a>旧样式数字  
 [!INCLUDE[TLA#tla_opentype](../../../../includes/tlasharptla-opentype-md.md)]字体支持旧样式数字格式。 这种格式可用于在不再是标准的样式显示数字。 下面的文本中使用的标准和旧样式数字格式显示 18 世纪日期。  
  
 ![使用 OpenType 旧样式数字的文本](../../../../docs/framework/wpf/advanced/media/opentypefont24.png "OpenTypeFont24")  
使用 OpenType 旧样式数字的文本  
  
 下面的文本显示标准使用字体跟旧样式数字的数字。  
  
 ![使用 OpenType 旧样式数字集的文本](../../../../docs/framework/wpf/advanced/media/opentypefont13.png "opentypefont13")  
使用 OpenType 旧样式数字集的文本  
  
 下面的标记示例演示如何定义使用的属性的使用字体的旧样式数字<xref:System.Windows.Documents.Typography>对象。  
  
 [!code-xml[OpenTypeFontSamples#11](../../../../samples/snippets/csharp/VS_Snippets_Wpf/OpenTypeFontSamples/CS/PageOne.xaml#11)]  
  
### <a name="proportional-and-tabular-figures"></a>比例和表格式数字  
 [!INCLUDE[TLA#tla_opentype](../../../../includes/tlasharptla-opentype-md.md)]字体支持按比例和表格图功能，以使用数字时控制宽度的对齐方式。 比例数字将每个数字视为具有不同的宽度，"1"是窄于"5"。 将表格数字视作等宽的数字，以便它们垂直对齐，这提高了财务类型信息的可读性。  
  
 下面的文本中使用 Miramonte 字体的第一列显示两个比例数字。 请注意宽度数字"5"和"1"之间的差异。 第二列显示相同的两个数值，通过使用表格格式数字功能调整其宽度。  
  
 ![使用 OpenType 比例 & 表格式数字的文本](../../../../docs/framework/wpf/advanced/media/opentypefont22.png "OpenTypeFont22")  
使用 OpenType 比例和表格式数字的文本  
  
 下面的标记示例演示如何定义 Miramonte 字体使用的属性的比例和表格式数字<xref:System.Windows.Documents.Typography>对象。  
  
 [!code-xml[OpenTypeFontSamples#OpenTypeFontSnippet19](../../../../samples/snippets/csharp/VS_Snippets_Wpf/OpenTypeFontSamples/CS/Window1.xaml#opentypefontsnippet19)]  
  
### <a name="slashed-zero"></a>前面带有斜线的零  
 [!INCLUDE[TLA#tla_opentype](../../../../includes/tlasharptla-opentype-md.md)]字体支持前面带有斜线零数字的格式，以强调"O"的字母和数字"0"之间的差异。 前面带有斜线零数字通常用于财务和业务信息中的标识符。  
  
 下面的文本显示使用 Miramonte 字体的示例订单标识符。 第一行使用标准的数字。 第二行使用斜线零数字，以便更易于使用大写字母"O"。  
  
 ![文本使用 OpenType 斜线零数字](../../../../docs/framework/wpf/advanced/media/opentypefont17.png "OpenTypeFont17")  
使用 OpenType 斜线零数字的文本  
  
 下面的标记示例演示如何定义斜线零数字 Miramonte 字体使用的属性的<xref:System.Windows.Documents.Typography>对象。  
  
 [!code-xml[OpenTypeFontSamples#OpenTypeFontSnippet15](../../../../samples/snippets/csharp/VS_Snippets_Wpf/OpenTypeFontSamples/CS/PageOne.xaml#opentypefontsnippet15)]  
  
<a name="typography_class"></a>   
## <a name="typography-class"></a>版式类  
 <xref:System.Windows.Documents.Typography>对象公开的功能集，[!INCLUDE[TLA#tla_opentype](../../../../includes/tlasharptla-opentype-md.md)]字体支持。 通过设置的属性<xref:System.Windows.Documents.Typography>在标记中，您可以轻松地编写文档，从而利用[!INCLUDE[TLA#tla_opentype](../../../../includes/tlasharptla-opentype-md.md)]功能。  
  
 下面的文本显示 Pescadero 字体的样式设置为"SmallCaps"和"AllSmallCaps"的字母后跟的是标准大写字母。 在这种情况下，相同的字体大小适用于所有三个单词。  
  
 ![使用 OpenType 大写字母的文本](../../../../docs/framework/wpf/advanced/media/opentypefont11.png "opentypefont11")  
使用 OpenType 大写字母的文本  
  
 下面的标记示例演示如何定义使用的属性的 Pescadero 字体的大写字母<xref:System.Windows.Documents.Typography>对象。 当使用"SmallCaps"格式时，将忽略任何前导大写字母。  
  
 [!code-xml[OpenTypeFontSamples#9](../../../../samples/snippets/csharp/VS_Snippets_Wpf/OpenTypeFontSamples/CS/PageOne.xaml#9)]  
  
 下面的代码示例完成同样的任务与前面的标记示例。  
  
 [!code-csharp[TypographyCodeSnippets#TypographyCodeSnippet1](../../../../samples/snippets/csharp/VS_Snippets_Wpf/TypographyCodeSnippets/CSharp/Page1.xaml.cs#typographycodesnippet1)]
 [!code-vb[TypographyCodeSnippets#TypographyCodeSnippet1](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/TypographyCodeSnippets/visualbasic/page1.xaml.vb#typographycodesnippet1)]  
  
### <a name="typography-class-properties"></a>版式类属性  
 下表列出了属性、 值和默认设置<xref:System.Windows.Documents.Typography>对象。  
  
|属性|值|默认值|  
|--------------|----------------|-------------------|  
|<xref:System.Windows.Documents.Typography.AnnotationAlternates%2A>|数字值的字节|0|  
|<xref:System.Windows.Documents.Typography.Capitals%2A>|<xref:System.Windows.FontCapitals> |<xref:System.Windows.FontCapitals> |<xref:System.Windows.FontCapitals> |<xref:System.Windows.FontCapitals> |<xref:System.Windows.FontCapitals> |<xref:System.Windows.FontCapitals> |<xref:System.Windows.FontCapitals>|<xref:System.Windows.FontCapitals?displayProperty=fullName>|  
|<xref:System.Windows.Documents.Typography.CapitalSpacing%2A>|<xref:System.Boolean>|`false`|  
|<xref:System.Windows.Documents.Typography.CaseSensitiveForms%2A>|<xref:System.Boolean>|`false`|  
|<xref:System.Windows.Documents.Typography.ContextualAlternates%2A>|<xref:System.Boolean>|`true`|  
|<xref:System.Windows.Documents.Typography.ContextualLigatures%2A>|<xref:System.Boolean>|`true`|  
|<xref:System.Windows.Documents.Typography.ContextualSwashes%2A>|数字值的字节|0|  
|<xref:System.Windows.Documents.Typography.DiscretionaryLigatures%2A>|<xref:System.Boolean>|`false`|  
|<xref:System.Windows.Documents.Typography.EastAsianExpertForms%2A>|<xref:System.Boolean>|`false`|  
|<xref:System.Windows.Documents.Typography.EastAsianLanguage%2A>|<xref:System.Windows.FontEastAsianLanguage> |<xref:System.Windows.FontEastAsianLanguage> |<xref:System.Windows.FontEastAsianLanguage> |<xref:System.Windows.FontEastAsianLanguage> |<xref:System.Windows.FontEastAsianLanguage> |<xref:System.Windows.FontEastAsianLanguage> |<xref:System.Windows.FontEastAsianLanguage> |<xref:System.Windows.FontEastAsianLanguage>|<xref:System.Windows.FontEastAsianLanguage>|<xref:System.Windows.FontEastAsianLanguage>|<xref:System.Windows.FontEastAsianLanguage?displayProperty=fullName>|  
|<xref:System.Windows.Documents.Typography.EastAsianWidths%2A>|<xref:System.Windows.FontEastAsianWidths> |<xref:System.Windows.FontEastAsianWidths> |<xref:System.Windows.FontEastAsianWidths> |<xref:System.Windows.FontEastAsianWidths>|<xref:System.Windows.FontEastAsianWidths> |<xref:System.Windows.FontEastAsianWidths>|<xref:System.Windows.FontEastAsianWidths?displayProperty=fullName>|  
|<xref:System.Windows.Documents.Typography.Fraction%2A>|<xref:System.Windows.FontFraction>|<xref:System.Windows.FontFraction> |<xref:System.Windows.FontFraction>|<xref:System.Windows.FontFraction?displayProperty=fullName>|  
|<xref:System.Windows.Documents.Typography.HistoricalForms%2A>|<xref:System.Boolean>|`false`|  
|<xref:System.Windows.Documents.Typography.HistoricalLigatures%2A>|<xref:System.Boolean>|`false`|  
|<xref:System.Windows.Documents.Typography.Kerning%2A>|<xref:System.Boolean>|`true`|  
|<xref:System.Windows.Documents.Typography.MathematicalGreek%2A>|<xref:System.Boolean>|`false`|  
|<xref:System.Windows.Documents.Typography.NumeralAlignment%2A>|<xref:System.Windows.FontNumeralAlignment>|<xref:System.Windows.FontNumeralAlignment>|<xref:System.Windows.FontNumeralAlignment>|<xref:System.Windows.FontNumeralAlignment?displayProperty=fullName>|  
|<xref:System.Windows.Documents.Typography.NumeralStyle%2A>|<xref:System.Boolean>|<xref:System.Windows.FontNumeralStyle?displayProperty=fullName>|  
|<xref:System.Windows.Documents.Typography.SlashedZero%2A>|<xref:System.Boolean>|`false`|  
|<xref:System.Windows.Documents.Typography.StandardLigatures%2A>|<xref:System.Boolean>|`true`|  
|<xref:System.Windows.Documents.Typography.StandardSwashes%2A>|数值 – 字节|0|  
|<xref:System.Windows.Documents.Typography.StylisticAlternates%2A>|数值 – 字节|0|  
|<xref:System.Windows.Documents.Typography.StylisticSet1%2A>|<xref:System.Boolean>|`false`|  
|<xref:System.Windows.Documents.Typography.StylisticSet2%2A>|<xref:System.Boolean>|`false`|  
|<xref:System.Windows.Documents.Typography.StylisticSet3%2A>|<xref:System.Boolean>|`false`|  
|<xref:System.Windows.Documents.Typography.StylisticSet4%2A>|<xref:System.Boolean>|`false`|  
|<xref:System.Windows.Documents.Typography.StylisticSet5%2A>|<xref:System.Boolean>|`false`|  
|<xref:System.Windows.Documents.Typography.StylisticSet6%2A>|<xref:System.Boolean>|`false`|  
|<xref:System.Windows.Documents.Typography.StylisticSet7%2A>|<xref:System.Boolean>|`false`|  
|<xref:System.Windows.Documents.Typography.StylisticSet8%2A>|<xref:System.Boolean>|`false`|  
|<xref:System.Windows.Documents.Typography.StylisticSet9%2A>|<xref:System.Boolean>|`false`|  
|<xref:System.Windows.Documents.Typography.StylisticSet10%2A>|<xref:System.Boolean>|`false`|  
|<xref:System.Windows.Documents.Typography.StylisticSet11%2A>|<xref:System.Boolean>|`false`|  
|<xref:System.Windows.Documents.Typography.StylisticSet12%2A>|<xref:System.Boolean>|`false`|  
|<xref:System.Windows.Documents.Typography.StylisticSet13%2A>|<xref:System.Boolean>|`false`|  
|<xref:System.Windows.Documents.Typography.StylisticSet14%2A>|<xref:System.Boolean>|`false`|  
|<xref:System.Windows.Documents.Typography.StylisticSet15%2A>|<xref:System.Boolean>|`false`|  
|<xref:System.Windows.Documents.Typography.StylisticSet16%2A>|<xref:System.Boolean>|`false`|  
|<xref:System.Windows.Documents.Typography.StylisticSet17%2A>|<xref:System.Boolean>|`false`|  
|<xref:System.Windows.Documents.Typography.StylisticSet18%2A>|<xref:System.Boolean>|`false`|  
|<xref:System.Windows.Documents.Typography.StylisticSet19%2A>|<xref:System.Boolean>|`false`|  
|<xref:System.Windows.Documents.Typography.StylisticSet20%2A>|<xref:System.Boolean>|`false`|  
|<xref:System.Windows.Documents.Typography.Variants%2A>|<xref:System.Windows.FontVariants>|<xref:System.Windows.FontVariants> |<xref:System.Windows.FontVariants> |<xref:System.Windows.FontVariants> |<xref:System.Windows.FontVariants> |<xref:System.Windows.FontVariants>|<xref:System.Windows.FontVariants?displayProperty=fullName>|  
  
## <a name="see-also"></a>另请参阅  
 <xref:System.Windows.Documents.Typography>   
 [OpenType 规范](http://go.microsoft.com/fwlink/?LinkId=96731)   
 [WPF 中的版式](../../../../docs/framework/wpf/advanced/typography-in-wpf.md)   
 [示例 OpenType 字体包](../../../../docs/framework/wpf/advanced/sample-opentype-font-pack.md)   
 [字体与应用程序一起打包](../../../../docs/framework/wpf/advanced/packaging-fonts-with-applications.md)