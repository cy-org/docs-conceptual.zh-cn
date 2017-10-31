---
title: "Freezable 对象概述 | Microsoft Docs"
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
  - "类, Freezable"
  - "Freezable 对象, description"
  - "解冻 Freezable 对象"
ms.assetid: 89c71692-4f43-4057-b611-67c6a8a863a2
caps.latest.revision: 30
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 30
---
# Freezable 对象概述
本主题说明如何有效地使用和创建 <xref:System.Windows.Freezable> 对象，这些对象提供可帮助改进应用程序性能的特殊功能。  Freezable 对象的示例包括画笔、钢笔、变换、几何图形和动画。  
  
 本主题包含以下各节：  
  
<a name="autoTopLevelSectionsOUTLINE0"></a>   
<a name="whatisafreezable"></a>   
## 什么是 Freezable？  
 <xref:System.Windows.Freezable> 是一种特殊的对象类型，具有两个状态：解冻和冻结。  当处于解冻状态时，<xref:System.Windows.Freezable> 的行为与任何其他对象的行为一样。  <xref:System.Windows.Freezable> 一旦冻结，便无法修改。  
  
 <xref:System.Windows.Freezable> 提供了一个 <xref:System.Windows.Freezable.Changed> 事件以将对对象所做的任何修改通知给观察程序。  冻结 <xref:System.Windows.Freezable> 可以改进其性能，因为它不再需要因更改通知而消耗资源。  冻结的 <xref:System.Windows.Freezable> 也可以在线程之间共享，而解冻的 <xref:System.Windows.Freezable> 则不能。  
  
 虽然 <xref:System.Windows.Freezable> 类具有许多应用程序，但 [!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)] 中的大多数 <xref:System.Windows.Freezable> 对象都与图形子系统相关。  
  
 <xref:System.Windows.Freezable> 类使您在使用某些图形系统对象时更加轻松，并且有助于改进应用程序性能。  从 <xref:System.Windows.Freezable> 继承的类型示例包括 <xref:System.Windows.Media.Brush>、<xref:System.Windows.Media.Transform> 和 <xref:System.Windows.Media.Geometry> 类。  由于它们包含非托管资源，因此系统必须监视这些对象的修改情况，然后在对原始对象进行了更改的情况下，更新其相应的非托管资源。  即使实际上您并没有修改图形系统对象，但系统也必须花费一些资源来监视该对象，以防您对其进行更改。  
  
 例如，假设您要创建一个 <xref:System.Windows.Media.SolidColorBrush> 画笔，并使用它来绘制按钮的背景。  
  
 [!code-csharp[freezablesample_procedural#FrozenExamplePart1](../../../../samples/snippets/csharp/VS_Snippets_Wpf/freezablesample_procedural/CSharp/freezablesample.cs#frozenexamplepart1)]
 [!code-vb[freezablesample_procedural#FrozenExamplePart1](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/freezablesample_procedural/visualbasic/freezablesample.vb#frozenexamplepart1)]  
  
 呈现按钮时，[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 图形子系统使用您提供的信息来绘制一组像素，以创建按钮的外观。  虽然您使用了纯色画笔来描写应如何绘制按钮，但您的纯色画笔并未真正绘制。  图形系统为该按钮和画笔生成快速、低级别的对象，而屏幕上实际显示的正是这些对象。  
  
 如果要修改画笔，则必须重新生成这些低级别对象。  通过 Freezable 类，画笔可以找到相应的已生成低级别对象，并在画笔更改时更新这些对象。  当启用该功能时，画笔便被认为是“解冻的”。  
  
 使用 Freezable 对象的 <xref:System.Windows.Freezable.Freeze%2A> 方法可以禁用该自行更新功能。  可以使用该方法使画笔变为“冻结”或不可修改。  
  
> [!NOTE]
>  并不是每个 Freezable 对象都可以冻结。  若要避免引发 <xref:System.InvalidOperationException>，请在尝试冻结 Freezable 对象之前，查看其 <xref:System.Windows.Freezable.CanFreeze%2A> 属性的值，以确定它是否可以被冻结。  
  
 [!code-csharp[freezablesample_procedural#FrozenExamplePart2](../../../../samples/snippets/csharp/VS_Snippets_Wpf/freezablesample_procedural/CSharp/freezablesample.cs#frozenexamplepart2)]
 [!code-vb[freezablesample_procedural#FrozenExamplePart2](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/freezablesample_procedural/visualbasic/freezablesample.vb#frozenexamplepart2)]  
  
 当不再需要修改某个 Freezable 时，冻结它可以改进性能。  如果您在该示例中冻结画笔，则图形系统将不再需要监视它的更改情况。  图形系统还可以进行其他优化，因为它知道画笔不会更改。  
  
> [!NOTE]
>  出于方便，除非您显式冻结 Freezable 对象，否则它们保持解冻状态。  
  
<a name="frozenfreezables"></a>   
## 使用 Freezable  
 使用解冻的 Freezable 就像使用任何其他类型的对象一样。  在下面的示例中，使用 <xref:System.Windows.Media.SolidColorBrush> 来绘制按钮的背景之后，其颜色从黄色更改为红色。  图形系统在幕后工作，在下次刷新屏幕时将按钮从黄色自动更改为红色。  
  
 [!code-csharp[freezablesample_procedural#UnFrozenExampleShort](../../../../samples/snippets/csharp/VS_Snippets_Wpf/freezablesample_procedural/CSharp/freezablesample.cs#unfrozenexampleshort)]
 [!code-vb[freezablesample_procedural#UnFrozenExampleShort](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/freezablesample_procedural/visualbasic/freezablesample.vb#unfrozenexampleshort)]  
  
### 冻结 Freezable  
 若要使 <xref:System.Windows.Freezable> 不可修改，可调用其 <xref:System.Windows.Freezable.Freeze%2A> 方法。  冻结某个包含 Freezable 对象的对象时，也会冻结这些被包含的对象。  例如，如果您冻结某个 <xref:System.Windows.Media.PathGeometry>，则它包含的图形和线段也会被冻结。  
  
 如果下列任一情况属实，则**无法**冻结 Freezable：  
  
-   它有动画或数据绑定的属性。  
  
-   它有由动态资源设置的属性  （有关动态资源的更多信息，请参见[XAML 资源](../../../../docs/framework/wpf/advanced/xaml-resources.md)）。  
  
-   它包含无法冻结的 <xref:System.Windows.Freezable> 子对象。  
  
 如果不存在这些情况，并且您不希望修改 <xref:System.Windows.Freezable>，则应当像前面介绍的那样冻结该对象以改进性能。  
  
 一旦调用某个 Freezable 的 <xref:System.Windows.Freezable.Freeze%2A> 方法，便不能再修改该对象。  尝试修改冻结的对象会导致引发 <xref:System.InvalidOperationException>。  由于尝试修改已冻结的画笔，下面的代码将引发一个异常。  
  
 [!code-csharp[freezablesample_procedural#ExceptionExample](../../../../samples/snippets/csharp/VS_Snippets_Wpf/freezablesample_procedural/CSharp/freezablesample.cs#exceptionexample)]
 [!code-vb[freezablesample_procedural#ExceptionExample](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/freezablesample_procedural/visualbasic/freezablesample.vb#exceptionexample)]  
  
 为了避免引发此异常，可以使用 <xref:System.Windows.Freezable.IsFrozen%2A> 方法来确定 <xref:System.Windows.Freezable> 是否处于冻结状态。  
  
 [!code-csharp[freezablesample_procedural#CheckIsFrozenExample](../../../../samples/snippets/csharp/VS_Snippets_Wpf/freezablesample_procedural/CSharp/freezablesample.cs#checkisfrozenexample)]
 [!code-vb[freezablesample_procedural#CheckIsFrozenExample](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/freezablesample_procedural/visualbasic/freezablesample.vb#checkisfrozenexample)]  
  
 在前面的代码示例中，使用 <xref:System.Windows.Freezable.Clone%2A> 方法对一个冻结的对象创建了可修改副本。  下一节将更详细地讨论克隆操作。  
  
 **注意** 由于无法对冻结的 Freezable 进行动画处理，因此当您尝试使用 <xref:System.Windows.Media.Animation.Storyboard> 对冻结的 <xref:System.Windows.Freezable> 对象进行动画处理时，动画系统将自动创建这些对象的可修改复本。  为了消除由于克隆而导致的性能系统开销，当您希望对某个对象进行动画处理时，请使其保持解冻状态。  有关使用演示图板进行动画处理的更多信息，请参见[演示图板概述](../../../../docs/framework/wpf/graphics-multimedia/storyboards-overview.md)。  
  
### 从标记冻结  
 若要冻结在标记中声明的 <xref:System.Windows.Freezable> 对象，请使用 `PresentationOptions:Freeze` 特性。  在下面的示例中，将一个 <xref:System.Windows.Media.SolidColorBrush> 声明为页资源，并冻结它。  随后将它用于设置按钮的背景。  
  
 [!code-xml[FreezableSample#FreezeFromMarkupWholePage](../../../../samples/snippets/csharp/VS_Snippets_Wpf/FreezableSample/CS/FreezeFromMarkupExample.xaml#freezefrommarkupwholepage)]  
  
 若要使用 `Freeze` 特性，必须映射到表示选项命名空间：`http://schemas.microsoft.com/winfx/2006/xaml/presentation/options`。  `PresentationOptions` 是用于映射此命名空间时的建议前缀：  
  
```  
xmlns:PresentationOptions="http://schemas.microsoft.com/winfx/2006/xaml/presentation/options"   
```  
  
 由于并非所有 XAML 读取器都能识别该特性，因此建议使用 [mc:Ignorable 特性](../../../../docs/framework/wpf/advanced/mc-ignorable-attribute.md) 将 `Presentation:Freeze` 特性标记为可忽略：  
  
```  
xmlns:mc="http://schemas.openxmlformats.org/markup-compatibility/2006"  
mc:Ignorable="PresentationOptions"  
```  
  
 有关更多信息，请参见 [mc:Ignorable 特性](../../../../docs/framework/wpf/advanced/mc-ignorable-attribute.md)页。  
  
### “解冻”Freezable  
 <xref:System.Windows.Freezable> 一旦冻结，便不能再修改或解冻；不过，您可以使用 <xref:System.Windows.Freezable.Clone%2A> 或 <xref:System.Windows.Freezable.CloneCurrentValue%2A> 方法创建一个解冻的复本。  
  
 在下面的示例中，使用一个画笔设置按钮的背景，然后冻结该画笔。  使用 <xref:System.Windows.Freezable.Clone%2A> 方法创建该画笔的解冻的副本。  然后，修改该复本并使用它将按钮的背景从黄色更改为红色。  
  
 [!code-csharp[freezablesample_procedural#CloneExample](../../../../samples/snippets/csharp/VS_Snippets_Wpf/freezablesample_procedural/CSharp/freezablesample.cs#cloneexample)]
 [!code-vb[freezablesample_procedural#CloneExample](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/freezablesample_procedural/visualbasic/freezablesample.vb#cloneexample)]  
  
> [!NOTE]
>  无论使用哪一种克隆方法，都不会将动画复制到新的 <xref:System.Windows.Freezable>。  
  
 <xref:System.Windows.Freezable.Clone%2A> 和 <xref:System.Windows.Freezable.CloneCurrentValue%2A> 方法可生成 Freezable 的深层副本。  如果该 Freezable 包含其他冻结的 Freezable 对象，则还会克隆这些对象使它们可以修改。  例如，如果克隆某个冻结的 <xref:System.Windows.Media.PathGeometry> 以便使其可以修改，则还会复制它包含的图形和线段，使它们可以修改。  
  
<a name="createyourownfreezableclass"></a>   
## 创建自己的 Freezable 类  
 从 <xref:System.Windows.Freezable> 派生的类可以获取以下功能。  
  
-   特殊的状态：只读（冻结）状态和可写状态。  
  
-   线程安全：冻结的 <xref:System.Windows.Freezable> 可以在线程之间共享。  
  
-   详细的更改通知：与其他 <xref:System.Windows.DependencyObject> 不同，Freezable 对象会在子属性值更改时提供更改通知。  
  
-   轻松克隆：Freezable 类已经实现了多种生成深层复本的方法。  
  
 <xref:System.Windows.Freezable> 是一种 <xref:System.Windows.DependencyObject>，因而使用依赖项属性系统。  您的类属性不必是依赖项属性，但使用依赖项属性可以减少必须编写的代码量，因为设计 <xref:System.Windows.Freezable> 类时考虑了依赖项属性。  有关依赖项属性系统的更多信息，请参见[依赖项属性概述](../../../../docs/framework/wpf/advanced/dependency-properties-overview.md)。  
  
 每个 <xref:System.Windows.Freezable> 子类都必须重写 <xref:System.Windows.Freezable.CreateInstanceCore%2A> 方法。  如果您的类对于其所有数据都使用依赖项属性，则您的工作已完成。  
  
 如果您的类包含非依赖项属性数据成员，则还必须重写以下方法：  
  
-   <xref:System.Windows.Freezable.CloneCore%2A>  
  
-   <xref:System.Windows.Freezable.CloneCurrentValueCore%2A>  
  
-   <xref:System.Windows.Freezable.GetAsFrozenCore%2A>  
  
-   <xref:System.Windows.Freezable.GetCurrentValueAsFrozenCore%2A>  
  
-   <xref:System.Windows.Freezable.FreezeCore%2A>  
  
 在访问和写入不属于依赖项属性的数据成员时，还必须遵守以下规则：  
  
-   在读取非依赖项属性数据成员的任何 [!INCLUDE[TLA#tla_api](../../../../includes/tlasharptla-api-md.md)] 的开头，调用 <xref:System.Windows.Freezable.ReadPreamble%2A> 方法。  
  
-   在写入非依赖项属性数据成员的任何 API 的开头，调用 <xref:System.Windows.Freezable.WritePreamble%2A> 方法。  （在 [!INCLUDE[TLA2#tla_api](../../../../includes/tla2sharptla-api-md.md)] 中调用 <xref:System.Windows.Freezable.WritePreamble%2A> 之后，如果还应读取非依赖项属性数据成员，则不需要另外调用 <xref:System.Windows.Freezable.ReadPreamble%2A>）。  
  
-   在退出写入非依赖项属性数据成员的方法之前，调用 <xref:System.Windows.Freezable.WritePostscript%2A> 方法。  
  
 如果类包含的非依赖项属性数据成员为 <xref:System.Windows.DependencyObject> 对象，则每次更改这些成员的值时，还必须调用 <xref:System.Windows.Freezable.OnFreezablePropertyChanged%2A> 方法，即使您将这些成员设置为 `null` 也是如此。  
  
> [!NOTE]
>  通过调用基实现来开始重写的每个 <xref:System.Windows.Freezable> 方法，这一点非常重要。  
  
 有关自定义 <xref:System.Windows.Freezable> 类的示例，请参见 [Custom Animation Sample](http://go.microsoft.com/fwlink/?LinkID=159981)（自定义动画示例）。  
  
## 请参阅  
 <xref:System.Windows.Freezable>   
 [Custom Animation Sample](http://go.microsoft.com/fwlink/?LinkID=159981)   
 [依赖项属性概述](../../../../docs/framework/wpf/advanced/dependency-properties-overview.md)   
 [自定义依赖项属性](../../../../docs/framework/wpf/advanced/custom-dependency-properties.md)