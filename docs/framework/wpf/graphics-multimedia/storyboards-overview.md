---
title: "演示图板概述 | Microsoft Docs"
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
  - "演示图板语法"
  - "语法, Storyboard"
  - "时间线"
ms.assetid: 1a698c3c-30f1-4b30-ae56-57e8a39811bd
caps.latest.revision: 31
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 26
---
# 演示图板概述
本主题演示如何使用 <xref:System.Windows.Media.Animation.Storyboard> 对象来组织和应用动画，  还描述了如何交互操作 <xref:System.Windows.Media.Animation.Storyboard> 对象，并介绍了间接属性目标语法。  
  
<a name="autoTopLevelSectionsOUTLINE0"></a>   
<a name="prerequisites"></a>   
## 必备组件  
 要了解本主题，您应当熟悉不同的动画类型及其基本功能。  有关动画的简介，请参见[动画概述](../../../../docs/framework/wpf/graphics-multimedia/animation-overview.md)。  您还应当了解如何使用附加属性。  有关附加属性的更多信息，请参见[附加属性概述](../../../../docs/framework/wpf/advanced/attached-properties-overview.md)。  
  
<a name="whatisatimeline"></a>   
## 什么是 Storyboard？  
 动画不是唯一有用的时间线类型。  还提供了其他时间线类来帮助您组织时间线集合，并将时间线应用于属性。  容器时间线派生自 <xref:System.Windows.Media.Animation.TimelineGroup> 类，包括 <xref:System.Windows.Media.Animation.ParallelTimeline> 和 <xref:System.Windows.Media.Animation.Storyboard>。  
  
 <xref:System.Windows.Media.Animation.Storyboard> 是一种为其所包含的时间线提供目标信息的容器时间线。  演示图板可以包含任意类型的 <xref:System.Windows.Media.Animation.Timeline>，包括其他容器时间线和动画。  可以使用 <xref:System.Windows.Media.Animation.Storyboard> 对象将影响各种对象和属性的时间线组合成一个时间线树，以便于组织和控制复杂的计时行为。  例如，假设您需要一个执行以下三个操作的按钮。  
  
-   当用户选择该按钮时，该按钮增大并更改颜色。  
  
-   当单击该按钮时，该按钮缩小并恢复其原始大小。  
  
-   当该按钮变成禁用时，缩小且不透明度缩减到 50%。  
  
 在此例中，您具有适用于同一对象的多组动画，并且需要根据按钮的状态在不同的时间播放。  可以使用 <xref:System.Windows.Media.Animation.Storyboard> 对象来组织动画，并将它们成组地应用于一个或多个对象。  
  
<a name="wherecanyouuseastoryboard"></a>   
## 在什么情况下使用 Storyboard？  
 可以使用 <xref:System.Windows.Media.Animation.Storyboard> 对可动画处理的类的[依赖项属性](GTMT)进行动画处理（有关如何使类成为可动画处理的类的更多信息，请参见[动画概述](../../../../docs/framework/wpf/graphics-multimedia/animation-overview.md)）。  不过，由于图板演示是框架级别的功能，该对象必须属于 <xref:System.Windows.FrameworkElement> 或 <xref:System.Windows.FrameworkContentElement> 的 <xref:System.Windows.NameScope>。  
  
 例如，您可以使用 <xref:System.Windows.Media.Animation.Storyboard> 执行以下操作：  
  
-   对用于绘制按钮（一种 <xref:System.Windows.FrameworkElement>）背景的 <xref:System.Windows.Media.SolidColorBrush>（非框架元素）进行动画处理，  
  
-   对用于绘制使用 <xref:System.Windows.Controls.Image> \(<xref:System.Windows.FrameworkElement>\) 显示的 <xref:System.Windows.Media.GeometryDrawing>（非框架元素）的填充的 <xref:System.Windows.Media.SolidColorBrush>（非框架元素）进行动画处理，  
  
-   在代码中，如果 <xref:System.Windows.Media.SolidColorBrush> 向 <xref:System.Windows.FrameworkElement> 注册其名称，则对包含该 <xref:System.Windows.FrameworkElement> 的类所声明的 <xref:System.Windows.Media.SolidColorBrush> 进行动画处理。  
  
 但是，不能使用 <xref:System.Windows.Media.Animation.Storyboard> 来对未向 <xref:System.Windows.FrameworkElement> 或 <xref:System.Windows.FrameworkContentElement> 注册其名称或未用于设置 <xref:System.Windows.FrameworkElement> 或 <xref:System.Windows.FrameworkContentElement> 的属性的 <xref:System.Windows.Media.SolidColorBrush> 进行动画处理。  
  
<a name="applyanimationswithastoryboard"></a>   
## 如何使用 Storyboard 应用动画  
 若要使用 <xref:System.Windows.Media.Animation.Storyboard> 来组织和应用动画，可以将动画添加为 <xref:System.Windows.Media.Animation.Storyboard> 的子时间线。  <xref:System.Windows.Media.Animation.Storyboard> 类提供 <xref:System.Windows.Media.Animation.Storyboard.TargetName%2A?displayProperty=fullName> 和 <xref:System.Windows.Media.Animation.Storyboard.TargetProperty%2A?displayProperty=fullName> 附加属性。  您可以在动画上设置这些属性以指定其目标对象和属性。  
  
 若要将动画应用于其目标，您可以使用触发器操作或方法来开始 <xref:System.Windows.Media.Animation.Storyboard>。  在 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] 中，将 <xref:System.Windows.Media.Animation.BeginStoryboard> 对象与 <xref:System.Windows.EventTrigger>、<xref:System.Windows.Trigger> 或 <xref:System.Windows.DataTrigger> 一起使用。  在代码中，还可以使用 <xref:System.Windows.Media.Animation.Storyboard.Begin%2A> 方法。  
  
 下表列出了支持每个 <xref:System.Windows.Media.Animation.Storyboard> 开始技术的不同方面：基于实例、样式、控件模板和数据模板。"  基于实例”指的是直接将动画或演示图板应用于对象实例（而不是在样式、控件模板或数据模板中应用）的技术。  
  
|开始演示图板时使用…|基于实例|样式|控件模板|数据模板|示例|  
|----------------|----------|--------|----------|----------|--------|  
|<xref:System.Windows.Media.Animation.BeginStoryboard> 和 <xref:System.Windows.EventTrigger>|是|是|是|是|[使用演示图板对属性进行动画处理](../../../../docs/framework/wpf/graphics-multimedia/how-to-animate-a-property-by-using-a-storyboard.md)|  
|<xref:System.Windows.Media.Animation.BeginStoryboard> 和属性 <xref:System.Windows.Trigger>|否|是|是|是|[在属性值更改时触发动画](../../../../docs/framework/wpf/graphics-multimedia/how-to-trigger-an-animation-when-a-property-value-changes.md)|  
|<xref:System.Windows.Media.Animation.BeginStoryboard> 和 <xref:System.Windows.DataTrigger>|否|是|是|是|[How to: Trigger an Animation When Data Changes](http://msdn.microsoft.com/zh-cn/a736bb3a-2ae5-479a-a33a-75a27055d863)|  
|<xref:System.Windows.Media.Animation.Storyboard.Begin%2A> 方法|是|否|否|否|[使用演示图板对属性进行动画处理](../../../../docs/framework/wpf/graphics-multimedia/how-to-animate-a-property-by-using-a-storyboard.md)|  
  
 下面的示例使用 <xref:System.Windows.Media.Animation.Storyboard> 对 <xref:System.Windows.Shapes.Rectangle> 元素的 <xref:System.Windows.FrameworkElement.Width%2A> 和用于绘制该 <xref:System.Windows.Shapes.Rectangle> 的 <xref:System.Windows.Media.SolidColorBrush> 的 <xref:System.Windows.Media.SolidColorBrush.Color%2A> 进行动画处理。  
  
  
  
 [!code-csharp[storyboards_ovw_snip#100](../../../../samples/snippets/csharp/VS_Snippets_Wpf/storyboards_ovw_snip/CSharp/StoryboardsExample.cs#100)]  
  
 以下几节更详细地描述了 <xref:System.Windows.Media.Animation.Storyboard.TargetName%2A> 和 <xref:System.Windows.Media.Animation.Storyboard.TargetProperty%2A> 附加属性。  
  
<a name="targetingelementsandfreezables"></a>   
## 以框架元素、框架内容元素和 Freezable 元素为目标  
 上面一节提到对于动画，要查找其目标，必须知道目标的名称和要进行动画处理的属性。  指定要进行动画处理的属性非常直接：只需用要进行动画处理的属性的名称来设置 <xref:System.Windows.Media.Animation.Storyboard.TargetProperty%2A?displayProperty=fullName> 即可。  通过在动画上设置 <xref:System.Windows.Media.Animation.Storyboard.TargetName%2A?displayProperty=fullName> 属性来指定具有要进行动画处理的属性的对象的名称。  
  
 为了使 <xref:System.Windows.Setter.TargetName%2A> 属性起作用，目标对象必须有名称。  在 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] 中为 <xref:System.Windows.FrameworkElement> 或 <xref:System.Windows.FrameworkContentElement> 分配名称不同于为 <xref:System.Windows.Freezable> 对象分配名称。  
  
 框架元素是从 <xref:System.Windows.FrameworkElement> 类继承的类。  框架元素的示例包括 <xref:System.Windows.Window>、<xref:System.Windows.Controls.DockPanel>、<xref:System.Windows.Controls.Button> 和 <xref:System.Windows.Shapes.Rectangle>。  从本质上而言，所有窗口、面板和控件都是元素。  框架内容元素是从 <xref:System.Windows.FrameworkContentElement> 类继承的类。  框架内容元素的示例包括 <xref:System.Windows.Documents.FlowDocument> 和 <xref:System.Windows.Documents.Paragraph>。  如果您不确定某类型是否是框架元素或框架内容元素，请查看它是否具有 Name 属性。  如果它具有 Name 属性，则可能是框架元素或框架内容元素。  若要进一步确定，请检查其类型页面的“继承层次结构”部分。  
  
 若要在 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] 中以框架元素或框架内容元素为目标，请设置其 <xref:System.Windows.FrameworkElement.Name%2A> 属性。  在代码中，还需要使用 <xref:System.Windows.NameScope.RegisterName%2A> 方法向为其创建了 <xref:System.Windows.NameScope> 的元素注册该元素名称。  
  
 下面的示例摘自上一个示例，它为一个 <xref:System.Windows.Shapes.Rectangle>（一种 <xref:System.Windows.FrameworkElement>）分配名称 `MyRectangle`。  
  
  
  
 [!code-csharp[storyboards_ovw_snip#102](../../../../samples/snippets/csharp/VS_Snippets_Wpf/storyboards_ovw_snip/CSharp/StoryboardsExample.cs#102)]  
  
 在该元素具有名称后，可以对其属性进行动画处理。  
  
  
  
 [!code-csharp[storyboards_ovw_snip#105](../../../../samples/snippets/csharp/VS_Snippets_Wpf/storyboards_ovw_snip/CSharp/StoryboardsExample.cs#105)]  
  
 <xref:System.Windows.Freezable> 类型是从 <xref:System.Windows.Freezable> 类继承的类。  <xref:System.Windows.Freezable> 的示例包括 <xref:System.Windows.Media.SolidColorBrush>、<xref:System.Windows.Media.RotateTransform> 和 <xref:System.Windows.Media.GradientStop>。  
  
 若要在 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] 中以 <xref:System.Windows.Freezable> 作为动画的目标，可以使用 [x:Name 指令](../../../../docs/framework/xaml-services/x-name-directive.md)为其分配名称。  在代码中，可以使用 <xref:System.Windows.NameScope.RegisterName%2A> 方法向已为其创建了 <xref:System.Windows.NameScope> 的元素注册其名称。  
  
 下面的示例为 <xref:System.Windows.Freezable> 对象分配名称。  
  
  
  
 [!code-csharp[storyboards_ovw_snip#103](../../../../samples/snippets/csharp/VS_Snippets_Wpf/storyboards_ovw_snip/CSharp/StoryboardsExample.cs#103)]  
  
 然后动画可以以该对象为目标。  
  
  
  
 [!code-csharp[storyboards_ovw_snip#107](../../../../samples/snippets/csharp/VS_Snippets_Wpf/storyboards_ovw_snip/CSharp/StoryboardsExample.cs#107)]  
  
 <xref:System.Windows.Media.Animation.Storyboard> 对象使用名称范围解析 <xref:System.Windows.Media.Animation.Storyboard.TargetName%2A> 属性。  有关 WPF 名称范围的更多信息，请参见 [WPF XAML 名称范围](../../../../docs/framework/wpf/advanced/wpf-xaml-namescopes.md)。  如果忽略 <xref:System.Windows.Media.Animation.Storyboard.TargetName%2A> 属性，动画则以定义该属性时所在的元素为目标（如果存在样式，则以带样式的元素为目标）。  
  
 有时，不能为 <xref:System.Windows.Freezable> 对象分配名称。  例如，如果 <xref:System.Windows.Freezable> 声明为资源，或者用于设置样式中的属性值，则不能为该对象分配名称。  由于它没有名称，因此不能直接以它为目标 \- 但是可以间接以它为目标。  下面几节描述如何使用间接目标。  
  
<a name="pathsyntaxforchangeable"></a>   
## 间接目标  
 有时动画不能直接以 <xref:System.Windows.Freezable> 为目标，例如当 <xref:System.Windows.Freezable> 声明为资源或者用于设置样式中的属性值时。  在这些情况下，即使不能直接将 <xref:System.Windows.Freezable> 对象作为目标，您仍可以对其进行动画处理。  您可以为 <xref:System.Windows.Media.Animation.Storyboard.TargetName%2A> 属性分配 <xref:System.Windows.Freezable>“所属”的元素的名称，而不是使用 <xref:System.Windows.Freezable> 的名称来设置该属性。例如，<xref:System.Windows.Media.SolidColorBrush> 用于设置矩形元素的 <xref:System.Windows.Shapes.Shape.Fill%2A> 属于该矩形。  若要对该画笔进行动画处理，您需要使用一个属性链来设置动画的 <xref:System.Windows.Media.Animation.Storyboard.TargetProperty%2A>，这些属性起始于使用 <xref:System.Windows.Freezable> 设置的框架元素或框架内容元素的属性，结束于要进行动画处理的 <xref:System.Windows.Freezable> 属性。  
  
  
  
 [!code-csharp[storyboards_ovw_snip#134](../../../../samples/snippets/csharp/VS_Snippets_Wpf/storyboards_ovw_snip/CSharp/IndirectTargetingExample.xaml.cs#134)]  
  
 请注意，如果 <xref:System.Windows.Freezable> 被冻结，则将进行克隆，并且将对该克隆进行动画处理。  如果发生这种情况，原始对象的 <xref:System.Windows.Media.Animation.Animatable.HasAnimatedProperties%2A> 属性会继续返回 `false`，因为实际上并不会对原始对象进行动画处理。  有关克隆的更多信息，请参见 [Freezable 对象概述](../../../../docs/framework/wpf/advanced/freezable-objects-overview.md)。  
  
 另请注意，当使用间接属性目标时，可能会以不存在的对象为目标。  例如，您可能假设使用 <xref:System.Windows.Media.SolidColorBrush> 设置了特定按钮的 <xref:System.Windows.Controls.Control.Background%2A> 并尝试对其颜色进行动画处理，而实际上该按钮的 Background 是使用 <xref:System.Windows.Media.LinearGradientBrush> 设置的。  在这种情况下，不会引发异常；由于 <xref:System.Windows.Media.LinearGradientBrush> 不对 <xref:System.Windows.Media.SolidColorBrush.Color%2A> 属性的更改做出反应，因此动画不会具有可视效果。  
  
 下面几节更详细地描述了间接属性目标语法。  
  
<a name="xamlsyntaxchangeableproperty"></a>   
### 在 XAML 中间接以 Freezable 的属性为目标  
 若要在 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] 中以 Freezable 的属性为目标，请使用以下语法。  
  
||  
|-|  
|*ElementPropertyName*`.`*FreezablePropertyName*|  
  
 Where  
  
-   *ElementPropertyName* 是使用 <xref:System.Windows.Freezable> 设置的 <xref:System.Windows.FrameworkElement> 的属性，  
  
-   *FreezablePropertyName* 是要进行动画处理的 <xref:System.Windows.Freezable> 的属性。  
  
 下面的代码演示如何对用于设置矩形元素的 <xref:System.Windows.Shapes.Shape.Fill%2A> 的  <xref:System.Windows.Media.SolidColorBrush> 的 <xref:System.Windows.Media.SolidColorBrush.Color%2A> 进行  
  
 动画处理。  
  
  
  
 有时，您需要以集合或数组中包含的 Freezable 为目标。  
  
 若要以集合中包含的 Freezable 为目标，可以使用以下路径语法。  
  
||  
|-|  
|*ElementPropertyName* `.Children[` *CollectionIndex* `].` *FreezablePropertyName*|  
  
 其中 *CollectionIndex* 是对象在对象数组或集合中的索引。  
  
 例如，假设矩形具有应用于其 <xref:System.Windows.UIElement.RenderTransform%2A> 属性的 <xref:System.Windows.Media.TransformGroup> 资源，您希望对它包含的变换之一进行动画处理。  
  
  
  
 下面的代码演示如何对上例中演示的 <xref:System.Windows.Media.RotateTransform> 的 <xref:System.Windows.Media.RotateTransform.Angle%2A> 属性进行动画处理。  
  
  
  
<a name="targetingpropertyofchangeableincode"></a>   
### 在代码中间接以 Freezable 的属性为目标  
 在代码中，创建一个 <xref:System.Windows.PropertyPath> 对象。  当创建 <xref:System.Windows.PropertyPath> 时，请指定 <xref:System.Windows.PropertyPath.Path%2A> 和 <xref:System.Windows.PropertyPath.PathParameters%2A>。  
  
 若要创建 <xref:System.Windows.PropertyPath.PathParameters%2A>，需要创建 <xref:System.Windows.DependencyProperty> 类型的数组，其中包含依赖项属性标识符字段的列表。  第一个标识符字段用于使用 <xref:System.Windows.Freezable> 设置的 <xref:System.Windows.FrameworkElement> 或 <xref:System.Windows.FrameworkContentElement> 的属性。  下一个标识符字段表示目标 <xref:System.Windows.Freezable> 的属性。  将其看作一个属性链，该属性链将 <xref:System.Windows.Freezable> 连接到 <xref:System.Windows.FrameworkElement> 对象。  
  
 下面的示例是一个依赖项属性链，这些属性以用于设置矩形元素的 <xref:System.Windows.Shapes.Shape.Fill%2A> 的 <xref:System.Windows.Media.SolidColorBrush> 的 <xref:System.Windows.Media.SolidColorBrush.Color%2A> 为目标。  
  
 [!code-csharp[storyboards_ovw_snip#135](../../../../samples/snippets/csharp/VS_Snippets_Wpf/storyboards_ovw_snip/CSharp/IndirectTargetingExample.xaml.cs#135)]  
  
 您还需要指定 <xref:System.Windows.PropertyPath.Path%2A>。  <xref:System.Windows.PropertyPath.Path%2A> 是一个 <xref:System.String>，用于告知 <xref:System.Windows.PropertyPath.Path%2A> 如何解释其 <xref:System.Windows.PropertyPath.PathParameters%2A>。  它使用以下语法。  
  
||  
|-|  
|`(`*OwnerPropertyArrayIndex*`).(`*FreezablePropertyArrayIndex*`)`|  
  
 Where  
  
-   *OwnerPropertyArrayIndex* 是 <xref:System.Windows.DependencyProperty> 数组的索引，该数组包含使用 <xref:System.Windows.Freezable> 设置的 <xref:System.Windows.FrameworkElement> 对象属性的标识符，  
  
-   *FreezablePropertyArrayIndex* 是 <xref:System.Windows.DependencyProperty> 数组的索引，该数组包含目标属性的标识符。  
  
 下面的示例演示上例中定义的 <xref:System.Windows.PropertyPath.PathParameters%2A> 所附带的 <xref:System.Windows.PropertyPath.Path%2A>。  
  
 [!code-csharp[storyboards_ovw_snip#PropertyChainAndPath](../../../../samples/snippets/csharp/VS_Snippets_Wpf/storyboards_ovw_snip/CSharp/IndirectTargetingExample.xaml.cs#propertychainandpath)]  
  
 下面的示例将上例中的代码进行合并，以便对用于设置矩形元素的 <xref:System.Windows.Shapes.Shape.Fill%2A> 的 <xref:System.Windows.Media.SolidColorBrush> 的 <xref:System.Windows.Media.SolidColorBrush.Color%2A> 进行动画处理。  
  
 [!code-csharp[storyboards_ovw_snip#137](../../../../samples/snippets/csharp/VS_Snippets_Wpf/storyboards_ovw_snip/CSharp/IndirectTargetingExample.xaml.cs#137)]  
  
 有时，您需要以集合或数组中包含的 Freezable 为目标。  例如，假设矩形具有应用于其 <xref:System.Windows.UIElement.RenderTransform%2A> 属性的 <xref:System.Windows.Media.TransformGroup> 资源，您希望对它包含的变换之一进行动画处理。  
  
 [!code-xml[storyboards_ovw_snip#142](../../../../samples/snippets/csharp/VS_Snippets_Wpf/storyboards_ovw_snip/CSharp/IndirectTargetingExample.xaml#142)]  
  
 若要以集合中包含的 <xref:System.Windows.Freezable> 为目标，可以使用以下路径语法。  
  
||  
|-|  
|`(`*OwnerPropertyArrayIndex*`).(` *CollectionChildrenPropertyArrayIndex*`)` `[`*CollectionIndex* `].(`*FreezablePropertyArrayIndex*`)`|  
  
 其中 *CollectionIndex* 是对象在对象数组或集合中的索引。  
  
 若要以 <xref:System.Windows.Media.RotateTransform>（<xref:System.Windows.Media.TransformGroup> 中的第二个变换）的 <xref:System.Windows.Media.RotateTransform.Angle%2A> 属性为目标，请使用以下 <xref:System.Windows.PropertyPath.Path%2A> 和 <xref:System.Windows.PropertyPath.PathParameters%2A>。  
  
 [!code-csharp[storyboards_ovw_snip#139](../../../../samples/snippets/csharp/VS_Snippets_Wpf/storyboards_ovw_snip/CSharp/IndirectTargetingExample.xaml.cs#139)]  
  
 下面的示例演示用于对 <xref:System.Windows.Media.TransformGroup> 中包含的 <xref:System.Windows.Media.RotateTransform> 的 <xref:System.Windows.Media.RotateTransform.Angle%2A> 进行动画处理的完整代码。  
  
 [!code-csharp[storyboards_ovw_snip#138](../../../../samples/snippets/csharp/VS_Snippets_Wpf/storyboards_ovw_snip/CSharp/IndirectTargetingExample.xaml.cs#138)]  
  
### 间接以 Freezable 为目标并将其作为开始点  
 上面几节描述了如何通过从 <xref:System.Windows.FrameworkElement> 或 <xref:System.Windows.FrameworkContentElement> 开始为 <xref:System.Windows.Freezable> 子属性创建属性链，来间接以 <xref:System.Windows.Freezable> 为目标。  您还可以使用 <xref:System.Windows.Freezable> 作为开始点，并间接以其 <xref:System.Windows.Freezable> 子属性之一为目标。  如果使用 <xref:System.Windows.Freezable> 作为间接目标的开始点，则存在一个附加限制：起始 <xref:System.Windows.Freezable> 以及它与子属性间接目标之间的每个 <xref:System.Windows.Freezable> 都不能冻结。  
  
<a name="controllable_storyboards"></a>   
## 在 XAML 中以交互方式控制 Storyboard  
 若要在 [!INCLUDE[TLA#tla_xaml](../../../../includes/tlasharptla-xaml-md.md)] 中启动演示图板，可使用 <xref:System.Windows.Media.Animation.BeginStoryboard> 触发器操作。  <xref:System.Windows.Media.Animation.BeginStoryboard> 会将动画分发到要进行动画处理的对象和属性，然后启动演示图板。  （有关此过程的详细信息，请参见[动画和计时系统概述](../../../../docs/framework/wpf/graphics-multimedia/animation-and-timing-system-overview.md)）。如果通过指定 <xref:System.Windows.Media.Animation.BeginStoryboard> 的 <xref:System.Windows.Media.Animation.BeginStoryboard.Name%2A> 属性为它提供一个名称，则它将成为可控制的 Storyboard。  然后，可以在 Storyboard 启动后以交互方式对它进行控制。  下面列出与事件触发器一起用来控制 Storyboard 的可控制 Storyboard 操作。  
  
-   <xref:System.Windows.Media.Animation.PauseStoryboard>：暂停 Storyboard。  
  
-   <xref:System.Windows.Media.Animation.ResumeStoryboard>：继续暂停的 Storyboard。  
  
-   <xref:System.Windows.Media.Animation.SetStoryboardSpeedRatio>：更改 Storyboard 速度。  
  
-   <xref:System.Windows.Media.Animation.SkipStoryboardToFill>：使 Storyboard 前进到其填充期的末尾（如果有填充期）。  
  
-   <xref:System.Windows.Media.Animation.StopStoryboard>：停止 Storyboard。  
  
-   <xref:System.Windows.Media.Animation.RemoveStoryboard>：移除 Storyboard。  
  
 在下面的示例中，使用可控制的 Storyboard 操作来以交互方式控制 Storyboard。  
  
 [!code-xml[animation_ovws_snip#ControllableStoryboardExampleWholePage](../../../../samples/snippets/csharp/VS_Snippets_Wpf/animation_ovws_snip/CS/ControllableStoryboardExample.xaml#controllablestoryboardexamplewholepage)]  
  
<a name="controllable_storyboards_procedural"></a>   
## 使用代码以交互方式控制 Storyboard  
 上一示例已经演示了如何使用触发器操作进行动画处理。  在代码中，还可以使用 <xref:System.Windows.Media.Animation.Storyboard> 类的交互方法来控制 Storyboard。  若要使 <xref:System.Windows.Media.Animation.Storyboard> 在代码中可交互，必须使用该 Storyboard 的 <xref:System.Windows.Media.Animation.Storyboard.Begin%2A> 方法的适当重载并指定 `true` 使之可以控制。  有关更多信息，请参见 <xref:System.Windows.Media.Animation.Storyboard.Begin%28System.Windows.FrameworkElement%2CSystem.Boolean%29> 页。  
  
 下面的列表显示了在 <xref:System.Windows.Media.Animation.Storyboard> 启动之后可用来对其进行操作的方法：  
  
-   <xref:System.Windows.Media.Animation.Storyboard.Pause%2A>  
  
-   <xref:System.Windows.Media.Animation.Storyboard.Resume%2A>  
  
-   <xref:System.Windows.Media.Animation.Storyboard.Seek%2A>  
  
-   <xref:System.Windows.Media.Animation.Storyboard.SkipToFill%2A>  
  
-   <xref:System.Windows.Media.Animation.Storyboard.Stop%2A>  
  
-   <xref:System.Windows.Media.Animation.Storyboard.Remove%2A>  
  
 使用这些方法的优点是您不需要创建 <xref:System.Windows.Trigger> 或 <xref:System.Windows.TriggerAction> 对象，只需要一个对要操作的可控制 <xref:System.Windows.Media.Animation.Storyboard> 的引用。  
  
 **注意：**对 <xref:System.Windows.Media.Animation.Clock> 采取的所有交互操作（因而也会对 <xref:System.Windows.Media.Animation.Storyboard> 采取这些操作）将在计时引擎下次滴答时执行，也就是在快要进行下次呈现时执行。  例如，如果使用 <xref:System.Windows.Media.Animation.Storyboard.Seek%2A> 方法跳到动画中的另一点，属性值不会立即更改，而是在计时引擎下次滴答时更改。  
  
 下面的示例演示如何使用 <xref:System.Windows.Media.Animation.Storyboard> 类的交互方法来应用和控制动画。  
  
 [!code-csharp[animation_ovws_procedural_snip#ControllableStoryboardExampleWholePage](../../../../samples/snippets/csharp/VS_Snippets_Wpf/animation_ovws_procedural_snip/CSharp/ControllableStoryboardExample.cs#controllablestoryboardexamplewholepage)]
 [!code-vb[animation_ovws_procedural_snip#ControllableStoryboardExampleWholePage](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/animation_ovws_procedural_snip/visualbasic/controllablestoryboardexample.vb#controllablestoryboardexamplewholepage)]  
  
<a name="usingstoryboardsinstyles"></a>   
## 在样式中进行动画处理  
 可以使用 <xref:System.Windows.Media.Animation.Storyboard> 对象在 <xref:System.Windows.Style> 中定义动画。  在 <xref:System.Windows.Style> 中使用 <xref:System.Windows.Media.Animation.Storyboard> 进行动画处理与在别处使用 <xref:System.Windows.Media.Animation.Storyboard> 类似，不过，有以下三个例外：  
  
-   您不必指定 <xref:System.Windows.Media.Animation.Storyboard.TargetName%2A>；<xref:System.Windows.Media.Animation.Storyboard> 始终以 <xref:System.Windows.Style> 应用到的元素为目标。  若要以 <xref:System.Windows.Freezable> 为目标，必须使用间接目标。  有关间接目标的更多信息，请参见[间接目标](#pathsyntaxforchangeable)部分。  
  
-   您不能指定 <xref:System.Windows.EventTrigger> 或 <xref:System.Windows.Trigger> 的 <xref:System.Windows.EventTrigger.SourceName%2A>。  
  
-   您不能使用动态资源引用或数据绑定表达式来设置 <xref:System.Windows.Media.Animation.Storyboard> 或动画属性值。  这是因为 <xref:System.Windows.Style> 中的任何内容都必须是线程安全的，计时系统必须 <xref:System.Windows.Freezable.Freeze%2A> <xref:System.Windows.Media.Animation.Storyboard> 对象以使其变为线程安全。  如果 <xref:System.Windows.Media.Animation.Storyboard> 或其子时间线包含动态资源引用或数据绑定表达式，则不能将其冻结。  有关冻结和其他 <xref:System.Windows.Freezable> 功能的更多信息，请参见 [Freezable 对象概述](../../../../docs/framework/wpf/advanced/freezable-objects-overview.md)。  
  
-   在 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] 中，不能为 <xref:System.Windows.Media.Animation.Storyboard> 或动画事件声明事件处理程序。  
  
 有关演示如何在样式中定义 Storyboard 的示例，请参见[在样式中进行动画处理](../../../../docs/framework/wpf/graphics-multimedia/how-to-animate-in-a-style.md)示例。  
  
<a name="defineAStoryboardInAControlTemplateSection"></a>   
## 在 ControlTemplate 中进行动画处理  
 可以使用 <xref:System.Windows.Media.Animation.Storyboard> 对象在 <xref:System.Windows.Controls.ControlTemplate> 中定义动画。  在 <xref:System.Windows.Controls.ControlTemplate> 中使用 <xref:System.Windows.Media.Animation.Storyboard> 进行动画处理与在别处使用 <xref:System.Windows.Media.Animation.Storyboard> 类似，不过，有以下四个例外：  
  
-   <xref:System.Windows.Media.Animation.Storyboard.TargetName%2A> 只能引用 <xref:System.Windows.Controls.ControlTemplate> 的子对象。  如果未指定 <xref:System.Windows.Media.Animation.Storyboard.TargetName%2A>，则动画以 <xref:System.Windows.Controls.ControlTemplate> 所应用到的元素为目标。  
  
-   <xref:System.Windows.EventTrigger> 或 <xref:System.Windows.Trigger> 的 <xref:System.Windows.EventTrigger.SourceName%2A> 只能引用 <xref:System.Windows.Controls.ControlTemplate> 的子对象。  
  
-   您不能使用动态资源引用或数据绑定表达式来设置 <xref:System.Windows.Media.Animation.Storyboard> 或动画属性值。  这是因为 <xref:System.Windows.Controls.ControlTemplate> 中的任何内容都必须是线程安全的，计时系统必须 <xref:System.Windows.Freezable.Freeze%2A> <xref:System.Windows.Media.Animation.Storyboard> 对象以使其变为线程安全。  如果 <xref:System.Windows.Media.Animation.Storyboard> 或其子时间线包含动态资源引用或数据绑定表达式，则不能将其冻结。  有关冻结和其他 <xref:System.Windows.Freezable> 功能的更多信息，请参见 [Freezable 对象概述](../../../../docs/framework/wpf/advanced/freezable-objects-overview.md)。  
  
-   在 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] 中，不能为 <xref:System.Windows.Media.Animation.Storyboard> 或动画事件声明事件处理程序。  
  
 有关演示如何在 <xref:System.Windows.Controls.ControlTemplate> 中定义 Storyboard 的示例，请参见[在 ControlTemplate 中进行动画处理](../../../../docs/framework/wpf/graphics-multimedia/how-to-animate-in-a-controltemplate.md)示例。  
  
<a name="animateWhenAPropertyValueChanges"></a>   
## 在属性值更改时进行动画处理  
 在样式和控件模板中，当属性更改时，可以使用 Trigger 对象来启动 Storyboard。  有关示例，请参见[在属性值更改时触发动画](../../../../docs/framework/wpf/graphics-multimedia/how-to-trigger-an-animation-when-a-property-value-changes.md)和[在 ControlTemplate 中进行动画处理](../../../../docs/framework/wpf/graphics-multimedia/how-to-animate-in-a-controltemplate.md)。  
  
 属性 <xref:System.Windows.Trigger> 对象所应用的动画的行为比 <xref:System.Windows.EventTrigger> 动画或使用 <xref:System.Windows.Media.Animation.Storyboard> 方法启动的动画的行为更复杂一些。  它们在“提交”时使用的是其他 <xref:System.Windows.Trigger> 对象定义的动画，但是在编写时使用 <xref:System.Windows.EventTrigger> 和方法触发的动画。  
  
## 请参阅  
 [动画概述](../../../../docs/framework/wpf/graphics-multimedia/animation-overview.md)   
 [属性动画技术概述](../../../../docs/framework/wpf/graphics-multimedia/property-animation-techniques-overview.md)   
 [Freezable 对象概述](../../../../docs/framework/wpf/advanced/freezable-objects-overview.md)