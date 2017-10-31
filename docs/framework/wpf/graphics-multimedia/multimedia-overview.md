---
title: "多媒体概述 | Microsoft Docs"
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
  - "媒体"
  - "多媒体"
ms.assetid: feb25b15-d741-4ac3-818f-1b19f63a3562
caps.latest.revision: 19
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 18
---
# 多媒体概述
使用 [!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)] 中的多媒体功能，可以将音频和视频集成到应用程序中，从而增强用户体验。本主题将介绍 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 的多媒体功能。  
  
   
  
<a name="mediaapi"></a>   
## 媒体 API  
 <xref:System.Windows.Controls.MediaElement> 和 <xref:System.Windows.Media.MediaPlayer> 类用于播放音频或视频内容。  这些类可以通过交互方式或通过时钟进行控制。  这些类可在 [!INCLUDE[TLA#tla_wmp](../../../../includes/tlasharptla-wmp-md.md)] 10 控件用于进行媒体播放。使用哪个类取决于具体方案。  
  
 <xref:System.Windows.Controls.MediaElement> 是一个 <xref:System.Windows.UIElement>，它受 [布局](../../../../docs/framework/wpf/advanced/layout.md) 支持并可用作许多控件的内容。  它也可用在[!INCLUDE[TLA#tla_xaml](../../../../includes/tlasharptla-xaml-md.md)] 以及代码中。另一方面，<xref:System.Windows.Media.MediaPlayer> 用于 <xref:System.Windows.Media.Drawing> 对象，因而缺少对布局的支持。  只能使用 <xref:System.Windows.Media.VideoDrawing> 或通过直接与 <xref:System.Windows.Media.DrawingContext> 进行交互来呈现使用 <xref:System.Windows.Media.MediaPlayer> 加载的媒体。  不能在 XAML 中使用 <xref:System.Windows.Media.MediaPlayer>。  
  
 有关绘图对象和绘图上下文的更多信息，请参见 [Drawing 对象概述](../../../../docs/framework/wpf/graphics-multimedia/drawing-objects-overview.md)。  
  
> [!NOTE]
>  在将媒体与应用程序一起分发时，不能将媒体文件用作项目资源。  在项目文件中，必须将媒体类型改设为 `Content`，并将 `CopyToOutputDirectory` 设置为 `PreserveNewest` 或 `Always`。  
  
<a name="mediaplaybackmodes"></a>   
## 媒体播放模式  
  
> [!NOTE]
>  <xref:System.Windows.Controls.MediaElement> 和 <xref:System.Windows.Media.MediaPlayer> 具有类似的成员。  本部分中的链接指的是 <xref:System.Windows.Controls.MediaElement> 类成员。  除非明确说明，否则链接到 <xref:System.Windows.Controls.MediaElement> 类中的成员也可在 <xref:System.Windows.Media.MediaPlayer> 类中找到。  
  
 若要了解 [!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)] 中的媒体播放，需要先了解可播放媒体的不同模式。  <xref:System.Windows.Controls.MediaElement> 和 <xref:System.Windows.Media.MediaPlayer> 可以用于两种不同的媒体模式中：独立模式和时钟模式。  媒体模式由 <xref:System.Windows.Controls.MediaElement.Clock%2A> 属性确定。  如果 <xref:System.Windows.Controls.MediaElement.Clock%2A> 为 `null`，则媒体对象处于独立模式。  如果 <xref:System.Windows.Controls.MediaElement.Clock%2A> 不为 null，则媒体对象处于时钟模式。  默认情况下，媒体对象处于独立模式。  
  
### 独立模式  
 在独立模式下，由媒体内容驱动媒体播放。  独立模式实现了下列功能选项：  
  
-   可直接指定媒体的 <xref:System.Uri>。  
  
-   可直接控制媒体播放。  
  
-   可修改媒体的 <xref:System.Windows.Controls.MediaElement.Position%2A> 和 <xref:System.Windows.Controls.MediaElement.SpeedRatio%2A> 属性。  
  
 通过设置 <xref:System.Windows.Controls.MediaElement> 对象的 <xref:System.Windows.Controls.MediaElement.Source%2A> 属性或者调用 <xref:System.Windows.Media.MediaPlayer> 对象的 <xref:System.Windows.Media.MediaPlayer.Open%2A> 方法来加载媒体。  
  
 若要在独立模式下控制媒体播放，可使用媒体对象的控制方法。  提供了下列控制方法：<xref:System.Windows.Controls.MediaElement.Play%2A>、<xref:System.Windows.Controls.MediaElement.Pause%2A>、<xref:System.Windows.Controls.MediaElement.Close%2A> 和 <xref:System.Windows.Controls.MediaElement.Stop%2A>。  对于 <xref:System.Windows.Controls.MediaElement>，仅当将 <xref:System.Windows.Controls.MediaElement.LoadedBehavior%2A> 设置为 <xref:System.Windows.Controls.MediaState> 时，使用这些方法的交互式控件才可用。  当媒体对象处于时钟模式时，这些方法将不可用。  
  
 有关独立模式的示例，请参见[控制 MediaElement（播放、暂停、停止、音量和速度）](../../../../docs/framework/wpf/graphics-multimedia/how-to-control-a-mediaelement-play-pause-stop-volume-and-speed.md)。  
  
### 时钟模式  
 在时钟模式下，由 <xref:System.Windows.Media.MediaTimeline> 驱动媒体播放。  时钟模式具有下列特征：  
  
-   媒体的 <xref:System.Uri> 是通过 <xref:System.Windows.Media.MediaTimeline> 间接设置的。  
  
-   可由时钟控制媒体播放。  不能使用媒体对象的控制方法。  
  
-   可通过以下方法加载媒体：设置 <xref:System.Windows.Media.MediaTimeline> 对象的 <xref:System.Windows.Media.MediaTimeline.Source%2A> 属性，从时间线创建时钟，并将时钟分配给媒体对象。  当位于 <xref:System.Windows.Media.Animation.Storyboard> 中的 <xref:System.Windows.Media.MediaTimeline> 针对 <xref:System.Windows.Controls.MediaElement> 时，也可用这种方法加载媒体。  
  
 若要在时钟模式下控制媒体播放，必须使用 <xref:System.Windows.Media.Animation.ClockController> 控制方法。  <xref:System.Windows.Media.Animation.ClockController> 是从 <xref:System.Windows.Media.MediaClock> 的 <xref:System.Windows.Media.Animation.ClockController> 属性获取的。  如果尝试在时钟模式下使用 <xref:System.Windows.Controls.MediaElement> 或 <xref:System.Windows.Media.MediaPlayer> 对象的控制方法，则会引发 <xref:System.InvalidOperationException>。  
  
 有关时钟和时间线的更多信息，请参见[动画概述](../../../../docs/framework/wpf/graphics-multimedia/animation-overview.md)。  
  
 有关时钟模式的示例，请参见[使用演示图板控制 MediaElement](../../../../docs/framework/wpf/graphics-multimedia/how-to-control-a-mediaelement-by-using-a-storyboard.md)。  
  
<a name="mediaelement"></a>   
## MediaElement 类  
 向应用程序添加媒体的操作十分简单，只需向应用程序的[!INCLUDE[TLA#tla_ui](../../../../includes/tlasharptla-ui-md.md)] 添加 <xref:System.Windows.Controls.MediaElement> 控件，并为要包含的媒体提供 <xref:System.Uri>。  [!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)] 中支持 [!INCLUDE[TLA#tla_wmp](../../../../includes/tlasharptla-wmp-md.md)] 10 所支持的所有媒体类型。下面的示例演示 <xref:System.Windows.Controls.MediaElement> 在[!INCLUDE[TLA#tla_xaml](../../../../includes/tlasharptla-xaml-md.md)] 中的简单用法。  
  
 [!code-xml[MediaElement_snip#SimpleMediaElementUsageWholePage](../../../../samples/snippets/csharp/VS_Snippets_Wpf/MediaElement_snip/CSharp/SimpleUsage.xaml#simplemediaelementusagewholepage)]  
  
 在此示例中，媒体在加载后即会自动播放。  播放完后，就会关闭媒体，并且会释放所有媒体资源（包括视频内存）。  此行为是 <xref:System.Windows.Controls.MediaElement> 对象的默认行为，由 <xref:System.Windows.Controls.MediaElement.LoadedBehavior%2A> 和 <xref:System.Windows.Controls.MediaElement.UnloadedBehavior%2A> 属性控制。  
  
### 控制 MediaElement  
 当 <xref:System.Windows.FrameworkElement.IsLoaded%2A> 为 `true` 或 `false` 时，可分别使用 <xref:System.Windows.Controls.MediaElement.LoadedBehavior%2A> 和 <xref:System.Windows.Controls.MediaElement.UnloadedBehavior%2A> 属性控制 <xref:System.Windows.Controls.MediaElement> 的行为。  设置 <xref:System.Windows.Controls.MediaState> 属性的目的是影响媒体播放行为。  例如，默认的 <xref:System.Windows.Controls.MediaElement.LoadedBehavior%2A> 为 <xref:System.Windows.Controls.MediaState>，而默认的 <xref:System.Windows.Controls.MediaElement.UnloadedBehavior%2A> 为 <xref:System.Windows.Controls.MediaState>。  这意味着加载 <xref:System.Windows.Controls.MediaElement> 并完成[预播放](GTMT)后，即会开始播放媒体。  播放完后，就会关闭媒体，并且会释放所有媒体资源。  
  
 <xref:System.Windows.Controls.MediaElement.LoadedBehavior%2A> 和 <xref:System.Windows.Controls.MediaElement.UnloadedBehavior%2A> 属性不是控制媒体播放的唯一方法。  在时钟模式下，时钟可以控制 <xref:System.Windows.Controls.MediaElement>，并且这些交互式控制方法在 <xref:System.Windows.Controls.MediaElement.LoadedBehavior%2A> 为 <xref:System.Windows.Controls.MediaState> 时具有控制权。  <xref:System.Windows.Controls.MediaElement> 通过计算下列优先级来处理对控制权的这种竞争。  
  
1.  <xref:System.Windows.Controls.MediaElement.UnloadedBehavior%2A>.  在卸载媒体时发生。  这可确保默认情况下释放所有媒体资源，即使 <xref:System.Windows.Media.MediaClock> 与 <xref:System.Windows.Controls.MediaElement> 关联也是如此。  
  
2.  <xref:System.Windows.Media.MediaClock>.  在媒体具有 <xref:System.Windows.Controls.MediaElement.Clock%2A> 时发生。  如果卸载媒体，则只要 <xref:System.Windows.Controls.MediaElement.UnloadedBehavior%2A> 为 <xref:System.Windows.Controls.MediaState>，<xref:System.Windows.Media.MediaClock> 就会生效。  时钟模式始终重写 <xref:System.Windows.Controls.MediaElement> 的加载行为。  
  
3.  <xref:System.Windows.Controls.MediaElement.LoadedBehavior%2A>.  在加载媒体时发生。  
  
4.  交互式控制方法。  在 <xref:System.Windows.Controls.MediaElement.LoadedBehavior%2A> 为 <xref:System.Windows.Controls.MediaState> 时发生。  提供了下列控制方法：<xref:System.Windows.Controls.MediaElement.Play%2A>、<xref:System.Windows.Controls.MediaElement.Pause%2A>、<xref:System.Windows.Controls.MediaElement.Close%2A> 和 <xref:System.Windows.Controls.MediaElement.Stop%2A>。  
  
### 显示 MediaElement  
 若要显示 <xref:System.Windows.Controls.MediaElement>，它必须具有要呈现的内容，并在加载内容之前将其 <xref:System.Windows.FrameworkElement.ActualWidth%2A> 和 <xref:System.Windows.FrameworkElement.ActualHeight%2A> 属性设置为零。  对于仅包含音频的内容，这些属性将始终为零。  对于视频内容，在 <xref:System.Windows.Controls.MediaElement.MediaOpened> 事件引发 <xref:System.Windows.FrameworkElement.ActualWidth%2A> 和 <xref:System.Windows.FrameworkElement.ActualHeight%2A> 后，会报告已加载媒体的大小。  这意味着在加载媒体之前，<xref:System.Windows.Controls.MediaElement> 不会占用[!INCLUDE[TLA#tla_ui](../../../../includes/tlasharptla-ui-md.md)] 中的任何物理空间，除非设置了 <xref:System.Windows.FrameworkElement.Width%2A> 或 <xref:System.Windows.FrameworkElement.Height%2A> 属性。  
  
 如果设置 <xref:System.Windows.FrameworkElement.Width%2A> 和 <xref:System.Windows.FrameworkElement.Height%2A> 属性，则会导致拉伸媒体来填充为 <xref:System.Windows.Controls.MediaElement> 提供的区域。  若要保持媒体的原始[纵横比](GTMT)，应设置 <xref:System.Windows.FrameworkElement.Width%2A> 或 <xref:System.Windows.FrameworkElement.Height%2A> 属性，但不能同时设置这两者。  如果同时设置 <xref:System.Windows.FrameworkElement.Width%2A> 和 <xref:System.Windows.FrameworkElement.Height%2A> 属性，则会使媒体以固定元素大小显示，可能无法达到预期效果。  
  
 为避免元素大小固定，[!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)] 可以[预播放](GTMT)媒体。  为此，需要将 <xref:System.Windows.Controls.MediaElement.LoadedBehavior%2A> 设置为 <xref:System.Windows.Controls.MediaState> 或 <xref:System.Windows.Controls.MediaState>。  在 <xref:System.Windows.Controls.MediaState> 状态下，媒体将预先缓冲，并将显示第一帧。  在 <xref:System.Windows.Controls.MediaState> 状态下，媒体将[预先缓冲](GTMT)，然后再开始播放。  
  
<a name="mediaplayer"></a>   
## MediaPlayer 类  
 当 <xref:System.Windows.Controls.MediaElement> 类为框架元素时，<xref:System.Windows.Media.MediaPlayer> 类设计为在 <xref:System.Windows.Media.Drawing> 对象中使用。  当可以牺牲框架级别功能而提高性能或需要 <xref:System.Windows.Freezable> 功能时将使用图形对象。  通过 <xref:System.Windows.Media.MediaPlayer>，可以在应用程序中提供媒体内容的同时利用这些功能。  与 <xref:System.Windows.Controls.MediaElement> 类似，<xref:System.Windows.Media.MediaPlayer> 可在独立模式或时钟模式下使用，但不具有 <xref:System.Windows.Controls.MediaElement> 对象的卸载和加载状态。  这会降低 <xref:System.Windows.Media.MediaPlayer> 的播放控制的复杂程度。  
  
### 控制 MediaPlayer  
 由于 <xref:System.Windows.Media.MediaPlayer> 是无状态的，因此只能使用两种方法控制媒体播放。  
  
1.  交互式控制方法。  在处于独立模式（`null` <xref:System.Windows.Media.MediaPlayer.Clock%2A> 属性）时采用。  
  
2.  <xref:System.Windows.Media.MediaClock>.  在媒体具有 <xref:System.Windows.Media.MediaPlayer.Clock%2A> 时采用。  
  
### 显示 MediaPlayer  
 从技术角度来说，不能显示 <xref:System.Windows.Media.MediaPlayer>，因为它没有物理表示形式。  但它可用于通过使用 <xref:System.Windows.Media.VideoDrawing> 类在 <xref:System.Windows.Media.Drawing> 中呈现媒体。  下面的示例演示如何使用 <xref:System.Windows.Media.VideoDrawing> 显示媒体。  
  
 [!code-csharp[DrawingMiscSnippets_snip#VideoDrawingExampleInline](../../../../samples/snippets/csharp/VS_Snippets_Wpf/DrawingMiscSnippets_snip/CSharp/VideoDrawingExample.cs#videodrawingexampleinline)]  
  
 有关 <xref:System.Windows.Media.Drawing> 对象的更多信息，请参见 [Drawing 对象概述](../../../../docs/framework/wpf/graphics-multimedia/drawing-objects-overview.md)。  
  
## 请参阅  
 <xref:System.Windows.Media.DrawingGroup>   
 [布局](../../../../docs/framework/wpf/advanced/layout.md)   
 [帮助主题](../../../../docs/framework/wpf/graphics-multimedia/audio-and-video-how-to-topics.md)