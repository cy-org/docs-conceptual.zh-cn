---
title: "计时事件概述 | Microsoft Docs"
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
  - "Clock 类"
  - "类中时钟"
  - "时间线"
  - "计时事件"
ms.assetid: 597e3280-0867-4359-a97b-5b2f4149e350
caps.latest.revision: 14
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 14
---
# 计时事件概述
本主题介绍如何使用上可用的五个计时事件<xref:System.Windows.Media.Animation.Timeline>和<xref:System.Windows.Media.Animation.Clock>对象。  
  
<a name="autoTopLevelSectionsOUTLINE0"></a>   
## <a name="prerequisites"></a>先决条件  
 若要了解本主题，应了解如何创建和使用动画。 若要开始使用动画，请参阅[动画概述](../../../../docs/framework/wpf/graphics-multimedia/animation-overview.md)。  
  
 有多种方法中的属性进行动画处理[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]:  
  
-   **使用情节提要对象**（标记和代码）︰ 您可以使用<xref:System.Windows.Media.Animation.Storyboard>对象来排列和分发到一个或多个对象的动画。 有关示例，请参阅[使用演示图板对属性进行动画处理](../../../../docs/framework/wpf/graphics-multimedia/how-to-animate-a-property-by-using-a-storyboard.md)。  
  
-   **使用本地动画**（仅代码）︰ 您可以将应用<xref:System.Windows.Media.Animation.AnimationTimeline>对象直接与它们进行动画处理的属性。 有关示例，请参阅[进行动画处理属性而不使用演示图板](../../../../docs/framework/wpf/graphics-multimedia/how-to-animate-a-property-without-using-a-storyboard.md)。  
  
-   **使用时钟**（仅代码）︰ 您可以显式管理时钟创建并将分发用户的动画时钟。  有关示例，请参阅[使用 AnimationClock 对属性进行动画处理](../../../../docs/framework/wpf/graphics-multimedia/how-to-animate-a-property-by-using-an-animationclock.md)。  
  
 因为您可以使用这些标记和代码中，此概述中的示例使用<xref:System.Windows.Media.Animation.Storyboard>对象。 但是，所述的概念可以应用于属性进行动画处理的其他方法。  
  
### <a name="what-is-a-clock"></a>时钟是什么？  
 时间线，其本身而言，实际上没有任何除了描述一个时间段。 它是时间线的<xref:System.Windows.Media.Animation.Clock>对象，不能实际工作︰ 维护与计时相关用于时间线的运行时状态。 在大多数情况下，例如使用演示图板时，一个时钟自动创建为时间线。 您还可以创建<xref:System.Windows.Media.Animation.Clock>使用由显式<xref:System.Windows.Media.Animation.Timeline.CreateClock%2A>方法。 有关详细信息<xref:System.Windows.Media.Animation.Clock>对象，请参阅[动画和计时系统概述](../../../../docs/framework/wpf/graphics-multimedia/animation-and-timing-system-overview.md)。  
  
## <a name="why-use-events"></a>为什么使用事件？  
 除了一个 （寻道对齐为最后一个时钟周期），是异步的所有交互计时操作。 没有，您需要知道正好在其将执行方法。 当您有其他代码，取决于您的计时操作时，这可以是个问题。 假设您想要停止一个矩形进行动画处理的时间线。 时间线停止后，您可以更改矩形的颜色。  
  
 [!code-csharp[events_procedural#NeedForEventsFragment](../../../../samples/snippets/csharp/VS_Snippets_Wpf/events_procedural/CSharp/EventExample.cs#needforeventsfragment)]
 [!code-vb[events_procedural#NeedForEventsFragment](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/events_procedural/VisualBasic/EventExample.vb#needforeventsfragment)]  
  
 在上一示例中，第二行代码可能会在情节提要停止前执行。 这是因为停止是一个异步操作。 告诉时间线或时钟停止创建"停止"的排序不处理请求之前计时引擎下一步刻度线。  
  
 若要执行命令，在时间线完成后，使用计时事件。 在下面的示例中，事件处理程序用于在演示图板停止播放后更改矩形的颜色。  
  
 [!code-csharp[events_procedural#RegisterForStoryboardCurrentStateInvalidatedEvent](../../../../samples/snippets/csharp/VS_Snippets_Wpf/events_procedural/CSharp/EventExample.cs#registerforstoryboardcurrentstateinvalidatedevent)]
 [!code-vb[events_procedural#RegisterForStoryboardCurrentStateInvalidatedEvent](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/events_procedural/VisualBasic/EventExample.vb#registerforstoryboardcurrentstateinvalidatedevent)]  
[!code-csharp[events_procedural#StoryboardCurrentStateInvalidatedEvent2](../../../../samples/snippets/csharp/VS_Snippets_Wpf/events_procedural/CSharp/EventExample.cs#storyboardcurrentstateinvalidatedevent2)]
[!code-vb[events_procedural#StoryboardCurrentStateInvalidatedEvent2](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/events_procedural/VisualBasic/EventExample.vb#storyboardcurrentstateinvalidatedevent2)]  
  
 有关更完整的示例，请参阅[收到通知时时钟的状态更改](../../../../docs/framework/wpf/graphics-multimedia/how-to-receive-notification-when-clock-state-changes.md)。  
  
## <a name="public-events"></a>公共事件  
 <xref:System.Windows.Media.Animation.Timeline>和<xref:System.Windows.Media.Animation.Clock>类都提供&5; 个计时事件。 下表列出这些事件，触发它们的条件。  
  
|事件|触发交互操作|其他触发器|  
|-----------|--------------------------------------|--------------------|  
|**已完成**|跳过以填充|时钟完成。|  
|**CurrentGlobalSpeedInvalidated**|暂停、 恢复、 查找、 设置速度比、 跳过以填充、 停止|时钟反转、 加快了、 启动或停止。|  
|**CurrentStateInvalidated**|开始、 跳过以填充、 停止|时钟开始、 停止或填充。|  
|**CurrentTimeInvalidated**|开始、 查找、 跳过以填充、 停止|时钟前进。|  
|**RemoveRequested**|删除||  
  
## <a name="ticking-and-event-consolidation"></a>计时和事件合并  
 当您设置中的对象有动画效果[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]，它是管理您的动画的计时引擎。 计时引擎跟踪时间的进度，并计算每个动画的状态。 它使第二个中的很多这样的计算过程。 这些计算过程被称为"时钟周期。  
  
 虽然计时周期频繁发生，则可能会有很多种刻度之间发生这种情况。 例如，时间线可能会停止、 启动，并且再次停止，在这种情况下其当前状态将更改三次。 从理论上讲，可能会引发此事件多次在为一个时钟周期;但是，计时引擎将合并事件，以便每滴答一次引发的每个事件。  
  
## <a name="registering-for-events"></a>正在注册的事件  
 有两种方法来注册，以便计时事件︰ 您可以注册时间线以及与创建从该时间线的时钟。 直接向时钟注册事件是相当简单明了，但只能通过编写代码实现。 您可以注册的事件的时间线从标记或代码。 下一节介绍如何注册时间线的时钟事件。  
  
<a name="registeringforclockeventswithatimeline"></a>   
## <a name="registering-for-clock-events-with-a-timeline"></a>正在注册的时钟时间线事件  
 虽然时间线的<xref:System.Windows.Media.Animation.Timeline.Completed>， <xref:System.Windows.Media.Animation.Timeline.CurrentGlobalSpeedInvalidated>， <xref:System.Windows.Media.Animation.Timeline.CurrentStateInvalidated>， <xref:System.Windows.Media.Animation.Timeline.CurrentTimeInvalidated>，和<xref:System.Windows.Media.Animation.Timeline.RemoveRequested>事件似乎与时间线上，这些事件实际上将与一个事件处理程序相关联的注册相关联<xref:System.Windows.Media.Animation.Clock>创建时间线。  
  
 当您注册，以便<xref:System.Windows.Media.Animation.Timeline.Completed>时间线上的事件，例如，您实际上通知系统注册为<xref:System.Windows.Media.Animation.Clock.Completed>事件的时间线创建每个时钟。 在代码中，您必须注册此事件之前<xref:System.Windows.Media.Animation.Clock>创建为此时间线; 否则，不会收到通知。 发生这种情况中自动[!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)]; 分析器自动为该事件注册<xref:System.Windows.Media.Animation.Clock>创建。  
  
## <a name="see-also"></a>另请参阅  
 [动画和计时系统概述](../../../../docs/framework/wpf/graphics-multimedia/animation-and-timing-system-overview.md)   
 [动画概述](../../../../docs/framework/wpf/graphics-multimedia/animation-overview.md)   
 [计时行为概述](../../../../docs/framework/wpf/graphics-multimedia/timing-behaviors-overview.md)