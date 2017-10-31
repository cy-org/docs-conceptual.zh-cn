---
title: "位图效果概述 | Microsoft Docs"
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
  - "位图效果"
ms.assetid: 23cb338e-4b59-4b52-b294-96431f9c9568
caps.latest.revision: 34
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 31
---
# 位图效果概述
使用位图效果，设计人员和开发人员可以将可视化效果应用到已呈现的 [!INCLUDE[TLA#tla_wpf](../../../../includes/tlasharptla-wpf-md.md)] 内容。  例如，使用位图效果，您可以轻松地将 <xref:System.Windows.Media.Effects.DropShadowBitmapEffect> 效果或模糊效果应用到图像或按钮。  
  
> [!IMPORTANT]
>  在 [!INCLUDE[net_v40_short](../../../../includes/net-v40-short-md.md)] 或更高版本，<xref:System.Windows.Media.Effects.BitmapEffect> 类已过时。  如果尝试使用 <xref:System.Windows.Media.Effects.BitmapEffect> 类，将会得到过时异常。  <xref:System.Windows.Media.Effects.BitmapEffect> 类的非过时替代项为 <xref:System.Windows.Media.Effects.Effect> 类。  在大多数情况下，<xref:System.Windows.Media.Effects.Effect> 类速度快得多。  
  
   
  
<a name="wpf_effects"></a>   
## WPF 位图效果  
 位图效果（<xref:System.Windows.Media.Effects.BitmapEffect> 对象）是简单的像素处理操作。  位图效果将 <xref:System.Windows.Media.Imaging.BitmapSource> 作为输入并在应用效果（如模糊或投影）之后生成新的 <xref:System.Windows.Media.Imaging.BitmapSource>。  每个位图效果都公开了控制筛选属性的属性，如 <xref:System.Windows.Media.Effects.BlurBitmapEffect> 的 <xref:System.Windows.Media.Effects.BlurBitmapEffect.Radius%2A>。  
  
 在 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 中，可以将效果设置为活动 <xref:System.Windows.Media.Visual> 对象的属性，如 <xref:System.Windows.Controls.Button> 或 <xref:System.Windows.Controls.TextBox>，这是一种特殊情况。  像素处理在运行时应用和呈现。  在这种情况下，呈现时 <xref:System.Windows.Media.Visual> 将自动转换为其等效 <xref:System.Windows.Media.Imaging.BitmapSource>，并作为输入提供给 <xref:System.Windows.Media.Effects.BitmapEffect>。  输出替换 <xref:System.Windows.Media.Visual> 对象的默认呈现行为。  这就是 <xref:System.Windows.Media.Effects.BitmapEffect> 对象强制仅以软件方式呈现 Visual 对象，  （即应用效果时不对 Visual 对象进行硬件加速）的原因。  
  
-   <xref:System.Windows.Media.Effects.BlurBitmapEffect> 模拟看上去离焦的对象。  
  
-   <xref:System.Windows.Media.Effects.OuterGlowBitmapEffect> 围绕对象周边创建颜色光晕。  
  
-   <xref:System.Windows.Media.Effects.DropShadowBitmapEffect> 创建对象后的阴影。  
  
-   <xref:System.Windows.Media.Effects.BevelBitmapEffect> 创建斜面，即根据指定的曲线提高图像表面。  
  
-   <xref:System.Windows.Media.Effects.EmbossBitmapEffect> 创建 <xref:System.Windows.Media.Visual> 的凹凸贴图，以产生一种在人工光源下的深度和纹理效果。  
  
> [!NOTE]
>  [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] 位图效果以软件模式呈现。  应用效果的任何对象都将在软件中呈现。  将位图效果应用于大型 Visual 类或对位图效果的属性进行动画处理时，将最大程度地降低性能。  这并不表示您不能按照这种方式使用位图效果，而是指使用时应谨慎并进行充分的测试，以保证您的用户获得的体验和您预期的一样。  
  
> [!NOTE]
>  [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] 位图效果不支持部分信任执行。  若要使用位图效果，应用程序必须具有完全信任权限。  
  
<a name="applyeffects"></a>   
## 如何应用效果  
 <xref:System.Windows.Media.Effects.BitmapEffect> 是 <xref:System.Windows.Media.Visual> 的一个属性。  因此，将效果应用于诸如 <xref:System.Windows.Controls.Button>、<xref:System.Windows.Controls.Image>、<xref:System.Windows.Media.DrawingVisual> 或 <xref:System.Windows.UIElement> 等 Visual 对象就如同设置属性一样简单。  可以将 <xref:System.Windows.UIElement.BitmapEffect%2A> 设置为单个 <xref:System.Windows.Media.Effects.BitmapEffect> 对象，或可以通过使用 <xref:System.Windows.Media.Effects.BitmapEffectGroup> 对象将多个效果链接在一起。。  
  
 下面的示例演示如何在[!INCLUDE[TLA#tla_xaml](../../../../includes/tlasharptla-xaml-md.md)] 中应用 <xref:System.Windows.Media.Effects.BitmapEffect>。  
  
 [!code-xml[EffectsGallery_snip#BlurSimpleExampleInline](../../../../samples/snippets/csharp/VS_Snippets_Wpf/EffectsGallery_snip/CSharp/blursimpleexample.xaml#blursimpleexampleinline)]  
  
 下面的示例演示如何在代码中应用 <xref:System.Windows.Media.Effects.BitmapEffect>。  
  
 [!code-csharp[EffectsGallery_snip#CodeBehindBlurCodeBehindExampleInline](../../../../samples/snippets/csharp/VS_Snippets_Wpf/EffectsGallery_snip/CSharp/blurcodebehindexample.xaml.cs#codebehindblurcodebehindexampleinline)]  
  
> [!NOTE]
>  将 <xref:System.Windows.Media.Effects.BitmapEffect> 应用到某个布局容器（如 <xref:System.Windows.Controls.DockPanel> 或 <xref:System.Windows.Controls.Canvas>）时，该效果将被应用到该元素或 Visual 类及其所有子元素的可视化树中。  
  
<a name="customeffects"></a>   
## 创建自定义效果  
 [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] 还提供了非托管接口，用于创建可在托管的 [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] 应用程序中使用的自定义效果。  有关创建自定义位图效果的其他参考资料，请参见[非托管 WPF 位图效果](_wibe_lh)文档。  
  
## 请参阅  
 <xref:System.Windows.Media.Effects.BitmapEffectGroup>   
 <xref:System.Windows.Media.Effects.BitmapEffectInput>   
 <xref:System.Windows.Media.Effects.BitmapEffectCollection>   
 [Unmanaged WPF Bitmap Effect](_wibe_lh)   
 [图像处理概述](../../../../docs/framework/wpf/graphics-multimedia/imaging-overview.md)   
 [安全性](../../../../docs/framework/wpf/security-wpf.md)   
 [WPF 图形呈现疑难解答](../../../../docs/framework/wpf/graphics-multimedia/wpf-graphics-rendering-overview.md)   
 [二维图形和图像处理](../../../../docs/framework/wpf/advanced/optimizing-performance-2d-graphics-and-imaging.md)