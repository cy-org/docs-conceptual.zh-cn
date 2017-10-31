---
title: "如何：同步定位时钟 | Microsoft Docs"
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
  - "时钟, 同步查找"
  - "同步查找时钟"
ms.assetid: e5b7529b-b7d0-40d2-9e1d-fa4b5e736e96
caps.latest.revision: 4
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 4
---
# 如何：同步定位时钟
使用 <xref:System.Windows.Media.Animation.ClockController.SeekAlignedToLastTick%2A> 方法，能够以同步方式将时钟定位到特定点。  下面的示例演示 <xref:System.Windows.Media.Animation.ClockController> 的 <xref:System.Windows.Media.Animation.ClockController.Seek%2A> 方法和 <xref:System.Windows.Media.Animation.ClockController.SeekAlignedToLastTick%2A> 方法。  
  
 本示例演示如何定位 <xref:System.Windows.Media.Animation.Clock>；有关演示如何定位演示图板的示例，请参见[同步搜寻演示图板](../../../../docs/framework/wpf/graphics-multimedia/how-to-seek-a-storyboard-synchronously.md)。  
  
## 示例  
 [!code-csharp[ClockController_procedural_snip#ClockControllerSeekExample](../../../../samples/snippets/csharp/VS_Snippets_Wpf/ClockController_procedural_snip/CSharp/SeekAlignedToLastTickExample.cs#clockcontrollerseekexample)]
 [!code-vb[ClockController_procedural_snip#ClockControllerSeekExample](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/ClockController_procedural_snip/visualbasic/seekalignedtolasttickexample.vb#clockcontrollerseekexample)]