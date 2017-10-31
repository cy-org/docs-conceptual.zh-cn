---
title: "依赖项属性值优先级 | Microsoft Docs"
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
  - "类, 依赖项属性的所有者"
  - "依赖项属性, 作为所有者的类"
  - "依赖项属性, 元数据"
  - "元数据, 依赖项属性"
ms.assetid: 1fbada8e-4867-4ed1-8d97-62c07dad7ebc
caps.latest.revision: 27
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 26
---
# 依赖项属性值优先级
<a name="introduction"></a> 本主题说明 [!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)] 属性系统的工作机制如何影响[依赖项属性](GTMT)的值，并介绍应用于属性有效值的属性系统的各方面所依据的优先级。  
  
   
  
<a name="prerequisites"></a>   
## 必备组件  
 本主题假定您从 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 类的现有依赖项属性的使用者角度了解依赖项属性，并且已阅读[依赖项属性概述](../../../../docs/framework/wpf/advanced/dependency-properties-overview.md)。  若要采用本主题中的示例，还应当了解[!INCLUDE[TLA#tla_xaml](../../../../includes/tlasharptla-xaml-md.md)] 并知道如何编写 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 应用程序。  
  
<a name="intro"></a>   
## WPF 属性系统  
 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 属性系统提供了一个强大的方法，使得依赖项属性的值由多种因素决定，从而实现了诸如实时属性验证、后期绑定以及向相关属性发出有关其他属性值发生更改的通知等功能。  用来确定依赖项属性值的确切顺序和逻辑相当复杂。  了解此顺序将帮助您避免不必要的属性设置，并且还有可能澄清混淆，使您正确了解为何某些影响或预测依赖项属性值的尝试最终却没有得出您所期望的值。  
  
<a name="multiple_sets"></a>   
## 依赖项属性可以在多个位置“设置”  
 在下面的示例 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] 中，同一个属性 \(<xref:System.Windows.Controls.Control.Background%2A>\) 具有三个不同的“设置”操作，它们都可能会影响属性值。  
  
 [!code-xml[PropertiesOvwSupport#DPPrecedence](../../../../samples/snippets/csharp/VS_Snippets_Wpf/PropertiesOvwSupport/CSharp/page4.xaml#dpprecedence)]  
  
 这里，您希望应用什么颜色 \- 红色、绿色还是蓝色？  
  
 本地属性集在设置时具有最高优先级，动画值和强制转换除外。  如果您在本地设置某个值，一定会希望该值能优先得到应用，甚至希望其优先级高于任何样式或控件模板。  在本示例中，<xref:System.Windows.Controls.Control.Background%2A> 在本地设置为“Red”（红色）。  因此，在此范围内定义的样式（即使是可能会应用于该范围内该类型的所有元素的隐式样式）在向 <xref:System.Windows.Controls.Control.Background%2A> 属性提供其值时也并没有最高优先级。  如果您从该“Button”（按钮）实例中移除本地值“Red”（红色），样式将获得优先级，而按钮将从该样式中获得“Background”（背景）值。  在该样式中，触发器具有优先级，因此当鼠标位于按钮上时，按钮为蓝色，其他情况下则为绿色。  
  
<a name="listing"></a>   
## 依赖项属性设置优先级列表  
 下面是属性系统在指定依赖项属性的运行时值时所使用的最终顺序。  最高优先级将最先列出。  此列表对[依赖项属性概述](../../../../docs/framework/wpf/advanced/dependency-properties-overview.md)中的某些一般化内容进行了扩充。  
  
1.  **属性系统强制转换。**有关强制转换的详细信息，请参见本主题后面的[强制转换、动画和基值](#animations)。  
  
2.  **活动动画或具有 Hold 行为的动画。**为了获得任何实用效果，属性的动画必须优先于基（未动画）值，即使该值是在本地设置的情况下也将如此。  有关详细信息，请参见本主题后面的[强制转换、动画和基值](#animations)。  
  
3.  **本地值。**本地值可以通过“包装”属性的便利性进行设置，这也相当于在 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] 中设置特性或属性元素，或者使用特定实例的属性调用 <xref:System.Windows.DependencyObject.SetValue%2A> [!INCLUDE[TLA#tla_api](../../../../includes/tlasharptla-api-md.md)]。  如果您使用绑定或资源来设置本地值，则每个值都按照直接设置值的优先级顺序来应用。  
  
4.  **TemplatedParent 模板属性。**如果元素是作为模板（<xref:System.Windows.Controls.ControlTemplate> 或 <xref:System.Windows.DataTemplate>）的一部分创建的，则具有 <xref:System.Windows.FrameworkElement.TemplatedParent%2A>。  有关何时应用此原则的详细信息，请参见本主题后面的 [TemplatedParent](#templatedparent)。  在模板中，按以下优先级顺序应用：  
  
    1.  来自 <xref:System.Windows.FrameworkElement.TemplatedParent%2A> 模板的触发器。  
  
    2.  <xref:System.Windows.FrameworkElement.TemplatedParent%2A> 模板中的属性集。（通常通过 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] 特性进行设置。）  
  
5.  **隐式样式。**仅应用于 `Style` 属性。  `Style` 属性是由任何样式资源通过与其类型匹配的键来填充的。  该样式资源必须存在于页面或应用程序中；查找隐式样式资源不会进入到主题中。  
  
6.  **样式触发器。**来自页面或应用程序上的样式中的触发器。（这些样式可以是显式或隐式样式，但不是来自优先级较低的默认样式。）  
  
7.  **模板触发器。**来自样式中的模板或者直接应用的模板的任何触发器。  
  
8.  **样式 Setter。**来自页面或应用程序的样式中的 <xref:System.Windows.Setter> 的值。  
  
9. **默认（主题）样式。**有关何时应用此样式以及主题样式如何与主题样式中的模板相关的详细信息，请参见本主题后面的[默认（主题）样式](#themestyles)。  在默认样式中，按以下优先级顺序应用：  
  
    1.  主题样式中的活动触发器。  
  
    2.  主题样式中的 Setter。  
  
10. **继承。**有几个依赖项属性从父元素向子元素继承值，因此不需要在应用程序中的每个元素上专门设置这些属性。  有关详细信息，请参见[属性值继承](../../../../docs/framework/wpf/advanced/property-value-inheritance.md)。  
  
11. **来自依赖项属性元数据的默认值。**任何给定的依赖项属性都具有一个默认值，它由该特定属性的属性系统注册来确定。  而且，继承依赖项属性的派生类具有按照类型重写该元数据（包括默认值）的选项。  有关更多信息，请参见[依赖项属性元数据](../../../../docs/framework/wpf/advanced/dependency-property-metadata.md)。  因为继承是在默认值之前检查的，所以对于继承的属性，父元素的默认值优先于子元素。  因此，如果任何地方都没有设置可继承的属性，将使用在根元素或父元素中指定的默认值，而不是子元素的默认值。  
  
<a name="templatedparent"></a>   
## TemplatedParent  
 TemplatedParent 作为一个优先级项并不应用于您在标准应用程序标记中直接声明的元素的任何属性。  只有对于通过应用模板而产生的可视化树中的子项而言，才存在 TemplatedParent 概念。  当属性系统在 <xref:System.Windows.FrameworkElement.TemplatedParent%2A> 模板中搜索某个值时，就是在搜索创建该元素的模板。  来自 <xref:System.Windows.FrameworkElement.TemplatedParent%2A> 模板的属性值通常就像在子元素上设置的本地值一样来应用，但是这些属性值的优先级低于本地值，因为模板有可能被共享。  有关详细信息，请参见 <xref:System.Windows.FrameworkElement.TemplatedParent%2A>。  
  
<a name="style_property"></a>   
## 样式属性  
 前面介绍的查找顺序适用于除 <xref:System.Windows.FrameworkElement.Style%2A> 属性之外的所有可能的依赖项属性。  <xref:System.Windows.FrameworkElement.Style%2A> 属性的独特之处在于它不能为自己设置样式，因此优先级项 5 到 8 不适用。  此外，建议不要进行动画处理或强制转换 <xref:System.Windows.FrameworkElement.Style%2A>。（对 <xref:System.Windows.FrameworkElement.Style%2A> 进行动画处理需要一个自定义动画类。）  这产生了三种设置 <xref:System.Windows.FrameworkElement.Style%2A> 属性的方法：  
  
-   **显式样式。** <xref:System.Windows.FrameworkElement.Style%2A> 属性是直接设置的。  在大多数情况下，样式不是内联定义的，而是作为资源由显式键进行引用的。  在这种情况下，Style 属性本身就像本地值（优先级项 3）一样来应用。  
  
-   **隐式样式。** <xref:System.Windows.FrameworkElement.Style%2A> 属性不是直接设置的。  但是，<xref:System.Windows.FrameworkElement.Style%2A> 在某种程度上存在于资源查找序列（页面、应用程序）中，并且使用与要应用样式的类型相匹配的资源键进行键控。  在这种情况下，<xref:System.Windows.FrameworkElement.Style%2A> 属性本身按照在该序列中标识为第 5 项的优先级来应用。  通过对 <xref:System.Windows.FrameworkElement.Style%2A> 属性使用 <xref:System.Windows.DependencyPropertyHelper> 并在结果中查找 <xref:System.Windows.BaseValueSource> 可检测此条件。  
  
-   **默认样式**，也称为**主题样式**。<xref:System.Windows.FrameworkElement.Style%2A> 属性不是直接设置的，并且实际上将作为 `null` 读取，一直到运行时为止。  在这种情况下，样式来自作为 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 表示引擎一部分的运行时主题评估。  
  
 对于主题中不存在的隐式样式，类型必须完全匹配 \- `MyButton` `Button` 派生的类将不会对 `Button` 隐式使用样式。  
  
<a name="themestyles"></a>   
## 默认（主题）样式  
 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 附带的每个控件都有一个默认样式。  默认样式可能因主题而异，这就是默认样式有时候称为主题样式的原因。  
  
 在默认样式中，对于控件最重要的信息就是其控件模板，它作为其 <xref:System.Windows.Controls.Control.Template%2A> 属性的 Setter 存在于主题样式中。  如果默认样式中没有模板，自定义样式中没有自定义模板的控件将根本没有可视化外观。  默认样式中的模板为每个控件的可视化外观提供了一个基本结构，还定义了在模板的可视化树中定义的属性与对应的控件类之间的联系。  每个控件都公开一组属性，这些属性可以影响控件的可视化外观，而无需完全替换模板。  例如，请考虑 <xref:System.Windows.Controls.Primitives.Thumb> 控件（<xref:System.Windows.Controls.Primitives.ScrollBar> 的一个组件）的默认可视化外观。  
  
 <xref:System.Windows.Controls.Primitives.Thumb> 具有一些可自定义属性。  <xref:System.Windows.Controls.Primitives.Thumb> 的默认模板创建了一个基本结构\/可视化树（具有几个嵌套的 <xref:System.Windows.Controls.Border> 组件），以产生倾斜的外观。  如果模板中的某个属性要通过 <xref:System.Windows.Controls.Primitives.Thumb> 类公开以进行自定义，则该属性必须通过 [TemplateBinding](../../../../docs/framework/wpf/advanced/templatebinding-markup-extension.md) 在模板中公开。  对于 <xref:System.Windows.Controls.Primitives.Thumb>，这些边界的各种属性都将共享对属性（如 <xref:System.Windows.Controls.Border.Background%2A> 或 <xref:System.Windows.Controls.Border.BorderThickness%2A>）的模板绑定。  但是其他某些属性或可视化排列被硬编码到控件模板中，或者绑定到直接来自主题的值，除了替换整个模板外，不能对其进行更改。  一般而言，如果属性来自模板化的父元素，并且不是通过模板绑定公开的，则不能通过样式进行调整，因为没有简单的方法可以将其设置为目标。  但是，该属性仍然可能会受所应用的模板中的属性值继承的影响，或受默认值的影响。  
  
 主题样式将类型用作其定义中的键。  但是，当主题应用于给定的元素实例时，主题将通过检查控件上是否具有 <xref:System.Windows.FrameworkElement.DefaultStyleKey%2A> 属性来查找此类型。  这与使用文本类型的隐式样式正好相反。  <xref:System.Windows.FrameworkElement.DefaultStyleKey%2A> 的值将由派生类继承，即使实施者未更改该属性也是如此。（更改属性的理想方式不是在属性级将其重写，而是在属性元数据中更改其默认值。）  这种间接方式使基类可以为没有样式（或者该样式中没有模板，因此根本没有默认的可视化外观，这一点更为重要）的派生元素定义主题样式。  所以，您可以从 <xref:System.Windows.Controls.Button> 派生 `MyButton` 并且仍然能够获得 <xref:System.Windows.Controls.Button> 默认模板。  如果您是 `MyButton` 的控件作者，而您需要一个不同的行为，则可以为 `MyButton` 上的 <xref:System.Windows.FrameworkElement.DefaultStyleKey%2A> 重写依赖项属性元数据以返回一个不同的键，然后定义相关主题样式，包括必须与您的 `MyButton` 控件一起打包的 `MyButton` 的模板。  有关主题、样式和控件创作的详细信息，请参见[控件创作概述](../../../../docs/framework/wpf/controls/control-authoring-overview.md)。  
  
<a name="resources"></a>   
## 动态资源引用和绑定  
 动态资源引用和绑定操作遵守其设置位置的优先级。  例如，应用于本地值的动态资源作为优先级项 3 进行应用，主题样式中的属性 Setter 的绑定作为优先级项 9 进行应用，依此类推。  由于动态资源引用和绑定必须都能够从应用程序的运行时状态中获得值，这使确定任何给定属性的属性值优先级的实际处理也将扩展到运行时。  
  
 严格来讲，动态资源引用并不是属性系统的一部分，但它们的确具有自己的查找顺序，该顺序与上面列出的顺序交互。  [XAML 资源](../../../../docs/framework/wpf/advanced/xaml-resources.md)中对该优先级进行了更全面的介绍。  优先级的基本概括是：元素到页面根元素、应用程序、主题、系统。  
  
 动态资源和绑定具有其设置位置的优先级，但是值会延迟。  这样的一个后果是，如果您将动态资源或绑定设置为某个本地值，则对该本地值的任何更改都将完全替换该动态资源或绑定。  即使您调用 <xref:System.Windows.DependencyObject.ClearValue%2A> 方法清除本地设置的值，该动态资源或绑定也不会还原。  实际上，如果您对具有动态资源或绑定的属性（没有“文字”本地值）调用 <xref:System.Windows.DependencyObject.ClearValue%2A>，它们也会被 <xref:System.Windows.DependencyObject.ClearValue%2A> 调用清除掉。  
  
<a name="setcurrentvalue"></a>   
## SetCurrentValue  
 <xref:System.Windows.DependencyObject.SetCurrentValue%2A> 方法是设置属性的另一种方法，但它不具有优先级顺序。  相反，使用 <xref:System.Windows.DependencyObject.SetCurrentValue%2A> 可以更改属性值而不会覆盖以前值的源。  每当您要设置一个值但是不向该值提供某个本地值的优先级时，便可以使用 <xref:System.Windows.DependencyObject.SetCurrentValue%2A>。  例如，如果一个属性是通过触发器设置的，然后通过 <xref:System.Windows.DependencyObject.SetCurrentValue%2A> 分配了另一个值，则属性系统仍将遵循该触发器，并且在触发器操作发生时该属性将更改。  使用 <xref:System.Windows.DependencyObject.SetCurrentValue%2A> 可以更改属性值而不必为其提供具有更高优先级的源。  同样，您可以使用 <xref:System.Windows.DependencyObject.SetCurrentValue%2A> 更改属性值而不覆盖绑定。  
  
<a name="animations"></a>   
## 强制转换、动画和基值  
 强制转换和动画在本 [!INCLUDE[TLA2#tla_sdk](../../../../includes/tla2sharptla-sdk-md.md)] 中都作用于称为“基值”的值。  因此，基值是在各项中通过向上计算一直到第 2 项为止而确定的任何值。  
  
 对于动画，如果没有为某些行为指定“From”和“To”值，或者动画在完成时故意恢复为基值，那么基值将影响动画值。  若要了解实际效果，请运行 [From, To, and By Animation Target Values Sample](http://go.microsoft.com/fwlink/?LinkID=159988)（From、To 和 By 动画目标值示例）。  尝试为示例中的矩形高度设置本地值，使初始本地值不同于动画中的任何“From”值。  您将注意到动画立即使用“From”值开始，并在开始后替换基值。  可以指定动画完成之前返回发现的值，具体操作是指定 Stop <xref:System.Windows.Media.Animation.FillBehavior>。  然后，根据正常优先级来确定基值。  
  
 多个动画可能应用于一个属性，而每个动画可能是从值优先级中的不同点进行定义的。  但是，这些动画的值可能会组合起来，而不仅仅是从较高的优先级开始应用动画。  这完全取决于动画的定义方式以及执行动画操作的值类型。  有关对属性进行动画处理的更多信息，请参见[动画概述](../../../../docs/framework/wpf/graphics-multimedia/animation-overview.md)。  
  
 强制转换在最高级别应用。  即使正在运行的动画也将受到值强制转换的制约。  [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 中的某些现有的依赖项属性具有内置的强制转换。  对于自定义依赖项属性，您可以在创建该属性时通过编写 <xref:System.Windows.CoerceValueCallback> 并作为元数据的一部分传递回调来为其定义强制转换行为。  还可以通过在派生类中重写现有属性的元数据来重写其强制转换行为。  强制转换与基值的交互使强制转换上的约束就像当时存在这些约束一样进行应用，但基值仍将保留。  因此，如果强制转换的约束后来被解除，强制转换将返回与基值最接近的值，并且一旦所有约束都解除，强制转换对属性的影响可能会立即停止。  有关强制转换行为的更多信息，请参见[依赖项属性回调和验证](../../../../docs/framework/wpf/advanced/dependency-property-callbacks-and-validation.md)。  
  
<a name="triggers"></a>   
## 触发器行为  
 控件常常在主题中将触发器行为定义为其默认样式的一部分。  为控件设置本地属性可能会阻止触发器从视觉或行为上响应用户驱动的事件。  属性触发器最常用于控件或状态属性，如 <xref:System.Windows.Controls.Primitives.Selector.IsSelected%2A>。  例如，默认情况下，当禁用 <xref:System.Windows.Controls.Button> 时（<xref:System.Windows.UIElement.IsEnabled%2A> 的触发器是 `false`），主题样式中的 <xref:System.Windows.Controls.Control.Foreground%2A> 值将导致控件“变灰”。  但是，如果您设置了本地 <xref:System.Windows.Controls.Control.Foreground%2A> 值，本地属性集将优先于普通灰显颜色，即使在这个属性触发的方案中也是如此。  为具有主题级触发器行为的属性设置值时要倍加小心，并要确保不要过度妨碍该控件应有的用户体验。  
  
<a name="clearvalue"></a>   
## ClearValue 和值优先级  
 <xref:System.Windows.DependencyObject.ClearValue%2A> 方法为从在元素上设置的[依赖项属性](GTMT)中清除任何本地应用的值提供了一个有利的途径。  但是，调用 <xref:System.Windows.DependencyObject.ClearValue%2A> 并不能保证注册属性时在元数据中指定的默认值就是新的有效值。  值优先级中的所有其他参与者仍然有效。  只有在本地设置的值才会从优先级序列中移除。  例如，如果您对同时也由主题样式设置的属性调用 <xref:System.Windows.DependencyObject.ClearValue%2A>，主题值将作为新值而不是基于元数据的默认值进行应用。  如果您希望取消过程中的所有属性值参与者，而将值设置为注册的元数据默认值，则可以通过查询依赖项属性元数据最终获得默认值，然后使用该默认值在本地设置属性并调用 <xref:System.Windows.DependencyObject.SetValue%2A>。  
  
## 请参阅  
 <xref:System.Windows.DependencyObject>   
 <xref:System.Windows.DependencyProperty>   
 [依赖项属性概述](../../../../docs/framework/wpf/advanced/dependency-properties-overview.md)   
 [自定义依赖项属性](../../../../docs/framework/wpf/advanced/custom-dependency-properties.md)   
 [依赖项属性回调和验证](../../../../docs/framework/wpf/advanced/dependency-property-callbacks-and-validation.md)