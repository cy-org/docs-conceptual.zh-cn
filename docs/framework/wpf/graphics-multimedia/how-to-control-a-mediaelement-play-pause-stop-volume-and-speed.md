---
title: "如何：控制 MediaElement（播放、暂停、停止、音量和速度） | Microsoft Docs"
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
  - "控制媒体的播放"
  - "媒体, 控制播放"
  - "多媒体, 控制媒体的播放"
  - "媒体播放, 控制"
ms.assetid: 6885a730-e054-4c16-8c1e-ffe17b1f7c32
caps.latest.revision: 9
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 9
---
# 如何：控制 MediaElement（播放、暂停、停止、音量和速度）
下面的示例演示如何使用 <xref:System.Windows.Controls.MediaElement> 来控制媒体播放。  该示例创建一个简单的媒体播放器，通过该播放器可以对媒体进行播放、暂停、停止、回退和快进，还可以调整音量和速度比。  
  
## 示例  
 下面的代码创建 UI。  
  
> [!NOTE]
>  <xref:System.Windows.Controls.MediaElement> 的 <xref:System.Windows.Controls.MediaElement.LoadedBehavior%2A> 属性必须设置为 `Manual` 才能以交互方式停止、暂停和播放媒体。  
  
 [!code-xml[MediaGallery_snip#MediaElementExampleWholePage](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/MediaGallery_snip/VB/MediaElementExample.xaml#mediaelementexamplewholepage)]  
  
## 示例  
 下面的代码实现示例 UI 控件的功能。  <xref:System.Windows.Controls.MediaElement.Play%2A>、<xref:System.Windows.Controls.MediaElement.Pause%2A> 和 <xref:System.Windows.Controls.MediaElement.Stop%2A> 方法分别用于播放、暂停和停止媒体。  可以通过更改 <xref:System.Windows.Controls.MediaElement> 的 <xref:System.Windows.Controls.MediaElement.Position%2A> 属性来在媒体中回退和快进。  最后，<xref:System.Windows.Controls.MediaElement.Volume%2A> 和 <xref:System.Windows.Controls.MediaElement.SpeedRatio%2A> 属性用于调整媒体的音量和播放速度。  
  
 [!code-csharp[MediaGallery_snip#CodeBehindMediaElementExampleWholePage](../../../../samples/snippets/csharp/VS_Snippets_Wpf/MediaGallery_snip/CSharp/MediaElementExample.xaml.cs#codebehindmediaelementexamplewholepage)]
 [!code-vb[MediaGallery_snip#CodeBehindMediaElementExampleWholePage](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/MediaGallery_snip/VB/MediaElementExample.xaml.vb#codebehindmediaelementexamplewholepage)]  
  
## 请参阅  
 [使用演示图板控制 MediaElement](../../../../docs/framework/wpf/graphics-multimedia/how-to-control-a-mediaelement-by-using-a-storyboard.md)