---
title: "如何：使用演示图板控制 MediaElement | Microsoft Docs"
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
  - "控制媒体的播放, 使用演示图板"
  - "媒体, 使用演示图板控制播放"
  - "多媒体, 使用演示图板控制媒体的播放"
  - "媒体播放, 使用演示图板进行控制"
  - "情节提要, 控制媒体的播放"
ms.assetid: 6128ca77-b826-4e36-b968-6f237157c543
caps.latest.revision: 12
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 12
---
# 如何：使用演示图板控制 MediaElement
本示例演示如何使用<xref:System.Windows.Media.Animation.Storyboard>中的 <xref:System.Windows.Media.MediaTimeline> 控制 <xref:System.Windows.Controls.MediaElement>。  
  
## 示例  
 当您使用<xref:System.Windows.Media.Animation.Storyboard>中的 <xref:System.Windows.Media.MediaTimeline> 控制 <xref:System.Windows.Controls.MediaElement> 的计时时，该功能与其他 <xref:System.Windows.Media.Animation.Timeline> 对象（如动画）的功能完全相同。  例如，<xref:System.Windows.Media.MediaTimeline> 使用 <xref:System.Windows.Media.Animation.Timeline> 属性（如 <xref:System.Windows.Media.Animation.Timeline.BeginTime%2A> 属性）指定何时开始 <xref:System.Windows.Controls.MediaElement>（开始媒体播放）。  它还使用 <xref:System.Windows.Media.Animation.Timeline.Duration%2A> 属性指定 <xref:System.Windows.Controls.MediaElement> 处于活动状态的时间（媒体播放的持续时间）。  有关将 <xref:System.Windows.Media.Animation.Timeline> 对象与<xref:System.Windows.Media.Animation.Storyboard>结合使用的更多信息，请参见[演示图板概述](../../../../docs/framework/wpf/graphics-multimedia/storyboards-overview.md)。  
  
 本示例演示如何创建一个简单的媒体播放器，它使用 <xref:System.Windows.Media.MediaTimeline> 控制播放。  此媒体播放器包括播放、暂停、继续和停止按钮。  此播放器还有一个 <xref:System.Windows.Controls.Slider> 控件，其作用相当于进度栏。  
  
 下面的示例为此媒体播放器创建[!INCLUDE[TLA#tla_ui](../../../../includes/tlasharptla-ui-md.md)]。  
  
 [!code-xml[MediaGallery_snip#MediaTimelineExampleWholePage](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/MediaGallery_snip/VB/MediaTimelineExample.xaml#mediatimelineexamplewholepage)]  
  
 下面的示例创建进度栏的功能。  
  
 [!code-csharp[MediaGallery_snip#CodeBehindMediaTimelineExampleWholePage](../../../../samples/snippets/csharp/VS_Snippets_Wpf/MediaGallery_snip/CSharp/MediaTimelineExample.xaml.cs#codebehindmediatimelineexamplewholepage)]
 [!code-vb[MediaGallery_snip#CodeBehindMediaTimelineExampleWholePage](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/MediaGallery_snip/VB/MediaTimelineExample.xaml.vb#codebehindmediatimelineexamplewholepage)]  
  
## 请参阅  
 <xref:System.Windows.Controls.MediaElement>   
 <xref:System.Windows.Media.MediaTimeline>   
 <xref:System.Windows.Media.Animation.Storyboard>   
 [控制 MediaElement（播放、暂停、停止、音量和速度）](../../../../docs/framework/wpf/graphics-multimedia/how-to-control-a-mediaelement-play-pause-stop-volume-and-speed.md)   
 [演示图板概述](../../../../docs/framework/wpf/graphics-multimedia/storyboards-overview.md)   
 [关键帧动画概述](../../../../docs/framework/wpf/graphics-multimedia/key-frame-animations-overview.md)   
 [动画概述](../../../../docs/framework/wpf/graphics-multimedia/animation-overview.md)   
 [帮助主题](../../../../docs/framework/wpf/graphics-multimedia/audio-and-video-how-to-topics.md)   
 [图形和多媒体](../../../../docs/framework/wpf/graphics-multimedia/index.md)