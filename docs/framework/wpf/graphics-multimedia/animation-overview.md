---
title: "动画概述 | Microsoft Docs"
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
  - "演示图板 [WPF] 动画"
  - "动画 [WPF] 概述"
ms.assetid: bd9ce563-725d-4385-87c9-d7ee38cf79ea
caps.latest.revision: 73
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 73
---
# 动画概述
<a name="introduction"></a>[!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)]提供一组强大的图形和布局功能，使您可以创建有吸引力的用户界面和吸引人的文档。 动画可以使一个很有吸引力的用户界面，甚至更引入注目和可用。 通过只是进行动画处理的背景色或应用动画<xref:System.Windows.Media.Transform>，可以创建出生动的屏幕转换或提供有用的视觉提示。  
  
 本概述介绍了[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]动画和计时系统。 它主要关注的动画[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]使用演示图板的对象。  

<a name="introducinganimations"></a>   
## <a name="introducing-animations"></a>动画简介  
 动画是通过快速播放一系列图像，每个略有不同的上一次创建这样的错觉。 人脑将作为一个变化的场景的映像组。 在电影中，使用记录许多照片或帧，每秒的照相机创建这种错觉。 当播放帧的投影仪时，观众看到的是运动的图片。  
  
 在计算机上的动画与此类似。 例如，可使矩形淡出视野之外的绘图程序可能会起作用，如下所示。  
  
-   该程序创建一个计时器。  
  
-   以设定间隔，以查看已用多少时间，则程序会检查计时器。  
  
-   每次程序检查计时器，它计算当前的不透明度值根据经过多长时间的矩形。  
  
-   程序然后使用新值更新该矩形，并重新绘制它。  
  
 之前[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]，[!INCLUDE[TLA#tla_win](../../../../includes/tlasharptla-win-md.md)]开发人员必须创建并管理其自己的计时系统或使用特殊的自定义库。                  [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]包括通过托管代码公开一个高效计时系统和[!INCLUDE[TLA#tla_xaml](../../../../includes/tlasharptla-xaml-md.md)]深入地集成到[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]框架。                  [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]动画，可以轻松地对控件和其他图形对象进行动画处理。  
  
 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]处理管理计时系统和高效地重绘屏幕的所有后台工作。 它提供使您能够专注于你想要创建，而不是实现这些效果的机制的效果的计时类。                  [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]此外可以轻松通过公开动画基类，这些类您的类可以从该基类继承来创建您自己的动画，以制作自定义的动画。 这些自定义动画获得很多标准的动画类的性能优势。  
  
<a name="thewpftimingsystem"></a>   
## <a name="wpf-property-animation-system"></a>WPF 属性动画系统  
 如果您了解有关计时系统的几个重要概念[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]动画可以是易于使用。 最重要的是，在[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]，通过将动画应用于其各个属性动态显示对象。 例如，若要使框架元素增大，您设置动画效果其<xref:System.Windows.FrameworkElement.Width%2A>和<xref:System.Windows.FrameworkElement.Height%2A>属性。 若要使淡出视图的对象，您设置动画效果其<xref:System.Windows.UIElement.Opacity%2A>属性。  
  
 为属性具有动画功能，它必须满足以下三个要求︰  
  
-   它必须是依赖项属性。  
  
-   它必须属于类，该类继承<xref:System.Windows.DependencyObject>并实现<xref:System.Windows.Media.Animation.IAnimatable>接口。  
  
-   必须有兼容的动画类型。 (如果[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]未提供，您可以创建您自己。 请参阅[自定义动画概述](../../../../docs/framework/wpf/graphics-multimedia/custom-animations-overview.md)。)  
  
 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]包含多个对象具有<xref:System.Windows.Media.Animation.IAnimatable>属性。 控件如<xref:System.Windows.Controls.Button>和<xref:System.Windows.Controls.TabControl>，以及<xref:System.Windows.Controls.Panel>和<xref:System.Windows.Shapes.Shape>对象继承自<xref:System.Windows.DependencyObject>。 它们的大多数属性是依赖项属性。  
  
 您可以使用动画几乎任意位置，其中包括样式和控件模板中。 动画不需要将 visual;您可以对不是用户界面的一部分，它们是否符合此部分所述的条件的对象进行动画处理。  
  
<a name="storyboardwalkthrough"></a>   
## <a name="example-make-an-element-fade-in-and-out-of-view"></a>示例︰ 使元素淡入淡出和移出视图  
 此示例演示如何使用[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]动画依赖项属性的值进行动画处理。 它使用<xref:System.Windows.Media.Animation.DoubleAnimation>，这是一种类型的生成的动画<xref:System.Double>值进行动画处理<xref:System.Windows.UIElement.Opacity%2A>属性<xref:System.Windows.Shapes.Rectangle>。 因此，<xref:System.Windows.Shapes.Rectangle>淡入淡出视图。  
  
 该示例的第一部分创建<xref:System.Windows.Shapes.Rectangle>元素。 所执行的步骤演示如何创建动画，并将其应用于矩形的<xref:System.Windows.UIElement.Opacity%2A>属性。  
  
 以下示例显示如何创建<xref:System.Windows.Shapes.Rectangle>中的元素<xref:System.Windows.Controls.StackPanel>在 XAML 中。  
  
 [!code-xml[animation_ovws2#RectangleOpacityFadeExampleXaml_1](../../../../samples/snippets/csharp/VS_Snippets_Wpf/animation_ovws2/CSharp/Window1.xaml#rectangleopacityfadeexamplexaml_1)]  
  
 以下示例显示如何创建<xref:System.Windows.Shapes.Rectangle>中的元素<xref:System.Windows.Controls.StackPanel>在代码中。  
  
 [!code-csharp[animation_ovws2#RectangleOpacityFadeExampleCode_1](../../../../samples/snippets/csharp/VS_Snippets_Wpf/animation_ovws2/CSharp/Class1.cs#rectangleopacityfadeexamplecode_1)]
 [!code-vb[animation_ovws2#RectangleOpacityFadeExampleCode_1](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/animation_ovws2/VisualBasic/Class1.vb#rectangleopacityfadeexamplecode_1)]  
  
<a name="opacity_animation_step1"></a>   
### <a name="part-1-create-a-doubleanimation"></a>第 1 部分︰ 创建 DoubleAnimation  
 要使淡入和移出视图元素的一种方法是进行动画处理其<xref:System.Windows.UIElement.Opacity%2A>属性。 因为<xref:System.Windows.UIElement.Opacity%2A>属性的类型为<xref:System.Double>，您需要生成双精度值的动画。 一个<xref:System.Windows.Media.Animation.DoubleAnimation>是这样的一个动画。 一个<xref:System.Windows.Media.Animation.DoubleAnimation>创建两个双精度值之间的过渡效果。 若要指定其起始值，将设置其<xref:System.Windows.Media.Animation.DoubleAnimation.From%2A>属性。 若要指定其结束的值，将设置其<xref:System.Windows.Media.Animation.DoubleAnimation.To%2A>属性。  
  
1.  不透明度值`1.0`使对象完全不透明，并且不透明度值`0.0`变得完全不可见。 To make the animation transition from                                  `1.0` to                                  `0.0` you set its                                  <xref:System.Windows.Media.Animation.DoubleAnimation.From%2A> property to                                  `1.0` and its                                  <xref:System.Windows.Media.Animation.DoubleAnimation.To%2A> property to                                  `0.0`. 以下示例显示如何创建<xref:System.Windows.Media.Animation.DoubleAnimation>在 XAML 中。  
  
     [!code-xml[animation_ovws2#RectangleOpacityFadeExampleXaml_2](../../../../samples/snippets/csharp/VS_Snippets_Wpf/animation_ovws2/CSharp/Window1.xaml#rectangleopacityfadeexamplexaml_2)]  
  
     以下示例显示如何创建<xref:System.Windows.Media.Animation.DoubleAnimation>在代码中。  
  
     [!code-csharp[animation_ovws2#RectangleOpacityFadeExampleCode_2](../../../../samples/snippets/csharp/VS_Snippets_Wpf/animation_ovws2/CSharp/Class1.cs#rectangleopacityfadeexamplecode_2)]
     [!code-vb[animation_ovws2#RectangleOpacityFadeExampleCode_2](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/animation_ovws2/VisualBasic/Class1.vb#rectangleopacityfadeexamplecode_2)]  
  
2.  接下来，您必须指定<xref:System.Windows.Media.Animation.Timeline.Duration%2A>。 <xref:System.Windows.Media.Animation.Timeline.Duration%2A>动画的指定要从其起始值转到其目标值花多长时间。 以下示例显示如何设置<xref:System.Windows.Media.Animation.Timeline.Duration%2A>为在 XAML 中的五秒。  
  
     [!code-xml[animation_ovws2#RectangleOpacityFadeExampleXaml_3](../../../../samples/snippets/csharp/VS_Snippets_Wpf/animation_ovws2/CSharp/Window1.xaml#rectangleopacityfadeexamplexaml_3)]  
  
     以下示例显示如何设置<xref:System.Windows.Media.Animation.Timeline.Duration%2A>为在代码中的五秒。  
  
     [!code-csharp[animation_ovws2#RectangleOpacityFadeExampleCode_3](../../../../samples/snippets/csharp/VS_Snippets_Wpf/animation_ovws2/CSharp/Class1.cs#rectangleopacityfadeexamplecode_3)]
     [!code-vb[animation_ovws2#RectangleOpacityFadeExampleCode_3](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/animation_ovws2/VisualBasic/Class1.vb#rectangleopacityfadeexamplecode_3)]  
  
3.  前面的代码显示了动画从托管代码转换`1.0`到`0.0`，这将导致目标元素从完全不透明逐渐转变为完全不可见。 若要使元素逐渐回到视野消失后，将设置<xref:System.Windows.Media.Animation.Timeline.AutoReverse%2A>到动画的属性`true`。 若要使动画无限期地重复，将设置其<xref:System.Windows.Media.Animation.Timeline.RepeatBehavior%2A>属性设置为<xref:System.Windows.Media.Animation.RepeatBehavior.Forever%2A>。以下示例显示如何设置<xref:System.Windows.Media.Animation.Timeline.AutoReverse%2A>和<xref:System.Windows.Media.Animation.Timeline.RepeatBehavior%2A> XAML 中的属性。  
  
     [!code-xml[animation_ovws2#RectangleOpacityFadeExampleXaml_4](../../../../samples/snippets/csharp/VS_Snippets_Wpf/animation_ovws2/CSharp/Window1.xaml#rectangleopacityfadeexamplexaml_4)]  
  
     以下示例显示如何设置<xref:System.Windows.Media.Animation.Timeline.AutoReverse%2A>和<xref:System.Windows.Media.Animation.Timeline.RepeatBehavior%2A>代码中的属性。  
  
     [!code-csharp[animation_ovws2#RectangleOpacityFadeExampleCode_4](../../../../samples/snippets/csharp/VS_Snippets_Wpf/animation_ovws2/CSharp/Class1.cs#rectangleopacityfadeexamplecode_4)]
     [!code-vb[animation_ovws2#RectangleOpacityFadeExampleCode_4](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/animation_ovws2/VisualBasic/Class1.vb#rectangleopacityfadeexamplecode_4)]  
  
<a name="opacity_animation_step2"></a>   
### <a name="part-2-create-a-storyboard"></a>第 2 部分︰ 创建一个情节提要  
 若要向对象应用动画，您创建<xref:System.Windows.Media.Animation.Storyboard>并用<xref:System.Windows.Media.Animation.Storyboard.TargetName%2A>和<xref:System.Windows.Media.Animation.Storyboard.TargetProperty%2A>附加属性来指定的对象和属性进行动画处理。  
  
1.  创建<xref:System.Windows.Media.Animation.Storyboard>和将动画添加作为其子级。 以下示例显示如何创建<xref:System.Windows.Media.Animation.Storyboard>在 XAML 中。  
  
     <!-- TODO: review snippet reference [!code-xml[animation_ovws2#RectangleOpacityFadeExampleXaml_5](../../../../samples/snippets/csharp/VS_Snippets_Wpf/animation_ovws2/CSharp/Window1.xaml#rectangleopacityfadeexamplexaml_5)]  -->  
  
     若要创建<xref:System.Windows.Media.Animation.Storyboard>在代码中，声明<xref:System.Windows.Media.Animation.Storyboard>在类级别变量。  
  
     [!code-csharp[animation_ovws2#RectangleOpacityFadeExampleCode_100](../../../../samples/snippets/csharp/VS_Snippets_Wpf/animation_ovws2/CSharp/MainWindow.xaml.cs#rectangleopacityfadeexamplecode_100)]
     [!code-vb[animation_ovws2#RectangleOpacityFadeExampleCode_100](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/animation_ovws2/VisualBasic/MainWindow.xaml.vb#rectangleopacityfadeexamplecode_100)]  
  
     然后初始化<xref:System.Windows.Media.Animation.Storyboard>和将动画添加作为其子级。  
  
     [!code-csharp[animation_ovws2#RectangleOpacityFadeExampleCode_101](../../../../samples/snippets/csharp/VS_Snippets_Wpf/animation_ovws2/CSharp/MainWindow.xaml.cs#rectangleopacityfadeexamplecode_101)]
     [!code-vb[animation_ovws2#RectangleOpacityFadeExampleCode_101](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/animation_ovws2/VisualBasic/MainWindow.xaml.vb#rectangleopacityfadeexamplecode_101)]  
  
2.  <xref:System.Windows.Media.Animation.Storyboard>必须知道在何处应用动画。 使用<xref:System.Windows.Media.Animation.Storyboard.TargetName%2A?displayProperty=fullName>附加属性来指定的对象进行动画处理。 以下示例显示如何设置的目标名称<xref:System.Windows.Media.Animation.DoubleAnimation>到`MyRectangle`在 XAML 中。  
  
     [!code-xml[animation_ovws2#RectangleOpacityFadeExampleXaml_6](../../../../samples/snippets/csharp/VS_Snippets_Wpf/animation_ovws2/CSharp/Window1.xaml#rectangleopacityfadeexamplexaml_6)]  
  
     以下示例显示如何设置的目标名称<xref:System.Windows.Media.Animation.DoubleAnimation>到`MyRectangle`在代码中。  
  
     [!code-csharp[animation_ovws2#RectangleOpacityFadeExampleCode_102](../../../../samples/snippets/csharp/VS_Snippets_Wpf/animation_ovws2/CSharp/MainWindow.xaml.cs#rectangleopacityfadeexamplecode_102)]
     [!code-vb[animation_ovws2#RectangleOpacityFadeExampleCode_102](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/animation_ovws2/VisualBasic/MainWindow.xaml.vb#rectangleopacityfadeexamplecode_102)]  
  
3.  使用<xref:System.Windows.Media.Animation.Storyboard.TargetProperty%2A>附加属性指定的属性进行动画处理。 下面的示例演示如何配置动画目标<xref:System.Windows.UIElement.Opacity%2A>属性<xref:System.Windows.Shapes.Rectangle>在 XAML 中。  
  
     [!code-xml[animation_ovws2#RectangleOpacityFadeExampleXaml_7](../../../../samples/snippets/csharp/VS_Snippets_Wpf/animation_ovws2/CSharp/Window1.xaml#rectangleopacityfadeexamplexaml_7)]  
  
     下面的示例演示如何配置动画目标<xref:System.Windows.UIElement.Opacity%2A>属性<xref:System.Windows.Shapes.Rectangle>在代码中。  
  
     [!code-csharp[animation_ovws2#RectangleOpacityFadeExampleCode_103](../../../../samples/snippets/csharp/VS_Snippets_Wpf/animation_ovws2/CSharp/MainWindow.xaml.cs#rectangleopacityfadeexamplecode_103)]
     [!code-vb[animation_ovws2#RectangleOpacityFadeExampleCode_103](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/animation_ovws2/VisualBasic/MainWindow.xaml.vb#rectangleopacityfadeexamplecode_103)]  
  
 有关详细信息<xref:System.Windows.Media.Animation.Storyboard.TargetProperty%2A>语法和其他示例，请参阅[演示图板概述](../../../../docs/framework/wpf/graphics-multimedia/storyboards-overview.md)。  
  
<a name="opacity_animation_step3"></a>   
### <a name="part-3-xaml-associate-the-storyboard-with-a-trigger"></a>第 3 (XAML) 部分︰ 关联与某个触发器情节提要  
 应用并启动的最简单办法<xref:System.Windows.Media.Animation.Storyboard>中[!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)]是使用一个事件触发器。                          本部分说明如何将相关联<xref:System.Windows.Media.Animation.Storyboard>与 XAML 中的触发器。  
  
1.  创建<xref:System.Windows.Media.Animation.BeginStoryboard>对象，并将你的情节提要与它相关联。 一个<xref:System.Windows.Media.Animation.BeginStoryboard>是一种<xref:System.Windows.TriggerAction>应用和启动<xref:System.Windows.Media.Animation.Storyboard>。  
  
     [!code-xml[animation_ovws_snippet#RectangleOpacityFadeExampleInline_3](../../../../samples/snippets/csharp/VS_Snippets_Wpf/animation_ovws_snippet/CS/RectangleOpacityFadeExample.xaml#rectangleopacityfadeexampleinline_3)]  
  
2.  创建<xref:System.Windows.EventTrigger>并添加<xref:System.Windows.Media.Animation.BeginStoryboard>到其<xref:System.Windows.EventTrigger.Actions%2A>集合。 设置<xref:System.Windows.EventTrigger.RoutedEvent%2A>属性<xref:System.Windows.EventTrigger>到想要启动的路由事件<xref:System.Windows.Media.Animation.Storyboard>。 (有关路由事件的详细信息，请参阅[路由事件概述](../../../../docs/framework/wpf/advanced/routed-events-overview.md)。)  
  
     [!code-xml[animation_ovws_snippet#RectangleOpacityFadeExampleInline_2](../../../../samples/snippets/csharp/VS_Snippets_Wpf/animation_ovws_snippet/CS/RectangleOpacityFadeExample.xaml#rectangleopacityfadeexampleinline_2)]  
  
3.  添加<xref:System.Windows.EventTrigger>到<xref:System.Windows.FrameworkElement.Triggers%2A>的矩形的集合。  
  
     [!code-xml[animation_ovws_snippet#RectangleOpacityFadeExampleInline_1](../../../../samples/snippets/csharp/VS_Snippets_Wpf/animation_ovws_snippet/CS/RectangleOpacityFadeExample.xaml#rectangleopacityfadeexampleinline_1)]  
  
<a name="opacity_animation_step3code"></a>   
### <a name="part-3-code-associate-the-storyboard-with-an-event-handler"></a>第 3 （代码） 部分︰ 关联演示图板与事件处理程序  
 应用并启动的最简单办法<xref:System.Windows.Media.Animation.Storyboard>在代码中是使用一个事件处理程序。 本部分说明如何将相关联<xref:System.Windows.Media.Animation.Storyboard>与在代码中的事件处理程序。  
  
1.  注册以进行<xref:System.Windows.FrameworkElement.Loaded>的矩形的事件。  
  
     [!code-csharp[animation_ovws2#RectangleOpacityFadeExampleCode_104](../../../../samples/snippets/csharp/VS_Snippets_Wpf/animation_ovws2/CSharp/MainWindow.xaml.cs#rectangleopacityfadeexamplecode_104)]
     [!code-vb[animation_ovws2#RectangleOpacityFadeExampleCode_104](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/animation_ovws2/VisualBasic/MainWindow.xaml.vb#rectangleopacityfadeexamplecode_104)]  
  
2.  声明事件处理程序。 在事件处理程序中，使用<xref:System.Windows.Media.Animation.Storyboard.Begin%2A>方法应用情节提要。  
  
     [!code-csharp[animation_ovws2#RectangleOpacityFadeExampleCode_105](../../../../samples/snippets/csharp/VS_Snippets_Wpf/animation_ovws2/CSharp/MainWindow.xaml.cs#rectangleopacityfadeexamplecode_105)]
     [!code-vb[animation_ovws2#RectangleOpacityFadeExampleCode_105](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/animation_ovws2/VisualBasic/MainWindow.xaml.vb#rectangleopacityfadeexamplecode_105)]  
  
### <a name="complete-example"></a>完整的示例  
 下面演示如何创建一个淡入淡出视图在 XAML 中的矩形。  
  
 [!code-xml[animation_ovws2#RectangleOpacityFadeExampleXaml](../../../../samples/snippets/csharp/VS_Snippets_Wpf/animation_ovws2/CSharp/MainWindow.xaml#rectangleopacityfadeexamplexaml)]  
  
 下面演示如何创建一个淡入淡出代码中的视图的矩形。  
  
 [!code-csharp[animation_ovws2#RectangleOpacityFadeExampleCode](../../../../samples/snippets/csharp/VS_Snippets_Wpf/animation_ovws2/CSharp/MainWindow.xaml.cs#rectangleopacityfadeexamplecode)]
 [!code-vb[animation_ovws2#RectangleOpacityFadeExampleCode](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/animation_ovws2/VisualBasic/MainWindow.xaml.vb#rectangleopacityfadeexamplecode)]  
  
<a name="animationtypes"></a>   
## <a name="animation-types"></a>动画类型  
 由于动画生成属性值，不同的动画类型存在不同的属性类型。 采用属性进行动画处理<xref:System.Double>，如<xref:System.Windows.FrameworkElement.Width%2A>的元素属性的使用会产生一个动画<xref:System.Double>值。 采用属性进行动画处理<xref:System.Windows.Point>，使用生成的动画<xref:System.Windows.Point>值，等等。 由于不同的属性类型的数目，几个动画类中的<xref:System.Windows.Media.Animation>命名空间。 幸运的是，它们遵循严格的命名约定，可方便地了解它们之间的区别︰  
  
-   \<                         *类型*1> 动画  
  
     也称为"From/To/By"或"基本"动画，这些设置动画效果开始值和目标值之间，或通过向其起始值添加偏移量的值。  
  
    -   若要指定一个起始值，设置动画的 From 属性。  
  
    -   若要指定的结束值，设置动画的 To 属性。  
  
    -   若要指定的偏移量的值，设置动画的 By 属性。  
  
     此概述中的示例使用这些动画，因为它们是最容易使用。 From/To/By 动画概述中详细描述了 From/To/By 动画。  
  
-   \<                         *类型*1> 备选项  
  
     关键帧动画可以比 From/To/By 动画功能更强大，因为您可以指定任意数量的目标值，甚至可以控制它们的插值方法。 某些类型只使用关键帧动画进行动画处理。 中详细描述了关键帧动画[关键帧动画概述](../../../../docs/framework/wpf/graphics-multimedia/key-frame-animations-overview.md)。  
  
-   \<                         *类型*1> AnimationUsingPath  
  
     路径动画，可以使用几何路径来生成动画的值。  
  
-   \<                         *类型*1> AnimationBase  
  
     抽象类在实现时进行动画处理<>*类型*1> 的值。 此类用作类的基类<>*类型*1> 动画和<>*类型*1> 备选项的类。 您必须直接处理这些类，仅当你想要创建自定义动画。 否则，请使用<>*类型*1> 动画或关键帧<>*类型*1> 动画。  
  
 在大多数情况下，您将想要使用<>*类型*1> 动画类，如<xref:System.Windows.Media.Animation.DoubleAnimation>和<xref:System.Windows.Media.Animation.ColorAnimation>。  
  
 下表显示了一些常见动画类型以及同它们使用某些属性。  
  
|属性类型|对应的 (From/To/By) 的基本动画|对应的关键帧动画|对应的路径动画|用法示例|  
|-------------------|----------------------------------------------------|---------------------------------------|----------------------------------|-------------------|  
|<xref:System.Windows.Media.Color>|<xref:System.Windows.Media.Animation.ColorAnimation>|<xref:System.Windows.Media.Animation.ColorAnimationUsingKeyFrames>|无|Animate the                                  <xref:System.Windows.Media.SolidColorBrush.Color%2A> of a                                  <xref:System.Windows.Media.SolidColorBrush> or a                                  <xref:System.Windows.Media.GradientStop>.|  
|<xref:System.Double>|<xref:System.Windows.Media.Animation.DoubleAnimation>|<xref:System.Windows.Media.Animation.DoubleAnimationUsingKeyFrames>|<xref:System.Windows.Media.Animation.DoubleAnimationUsingPath>|Animate the                                  <xref:System.Windows.FrameworkElement.Width%2A> of a                                  <xref:System.Windows.Controls.DockPanel> or the                                  <xref:System.Windows.FrameworkElement.Height%2A> of a                                  <xref:System.Windows.Controls.Button>.|  
|<xref:System.Windows.Point>|<xref:System.Windows.Media.Animation.PointAnimation>|<xref:System.Windows.Media.Animation.PointAnimationUsingKeyFrames>|<xref:System.Windows.Media.Animation.PointAnimationUsingPath>|进行动画处理<xref:System.Windows.Media.EllipseGeometry.Center%2A>位置<xref:System.Windows.Media.EllipseGeometry>。|  
|<xref:System.String>|无|<xref:System.Windows.Media.Animation.StringAnimationUsingKeyFrames>|无|Animate the                                  <xref:System.Windows.Controls.TextBlock.Text%2A> of a                                  <xref:System.Windows.Controls.TextBlock> or the                                  <xref:System.Windows.Controls.ContentControl.Content%2A> of a                                  <xref:System.Windows.Controls.Button>.|  
  
<a name="animationsaretimelines"></a>   
### <a name="animations-are-timelines"></a>动画是时间线  
 所有动画类型都继承自<xref:System.Windows.Media.Animation.Timeline>类; 因此，所有动画都是特殊的类型的时间线。 一个<xref:System.Windows.Media.Animation.Timeline>定义的时间段。 您可以指定*计时行为*时间线的︰ 其<xref:System.Windows.Media.Animation.Timeline.Duration%2A>，它是重复发生，或甚至多快时间走得多少次。  
  
 因为动画是<xref:System.Windows.Media.Animation.Timeline>，它还表示一个时间段。 动画还计算输出值逐步的过程但是其指定的时间段 (或<xref:System.Windows.Media.Animation.Timeline.Duration%2A>)。 作为动画运行时，或"播放"中，它将更新与之关联的属性。  
  
 有三个常用的计时属性<xref:System.Windows.Media.Animation.Timeline.Duration%2A>， <xref:System.Windows.Media.Animation.Timeline.AutoReverse%2A>，和<xref:System.Windows.Media.Animation.Timeline.RepeatBehavior%2A>。  
  
#### <a name="the-duration-property"></a>持续时间属性  
 如前文所述，时间线表示时间的段。 段的长度由<xref:System.Windows.Media.Animation.Timeline.Duration%2A>时间线上，通常通过使用指定的<xref:System.Windows.Duration.TimeSpan%2A>值。 当时间线达到其持续时间的末尾时，则已经完成一次迭代。  
  
 动画使用其<xref:System.Windows.Media.Animation.Timeline.Duration%2A>属性来确定其当前值。 如果未指定<xref:System.Windows.Media.Animation.Timeline.Duration%2A>值动画，它使用 1 秒，这是默认值。  
  
 下面的语法演示的简化的版本[!INCLUDE[TLA#tla_xaml](../../../../includes/tlasharptla-xaml-md.md)]特性语法<xref:System.Windows.Media.Animation.Timeline.Duration%2A>属性。  
  
||  
|-|  
|*hours* `:` *minutes* `:` *seconds*|  
  
 下表显示了几个<xref:System.Windows.Duration>设置及其生成的值。  
  
|设置|生成的值|  
|-------------|---------------------|  
|0:0:5.5|5.5 秒。|  
|0:30:5.5|30 分钟 5.5 秒。|  
|1:30:5.5|1 小时 30 分钟，和 5.5 秒。|  
  
 指定的一种方法<xref:System.Windows.Duration>在代码中是使用<xref:System.TimeSpan.FromSeconds%2A>方法来创建<xref:System.TimeSpan>，然后，声明一个新<xref:System.Windows.Duration>结构使用，而这些<xref:System.TimeSpan>。  
  
 有关详细信息<xref:System.Windows.Duration>值和完整[!INCLUDE[TLA#tla_xaml](../../../../includes/tlasharptla-xaml-md.md)]语法，请参阅<xref:System.Windows.Duration>结构。  
  
#### <a name="autoreverse"></a>AutoReverse  
 <xref:System.Windows.Media.Animation.Timeline.AutoReverse%2A>属性指定时间线的向后播放在达到结束后其<xref:System.Windows.Media.Animation.Timeline.Duration%2A>。 如果此动画属性设置为`true`，动画则完全反转后到达末尾其<xref:System.Windows.Media.Animation.Timeline.Duration%2A>、 播放从其终止值返回到其起始值。 默认情况下，此属性是`false`。  
  
#### <a name="repeatbehavior"></a>RepeatBehavior  
 <xref:System.Windows.Media.Animation.Timeline.RepeatBehavior%2A>属性指定的时间线播放的次数。 默认情况下，时间线有个迭代计数`1.0`，这意味着他们玩一个游戏时间，并执行不会重复。  
  
 有关这些属性和其他工具的详细信息，请参阅[计时行为概述](../../../../docs/framework/wpf/graphics-multimedia/timing-behaviors-overview.md)。  
  
<a name="applyanimationstoproperty"></a>   
## <a name="applying-an-animation-to-a-property"></a>与某个属性应用动画  
 前面几节描述了不同类型的动画和其执行时间属性。 本部分说明如何将动画应用于要进行动画处理的属性。                  <xref:System.Windows.Media.Animation.Storyboard>对象提供了一种方法将动画应用于属性。 一个<xref:System.Windows.Media.Animation.Storyboard>是*容器时间线*提供有关它所包含的动画的目标信息。  
  
### <a name="targeting-objects-and-properties"></a>目标对象和属性  
 <xref:System.Windows.Media.Animation.Storyboard>类提供了<xref:System.Windows.Media.Animation.Storyboard.TargetName%2A>和<xref:System.Windows.Media.Animation.Storyboard.TargetProperty%2A>附加属性。 通过在动画上设置这些属性，可指示动画内容进行动画处理。 但是，动画可以针对一个对象之前，该对象必须通常为指定名称。  
  
 指定将名称传递给<xref:System.Windows.FrameworkElement>不同于分配将名称传递给<xref:System.Windows.Freezable>对象。 大多数控件和面板是框架元素;但是，大多数纯粹图形对象，例如画笔、 转换和几何图形，是 freezable 对象。 如果您不能确定某类型是否是<xref:System.Windows.FrameworkElement>或<xref:System.Windows.Freezable>，请参阅**继承层次结构**其参考文档的部分。  
  
-   若要使<xref:System.Windows.FrameworkElement>成为动画目标，则指定的名称通过设置其<xref:System.Windows.FrameworkElement.Name%2A>属性。 在代码中，您必须使用<xref:System.Windows.FrameworkElement.RegisterName%2A>方法以向它属于页上注册的元素名称。  
  
-   若要使<xref:System.Windows.Freezable>对象中的动画目标[!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)]，您使用[X:name 指令](../../../../docs/framework/xaml-services/x-name-directive.md)以将其分配一个名称。 在代码中，您只需使用<xref:System.Windows.FrameworkElement.RegisterName%2A>方法以向它属于页上注册该对象。  
  
 以下各节提供举例说明如何为元素命名[!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)]和代码。 有关命名和确定目标的更多详细信息，请参阅[演示图板概述](../../../../docs/framework/wpf/graphics-multimedia/storyboards-overview.md)。  
  
### <a name="applying-and-starting-storyboards"></a>应用和启动情节提要  
 若要启动演示图板[!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)]，与之相关<xref:System.Windows.EventTrigger>。 <xref:System.Windows.EventTrigger>是一个对象，描述了指定的事件发生时要采取的操作。 其中一个这些操作可以是<xref:System.Windows.Media.Animation.BeginStoryboard>用于启动你的情节提要的操作。 事件触发器是在概念上类似于事件处理程序，因为它们使你可以指定您的应用程序如何响应特定事件。 与事件处理程序不同，事件触发器可全面地描述了在[!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)]; 不不需要任何其他代码。  
  
 若要启动<xref:System.Windows.Media.Animation.Storyboard>在代码中，您可以使用<xref:System.Windows.EventTrigger>或使用<xref:System.Windows.Media.Animation.Storyboard.Begin%2A>方法<xref:System.Windows.Media.Animation.Storyboard>类。  
  
<a name="controllingstoryboards"></a>   
## <a name="interactively-control-a-storyboard"></a>以交互方式控制演示图板  
 前面的示例演示如何启动<xref:System.Windows.Media.Animation.Storyboard>事件的发生时间。 您可以采用交互方式控制<xref:System.Windows.Media.Animation.Storyboard>启动后对它︰ 可以 pause、 resume、 停止、 前进至其填充周期、 搜索和删除<xref:System.Windows.Media.Animation.Storyboard>。 有关详细信息和示例演示如何以交互方式控制<xref:System.Windows.Media.Animation.Storyboard>，请参阅[演示图板概述](../../../../docs/framework/wpf/graphics-multimedia/storyboards-overview.md)。  
  
<a name="fillbehaviorsection"></a>   
## <a name="what-happens-after-an-animation-ends"></a>动画结束后，会发生什么情况？  
 <xref:System.Windows.Media.Animation.FillBehavior>属性指定时间线结束时的行为。 默认情况下，时间线开始<xref:System.Windows.Media.Animation.ClockState>结束的时候。 是一个动画<xref:System.Windows.Media.Animation.ClockState>保持其最终输出值。  
  
 <xref:System.Windows.Media.Animation.DoubleAnimation>在前面的示例不会结束因为其<xref:System.Windows.Media.Animation.Timeline.RepeatBehavior%2A>属性设置为<xref:System.Windows.Media.Animation.RepeatBehavior.Forever%2A>。 下面的示例使用类似的动画，进行动画处理一个矩形。 与上述示例中，不同<xref:System.Windows.Media.Animation.Timeline.RepeatBehavior%2A>和<xref:System.Windows.Media.Animation.Timeline.AutoReverse%2A>此动画的属性保留为其默认值。 因此，该动画从进展 1 为 0 时间超过五秒，然后停止。  
  
 [!code-xml[animation_ovws_snippet#FillBehaviorExampleRectangleInline](../../../../samples/snippets/csharp/VS_Snippets_Wpf/animation_ovws_snippet/CS/FillBehaviorExample.xaml#fillbehaviorexamplerectangleinline)]  
  
 [!code-csharp[animation_ovws_procedural_snip#FillBehaviorExampleRectangleInline](../../../../samples/snippets/csharp/VS_Snippets_Wpf/animation_ovws_procedural_snip/CSharp/FillBehaviorExample.cs#fillbehaviorexamplerectangleinline)]
 [!code-vb[animation_ovws_procedural_snip#FillBehaviorExampleRectangleInline](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/animation_ovws_procedural_snip/visualbasic/fillbehaviorexample.vb#fillbehaviorexamplerectangleinline)]  
  
 由于其<xref:System.Windows.Media.Animation.Timeline.FillBehavior%2A>未发生变化，其默认值，即<xref:System.Windows.Media.Animation.FillBehavior>，动画将保持其最终值为 0，它何时结束。 因此，<xref:System.Windows.UIElement.Opacity%2A>矩形仍然为动画之后的 0 的结束。 如果您设置<xref:System.Windows.UIElement.Opacity%2A>为其他值在该矩形，代码似乎不起作用，因为动画仍将影响<xref:System.Windows.UIElement.Opacity%2A>属性。  
  
 若要重新获得的代码中的动态属性控制的一种方法是使用<xref:System.Windows.Media.Animation.Animatable.BeginAnimation%2A>方法并指定为 null <xref:System.Windows.Media.Animation.AnimationTimeline>参数。 有关详细信息和示例，请参阅[属性之后进行动画处理将其设置使用演示图板](../../../../docs/framework/wpf/graphics-multimedia/how-to-set-a-property-after-animating-it-with-a-storyboard.md)。  
  
 请注意，尽管设置属性值具有<xref:System.Windows.Media.Animation.ClockState>或<xref:System.Windows.Media.Animation.ClockState>动画似乎不起作用，属性值确实更改。 有关详细信息，请参阅[动画和计时系统概述](../../../../docs/framework/wpf/graphics-multimedia/animation-and-timing-system-overview.md)。  
  
<a name="databindingAndAnimatingAnimationsSection"></a>   
## <a name="data-binding-and-animating-animations"></a>数据绑定和动画处理  
 大多数动画的属性可以进行数据绑定或动画;例如，您可以设置动画效果<xref:System.Windows.Media.Animation.Timeline.Duration%2A>属性<xref:System.Windows.Media.Animation.DoubleAnimation>。 但是，由于计时系统工作的方式，数据绑定或动画的动画不类似于其他数据绑定或动画处理的对象。 若要了解它们的行为，它有助于理解其含义将动画应用于属性。  
  
 介绍了如何进行动画处理的上一节中的示例，请参阅<xref:System.Windows.UIElement.Opacity%2A>的矩形。 当加载上一示例中的矩形时，它的事件触发器适用<xref:System.Windows.Media.Animation.Storyboard>。 计时系统会创建一份<xref:System.Windows.Media.Animation.Storyboard>及其动画。 这些副本均已冻结 （使其只读的） 和<xref:System.Windows.Media.Animation.Clock>从中创建对象。 这些时钟执行目标的属性进行动画处理的实际工作。  
  
 计时系统创建的时钟<xref:System.Windows.Media.Animation.DoubleAnimation>并将其应用到的对象和属性所指定的<xref:System.Windows.Media.Animation.Storyboard.TargetName%2A>和<xref:System.Windows.Media.Animation.Storyboard.TargetProperty%2A>的<xref:System.Windows.Media.Animation.DoubleAnimation>。 计时系统在这种情况下，应用到时钟<xref:System.Windows.UIElement.Opacity%2A>名为"MyRectangle。"的对象属性  
  
 尽管对于还创建一个时钟<xref:System.Windows.Media.Animation.Storyboard>，时钟不应用于任何属性。 其目的是控制其子时钟，为创建的时钟<xref:System.Windows.Media.Animation.DoubleAnimation>。  
  
 供动画使用，以反映数据绑定或动画更改，必须重新生成它的时钟。 时钟不会重新生成为你自动。 若要使动画反映的变化，其情节提要，通过重新应用使用<xref:System.Windows.Media.Animation.BeginStoryboard>或<xref:System.Windows.Media.Animation.Storyboard.Begin%2A>方法。 在使用上述任一方法时，将重新启动动画。 在代码中，您可以使用<xref:System.Windows.Media.Animation.Storyboard.Seek%2A>方法将演示图板移回到其以前的位置。  
  
 有关举例说明如何数据绑定动画，请参阅[密钥样条动画示例](http://go.microsoft.com/fwlink/?LinkID=160011)。                  有关动画和计时系统的工作原理的详细信息，请参阅[动画和计时系统概述](../../../../docs/framework/wpf/graphics-multimedia/animation-and-timing-system-overview.md)。  
  
<a name="otherWaysToAnimateSection"></a>   
## <a name="other-ways-to-animate"></a>其他方法进行动画处理  
 本概述中的示例演示如何使用演示图板进行动画处理。 当您使用的代码时，您可以其它几种方法中创建动画。 有关详细信息，请参阅[属性动画技术概述](../../../../docs/framework/wpf/graphics-multimedia/property-animation-techniques-overview.md)。  
  
<a name="animation_samples"></a>   
## <a name="animation-samples"></a>动画示例  
 以下示例可帮助您开始将动画添加到您的应用程序。  
  
-   [From、 To 和动画目标值示例](http://go.microsoft.com/fwlink/?LinkID=159988)  
  
     演示不同 From/To/By 的设置。  
  
-   [动画计时行为的示例](http://go.microsoft.com/fwlink/?LinkID=159970)  
  
     演示您可以控制动画的计时行为的不同方法。 此示例还演示如何将数据绑定到动画的目标值。  
  
<a name="related_topics"></a>   
## <a name="related-topics"></a>相关主题  
  
|标题|描述|  
|-----------|-----------------|  
|[动画和计时系统概述](../../../../docs/framework/wpf/graphics-multimedia/animation-and-timing-system-overview.md)|描述如何使用计时系统<xref:System.Windows.Media.Animation.Timeline>和<xref:System.Windows.Media.Animation.Clock>类，该类允许您创建动画。|  
|[动画提示和技巧](../../../../docs/framework/wpf/graphics-multimedia/animation-tips-and-tricks.md)|列出有关解决与动画、 性能等相关问题的有用提示。|  
|[自定义动画概述](../../../../docs/framework/wpf/graphics-multimedia/custom-animations-overview.md)|描述如何扩展动画系统使用关键帧，动画类或每帧回调。|  
|From/To/By 动画概述|描述如何创建两个值之间进行过渡动画。|  
|[关键帧动画概述](../../../../docs/framework/wpf/graphics-multimedia/key-frame-animations-overview.md)|描述如何使用多个目标值，包括能够控制的内插方法创建动画。|  
|[缓动函数](../../../../docs/framework/wpf/graphics-multimedia/easing-functions.md)|说明如何将数学公式应用于动画以获得真实的行为，如弹跳。|  
|[路径动画概述](../../../../docs/framework/wpf/graphics-multimedia/path-animations-overview.md)|描述如何移动或旋转沿复杂路径对象。|  
|[属性动画技术概述](../../../../docs/framework/wpf/graphics-multimedia/property-animation-techniques-overview.md)|描述使用演示图板属性动画、 本地动画、 时钟和基于帧的动画。|  
|[演示图板概述](../../../../docs/framework/wpf/graphics-multimedia/storyboards-overview.md)|描述如何使用多个时间线的情节提要创建复杂的动画。|  
|[计时行为概述](../../../../docs/framework/wpf/graphics-multimedia/timing-behaviors-overview.md)|描述<xref:System.Windows.Media.Animation.Timeline>类型和动画中使用的属性。|  
|[计时事件概述](../../../../docs/framework/wpf/graphics-multimedia/timing-events-overview.md)|描述上可用的事件<xref:System.Windows.Media.Animation.Timeline>和<xref:System.Windows.Media.Animation.Clock>对象的点上执行代码在时间线，如开始、 暂停、 恢复、 跳过，或停止。|  
|[操作指南主题](../../../../docs/framework/wpf/graphics-multimedia/animation-and-timing-how-to-topics.md)|包含在您的应用程序中使用动画和时间线的代码示例。|  
|[时钟帮助主题](../../../../docs/framework/wpf/graphics-multimedia/clocks-how-to-topics.md)|包含代码示例使用<xref:System.Windows.Media.Animation.Clock>应用程序中的对象。|  
|[关键帧动画帮助主题](../../../../docs/framework/wpf/graphics-multimedia/key-frame-animation-how-to-topics.md)|包含在您的应用程序中使用关键帧动画的代码示例。|  
|[路径动画帮助主题](../../../../docs/framework/wpf/graphics-multimedia/path-animation-how-to-topics.md)|包含在您的应用程序中使用路径动画的代码示例。|  
  
<a name="reference"></a>   
## <a name="reference"></a>参考  
 <xref:System.Windows.Media.Animation.Timeline>  
  
 <xref:System.Windows.Media.Animation.Storyboard>  
  
 <xref:System.Windows.Media.Animation.BeginStoryboard>  
  
 <xref:System.Windows.Media.Animation.Clock>