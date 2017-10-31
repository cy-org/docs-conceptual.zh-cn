---
title: "GlyphRun 对象和 Glyphs 元素简介 | Microsoft Docs"
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
  - "版式，Glyphs 元素"
  - "Glyphs 元素"
  - "GlyphRun 对象"
  - "文本、 标志符号"
  - "标志符号 [WPF]"
  - "GlyphRun 对象的版式"
ms.assetid: 746ca769-a331-4435-9b95-f72a883b67c1
caps.latest.revision: 21
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 20
---
# GlyphRun 对象和 Glyphs 元素简介
本主题介绍<xref:System.Windows.Media.GlyphRun>对象和<xref:System.Windows.Documents.Glyphs>元素。  
  
   
  
<a name="text_glyphrunovw_intro"></a>   
## <a name="introduction-to-glyphrun"></a>GlyphRun 简介  
 [!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)]提供高级的文本支持，包括具有直接访问权限的标志符号级别标记<xref:System.Windows.Documents.Glyphs>的用户想要截获并保存在格式化后的文本。 这些功能提供关键支持的不同文本呈现要求在每个以下方案。  
  
1.  屏幕上显示的固定格式文档。  
  
2.  打印方案。  
  
    -   [!INCLUDE[TLA#tla_xaml](../../../../includes/tlasharptla-xaml-md.md)]作为设备的打印机语言。  
  
    -   [!INCLUDE[TLA#tla_mxdw](../../../../includes/tlasharptla-mxdw-md.md)]。  
  
    -   以前的打印机驱动程序，从输出[!INCLUDE[TLA#tla_win32](../../../../includes/tlasharptla-win32-md.md)]为固定格式的应用程序。  
  
    -   打印后台处理格式。  
  
3.  固定格式的文档表示形式，包括以前版本的客户端[!INCLUDE[TLA#tla_mswin](../../../../includes/tlasharptla-mswin-md.md)]和其他计算设备。  
  
> [!NOTE]
>  <xref:System.Windows.Documents.Glyphs>和<xref:System.Windows.Media.GlyphRun>旨在用于固定格式的文档演示文稿和打印方案。                      [!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)]为常规布局提供了几个元素和[!INCLUDE[TLA#tla_ui](../../../../includes/tlasharptla-ui-md.md)]方案如<xref:System.Windows.Controls.Label>和<xref:System.Windows.Controls.TextBlock>。 有关详细信息布局和[!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)]方案，请参阅[WPF 中的版式](../../../../docs/framework/wpf/advanced/typography-in-wpf.md)。  
  
<a name="text_glyphrunovw_glyphrunobject"></a>   
## <a name="the-glyphrun-object"></a>GlyphRun 对象  
 <xref:System.Windows.Media.GlyphRun>对象表示从一种字体在一个大小，并且一种呈现样式的单个字体标志符号的序列。  
  
 <xref:System.Windows.Media.GlyphRun>包括这两种字体的详细信息如标志符号<xref:System.Windows.Documents.Glyphs.Indices%2A>和单个标志符号位置。 它还包括原始[!INCLUDE[TLA#tla_unicode](../../../../includes/tlasharptla-unicode-md.md)]码的位从字符标志符号缓冲区偏移量的映射信息，以及每个字符和每个标志符号的标志生成运行。  
  
 <xref:System.Windows.Media.GlyphRun>都有一个相应的高级<xref:System.Windows.FrameworkElement>，<xref:System.Windows.Documents.Glyphs>。                  <xref:System.Windows.Documents.Glyphs>在元素树中，在可以使用[!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)]标记来表示<xref:System.Windows.Media.GlyphRun>输出。  
  
<a name="text_glyphrunovw_glyphselement"></a>   
## <a name="the-glyphs-element"></a>Glyphs 元素  
 <xref:System.Windows.Documents.Glyphs>元素表示的输出<xref:System.Windows.Media.GlyphRun>中[!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)]。 下面的标记语法用于描述<xref:System.Windows.Documents.Glyphs>元素。  
  
 [!code-xml[GlyphsOvwSample1#1](../../../../samples/snippets/csharp/VS_Snippets_Wpf/GlyphsOvwSample1/CS/default.xaml#1)]  
  
 下面的属性定义对应于示例标记中的前四个特性。  
  
|属性|描述|  
|--------------|-----------------|  
|<xref:System.Windows.Documents.Glyphs.FontUri%2A>|指定资源标识符︰ 文件名、 Web [!INCLUDE[TLA#tla_uri](../../../../includes/tlasharptla-uri-md.md)]，或在应用程序.exe 或容器资源引用。|  
|<xref:System.Windows.Documents.Glyphs.FontRenderingEmSize%2A>|在绘图图面 （默认值为.96 英寸） 的单位中指定的字体大小。|  
|<xref:System.Windows.Documents.Glyphs.StyleSimulations%2A>|指定用于粗体和斜体样式的标志。|  
|<xref:System.Windows.Documents.Glyphs.BidiLevel%2A>|指定双向布局级别。 偶数编号，而零值表示从左到右的布局;奇数数目的值表示从右到左布局。|  
  
<a name="text_glyphrunovw_indicesproperty"></a>   
### <a name="indices-property"></a>索引属性  
 <xref:System.Windows.Documents.Glyphs.Indices%2A>属性是一个字符串的字形规范。 其中的标志符号序列形成一个群集，群集中的第一个标志符号的规范的前面有多少个标志符号的规范和多少个代码点结合在一起形成群集。 <xref:System.Windows.Documents.Glyphs.Indices%2A>属性收集在一个字符串中的以下属性。  
  
-   标志符号索引  
  
-   标志符号前进宽度  
  
-   组合标志符号附加向量  
  
-   从代码数据点到字形群集映射  
  
-   标志符号标志  
  
 每个字形规范具有以下形式。  
  
 `[GlyphIndex][,[Advance][,[uOffset][,[vOffset][,[Flags]]]]]`  
  
<a name="text_glyphrunovw_glyphmetrics"></a>   
## <a name="glyph-metrics"></a>标志符号度量值  
 每个字形定义度量值，指定与其他的对齐方式<xref:System.Windows.Documents.Glyphs>。 下图定义了两个不同的标志符号字符的各种版式质量。  
  
 ![标志符号度量示意图](../../../../docs/framework/wpf/advanced/media/glyph-example.png "glyph_example")  
  
<a name="text_glyphrunovw_glyphsmarkup"></a>   
## <a name="glyphs-markup"></a>标志符号标记  
 下面的代码示例演示如何使用的各种属性<xref:System.Windows.Documents.Glyphs>中的元素[!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)]。  
  
 [!code-xml[GlyphsOvwSamp2#1](../../../../samples/snippets/csharp/VS_Snippets_Wpf/GlyphsOvwSamp2/CS/default.xaml#1)]  
  
## <a name="see-also"></a>另请参阅  
 [WPF 中的版式](../../../../docs/framework/wpf/advanced/typography-in-wpf.md)   
 [WPF 中的文档](../../../../docs/framework/wpf/advanced/documents-in-wpf.md)   
 [文本](../../../../docs/framework/wpf/advanced/optimizing-performance-text.md)