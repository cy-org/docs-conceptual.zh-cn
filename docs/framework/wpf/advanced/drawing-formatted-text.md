---
title: "绘制格式化文本 | Microsoft Docs"
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
  - "绘图, 格式化文本"
  - "格式化文本 [WPF]"
  - "文本 [WPF]"
  - "版式, 绘制格式化文本"
ms.assetid: b1d851c1-331c-4814-9964-6fe769db6f1f
caps.latest.revision: 14
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 13
---
# 绘制格式化文本
本主题概述 <xref:System.Windows.Media.FormattedText> 对象的功能。  该对象为在 [!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)] 应用程序中绘制文本提供低级别控制。  
  
   
  
<a name="technology_overview"></a>   
## 技术概述  
 使用 <xref:System.Windows.Media.FormattedText> 对象可以绘制多行文本，且可以单独对该文本中的每个字符设置格式。  下面的示例演示应用了多种格式的文本。  
  
 ![使用 FormattedText 对象显示的文本](../../../../docs/framework/wpf/advanced/media/formattedtext01.png "FormattedText01")  
使用 FormattedText 方法显示的文本  
  
> [!NOTE]
>  对于从 [!INCLUDE[TLA#tla_win32](../../../../includes/tlasharptla-win32-md.md)] API 迁移的开发人员，[Win32 迁移](#win32_migration)一节中的表列出了 [!INCLUDE[TLA#tla_win32](../../../../includes/tlasharptla-win32-md.md)] DrawText 标志和 [!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)] 中的近似等效项。  
  
### 使用格式化文本的原因  
 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 包括多个用于在屏幕中绘制文本的控件。  每个控件都面向不同的方案，并具有自己的功能和限制列表。  通常，当需要支持的文本有限（例如[!INCLUDE[TLA#tla_ui](../../../../includes/tlasharptla-ui-md.md)] 中的简短语句）时，应使用 <xref:System.Windows.Controls.TextBlock> 元素。  当需要支持文本极少时，可以使用 <xref:System.Windows.Controls.Label>。  有关更多信息，请参见 [WPF 中的文档](../../../../docs/framework/wpf/advanced/documents-in-wpf.md)。  
  
 <xref:System.Windows.Media.FormattedText> 对象提供的文本格式设置功能比 [!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)] 文本控件提供的相应功能更强大，并且在要将文本用作装饰元素时很有用。有关更多信息，请参见下一节[将格式化文本转换为几何图形](#converting_formatted_text)。  
  
 此外，<xref:System.Windows.Media.FormattedText> 对象对于创建面向文本的 <xref:System.Windows.Media.DrawingVisual> 派生对象也很有用。  <xref:System.Windows.Media.DrawingVisual> 是一个轻量绘图类，用于呈现形状、图像或文本。  有关更多信息，请参见 [Hit Test Using DrawingVisuals Sample](http://go.microsoft.com/fwlink/?LinkID=159994)（使用 DrawingVisuals 的命中测试示例）。  
  
<a name="using_the_formattedtext_object"></a>   
## 使用 FormattedText 对象  
 若要创建格式化文本，请调用 <xref:System.Windows.Media.FormattedText.%23ctor%2A> 构造函数以创建一个 <xref:System.Windows.Media.FormattedText> 对象。  一旦创建了初始格式化文本字符串，便可以应用某一范围的格式样式。  
  
 使用 <xref:System.Windows.Media.FormattedText.MaxTextWidth%2A> 属性可以将文本约束为特定宽度。  文本将自动换行，以避免超过指定宽度。  使用 <xref:System.Windows.Media.FormattedText.MaxTextHeight%2A> 属性可以将文本约束为特定高度。  超过指定高度的文本将显示一个省略号“…”。  
  
 ![使用 FormattedText 对象显示的文本](../../../../docs/framework/wpf/advanced/media/formattedtext02.png "FormattedText02")  
显示自动换行和省略号的文本  
  
 您可以向一个或多个字符应用多种格式样式。  例如，您可以调用 <xref:System.Windows.Media.FormattedText.SetFontSize%2A> 和 <xref:System.Windows.Media.FormattedText.SetForegroundBrush%2A> 方法来更改文本中前五个字符的格式。  
  
 下面的代码示例创建一个 <xref:System.Windows.Media.FormattedText> 对象，然后向文本应用多种格式化样式。  
  
 [!code-csharp[FormattedTextSnippets#FormattedTextSnippets1](../../../../samples/snippets/csharp/VS_Snippets_Wpf/FormattedTextSnippets/CSharp/Window1.xaml.cs#formattedtextsnippets1)]
 [!code-vb[FormattedTextSnippets#FormattedTextSnippets1](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/FormattedTextSnippets/visualbasic/window1.xaml.vb#formattedtextsnippets1)]  
  
### 字号度量单位  
 如同 [!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)] 应用程序中的其他文本对象，<xref:System.Windows.Media.FormattedText> 对象使用与设备无关的像素作为度量单位。  但是，大多数 [!INCLUDE[TLA#tla_win32](../../../../includes/tlasharptla-win32-md.md)] 应用程序使用磅作为度量单位。  如果您要在 [!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)] 应用程序中以磅为单位显示文本，需要将[!INCLUDE[TLA#tla_dipixel#plural](../../../../includes/tlasharptla-dipixelsharpplural-md.md)]转换为磅。  下面的代码示例演示如何执行该转换。  
  
 [!code-csharp[FormattedTextSnippets#FormattedTextSnippets2](../../../../samples/snippets/csharp/VS_Snippets_Wpf/FormattedTextSnippets/CSharp/Window1.xaml.cs#formattedtextsnippets2)]
 [!code-vb[FormattedTextSnippets#FormattedTextSnippets2](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/FormattedTextSnippets/visualbasic/window1.xaml.vb#formattedtextsnippets2)]  
  
<a name="converting_formatted_text"></a>   
### 将格式化文本转换为几何图形  
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
  
 将文本转换为 <xref:System.Windows.Media.Geometry> 对象时，它不再是字符的集合 \- 您不能修改文本字符串中的字符。  但是，可以修改已转换文本的笔画和填充属性，以此来影响该文本的外观。  笔画指的是已转换文本的轮廓；填充指的是已转换文本的轮廓的内部区域。  有关更多信息，请参见[创建空心文字](../../../../docs/framework/wpf/advanced/how-to-create-outlined-text.md)。  
  
 您还可以将格式化文本转换为 <xref:System.Windows.Media.PathGeometry> 对象，并使用此对象突出显示文本。  例如，您可以将动画应用于 <xref:System.Windows.Media.PathGeometry> 对象，使此动画沿着格式化文本的轮廓显示。  
  
 下面的示例演示已转换为 <xref:System.Windows.Media.PathGeometry> 对象的格式化文本。  经过动画处理的椭圆会沿着所呈现文本的笔画路径显示。  
  
 ![沿着文本路径几何图形运动的球](../../../../docs/framework/wpf/advanced/media/textpathgeometry01.png "TextPathGeometry01")  
沿着文本的路径几何图形显示的球体  
  
 有关更多信息，请参见[How to: Create a PathGeometry Animation for Text](http://msdn.microsoft.com/zh-cn/29f8051e-798a-463f-a926-a099a99e9c67)。  
  
 将格式化文本转换为 <xref:System.Windows.Media.PathGeometry> 对象之后，您可以为其创建其他有趣的用法。  例如，您可以剪辑视频，以便在格式化文本中显示。  
  
 ![文本路径几何图形中的视频显示](../../../../docs/framework/wpf/advanced/media/videotextdemo01.png "VideoTextDemo01")  
在文本的路径几何图形中显示的视频  
  
<a name="win32_migration"></a>   
## Win32 迁移  
 <xref:System.Windows.Media.FormattedText> 用于绘制文本的功能与 [!INCLUDE[TLA#tla_win32](../../../../includes/tlasharptla-win32-md.md)] DrawText 函数的功能相似。  对于从 [!INCLUDE[TLA#tla_win32](../../../../includes/tlasharptla-win32-md.md)] API 迁移的开发人员，下表列出了 [!INCLUDE[TLA#tla_win32](../../../../includes/tlasharptla-win32-md.md)] DrawText 标志和 [!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)] 中的近似等效项。  
  
|DrawText 标志|WPF 等效项|注释|  
|-----------------|-------------|--------|  
|DT\_BOTTOM|<xref:System.Windows.Media.FormattedText.Height%2A>|使用 <xref:System.Windows.Media.FormattedText.Height%2A> 属性可以计算相应的 [!INCLUDE[TLA#tla_win32](../../../../includes/tlasharptla-win32-md.md)] DrawText 的“y”位置。|  
|DT\_CALCRECT|<xref:System.Windows.Media.FormattedText.Height%2A>, <xref:System.Windows.Media.FormattedText.Width%2A>|使用 <xref:System.Windows.Media.FormattedText.Height%2A> 和 <xref:System.Windows.Media.FormattedText.Width%2A> 属性可以计算输出矩形。|  
|DT\_CENTER|<xref:System.Windows.Media.FormattedText.TextAlignment%2A>|使用值设置为 <xref:System.Windows.TextAlignment> 的 <xref:System.Windows.Media.FormattedText.TextAlignment%2A> 属性。|  
|DT\_EDITCONTROL|无|不需要。  间距宽度和最后一行的呈现与在框架编辑控件中相同。|  
|DT\_END\_ELLIPSIS|<xref:System.Windows.Media.FormattedText.Trimming%2A>|使用值为 <xref:System.Windows.TextTrimming> 的 <xref:System.Windows.Media.FormattedText.Trimming%2A> 属性。<br /><br /> 使用 <xref:System.Windows.TextTrimming> 来获取带有 DT\_WORD\_ELIPSIS 尾部省略号的 [!INCLUDE[TLA#tla_win32](../../../../includes/tlasharptla-win32-md.md)] DT\_END\_ELLIPSIS。在该情况下，省略号字符仅出现在无法适合于单个行的字中。|  
|DT\_EXPAND\_TABS|无|不需要。  制表符自动扩展为在每 4 个 em 后停止，这大约为 8 个与语言无关的字符的宽度。|  
|DT\_EXTERNALLEADING|无|不需要。  行距中始终包括外部间隙。  使用 <xref:System.Windows.Media.FormattedText.LineHeight%2A> 属性可以创建用户定义的行距。|  
|DT\_HIDEPREFIX|无|不支持。  在构造 <xref:System.Windows.Media.FormattedText> 对象之前从该字符串中移除“&”。|  
|DT\_LEFT|<xref:System.Windows.Media.FormattedText.TextAlignment%2A>|这是默认文本对齐方式。  使用值设置为 <xref:System.Windows.TextAlignment> 的 <xref:System.Windows.Media.FormattedText.TextAlignment%2A> 属性。  （仅限 WPF）|  
|DT\_MODIFYSTRING|无|不支持。|  
|DT\_NOCLIP|<xref:System.Windows.Media.Visual.VisualClip%2A>|剪辑不会自动发生。  如果要剪辑文本，请使用 <xref:System.Windows.Media.Visual.VisualClip%2A> 属性。|  
|DT\_NOFULLWIDTHCHARBREAK|无|不支持。|  
|DT\_NOPREFIX|无|不需要。  字符串中的“&”字符始终作为正常字符进行处理。|  
|DT\_PATHELLIPSIS|无|使用值为 <xref:System.Windows.TextTrimming> 的 <xref:System.Windows.Media.FormattedText.Trimming%2A> 属性。|  
|DT\_PREFIX|无|不支持。  如果要对文本（例如快捷键或链接）使用下划线，请使用 <xref:System.Windows.Media.FormattedText.SetTextDecorations%2A> 方法。|  
|DT\_PREFIXONLY|无|不支持。|  
|DT\_RIGHT|<xref:System.Windows.Media.FormattedText.TextAlignment%2A>|使用值设置为 <xref:System.Windows.TextAlignment> 的 <xref:System.Windows.Media.FormattedText.TextAlignment%2A> 属性。  （仅限 WPF）|  
|DT\_RTLREADING|<xref:System.Windows.Media.FormattedText.FlowDirection%2A>|将 <xref:System.Windows.Media.FormattedText.FlowDirection%2A> 属性设置为 <xref:System.Windows.FlowDirection>。|  
|DT\_SINGLELINE|无|不需要。  <xref:System.Windows.Media.FormattedText> 对象的行为就像单行控件那样，除非设置了 <xref:System.Windows.Media.FormattedText.MaxTextWidth%2A> 属性或者文本包含回车\/换行 \(CR\/LF\)。|  
|DT\_TABSTOP|无|不支持用户定义的制表位位置。|  
|DT\_TOP|<xref:System.Windows.Media.FormattedText.Height%2A>|不需要。  上对齐是默认设置。  其他垂直定位值可以通过使用 <xref:System.Windows.Media.FormattedText.Height%2A> 属性计算相应的 [!INCLUDE[TLA#tla_win32](../../../../includes/tlasharptla-win32-md.md)] DrawText“y”位置来定义。|  
|DT\_VCENTER|<xref:System.Windows.Media.FormattedText.Height%2A>|使用 <xref:System.Windows.Media.FormattedText.Height%2A> 属性可以计算相应的 [!INCLUDE[TLA#tla_win32](../../../../includes/tlasharptla-win32-md.md)] DrawText 的“y”位置。|  
|DT\_WORDBREAK|无|不需要。  对 <xref:System.Windows.Media.FormattedText> 对象自动断词。  您无法禁用它。|  
|DT\_WORD\_ELLIPSIS|<xref:System.Windows.Media.FormattedText.Trimming%2A>|使用值为 <xref:System.Windows.TextTrimming> 的 <xref:System.Windows.Media.FormattedText.Trimming%2A> 属性。|  
  
## 请参阅  
 <xref:System.Windows.Media.FormattedText>   
 [WPF 中的文档](../../../../docs/framework/wpf/advanced/documents-in-wpf.md)   
 [WPF 中的版式](../../../../docs/framework/wpf/advanced/typography-in-wpf.md)   
 [创建空心文字](../../../../docs/framework/wpf/advanced/how-to-create-outlined-text.md)   
 [How to: Create a PathGeometry Animation for Text](http://msdn.microsoft.com/zh-cn/29f8051e-798a-463f-a926-a099a99e9c67)