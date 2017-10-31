---
title: "图像处理概述 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-wpf"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "转换图像"
  - "裁剪图像"
  - "解码图像格式"
  - "显示图像"
  - "编码图像格式"
  - "对图像进行格式解码"
  - "对图像进行格式编码"
  - "图像元数据"
  - "图像, 关于图像处理"
  - "图像处理 API"
  - "元数据, 图像"
  - "使用图像进行绘制"
  - "旋转图像"
  - "拉伸图像"
ms.assetid: 72aad87a-e6f3-4937-94cd-a18b7766e990
caps.latest.revision: 32
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 29
---
# 图像处理概述
本主题介绍 [!INCLUDE[TLA#tla_wic](../../../../includes/tlasharptla-wic-md.md)]。  借助 [!INCLUDE[TLA2#tla_wic](../../../../includes/tla2sharptla-wic-md.md)]，开发人员可以显示、转换图像和设置图像的格式。  
  
   
  
<a name="_wpfImaging"></a>   
## WPF 图像处理组件  
 [!INCLUDE[TLA2#tla_wic](../../../../includes/tla2sharptla-wic-md.md)]使得 [!INCLUDE[TLA#tla_win](../../../../includes/tlasharptla-win-md.md)] 内的图像处理功能得到了极大改进。  以前，图像处理功能（例如在公共控件上显示位图或使用图像）依赖于 [!INCLUDE[TLA#tla_gdi](../../../../includes/tlasharptla-gdi-md.md)] 或 [!INCLUDE[TLA#tla_gdiplus](../../../../includes/tlasharptla-gdiplus-md.md)] 库。  这些 [!INCLUDE[TLA2#tla_api](../../../../includes/tla2sharptla-api-md.md)] 提供了基线图像处理功能，但缺乏诸如编解码器扩展性支持和高保真图像支持之类的功能。  [!INCLUDE[TLA2#tla_wic](../../../../includes/tla2sharptla-wic-md.md)] 旨在克服 [!INCLUDE[TLA2#tla_gdi](../../../../includes/tla2sharptla-gdi-md.md)] 和 [!INCLUDE[TLA2#tla_gdiplus](../../../../includes/tla2sharptla-gdiplus-md.md)] 的缺点，并提供一组新的 [!INCLUDE[TLA2#tla_api](../../../../includes/tla2sharptla-api-md.md)]，用以在应用程序内显示和使用图像。  
  
 有两种方式可以访问 [!INCLUDE[TLA2#tla_wic](../../../../includes/tla2sharptla-wic-md.md)] [!INCLUDE[TLA2#tla_api](../../../../includes/tla2sharptla-api-md.md)]：托管组件和非托管组件。  非托管组件提供以下功能。  
  
-   适用于新的或专用图像格式的扩展性模型。  
  
-   对包括[!INCLUDE[TLA#tla_bmp](../../../../includes/tlasharptla-bmp-md.md)]、[!INCLUDE[TLA#tla_jpegorg](../../../../includes/tlasharptla-jpegorg-md.md)]、[!INCLUDE[TLA#tla_png](../../../../includes/tlasharptla-png-md.md)]、[!INCLUDE[TLA#tla_tiff](../../../../includes/tlasharptla-tiff-md.md)]、[!INCLUDE[TLA#tla_wdp](../../../../includes/tlasharptla-wdp-md.md)]、[!INCLUDE[TLA#tla_gif](../../../../includes/tlasharptla-gif-md.md)] 和图标 \(.ico\) 在内的本机图像格式增强了性能和安全性。  
  
-   高位深图像数据的保留最多 8 位\/通道（32 位\/像素）。  
  
-   非破坏性图像缩放、裁切和旋转。  
  
-   简化的颜色管理  
  
-   支持文件内的专用元数据。  
  
-   托管组件利用非托管基础结构提供图像与其他 [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] 功能（如[!INCLUDE[TLA#tla_ui](../../../../includes/tlasharptla-ui-md.md)]、动画和图形）的无缝集成。  托管组件还可以从 [!INCLUDE[TLA#tla_wpf](../../../../includes/tlasharptla-wpf-md.md)] 图像处理编解码器扩展性模型获益，利用该模型可以自动识别 [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] 应用程序中的新图像格式。  
  
 大部分托管的 [!INCLUDE[TLA2#tla_wic](../../../../includes/tla2sharptla-wic-md.md)] [!INCLUDE[TLA2#tla_api](../../../../includes/tla2sharptla-api-md.md)] 驻留在 <xref:System.Windows.Media.Imaging?displayProperty=fullName> 命名空间中，不过，几个重要的类型（如 <xref:System.Windows.Media.ImageBrush> 和 <xref:System.Windows.Media.ImageDrawing>）都驻留在 <xref:System.Windows.Media?displayProperty=fullName> 命名空间，<xref:System.Windows.Controls.Image> 驻留在 <xref:System.Windows.Controls?displayProperty=fullName> 命名空间。  
  
 本主题提供有关托管组件的其他信息。  有关非托管 [!INCLUDE[TLA2#tla_api](../../../../includes/tla2sharptla-api-md.md)] 的更多信息，请参见[非托管 WPF 图像处理组件](_wic_lh)文档。  
  
<a name="_imageformats"></a>   
## WPF 图像格式  
 编解码器用于对特定媒体格式进行解码或编码。  [!INCLUDE[TLA2#tla_wic](../../../../includes/tla2sharptla-wic-md.md)]包括一个适用于[!INCLUDE[TLA2#tla_bmp](../../../../includes/tla2sharptla-bmp-md.md)]、[!INCLUDE[TLA2#tla_jpeg](../../../../includes/tla2sharptla-jpeg-md.md)]、[!INCLUDE[TLA2#tla_png](../../../../includes/tla2sharptla-png-md.md)]、[!INCLUDE[TLA2#tla_tiff](../../../../includes/tla2sharptla-tiff-md.md)]、[!INCLUDE[TLA2#tla_wdp](../../../../includes/tla2sharptla-wdp-md.md)]、[!INCLUDE[TLA2#tla_gif](../../../../includes/tla2sharptla-gif-md.md)] 和图标图像格式的编解码器。  利用上述每个编解码器，应用程序可以对其各自的图像格式进行解码（ICON 除外）和编码。  
  
 <xref:System.Windows.Media.Imaging.BitmapSource> 是一个重要的类，用于对图像进行解码和编码。  它是 [!INCLUDE[TLA2#tla_wic](../../../../includes/tla2sharptla-wic-md.md)]管线的基本构造块，表示具有特定大小和分辨率的单个不变的像素集。  <xref:System.Windows.Media.Imaging.BitmapSource> 可以是多个帧图像中的单个帧，或者可以是在 <xref:System.Windows.Media.Imaging.BitmapSource> 上执行转换的结果。  它是 [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] 图像处理中使用的许多主要类（如 <xref:System.Windows.Media.Imaging.BitmapFrame>）的父级。  
  
 <xref:System.Windows.Media.Imaging.BitmapFrame> 用于存储图像格式的实际位图数据。  许多图像格式仅支持单一 <xref:System.Windows.Media.Imaging.BitmapFrame>，不过 [!INCLUDE[TLA2#tla_gif](../../../../includes/tla2sharptla-gif-md.md)] 和 [!INCLUDE[TLA2#tla_tiff](../../../../includes/tla2sharptla-tiff-md.md)] 等格式的图像支持每个图像有多个帧。  帧由解码器用作输入数据，并传递到编码器以创建图像文件。  
  
 下面的示例演示如何从 <xref:System.Windows.Media.Imaging.BitmapSource> 创建一个 <xref:System.Windows.Media.Imaging.BitmapFrame> 并将其添加到 [!INCLUDE[TLA2#tla_tiff](../../../../includes/tla2sharptla-tiff-md.md)] 图像。  
  
 [!code-csharp[BitmapFrameExample#10](../../../../samples/snippets/csharp/VS_Snippets_Wpf/BitmapFrameExample/CSharp/BitmapFrame.cs#10)]
 [!code-vb[BitmapFrameExample#10](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/BitmapFrameExample/VB/BitmapFrame.vb#10)]  
  
### 图像格式解码  
 图像解码是指将某种图像格式转换为可以由系统使用的图像数据。  然后，此图像数据可以用于显示、处理或编码为其他格式。  解码器的选择是基于图像格式做出的。  编解码器的选择是自动做出的，除非指定了特定的解码器。  [在 WPF 中显示图像](#_displayingimages)小节中的示例演示了自动解码。  使用非托管 [!INCLUDE[TLA2#tla_wic](../../../../includes/tla2sharptla-wic-md.md)]界面开发并向系统注册的自定义格式解码器会自动加入到解码器选择队列。  这将使得自定义格式可以自动显示在 [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] 应用程序中。  
  
 下面的示例演示使用位图解码器对 [!INCLUDE[TLA2#tla_bmp](../../../../includes/tla2sharptla-bmp-md.md)] 格式的图像进行解码。  
  
 [!code-cpp[BmpBitmapDecoderEncoder#5](../../../../samples/snippets/cpp/VS_Snippets_Wpf/BmpBitmapDecoderEncoder/CPP/anotherfile.cpp#5)]
 [!code-csharp[BmpBitmapDecoderEncoder#5](../../../../samples/snippets/csharp/VS_Snippets_Wpf/BmpBitmapDecoderEncoder/CSharp/BitmapFrame.cs#5)]
 [!code-vb[BmpBitmapDecoderEncoder#5](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/BmpBitmapDecoderEncoder/VB/BitmapFrame.vb#5)]  
  
### 图像格式编码  
 图像编码是指将图像数据转换为特定图像格式的过程。  然后，已编码的图像数据可以用于创建新图像文件。  [!INCLUDE[TLA2#tla_wic](../../../../includes/tla2sharptla-wic-md.md)]为上面介绍的每种图像格式提供编码器。  
  
 下面的示例演示使用编码器保存一个新创建的位图图像。  
  
 [!code-cpp[BmpBitmapDecoderEncoder#3](../../../../samples/snippets/cpp/VS_Snippets_Wpf/BmpBitmapDecoderEncoder/CPP/anotherfile.cpp#3)]
 [!code-csharp[BmpBitmapDecoderEncoder#3](../../../../samples/snippets/csharp/VS_Snippets_Wpf/BmpBitmapDecoderEncoder/CSharp/BitmapFrame.cs#3)]
 [!code-vb[BmpBitmapDecoderEncoder#3](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/BmpBitmapDecoderEncoder/VB/BitmapFrame.vb#3)]  
  
<a name="_displayingimages"></a>   
## 在 WPF 中显示图像  
 可以通过多种方式在 [!INCLUDE[TLA#tla_wpf](../../../../includes/tlasharptla-wpf-md.md)] 应用程序中显示图像。  可以使用 <xref:System.Windows.Controls.Image> 控件显示图像、使用 <xref:System.Windows.Media.ImageBrush> 在可视图面上绘制图像或使用 <xref:System.Windows.Media.ImageDrawing> 绘制图像。  
  
### 使用 Image 控件  
 <xref:System.Windows.Controls.Image> 是一个框架元素，是在应用程序中显示图像的主要方式。  在 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] 中，有两种方式可以使用 <xref:System.Windows.Controls.Image>：特性语法或属性语法。  下面的示例演示如何使用特性语法或属性标记语法来呈现 200 像素宽的图像。  有关特性语法或属性语法的更多信息，请参见[依赖项属性概述](../../../../docs/framework/wpf/advanced/dependency-properties-overview.md)。  
  
 [!code-xml[ImageElementExample_snip#ImageSimpleExampleInlineMarkup](../../../../samples/snippets/csharp/VS_Snippets_Wpf/ImageElementExample_snip/CSharp/ImageSimpleExample.xaml#imagesimpleexampleinlinemarkup)]  
  
 许多示例使用 <xref:System.Windows.Media.Imaging.BitmapImage> 对象引用图像文件。  <xref:System.Windows.Media.Imaging.BitmapImage>是一个为加载 [!INCLUDE[TLA#tla_xaml](../../../../includes/tlasharptla-xaml-md.md)] 而优化的专用 <xref:System.Windows.Media.Imaging.BitmapSource>，并且是一种将图像显示为 <xref:System.Windows.Controls.Image> 控件的 <xref:System.Windows.Controls.Image.Source%2A> 的简便方式。  
  
 下面的示例演示如何使用代码呈现 200 像素宽的图像。  
  
> [!NOTE]
>  <xref:System.Windows.Media.Imaging.BitmapImage> 实现 <xref:System.ComponentModel.ISupportInitialize> 接口，以对多个属性的初始化进行优化。  只能在对象初始化过程中进行属性更改。  调用 <xref:System.Windows.Media.Imaging.BitmapImage.BeginInit%2A> 以表示初始化开始；调用 <xref:System.Windows.Media.Imaging.BitmapImage.EndInit%2A> 以表示初始化结束。  初始化一旦开始之后，将忽略所做的属性更改。  
  
 [!code-csharp[ImageElementExample_snip#ImageSimpleExampleInlineCode1](../../../../samples/snippets/csharp/VS_Snippets_Wpf/ImageElementExample_snip/CSharp/ImageSimpleExample.xaml.cs#imagesimpleexampleinlinecode1)]
 [!code-vb[ImageElementExample_snip#ImageSimpleExampleInlineCode1](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/ImageElementExample_snip/VB/ImageSimpleExample.xaml.vb#imagesimpleexampleinlinecode1)]  
  
#### 旋转、转换和裁切图像  
 通过 [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)]，用户可以使用 <xref:System.Windows.Media.Imaging.BitmapImage> 的属性或使用其他 <xref:System.Windows.Media.Imaging.BitmapSource> 对象（如 <xref:System.Windows.Media.Imaging.CroppedBitmap> 或 <xref:System.Windows.Media.Imaging.FormatConvertedBitmap>）来转换图像。  上述图像转换可以缩放或旋转图像、更改图像的像素格式或裁切图像。  
  
 可以使用 <xref:System.Windows.Media.Imaging.BitmapImage> 的 <xref:System.Windows.Media.Imaging.BitmapImage.Rotation%2A> 属性来执行图像旋转。  旋转只能以 90 度的增量来进行。  在下面的示例中，图像旋转了 90 度。  
  
 [!code-xml[ImageElementExample#TransformedXAML2](../../../../samples/snippets/csharp/VS_Snippets_Wpf/ImageElementExample/CSharp/TransformedImageExample.xaml#transformedxaml2)]  
  
 [!code-csharp[ImageElementExample#TransformedCSharp1](../../../../samples/snippets/csharp/VS_Snippets_Wpf/ImageElementExample/CSharp/TransformedImageExample.xaml.cs#transformedcsharp1)]
 [!code-vb[ImageElementExample#TransformedCSharp1](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/ImageElementExample/VB/TransformedImageExample.xaml.vb#transformedcsharp1)]  
  
 可以使用 <xref:System.Windows.Media.Imaging.FormatConvertedBitmap> 将图像转换为不同的像素格式，如灰度。  在下面的示例中，图像转换为 <xref:System.Windows.Media.PixelFormats.Gray4%2A>。  
  
 [!code-xml[ImageElementExample_snip#ConvertedXAML2](../../../../samples/snippets/csharp/VS_Snippets_Wpf/ImageElementExample_snip/CSharp/FormatConvertedExample.xaml#convertedxaml2)]  
  
 [!code-csharp[ImageElementExample_snip#ConvertedCSharp1](../../../../samples/snippets/csharp/VS_Snippets_Wpf/ImageElementExample_snip/CSharp/FormatConvertedExample.xaml.cs#convertedcsharp1)]
 [!code-vb[ImageElementExample_snip#ConvertedCSharp1](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/ImageElementExample_snip/VB/FormatConvertedExample.xaml.vb#convertedcsharp1)]  
  
 若要裁切图像，可以使用 <xref:System.Windows.Controls.Image> 或 <xref:System.Windows.Media.Imaging.CroppedBitmap> 的 <xref:System.Windows.UIElement.Clip%2A> 属性。  通常情况下，如果您只想调整图像的一部分，则应使用 <xref:System.Windows.UIElement.Clip%2A>。  如果需要编码和保存裁切过的图像，应使用 <xref:System.Windows.Media.Imaging.CroppedBitmap>。  下面的示例使用 <xref:System.Windows.Media.EllipseGeometry> 和 Clip 属性来裁切图像。  
  
 [!code-xml[ImageElementExample_snip#CroppedXAMLUsingClip1](../../../../samples/snippets/csharp/VS_Snippets_Wpf/ImageElementExample_snip/CSharp/CroppedImageExample.xaml#croppedxamlusingclip1)]  
  
 [!code-csharp[ImageElementExample_snip#CroppedCSharpUsingClip1](../../../../samples/snippets/csharp/VS_Snippets_Wpf/ImageElementExample_snip/CSharp/CroppedImageExample.xaml.cs#croppedcsharpusingclip1)]
 [!code-vb[ImageElementExample_snip#CroppedCSharpUsingClip1](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/ImageElementExample_snip/VB/CroppedImageExample.xaml.vb#croppedcsharpusingclip1)]  
  
#### 拉伸图像  
 <xref:System.Windows.Controls.Image.Stretch%2A> 属性控制如何拉伸一个图像以使其填充容器。  <xref:System.Windows.Controls.Image.Stretch%2A> 属性接受以下值（是由 <xref:System.Windows.Media.Stretch> 枚举定义的）：  
  
-   <xref:System.Windows.Media.Stretch>：不会拉伸图像以填充输出区域。  如果图像比输出区域大，则图像将绘制到输出区域，而无法容纳的内容将被剪裁掉。  
  
-   <xref:System.Windows.Media.Stretch>：会拉伸图像以适应输出区域。  由于图像的高度和宽度是独立进行缩放的，因此图像的原始长宽比可能不会保留。  也就是说，为了完全填充输出容器，图像可能会扭曲。  
  
-   <xref:System.Windows.Media.Stretch>：图像进行缩放，以便其完全适应输出区域。  图像的长宽比会保留。  
  
-   <xref:System.Windows.Media.Stretch>：图像会进行缩放，以便在保留图像原始长宽比的同时完全填充输出区域。  
  
 下面的示例将每个可用的 <xref:System.Windows.Media.Stretch> 枚举应用于 <xref:System.Windows.Controls.Image>。  
  
 下面的图像显示示例的输出，演示了不同的 <xref:System.Windows.Controls.Image.Stretch%2A> 设置在应用到图像时的效果。  
  
 ![不同的 TileBrush 拉伸设置](../../../../docs/framework/wpf/graphics-multimedia/media/img-mmgraphics-stretchenum.png "img\_mmgraphics\_stretchenum")  
不同的拉伸设置  
  
 [!code-xml[ImageElementExample_snip#ImageStretchExampleWholePage](../../../../samples/snippets/csharp/VS_Snippets_Wpf/ImageElementExample_snip/CSharp/ImageStretchExample.xaml#imagestretchexamplewholepage)]  
  
### 绘制图像  
 您还可以利用 <xref:System.Windows.Media.Brush> 进行绘制，从而在应用程序中显示图像。  利用画笔，您可以利用任意内容（从简单的纯色到复杂的图案和图像集）绘制 [!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)] 对象。  若要绘制图像，请使用 <xref:System.Windows.Media.ImageBrush>。  <xref:System.Windows.Media.ImageBrush> 是一种 <xref:System.Windows.Media.TileBrush> 类型，用于将其内容定义为位图图像。  <xref:System.Windows.Media.ImageBrush> 显示由其 <xref:System.Windows.Media.ImageBrush.ImageSource%2A> 属性指定的单个图像。  您可以控制图像的拉伸、对齐和平铺方式，从而可以防止失真并生成图案和其他效果。  下图显示了利用 <xref:System.Windows.Media.ImageBrush> 可以实现的几种效果。  
  
 ![ImageBrush 输出示例](../../../../docs/framework/wpf/graphics-multimedia/media/wcpsdk-mmgraphics-imagebrushexamples.png "wcpsdk\_mmgraphics\_imagebrushexamples")  
图像的画笔可以填充形状、控件、文本等  
  
 下面的示例演示如何使用 <xref:System.Windows.Media.ImageBrush> 绘制带图像的按钮的背景。  
  
 [!code-xml[UsingImageBrush#4](../../../../samples/snippets/csharp/VS_Snippets_Wpf/UsingImageBrush/CS/PaintingWithImages.xaml#4)]  
  
 有关 <xref:System.Windows.Media.ImageBrush> 和绘制图像的更多信息，请参见[使用图像、绘图和 Visual 进行绘制](../../../../docs/framework/wpf/graphics-multimedia/painting-with-images-drawings-and-visuals.md)。  
  
<a name="_metadata"></a>   
## 图像元数据  
 某些图像文件包含用于描述文件的内容或特征的元数据。  例如，大多数数码相机创建的图像中包含用于捕获该图像的照相机的品牌和型号的元数据。  每个图像格式处理元数据的方式不同，但 [!INCLUDE[TLA2#tla_wic](../../../../includes/tla2sharptla-wic-md.md)]提供一种统一的方式来为每个支持的图像格式存储和检索元数据。  
  
 对元数据的访问是通过 <xref:System.Windows.Media.Imaging.BitmapSource> 对象的 <xref:System.Windows.Media.Imaging.BitmapSource.Metadata%2A> 属性提供的。  <xref:System.Windows.Media.Imaging.BitmapSource.Metadata%2A> 返回一个 <xref:System.Windows.Media.Imaging.BitmapMetadata> 对象，其中包含该图像所包含的所有元数据。  此数据可以位于一个元数据架构中或位于不同方案的组合中。  [!INCLUDE[TLA2#tla_wic](../../../../includes/tla2sharptla-wic-md.md)]支持以下图像元数据架构：[!INCLUDE[TLA#tla_exif](../../../../includes/tlasharptla-exif-md.md)]、tEXt（PNG 文本数据）、[!INCLUDE[TLA#tla_ifd](../../../../includes/tlasharptla-ifd-md.md)]、[!INCLUDE[TLA#tla_iptc](../../../../includes/tlasharptla-iptc-md.md)] 和[!INCLUDE[TLA#tla_xmp](../../../../includes/tlasharptla-xmp-md.md)]。  
  
 为了简化读取元数据的过程，<xref:System.Windows.Media.Imaging.BitmapMetadata> 提供易于访问的若干命名属性（如 <xref:System.Windows.Media.Imaging.BitmapMetadata.Author%2A>、<xref:System.Windows.Media.Imaging.BitmapMetadata.Title%2A> 和 <xref:System.Windows.Media.Imaging.BitmapMetadata.CameraModel%2A>）。  许多命名属性还可以用于编写元数据。  元数据查询读取器提供对读取元数据的其他支持。  <xref:System.Windows.Media.Imaging.BitmapMetadata.GetQuery%2A> 方法用于检索元数据查询读取器，这是通过提供字符串查询（如 *"\/app1\/exif\/"*）来实现的。  在下面的示例中，<xref:System.Windows.Media.Imaging.BitmapMetadata.GetQuery%2A> 用于获取存储在 *"\/Text\/Description"* 位置中的文本。  
  
 [!code-cpp[BitmapMetadata#GetQuery](../../../../samples/snippets/cpp/VS_Snippets_Wpf/BitMapMetadata/CPP/BitmapMetadata.cpp#getquery)]
 [!code-csharp[BitmapMetadata#GetQuery](../../../../samples/snippets/csharp/VS_Snippets_Wpf/BitMapMetadata/CSharp/BitmapMetadata.cs#getquery)]
 [!code-vb[BitmapMetadata#GetQuery](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/BitMapMetadata/VB/BitmapMetadata.vb#getquery)]  
  
 若要编写元数据，请使用元数据查询编写器。  <xref:System.Windows.Media.Imaging.BitmapMetadata.SetQuery%2A> 包含查询编写器并设置所需的值。  在下面的示例中，<xref:System.Windows.Media.Imaging.BitmapMetadata.SetQuery%2A> 用于编写存储在 *"\/Text\/Description"* 位置中的文本。  
  
 [!code-cpp[BitmapMetadata#SetQuery](../../../../samples/snippets/cpp/VS_Snippets_Wpf/BitMapMetadata/CPP/BitmapMetadata.cpp#setquery)]
 [!code-csharp[BitmapMetadata#SetQuery](../../../../samples/snippets/csharp/VS_Snippets_Wpf/BitMapMetadata/CSharp/BitmapMetadata.cs#setquery)]
 [!code-vb[BitmapMetadata#SetQuery](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/BitMapMetadata/VB/BitmapMetadata.vb#setquery)]  
  
<a name="_extensibility"></a>   
## 编解码器扩展性  
 [!INCLUDE[TLA2#tla_wic](../../../../includes/tla2sharptla-wic-md.md)]的核心功能是用于新图像编解码器的扩展性模型。  通过这些非托管的接口，编解码器开发人员可以将编解码器与 [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] 集成，这样 [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] 应用程序就可以自动使用新的图像格式。  
  
 有关可扩展性 [!INCLUDE[TLA2#tla_api](../../../../includes/tla2sharptla-api-md.md)] 的示例，请参见 [Win32 Sample Codec](http://go.microsoft.com/fwlink/?LinkID=160052)（Win32 示例编解码器）。  此示例演示如何为自定义图像格式创建解码器和编码器。  
  
> [!NOTE]
>  编解码器必须进行数字签名，以便于系统识别。  
  
## 请参阅  
 <xref:System.Windows.Media.Imaging.BitmapSource>   
 <xref:System.Windows.Media.Imaging.BitmapImage>   
 <xref:System.Windows.Controls.Image>   
 <xref:System.Windows.Media.Imaging.BitmapMetadata>   
 [二维图形和图像处理](../../../../docs/framework/wpf/advanced/optimizing-performance-2d-graphics-and-imaging.md)   
 [Win32 Sample Codec](http://go.microsoft.com/fwlink/?LinkID=160052)