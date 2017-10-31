---
title: "如何：使用 VideoDrawing 播放媒体 | Microsoft Docs"
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
  - "类, MediaPlayer"
  - "类, VideoDrawing"
  - "MediaPlayer 类"
  - "媒体播放"
  - "VideoDrawing 类"
ms.assetid: 165d47ed-22ce-4ded-aa6a-aa9b7467de87
caps.latest.revision: 6
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 6
---
# 如何：使用 VideoDrawing 播放媒体
您可以使用 <xref:System.Windows.Media.VideoDrawing> 和 <xref:System.Windows.Media.MediaPlayer> 来播放音频或视频文件。  加载并播放媒体的方法有两种。  第一种方法是使用 <xref:System.Windows.Media.MediaPlayer> 和 <xref:System.Windows.Media.VideoDrawing> 自身，第二种方法是创建您自己的 <xref:System.Windows.Media.MediaTimeline>，并将其与 <xref:System.Windows.Media.MediaPlayer> 和 <xref:System.Windows.Media.VideoDrawing> 一起使用。  
  
> [!NOTE]
>  如果媒体随应用程序一起分发，则不能像图像那样将媒体文件用作项目资源。  在项目文件中，必须将媒体类型改设为 `Content`，并将 `CopyToOutputDirectory` 设置为 `PreserveNewest` 或 `Always`。  
  
## 示例  
 下面的示例使用 <xref:System.Windows.Media.VideoDrawing> 和 <xref:System.Windows.Media.MediaPlayer> 播放视频文件一次。  
  
 [!code-csharp[DrawingMiscSnippets_snip#VideoDrawingExampleInline](../../../../samples/snippets/csharp/VS_Snippets_Wpf/DrawingMiscSnippets_snip/CSharp/VideoDrawingExample.cs#videodrawingexampleinline)]  
  
 若要对媒体进行更多的计时控制，请将 <xref:System.Windows.Media.MediaTimeline> 与 <xref:System.Windows.Media.MediaPlayer> 和 <xref:System.Windows.Media.VideoDrawing> 对象一起使用。  通过 <xref:System.Windows.Media.MediaTimeline>，您可以指定是否重复播放视频。  
  
## 示例  
 下面的示例同时使用 <xref:System.Windows.Media.MediaTimeline> 以及 <xref:System.Windows.Media.MediaPlayer> 和 <xref:System.Windows.Media.VideoDrawing> 对象来重复播放视频。  
  
 [!code-csharp[DrawingMiscSnippets_snip#RepeatingVideoDrawingExampleInline](../../../../samples/snippets/csharp/VS_Snippets_Wpf/DrawingMiscSnippets_snip/CSharp/VideoDrawingExample.cs#repeatingvideodrawingexampleinline)]  
  
 请注意，使用 <xref:System.Windows.Media.MediaTimeline> 时，使用从 <xref:System.Windows.Media.MediaClock> 的 <xref:System.Windows.Media.Animation.Clock.Controller%2A> 属性返回的交互式 <xref:System.Windows.Media.Animation.ClockController> 控制媒体播放，而不是使用 <xref:System.Windows.Media.MediaPlayer> 的交互式方法。  
  
## 请参阅  
 <xref:System.Windows.Media.VideoDrawing>   
 [Drawing 对象概述](../../../../docs/framework/wpf/graphics-multimedia/drawing-objects-overview.md)