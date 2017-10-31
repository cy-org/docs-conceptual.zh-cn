---
title: "XAML 资源 | Microsoft Docs"
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
  - "重用资源"
  - "重复使用的资源"
  - "重用通常定义的对象"
  - "XAML 中，重用资源"
ms.assetid: 91580b89-a0a8-4889-aecb-fddf8e63175f
caps.latest.revision: 33
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 32
---
# XAML 资源
资源是可以在您的应用程序中的不同位置重复使用的对象。 资源的示例包括画笔和样式。 本概述介绍如何使用中的资源[!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)]。 您还可以创建和使用代码，或者通过互换使用代码访问的资源和[!INCLUDE[TLA#tla_xaml](../../../../includes/tlasharptla-xaml-md.md)]。 有关详细信息，请参阅[资源和代码](../../../../docs/framework/wpf/advanced/resources-and-code.md)。  
  
> [!NOTE]
>  本主题中所述的资源文件是不同于资源文件中所述[WPF 应用程序资源、 内容和数据文件](../../../../docs/framework/wpf/app-development/wpf-application-resource-content-and-data-files.md)和不同于中所述的嵌入或链接的资源[管理应用程序资源 (.NET)](../Topic/Managing%20Application%20Resources%20\(.NET\).md)。  
  
   
  
<a name="usingresources"></a>   
## <a name="using-resources-in-xaml"></a>在 XAML 中使用的资源  
 下面的示例定义<xref:System.Windows.Media.SolidColorBrush>作为页面的根元素上的资源。 该示例然后引用的资源，并使用它来设置属性的多个子元素，其中包括<xref:System.Windows.Shapes.Ellipse>、 <xref:System.Windows.Controls.TextBlock>，和一个<xref:System.Windows.Controls.Button>。  
  
 [!code-xml[FEResourceSH_snip#XAML](../../../../samples/snippets/csharp/VS_Snippets_Wpf/FEResourceSH_snip/CS/page1.xaml#xaml)]  
  
 每个框架级元素 ( <xref:System.Windows.FrameworkElement>或<xref:System.Windows.FrameworkContentElement>) 具有<xref:System.Windows.FrameworkElement.Resources%2A>属性，它是包含资源的属性 (作为<xref:System.Windows.ResourceDictionary>) 资源定义。 您可以在任何元素上定义的资源。 但是，在根元素，它是最常定义资源<xref:System.Windows.Controls.Page>在示例中。  
  
 在资源字典中的每个资源必须具有唯一键。 在标记中定义的资源，可将分配的唯一键通过[X:key 指令](../../../../docs/framework/xaml-services/x-key-directive.md)。 通常情况下，该密钥是一个字符串;但是，您还可以设置它对其他对象类型使用相应的标记扩展。 某些功能区中使用的资源的非字符串键[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]，值得注意的是对样式、 组件资源和数据的样式设置。  
  
 定义的资源后，你可以引用要使用的属性值，通过使用指定键的名称，例如资源标记扩展语法的资源︰  
  
 [!code-xml[FEResourceSH_snip#KeyNameUsage](../../../../samples/snippets/csharp/VS_Snippets_Wpf/FEResourceSH_snip/CS/page2.xaml#keynameusage)]  
  
 在前面的示例中，当[!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)]加载器处理值`{StaticResource MyBrush}`为<xref:System.Windows.Controls.Control.Background%2A>属性<xref:System.Windows.Controls.Button>，资源查找逻辑首先检查资源字典中的是否<xref:System.Windows.Controls.Button>元素。 如果<xref:System.Windows.Controls.Button>没有一个定义的资源键`MyBrush`（不是，其资源集合为空），查找接下来检查的父元素<xref:System.Windows.Controls.Button>，即<xref:System.Windows.Controls.Page>。 因此，当您定义的资源上<xref:System.Windows.Controls.Page>根元素中，在逻辑树中的所有元素<xref:System.Windows.Controls.Page>可以访问它，并为任何属性的值设置接受，您可以重复使用同一资源<xref:System.Type>该资源表示。 在上一示例中，相同`MyBrush`资源设置两个不同的属性︰<xref:System.Windows.Controls.Control.Background%2A>的<xref:System.Windows.Controls.Button>，和<xref:System.Windows.Shapes.Shape.Fill%2A>的<xref:System.Windows.Shapes.Rectangle>。  
  
<a name="staticdynamic"></a>   
## <a name="static-and-dynamic-resources"></a>静态和动态资源  
 可以作为静态资源或动态资源引用资源。 这通过使用[StaticResource 标记扩展](../../../../docs/framework/wpf/advanced/staticresource-markup-extension.md)或[DynamicResource 标记扩展](../../../../docs/framework/wpf/advanced/dynamicresource-markup-extension.md)。 标记扩展是一项功能的[!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)]，您可以通过使用标记扩展来处理特性字符串并返回到对象中指定的对象引用由此[!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)]加载程序。 有关标记扩展行为的详细信息，请参阅[标记扩展和 WPF XAML](../../../../docs/framework/wpf/advanced/markup-extensions-and-wpf-xaml.md)。  
  
 当您使用的标记扩展时，您通常会提供一个或多个参数采用字符串形式，由该特定标记扩展，处理，而不是所设置的属性的上下文中进行求值。 [StaticResource 标记扩展](../../../../docs/framework/wpf/advanced/staticresource-markup-extension.md)处理通过查找所有可用的资源字典中的键的值的键。 发生这种情况在加载期间，它是在加载过程需要分配采用静态资源引用的属性值的时间内的点。 [DynamicResource 标记扩展](../../../../docs/framework/wpf/advanced/dynamicresource-markup-extension.md)改为进程通过创建一个表达式，并且该表达式的键会一直保持未计算直到实际运行该应用程序，在这段时间的表达式进行计算和属性提供值。  
  
 在引用某个资源时，无论是使用静态资源引用还是动态资源引用可以影响下列注意事项︰  
  
-   如何为您的应用程序创建资源的整体设计 (每页上，在应用程序中，在松散[!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)]，资源的唯一程序集中)。  
  
-   应用程序功能︰ 正在更新的应用程序的要求的实际时间部分中的资源？  
  
-   该资源的引用类型的相应查找行为。  
  
-   特定属性或资源类型以及这些类型的本机行为。  
  
### <a name="static-resources"></a>静态资源  
 静态资源引用最适合于以下情况︰  
  
-   应用程序设计中最重要的是其资源集中到页或应用程序级别资源的集中字典。 静态资源引用不会重新计算基于运行时行为，如重新加载页，并且因此可以在不需要每个资源和应用程序设计时避免大量动态资源引用的某些性能优势。  
  
-   正在设置不在属性的值<xref:System.Windows.DependencyObject>或<xref:System.Windows.Freezable>。  
  
-   正在创建的资源字典，将编译成 DLL，并打包为应用程序的一部分或应用程序之间共享。  
  
-   要创建自定义控件的主题，并且定义在主题中使用的资源。 这种情况下，您通常不希望动态资源引用查找行为，以便查找可预测并且是独立的主题，你会转而考虑静态资源引用行为。 使用动态资源引用，甚至是主题中的引用进行求值直到运行时，并且没有应用主题时，某个本地元素会重新定义的键，您的主题试图引用，并且本地元素会位于主题本身在查找中之前有机会。 如果发生这种情况，您的主题不在预期的方式中的行为。  
  
-   正在使用资源来设置大量的依赖项属性。 依赖项属性具有有效值缓存为启用的属性系统，因此，如果依赖项属性可提供的值在加载时，计算依赖项属性而不必重新求值表达式检查并且可以返回的最后一个有效的值。 此方法可以提高性能。  
  
-   你想要为所有使用者，更改基础资源或者你想要使用的每个使用者维护单独的可写实例[x︰ 共享属性](../../../../docs/framework/xaml-services/x-shared-attribute.md)。  
  
#### <a name="static-resource-lookup-behavior"></a>静态资源查找行为  
  
1.  查找过程检查所请求的设置的属性的元素所定义的资源字典中的键。  
  
2.  查找过程然后遍历逻辑树上方，到父元素并且其资源字典。 此过程将继续，直至到达根元素。  
  
3.  接下来，检查应用程序资源。 应用程序资源是由定义的资源字典中的这些资源<xref:System.Windows.Application>对象您[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]应用程序。  
  
 从资源字典中的静态资源引用必须引用已定义词法资源引用之前的资源。 无法通过静态资源引用解析前向引用。 出于此原因，如果您使用静态资源引用，您必须设计资源字典结构以便将达到或接近每个相应资源字典的开头定义适用于按资源的资源。  
  
 静态资源查找可以扩展到主题，或系统资源，但支持这种情况只是因为[!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)]加载程序延迟了请求。 此延迟是必需的以便在加载页面时的运行时主题正确地应用于该应用程序。 但是，静态资源引用与已知仅存在于主题中或作为资源不推荐的系统的键。 这是因为如果用户实时更改主题，此类引用都不会重新计算。 请求主题或系统资源时，可以更可靠的动态资源引用。 例外情况是当主题元素自身请求另一个资源。 这些引用应该静态资源引用适用前面提到的原因。  
  
 如果找不到静态资源引用的异常行为会有所不同。 如果延迟资源，该异常发生在运行时。 如果资源未延迟，在加载时将发生异常。  
  
### <a name="dynamic-resources"></a>动态资源  
 动态资源最适合于在下列情况︰  
  
-   资源的值取决于直到运行时才知道的条件。 这包括系统资源或用户可设置的资源。 例如，创建参考系统属性的 setter 值公开<xref:System.Windows.SystemColors>， <xref:System.Windows.SystemFonts>，或<xref:System.Windows.SystemParameters>。 这些值是真正的动态的因为它们最终来自用户和操作系统的运行时环境。 您还可能会发生变化，其中页级别的资源访问还必须捕获更改的应用程序级主题。  
  
-   要创建或引用的自定义控件的主题样式。  
  
-   你想要调整的内容<xref:System.Windows.ResourceDictionary>在应用程序生存期内。  
  
-   必须具有相互依赖关系前, 向引用可能要求复杂的资源结构。 静态资源引用不支持前向引用，但动态资源引用支持，因为不需要在运行时以前, 计算资源前, 向引用因此彼此不相关的概念。  
  
-   引用是从编译或工作集的角度来看特别大的资源和资源可能不会立即加载页面时使用。 静态资源引用始终从加载[!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)]加载页面时; 但是，动态资源引用不会加载直到它被实际使用。  
  
-   要创建 setter 值可能来自其他受主题或其他用户设置的值的样式。  
  
-   正在将资源应用于应用程序生命周期内可能会在逻辑树中父级的元素。 也有可能更改父站点更改资源查找范围，因此如果您希望为设置了父级的元素将会重新计算资源基于新的作用域，始终使用动态资源引用。  
  
#### <a name="dynamic-resource-lookup-behavior"></a>动态资源查找行为  
 动态资源引用的资源查找行为类似在代码中的查找行为，如果调用<xref:System.Windows.FrameworkElement.FindResource%2A>或<xref:System.Windows.FrameworkElement.SetResourceReference%2A>。  
  
1.  查找过程检查所请求的设置的属性的元素所定义的资源字典中的键。  
  
    -   如果此元素可定义<xref:System.Windows.FrameworkElement.Style%2A>属性，<xref:System.Windows.Style.Resources%2A>字典内的<xref:System.Windows.Style>已选中。  
  
    -   如果此元素可定义<xref:System.Windows.Controls.Control.Template%2A>属性，<xref:System.Windows.FrameworkTemplate.Resources%2A>字典内的<xref:System.Windows.FrameworkTemplate>已选中。  
  
2.  查找过程然后遍历逻辑树上方，到父元素并且其资源字典。 此过程将继续，直至到达根元素。  
  
3.  接下来，检查应用程序资源。 应用程序资源是由定义的资源字典中的这些资源<xref:System.Windows.Application>对象您[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]应用程序。  
  
4.  检查了主题资源字典，为当前处于活动状态的主题。 如果该主题在运行时发生更改，则这是重新计算。  
  
5.  检查系统资源。  
  
 （如果有） 的异常行为会有所不同︰  
  
-   如果请求的资源的<xref:System.Windows.FrameworkElement.FindResource%2A>调用，并且未找到，则引发异常。  
  
-   如果请求的资源的<xref:System.Windows.FrameworkElement.TryFindResource%2A>调用，并且未找到，会引发任何异常，但返回的值为`null`。 如果要设置的属性不接受`null`，则它是仍有可能会引发更深的异常 （这取决于所设置的单个属性）。  
  
-   如果请求的资源中的动态资源引用的[!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)]，未找到，则行为取决于常规属性系统中，但的常规行为如同任何属性设置操作在存在相应的资源的级别发生。 例如，如果您尝试设置的背景上使用不会对计算资源对各个按钮元素，然后设置任何值的结果，但有效的值仍可能来自属性系统和值优先级中的其他参与者。 例如，背景值仍可能来自从一个本地定义的按钮样式，或从主题样式。 对于未定义的主题样式的属性，属性元数据中的默认值可能来自后失败的资源评估的生效值。  
  
#### <a name="restrictions"></a>限制  
 动态资源引用具有一些重要的限制。 至少一个以下必须满足︰  
  
-   要设置的属性必须是属性上<xref:System.Windows.FrameworkElement>或<xref:System.Windows.FrameworkContentElement>。 属性必须为后盾<xref:System.Windows.DependencyProperty>。  
  
-   引用是对中的一个值<xref:System.Windows.Style><xref:System.Windows.Setter>。  
  
-   要设置的属性必须是属性上<xref:System.Windows.Freezable>作为其中任何一个值提供<xref:System.Windows.FrameworkElement>或<xref:System.Windows.FrameworkContentElement>属性，或<xref:System.Windows.Setter>值。  
  
 由于所设置的属性必须是<xref:System.Windows.DependencyProperty>或<xref:System.Windows.Freezable>属性，属性的大多数更改可以传播到 UI，因为属性更改 （更改的动态资源值） 时确认了属性系统。 大多数控件包含逻辑，用于将强制另一个控件布局，如果<xref:System.Windows.DependencyProperty>更改和属性可能会影响布局。 但是，并非所有属性都具有[DynamicResource 标记扩展](../../../../docs/framework/wpf/advanced/dynamicresource-markup-extension.md)作为其值保证提供这种方式中用户界面中的实时更新中的值。 该功能仍可能会有所不同的具体取决于该属性，以及根据所拥有的属性或甚至您的应用程序的逻辑结构的类型。  
  
<a name="stylesimplicitkeys"></a>   
## <a name="styles-datatemplates-and-implicit-keys"></a>样式、 Datatemplate 和隐式键  
 前面曾提到中的所有项<xref:System.Windows.ResourceDictionary>必须具有一个键。 但是，也不表示所有资源必须都具有一个显式`x:Key`。 多个对象类型都支持隐式键时定义为资源，其中的密钥值绑定到另一个属性的值。 这称为隐式键，而`x:Key`属性是显式的键。 您可以通过指定显式键覆盖任何隐式键。  
  
 资源的一个非常重要的方案是在定义时<xref:System.Windows.Style>。 事实上，<xref:System.Windows.Style>几乎始终定义为将项记入资源字典中，因为样式本质上是适合于重复使用。 有关样式的详细信息，请参阅[样式和模板化](../../../../docs/framework/wpf/controls/styling-and-templating.md)。  
  
 控件样式可同时创建和使用隐式键引用。 定义控件的默认外观的主题样式依赖于此隐式键。 从请求该的角度来看，隐式键是<xref:System.Type>控件本身。 从定义该资源的角度来看，隐式键是<xref:System.Windows.Style.TargetType%2A>的样式。 因此，如果要创建自定义控件的主题，创建的样式的交互与现有主题样式，您不必指定[X:key 指令](../../../../docs/framework/xaml-services/x-key-directive.md)为此，<xref:System.Windows.Style>。 而且，如果您想要使用的主题的样式，不需要在所有指定的任何样式。 例如，下面的样式定义的工作原理，即使<xref:System.Windows.Style>资源似乎不具有键︰  
  
 [!code-xml[FEResourceSH_snip#ImplicitStyle](../../../../samples/snippets/csharp/VS_Snippets_Wpf/FEResourceSH_snip/CS/page2.xaml#implicitstyle)]  
  
 该样式实际上具有一个键︰ 隐式键`typeof(`<xref:System.Windows.Controls.Button>`)`。 在标记中，您可以指定<xref:System.Windows.Style.TargetType%2A>直接作为类型名称 (或您可以选择使用[{x︰ 类型...}](../../../../docs/framework/xaml-services/x-type-markup-extension.md) 若要返回<xref:System.Type>。  
  
 通过使用默认主题样式机制[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]，作为运行时样式的应用样式<xref:System.Windows.Controls.Button>在页上，即使<xref:System.Windows.Controls.Button>本身不会尝试指定其<xref:System.Windows.FrameworkElement.Style%2A>属性或特定资源引用的样式。 页中定义的样式位于前面部分中查找序列早于主题字典样式，使用同一主题字典样式的密钥对。 你可能只需指定`<Button>Hello</Button>`页上，使用定义的样式中的任意位置<xref:System.Windows.Style.TargetType%2A>的`Button`将应用于该按钮。 如果你想，仍显式键具有相同的类型值样式<xref:System.Windows.Style.TargetType%2A>，为了清楚起见，在标记中，但这是可选的。  
  
 如果不在控件上应用样式的隐式键<xref:System.Windows.FrameworkElement.OverridesDefaultStyle%2A>是`true`(另请注意， <xref:System.Windows.FrameworkElement.OverridesDefaultStyle%2A>可以将设置为控件的类，而不是显式的控件实例上的本机行为的一部分)。 此外，为了对派生的类方案支持隐式键，该控件必须重写<xref:System.Windows.FrameworkElement.DefaultStyleKey%2A> (作为的一部分提供的所有现有控件[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]这样做)。 有关样式、 主题和控件设计的详细信息，请参阅[设计可样式化控件的指导原则](../../../../docs/framework/wpf/controls/guidelines-for-designing-stylable-controls.md)。  
  
 <xref:System.Windows.DataTemplate>还具有隐式键。 隐式键<xref:System.Windows.DataTemplate>是<xref:System.Windows.DataTemplate.DataType%2A>属性值。                  <xref:System.Windows.DataTemplate.DataType%2A>也可以指定为的类型的名称，而不是使用显式[{x︰ 类型...}](../../../../docs/framework/xaml-services/x-type-markup-extension.md). 有关详细信息，请参阅[数据模板化概述](../../../../docs/framework/wpf/data/data-templating-overview.md)。  
  
## <a name="see-also"></a>另请参阅  
 <xref:System.Windows.ResourceDictionary>   
 [应用程序资源](../../../../docs/framework/wpf/advanced/optimizing-performance-application-resources.md)   
 [资源和代码](../../../../docs/framework/wpf/advanced/resources-and-code.md)   
 [定义和引用资源](../../../../docs/framework/wpf/advanced/how-to-define-and-reference-a-resource.md)   
 [应用程序管理概述](../../../../docs/framework/wpf/app-development/application-management-overview.md)   
 [X:type 标记扩展](../../../../docs/framework/xaml-services/x-type-markup-extension.md)   
 [StaticResource 标记扩展](../../../../docs/framework/wpf/advanced/staticresource-markup-extension.md)   
 [DynamicResource 标记扩展](../../../../docs/framework/wpf/advanced/dynamicresource-markup-extension.md)