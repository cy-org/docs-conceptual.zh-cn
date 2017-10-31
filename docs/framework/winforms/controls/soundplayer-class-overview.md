---
title: "SoundPlayer 类概述 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-winforms"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "jsharp"
helpviewer_keywords: 
  - "播放声音、 SoundPlayer 类"
  - "SoundPlayer 类，关于 SoundPlayer 类"
  - "播放声音"
ms.assetid: fcebb938-62b9-4677-9cbe-6465bc863e22
caps.latest.revision: 10
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 10
---
# SoundPlayer 类概述
<xref:System.Media.SoundPlayer>类使您能够轻松地将声音纳入您的应用程序。  
  
 <xref:System.Media.SoundPlayer>类可以播放声音文件的资源或从 UNC 或 HTTP 位置的.wav 格式。 此外， <xref:System.Media.SoundPlayer>类可用于加载或以异步方式播放声音。  
  
 您还可以使用<xref:System.Media.SystemSounds>类播放常见的系统声音，包括提示音。  
  
## <a name="commonly-used-properties-methods-and-events"></a>常用的属性、 方法和事件  
  
|名称|描述|  
|----------|-----------------|  
|<xref:System.Media.SoundPlayer.SoundLocation%2A>属性|文件路径或声音的 Web 地址。 可接受的值可以是 UNC 或 HTTP。|  
|<xref:System.Media.SoundPlayer.LoadTimeout%2A>属性|您的程序将等待加载声音之前的毫秒数引发异常。 默认值为 10 秒。|  
|<xref:System.Media.SoundPlayer.IsLoadCompleted%2A>属性|一个布尔值，该值指示是否发出声音加载完毕。|  
|<xref:System.Media.SoundPlayer.Load%2A>方法|以同步方式上载了一个声音。|  
|<xref:System.Media.SoundPlayer.LoadAsync%2A>方法|开始异步加载声音。 下载完成后，它会发出<xref:System.Media.SoundPlayer.OnLoadCompleted%2A>事件。|  
|<xref:System.Media.SoundPlayer.Play%2A>方法|在播放中指定的声音<xref:System.Media.SoundPlayer.SoundLocation%2A>或<xref:System.Media.SoundPlayer.Stream%2A>新线程中的属性。|  
|<xref:System.Media.SoundPlayer.PlaySync%2A>方法|在播放中指定的声音<xref:System.Media.SoundPlayer.SoundLocation%2A>或<xref:System.Media.SoundPlayer.Stream%2A>当前线程中的属性。|  
|<xref:System.Media.SoundPlayer.Stop%2A>方法|停止当前正在播放任何声音。|  
|<xref:System.Media.SoundPlayer.LoadCompleted>事件|在尝试加载声音后引发。|  
  
## <a name="see-also"></a>另请参阅  
 <xref:System.Media.SoundPlayer>   
 <xref:System.Media.SystemSounds>