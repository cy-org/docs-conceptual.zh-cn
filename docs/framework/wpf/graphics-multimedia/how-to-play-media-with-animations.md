---
title: "如何：播放带有动画的媒体 | Microsoft Docs"
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
  - "多媒体，播放带有动画"
  - "播放带有动画的媒体的"
  - "动画媒体播放"
  - "使用动画播放的媒体"
ms.assetid: 8982b7b7-1c6c-4b24-8801-b328862975f5
caps.latest.revision: 10
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 10
---
# 如何：播放带有动画的媒体
此示例演示如何通过使用在同一时间播放媒体和动画<xref:System.Windows.Media.MediaTimeline>和<xref:System.Windows.Media.Animation.DoubleAnimationUsingKeyFrames>在同一个类<xref:System.Windows.Media.Animation.Storyboard>。  
  
## <a name="example"></a>示例  
 可以使用一个或多个<xref:System.Windows.Media.MediaTimeline>中的对象<xref:System.Windows.Media.Animation.Storyboard>以及其他<xref:System.Windows.Media.Animation.Timeline>对象，如动画。  
  
 下面的示例设置<xref:System.Windows.Media.Animation.ParallelTimeline.SlipBehavior%2A>属性<xref:System.Windows.Media.Animation.Storyboard>为值`Slip`，它指定动画不播放之前在媒体 （在本例中视频） 的过程。 如果由于加载时间而延迟播放媒体，则可能需要此功能。  
  
 [!code-xml[MediaGallery_snippet#MediaTimelinePlusAnimationExampleWholePage](../../../../samples/snippets/csharp/VS_Snippets_Wpf/MediaGallery_snippet/CSharp/MediaTimelinePlusAnimationExample.xaml#mediatimelineplusanimationexamplewholepage)]  
  
## <a name="see-also"></a>另请参阅  
 <xref:System.Windows.Media.MediaTimeline>   
 <xref:System.Windows.Media.Animation.DoubleAnimationUsingKeyFrames>   
 <xref:System.Windows.Media.Animation.Storyboard>   
 <xref:System.Windows.Media.Animation.ParallelTimeline.SlipBehavior%2A>   
 [操作指南主题](../../../../docs/framework/wpf/graphics-multimedia/audio-and-video-how-to-topics.md)   
 [演示图板概述](../../../../docs/framework/wpf/graphics-multimedia/storyboards-overview.md)   
 [关键帧动画概述](../../../../docs/framework/wpf/graphics-multimedia/key-frame-animations-overview.md)   
 [动画概述](../../../../docs/framework/wpf/graphics-multimedia/animation-overview.md)   
 [图形和多媒体](../../../../docs/framework/wpf/graphics-multimedia/index.md)