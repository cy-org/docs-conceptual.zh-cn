---
title: "如何：以交互方式控制时钟 | Microsoft Docs"
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
  - "时钟, 以交互方式控制"
  - "以交互方式控制时钟"
ms.assetid: d0b520e0-2f18-4cef-977f-2909e709548a
caps.latest.revision: 4
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 4
---
# 如何：以交互方式控制时钟
使用 <xref:System.Windows.Media.Animation.Clock> 对象的 <xref:System.Windows.Media.Animation.ClockController> 属性，您能够以交互方式启动、暂停、继续、定位和停止时钟以及将时钟前进到其填充期。  只能以交互方式控制计时树的根时钟。  
  
> [!NOTE]
>  可通过其他方法来以交互方式控制不需要直接处理时钟的动画：您还可以使用演示图板。  演示图板在标记和代码中均受支持。  有关示例，请参见[使用演示图板对属性进行动画处理](../../../../docs/framework/wpf/graphics-multimedia/how-to-animate-a-property-by-using-a-storyboard.md)或[动画概述](../../../../docs/framework/wpf/graphics-multimedia/animation-overview.md)。  
  
 在下面的示例中，使用了几个按钮来以交互方式控制动画时钟。  
  
## 示例  
 [!code-csharp[timingbehaviors_procedural_snip#GraphicsMMClockControllerExample](../../../../samples/snippets/csharp/VS_Snippets_Wpf/timingbehaviors_procedural_snip/CSharp/ClockControllerExample.cs#graphicsmmclockcontrollerexample)]
 [!code-vb[timingbehaviors_procedural_snip#GraphicsMMClockControllerExample](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/timingbehaviors_procedural_snip/visualbasic/clockcontrollerexample.vb#graphicsmmclockcontrollerexample)]  
  
## 请参阅  
 [使用演示图板对属性进行动画处理](../../../../docs/framework/wpf/graphics-multimedia/how-to-animate-a-property-by-using-a-storyboard.md)   
 [动画概述](../../../../docs/framework/wpf/graphics-multimedia/animation-overview.md)