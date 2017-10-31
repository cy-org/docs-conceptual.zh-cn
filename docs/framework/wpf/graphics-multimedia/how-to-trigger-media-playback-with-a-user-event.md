---
title: "如何：使用用户事件来触发媒体播放功能 | Microsoft Docs"
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
  - "媒体播放与事件同步"
  - "媒体，与事件同步的播放"
  - "与事件同步播放的媒体"
  - "多媒体、媒体播放与事件同步"
ms.assetid: c4dbe632-6e7f-4d7f-9df5-98737a758bc3
caps.latest.revision: 10
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 10
---
# 如何：使用用户事件来触发媒体播放功能
此示例演示如何将媒体播放与事件同步。  
  
## <a name="example"></a>示例  
 下面的示例使用<xref:System.Windows.Controls.MediaElement>控件和<xref:System.Windows.Media.MediaTimeline>类来播放声音，当用户单击时发生<xref:System.Windows.Controls.Button>。  
  
 [!code-xml[MediaGallery_snippet#SoundFromUserEventExampleWholePage](../../../../samples/snippets/csharp/VS_Snippets_Wpf/MediaGallery_snippet/CSharp/SoundFromUserEventExample.xaml#soundfromusereventexamplewholepage)]  
  
## <a name="see-also"></a>另请参阅  
 <xref:System.Windows.Controls.MediaElement>   
 <xref:System.Windows.Media.MediaTimeline>   
 <xref:System.Windows.EventTrigger.RoutedEvent%2A>   
 <xref:System.Windows.Media.Animation.Storyboard>   
 [操作指南主题](../../../../docs/framework/wpf/graphics-multimedia/audio-and-video-how-to-topics.md)   
 [图形和多媒体](../../../../docs/framework/wpf/graphics-multimedia/index.md)