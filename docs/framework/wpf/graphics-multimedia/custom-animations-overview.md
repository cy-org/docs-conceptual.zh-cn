---
title: "自定义动画概述 | Microsoft Docs"
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
  - "动画, 自定义类"
  - "自定义动画类"
  - "自定义类, 动画"
  - "自定义关键帧"
  - "关键帧, 自定义"
ms.assetid: 9be69d50-3384-4938-886f-08ce00e4a7a6
caps.latest.revision: 14
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 10
---
# 自定义动画概述
本主题介绍如何以及何时通过以下方法来扩展 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 动画系统：创建自定义关键帧、动画类或者使用逐帧回调来绕过该系统。  
  
<a name="autoTopLevelSectionsOUTLINE0"></a>   
<a name="prerequisites"></a>   
## 必备组件  
 要了解本主题，您应当熟悉 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 提供的不同类型的动画。  有关更多信息，请参见 [From\/To\/By 动画概述](../../../../docs/framework/wpf/graphics-multimedia/from-to-by-animations-overview.md)、[关键帧动画概述](../../../../docs/framework/wpf/graphics-multimedia/key-frame-animations-overview.md)和[路径动画概述](../../../../docs/framework/wpf/graphics-multimedia/path-animations-overview.md)。  
  
 因为动画类继承自 <xref:System.Windows.Freezable> 类，所以您应当熟悉 <xref:System.Windows.Freezable> 对象以及如何继承 <xref:System.Windows.Freezable>。  有关更多信息，请参见 [Freezable 对象概述](../../../../docs/framework/wpf/advanced/freezable-objects-overview.md)。  
  
<a name="extendingtheanimationsystem"></a>   
## 扩展动画系统  
 有多种方法来扩展 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 动画系统，具体取决于您要使用的内置功能的级别。  [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 动画引擎中有三个主要的扩展性点：  
  
-   通过继承某个 *\<类型\>*KeyFrame 类（如 <xref:System.Windows.Media.Animation.DoubleKeyFrame>）来创建一个自定义关键帧对象。  此方法使用 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 动画引擎的大部分内置功能。  
  
-   通过继承 <xref:System.Windows.Media.Animation.AnimationTimeline> 或某个 *\<类型\>*AnimationBase 类来创建您自己的动画类。  
  
-   使用逐帧回调来逐帧生成动画。  此方法完全绕过动画和计时系统。  
  
 下表介绍了扩展动画系统的一些方案。  
  
|要执行此操作...|请使用此方法|  
|---------------|------------|  
|自定义具有对应 *\<类型\>*AnimationUsingKeyFrames 的类型的值之间的内插。|创建自定义关键帧。  有关更多信息，请参见[创建自定义关键帧](#createacustomkeyframe)部分。|  
|除了自定义具有对应 *\<类型\>*Animation 的类型的值之间的内插外，还要自定义其他内容。|创建继承自 *\<类型\>*AnimationBase 类的自定义动画类，该类对应于您要进行动画处理的类型。  有关更多信息，请参见[创建自定义动画类](#createcustomanimationtype)部分。|  
|对没有对应 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 动画的类型进行动画处理|使用 <xref:System.Windows.Media.Animation.ObjectAnimationUsingKeyFrames> 或创建继承自 <xref:System.Windows.Media.Animation.AnimationTimeline> 的类。  有关更多信息，请参见[创建自定义动画类](#createcustomanimationtype)部分。|  
|使用按每个帧计算并基于最后一组对象交互的值对多个对象进行动画处理|使用逐帧回调。  有关更多信息，请参见[创建并使用逐帧回调](#useperframecallback)部分。|  
  
<a name="createacustomkeyframe"></a>   
## 创建一个自定义关键帧  
 创建自定义关键帧类是扩展动画系统的最简单的方法。  当您需要对关键帧动画使用一种不同的内插方法时，可使用此方法。  如[关键帧动画概述](../../../../docs/framework/wpf/graphics-multimedia/key-frame-animations-overview.md)中所述，关键帧动画使用关键帧对象来生成它的输出值。  每个关键帧对象都执行三个功能：  
  
-   使用它的 <xref:System.Windows.Media.Animation.IKeyFrame.Value%2A> 属性指定一个目标值。  
  
-   使用它的 <xref:System.Windows.Media.Animation.IKeyFrame.KeyTime%2A> 属性指定达到该值的时间。  
  
-   通过实现 InterpolateValueCore 方法在前一关键帧的值与它自己的值之间进行内插。  
  
 **实现说明**  
  
 派生自 *\<类型\>*KeyFrame 抽象类并实现 InterpolateValueCore 方法。  InterpolateValueCore 方法返回关键帧的当前值。  它采用两个参数：前一个关键帧的值以及 0 到 1 之间的进度值。  进度值为 0 表示关键帧刚刚启动，值为 1 表示关键帧刚刚完成，应返回它的 <xref:System.Windows.Media.Animation.IKeyFrame.Value%2A> 属性所指定的值。  
  
 因为 *\<类型\>*KeyFrame 类继承自 <xref:System.Windows.Freezable> 类，所以您还必须重写 <xref:System.Windows.Freezable.CreateInstanceCore%2A> 核心来返回类的新实例。  如果该类未使用[依赖项属性](GTMT)来存储其数据或者在创建后需要额外的初始化，则您可能还需要重写其他方法；有关更多信息，请参见[Freezable 对象概述](../../../../docs/framework/wpf/advanced/freezable-objects-overview.md)。  
  
 在创建自定义 *\<类型\>*KeyFrame 动画后，您可以将它与该类型的 *\<类型\>*AnimationUsingKeyFrames 一起使用。  
  
<a name="createacustomanimationtype"></a>   
## 创建自定义动画类  
 通过创建自己的动画类型，您可以更好地控制对象的动画方式。  有两种推荐方法来创建自己的动画类型：从 <xref:System.Windows.Media.Animation.AnimationTimeline> 类或 *\<类型\>*AnimationBase 类派生。  不推荐从 *\<类型\>*Animation 或 *\<类型\>*AnimationUsingKeyFrames 类派生。  
  
### 从 \<类型\>AnimationBase 派生  
 从 *\<类型\>*AnimationBase 类派生是创建新的动画类型的最简单方法。  当您希望为已有对应 *\<类型\>*AnimationBase 类的类型创建新的动画时，可使用此方法。  
  
 **实现说明**  
  
 派生自 *\<类型\>*Animation 类并实现 GetCurrentValueCore 方法。  GetCurrentValueCore 方法返回动画的当前值。  它采用三个参数：建议的起始值、建议的结束值以及您用于确定动画进度的 <xref:System.Windows.Media.Animation.AnimationClock>。  
  
 因为 *\<类型\>*AnimationBase 类继承自 <xref:System.Windows.Freezable> 类，所以您还必须重写 <xref:System.Windows.Freezable.CreateInstanceCore%2A> 核心来返回类的新实例。  如果该类未使用[依赖项属性](GTMT)来存储其数据或者在创建后需要额外的初始化，则您可能还需要重写其他方法；有关更多信息，请参见[Freezable 对象概述](../../../../docs/framework/wpf/advanced/freezable-objects-overview.md)。  
  
 有关更多信息，请参见您要对其进行动画处理的类型的 *\<类型\>*AnimationBase 类的 GetCurrentValueCore 方法文档。  有关示例，请参见 [Custom Animation Sample](http://go.microsoft.com/fwlink/?LinkID=159981)（自定义动画示例）  
  
 **其他方法**  
  
 如果您仅仅希望更改动画值的内插方式，则应考虑从某个 *\<类型\>*KeyFrame 类派生。  您创建的关键帧可以与 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 所提供的对应 *\<类型\>*AnimationUsingKeyFrames 一起使用。  
  
### 从 AnimationTimeline 派生  
 当您希望为还没有匹配的 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 动画的类型创建动画，或者希望创建非强类型的动画时，应当从 <xref:System.Windows.Media.Animation.AnimationTimeline> 类派生。  
  
 **实现说明**  
  
 从 <xref:System.Windows.Media.Animation.AnimationTimeline> 类派生并重写以下成员：  
  
-   <xref:System.Windows.Freezable.CreateInstanceCore%2A> – 如果新类是具体的，则必须重写 <xref:System.Windows.Freezable.CreateInstanceCore%2A> 来返回类的新实例。  
  
-   <xref:System.Windows.Media.Animation.AnimationTimeline.GetCurrentValue%2A> – 重写此方法以返回动画的当前值。  它采用三个参数：默认初始值、默认目标值以及 <xref:System.Windows.Media.Animation.AnimationClock>。  使用 <xref:System.Windows.Media.Animation.AnimationClock> 来获取动画的当前时间或进度。  您可以选择是否使用默认初始值和目标值。  
  
-   <xref:System.Windows.Media.Animation.AnimationTimeline.IsDestinationDefault%2A> – 重写此属性来指示您的动画是否使用 <xref:System.Windows.Media.Animation.AnimationTimeline.GetCurrentValue%2A> 方法指定的默认目标值。  
  
-   <xref:System.Windows.Media.Animation.AnimationTimeline.TargetPropertyType%2A> – 重写此属性来指示动画产生的输出的 <xref:System.Type>。  
  
 如果该类未使用[依赖项属性](GTMT)来存储其数据或者在创建后需要额外的初始化，则您可能还需要重写其他方法；有关更多信息，请参见[Freezable 对象概述](../../../../docs/framework/wpf/advanced/freezable-objects-overview.md)。  
  
 推荐的范例（由 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 动画使用）将使用两个继承级别：  
  
1.  创建一个派生自 <xref:System.Windows.Media.Animation.AnimationTimeline> 的抽象 *\<类型\>*AnimationBase 类。  此类应重写 <xref:System.Windows.Media.Animation.AnimationTimeline.TargetPropertyType%2A> 方法。  它还应引入一个新的抽象方法 GetCurrentValueCore 并重写 <xref:System.Windows.Media.Animation.AnimationTimeline.GetCurrentValue%2A>，以便验证默认初始值和默认目标值参数的类型，然后调用 GetCurrentValueCore。  
  
2.  创建另一个类，该类继承自新的 *\<类型\>*AnimationBase 类并重写 <xref:System.Windows.Freezable.CreateInstanceCore%2A> 方法、您引入的 GetCurrentValueCore 方法以及 <xref:System.Windows.Media.Animation.AnimationTimeline.IsDestinationDefault%2A> 属性。  
  
 **其他方法**  
  
 如果您希望对没有对应 From\/To\/By 动画或关键帧动画的类型进行动画处理，应考虑使用 <xref:System.Windows.Media.Animation.ObjectAnimationUsingKeyFrames>。  因为它是弱类型，所以 <xref:System.Windows.Media.Animation.ObjectAnimationUsingKeyFrames> 可以对任何类型的值进行动画处理。  此方法的弱点是 <xref:System.Windows.Media.Animation.ObjectAnimationUsingKeyFrames> 仅支持[离散内插](GTMT)。  
  
<a name="useperframecallback"></a>   
## 使用逐帧回调  
 当需要完全绕过 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 动画系统时使用此方法。  此方法的一种方案是物理动画，在其中的每一个动画步骤，都需要基于最后一组对象交互重新计算动画对象的新方向或位置。  
  
 **实现说明**  
  
 与本概述中介绍的其他方法不同，要使用逐帧回调，不需要创建自定义动画或关键帧类，  
  
 而应注册需要进行动画处理的对象所在对象的 <xref:System.Windows.Media.CompositionTarget.Rendering> 事件。  每帧调用一次此事件处理程序方法。  每次 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 将[可视化树](GTMT)中持久呈现的数据封送到组合树中时，都将调用事件处理程序方法。  
  
 在事件处理程序中，执行动画效果所需的任意计算，并设置需要使用这些值进行动画处理的对象的属性。  
  
 要获取当前帧的显示时间，可以将与此事件关联的 <xref:System.EventArgs> 强制转换为 <xref:System.Windows.Media.RenderingEventArgs>，从而提供可用于获取当前帧呈现时间的 <xref:System.Windows.Media.RenderingEventArgs.RenderingTime%2A> 属性。  
  
 有关更多信息，请参见 <xref:System.Windows.Media.CompositionTarget.Rendering> 页。  
  
## 请参阅  
 <xref:System.Windows.Media.Animation.AnimationTimeline>   
 <xref:System.Windows.Media.Animation.IKeyFrame>   
 [属性动画技术概述](../../../../docs/framework/wpf/graphics-multimedia/property-animation-techniques-overview.md)   
 [Freezable 对象概述](../../../../docs/framework/wpf/advanced/freezable-objects-overview.md)   
 [From\/To\/By 动画概述](../../../../docs/framework/wpf/graphics-multimedia/from-to-by-animations-overview.md)   
 [关键帧动画概述](../../../../docs/framework/wpf/graphics-multimedia/key-frame-animations-overview.md)   
 [路径动画概述](../../../../docs/framework/wpf/graphics-multimedia/path-animations-overview.md)   
 [动画概述](../../../../docs/framework/wpf/graphics-multimedia/animation-overview.md)   
 [动画和计时系统概述](../../../../docs/framework/wpf/graphics-multimedia/animation-and-timing-system-overview.md)   
 [Custom Animation Sample](http://go.microsoft.com/fwlink/?LinkID=159981)