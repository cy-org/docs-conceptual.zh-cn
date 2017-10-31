---
title: "样式设置和模板化 | Microsoft Docs"
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
  - "触发器"
  - "引用的样式"
  - "事件触发器"
  - "样式，系统必备组件"
  - "声明的样式"
  - "样式概述"
  - "扩展的样式"
  - "触发器的样式"
  - "样式，将触发事件"
ms.assetid: 481765e5-5467-4a75-9f7b-e10e2ac410d9
caps.latest.revision: 34
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 33
---
# 样式设置和模板化
[!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)]样式和模板化是指一套功能 （样式、 模板、 触发器和情节提要），使开发人员和设计器来创建极具视觉表现力的效果，以创建一致的外观对其产品。 尽管开发人员和设计人员可以自定义广泛根据应用程序的应用程序的外观，则需要允许维护和外观内部以及各应用程序之间共享一个功能强大样式和模板化模型。 [!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)]提供了该模型。  
  
 另一项功能[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]样式模型是分离演示文稿和逻辑。 这意味着仅使用设计器可以处理应用程序的外观[!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)]在同时开发人员通过使用 C# 或 Visual Basic 的编程逻辑。  
  
 本概述侧重于应用程序的样式和模板化方面并不讨论任何数据绑定概念。 有关数据绑定的信息，请参阅[数据绑定概述](../../../../docs/framework/wpf/data/data-binding-overview.md)。  
  
 此外，务必了解启用样式和模板，可以重复使用的资源。 有关资源的详细信息，请参阅[XAML 资源](../../../../docs/framework/wpf/advanced/xaml-resources.md)。  
  
   
  
<a name="styling_and_templating_sample"></a>   
## <a name="styling-and-templating-sample"></a>样式和模板化示例  
 使用本概述中的代码示例基于下面的插图中所示的简单照片示例︰  
  
 ![设置 ListView 样式](../../../../docs/framework/wpf/controls/media/stylingintro-triggers.png "StylingIntro_triggers")  
  
 该简单照片示例使用样式和模板化来创建视觉效果更佳的用户体验。 此示例具有两个<xref:System.Windows.Controls.TextBlock>元素和一个<xref:System.Windows.Controls.ListBox>绑定到图像列表的控件。 有关完整的示例，请参阅[样式和模板化示例简介](http://go.microsoft.com/fwlink/?LinkID=160010)。  
  
<a name="styling_basics"></a>   
## <a name="style-basics"></a>样式基础知识  
 您可以认为<xref:System.Windows.Style>方便地将一组属性值应用于多个元素。 例如，考虑以下<xref:System.Windows.Controls.TextBlock>元素和它们的默认外观︰  
  
 [!code-xml[StylingIntroSample_snippet#TextBlocks](../../../../samples/snippets/csharp/VS_Snippets_Wpf/StylingIntroSample_snippet/CSharp/Window1.xaml#textblocks)]  
  
 ![样式示例屏幕快照](../../../../docs/framework/wpf/controls/media/stylingintro-textblocksbefore.png "StylingIntro_TextBlocksBefore")  
  
 您可以通过设置属性，如更改默认外观<xref:System.Windows.Controls.Control.FontSize%2A>和<xref:System.Windows.Controls.Control.FontFamily%2A>，每个<xref:System.Windows.Controls.TextBlock>直接元素。 但是，如果您希望您<xref:System.Windows.Controls.TextBlock>元素共享某些属性，您可以创建<xref:System.Windows.Style>中`Resources`部分您[!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)]文件，如下所示︰  
  
 [!code-xml[StylingIntroSnippet#Resources](../../../../samples/snippets/csharp/VS_Snippets_Wpf/StylingIntroSnippet/CS/window1.xaml#resources)]  
[!code-xml[StylingIntroSnippet#tb1](../../../../samples/snippets/csharp/VS_Snippets_Wpf/StylingIntroSnippet/CS/window1.xaml#tb1)]  
[!code-xml[StylingIntroSnippet#Resources2](../../../../samples/snippets/csharp/VS_Snippets_Wpf/StylingIntroSnippet/CS/window1.xaml#resources2)]  
  
 当您将设置<xref:System.Windows.Style.TargetType%2A>到方式的<xref:System.Windows.Controls.TextBlock>类型，该样式应用于所有<xref:System.Windows.Controls.TextBlock>窗口中的元素。  
  
 现在<xref:System.Windows.Controls.TextBlock>元素出现，如下所示︰  
  
 ![样式示例屏幕快照](../../../../docs/framework/wpf/controls/media/stylingintro-textblocksbasestyle.png "StylingIntro_TextBlocksBaseStyle")  
  
### <a name="extending-styles"></a>扩展样式  
 您可能需要两个<xref:System.Windows.Controls.TextBlock>元素共享某些属性值，如<xref:System.Windows.Controls.Control.FontFamily%2A>和居中<xref:System.Windows.FrameworkElement.HorizontalAlignment%2A>，但您还希望文本"图片收藏"具有一些附加属性。 通过创建一个新的样式，基于第一个样式，如下所示，可以执行的操作︰  
  
 [!code-xml[StylingIntroSnippet#Resources](../../../../samples/snippets/csharp/VS_Snippets_Wpf/StylingIntroSnippet/CS/window1.xaml#resources)]  
[!code-xml[StylingIntroSnippet#tb2](../../../../samples/snippets/csharp/VS_Snippets_Wpf/StylingIntroSnippet/CS/window1.xaml#tb2)]  
[!code-xml[StylingIntroSnippet#Resources2](../../../../samples/snippets/csharp/VS_Snippets_Wpf/StylingIntroSnippet/CS/window1.xaml#resources2)]  
  
 请注意，上面的样式提供`x:Key`。 若要将样式应用，请设置<xref:System.Windows.FrameworkElement.Style%2A>属性您<xref:System.Windows.Controls.TextBlock>到`x:Key`值，如下所示︰  
  
 [!code-xml[StylingIntroSnippet#UIText](../../../../samples/snippets/csharp/VS_Snippets_Wpf/StylingIntroSnippet/CS/window1.xaml#uitext)]  
  
 这<xref:System.Windows.Controls.TextBlock>样式现在有<xref:System.Windows.FrameworkElement.HorizontalAlignment%2A>值<xref:System.Windows.HorizontalAlignment>、 <xref:System.Windows.Controls.TextBlock.FontFamily%2A>值`Comic Sans MS`、 <xref:System.Windows.Controls.TextBlock.FontSize%2A>值为 26，和一个<xref:System.Windows.Controls.TextBlock.Foreground%2A>值设置为<xref:System.Windows.Media.LinearGradientBrush>示例所示。 请注意，它将重写<xref:System.Windows.Controls.Control.FontSize%2A>基样式的值。 如果有多个<xref:System.Windows.Setter>中设置同一属性<xref:System.Windows.Style>、 <xref:System.Windows.Setter> ，它是声明最后一个优先。  
  
 下面的示例演示什么<xref:System.Windows.Controls.TextBlock>元素现在如下所示︰  
  
 ![设置样式的 Textblock](../../../../docs/framework/wpf/controls/media/stylingintro-textblocks.png "StylingIntro_TextBlocks")  
  
 这`TitleText`样式扩展已为创建的样式<xref:System.Windows.Controls.TextBlock>类型。 您还可以扩展样式，它具有`x:Key`使用`x:Key`值。 有关示例，请参阅提供的示例<xref:System.Windows.Style.BasedOn%2A>属性。  
  
### <a name="relationship-of-the-targettype-property-and-the-xkey-attribute"></a>TargetType 属性和 X:key 特性之间的关系  
 第一个示例中所示，设置<xref:System.Windows.Style.TargetType%2A>属性设置为`TextBlock`而不将指定样式`x:Key`样式应用于所有<xref:System.Windows.Controls.TextBlock>元素。 在这种情况下，`x:Key`隐式设置为`{x:Type TextBlock}`。 这意味着，如果你显式设置`x:Key`以外值赋给任何`{x:Type TextBlock}`、<xref:System.Windows.Style>不应用于所有<xref:System.Windows.Controls.TextBlock>元素自动。 相反，你必须将样式应用 (通过使用`x:Key`值) 到<xref:System.Windows.Controls.TextBlock>元素显式。 如果您的样式将在资源部分，并且您未设置<xref:System.Windows.Style.TargetType%2A>属性在您的方式，则您必须提供`x:Key`。  
  
 除了提供默认值为`x:Key`、 <xref:System.Windows.Style.TargetType%2A>属性指定应用 setter 属性的类型。 如果未指定<xref:System.Windows.Style.TargetType%2A>，您必须有资格中的属性您<xref:System.Windows.Setter>对象使用的语法通过类名`Property="ClassName.Property"`。 例如，而不是设置`Property="FontSize"`，必须设置<xref:System.Windows.Setter.Property%2A>到`"TextBlock.FontSize"`或`"Control.FontSize"`。  
  
 另请注意，许多[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]控件包含的其他组合[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]控件。 如果您创建应用于一种类型的所有控件的样式，可能会得到意外的结果。 例如，如果您创建的样式针对<xref:System.Windows.Controls.TextBlock>键入<xref:System.Windows.Window>，该样式应用于所有<xref:System.Windows.Controls.TextBlock>控件在窗口中，即使<xref:System.Windows.Controls.TextBlock>属于另一个控件，如<xref:System.Windows.Controls.ListBox>。  
  
### <a name="styles-and-resources"></a>样式和资源  
 可以在派生自任何元素上使用样式<xref:System.Windows.FrameworkElement>或<xref:System.Windows.FrameworkContentElement>。 声明一种样式的最常见方法是作为其资源`Resources`中[!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)]文件，如前面的示例中所示。 由于样式为资源，它们遵循相同的作用域规则应用于所有资源;其中样式的声明位置应用该样式的影响。 例如，如果您声明您的应用程序定义的根元素中的样式[!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)]文件，该样式可以在您的应用程序的任何地方使用。 如果您创建导航应用程序，并声明中的应用程序的一个样式[!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)]文件，该样式可以使用只能在该[!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)]文件。 有关资源范围规则的详细信息，请参阅[XAML 资源](../../../../docs/framework/wpf/advanced/xaml-resources.md)。  
  
 此外，您可以找到有关样式和中的资源的详细信息[共享资源和主题](#styling_themes)本概述中更高版本。  
  
### <a name="setting-styles-programmatically"></a>以编程方式设置样式  
 若要以编程方式向元素分配已命名的样式，从资源集合中获取该样式，并将其分配给元素的<xref:System.Windows.FrameworkElement.Style%2A>属性。 请注意，资源集合中的项属于类型<xref:System.Object>。 因此，您必须强制转换为检索到的样式<xref:System.Windows.Style>之前将其分配给<xref:System.Windows.FrameworkElement.Style%2A>属性。 例如，若要设置定义`TitleText`样式上<xref:System.Windows.Controls.TextBlock>名为`textblock1`，执行以下操作︰  
  
 [!code-csharp[StylingIntroSample_snippet#Code](../../../../samples/snippets/csharp/VS_Snippets_Wpf/StylingIntroSample_snippet/CSharp/Window1.xaml.cs#code)]
 [!code-vb[StylingIntroSample_snippet#Code](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/StylingIntroSample_snippet/visualbasic/window1.xaml.vb#code)]  
  
 请注意，一旦应用了一种样式，它密封的不能更改。 如果您想要动态地更改已应用样式，必须创建新的样式来替换现有的一个。 有关详细信息，请参阅<xref:System.Windows.Style.IsSealed%2A>属性。  
  
 您可以创建一个对象，选择要应用根据自定义逻辑的样式。 有关示例，请参阅提供的示例<xref:System.Windows.Controls.StyleSelector>类。  
  
<a name="styling_binding_dynamicresource"></a>   
### <a name="bindings-dynamic-resources-and-event-handlers"></a>绑定、 动态资源和事件处理程序  
 请注意，您可以使用`Setter.Value`属性来指定[绑定标记扩展](../../../../docs/framework/wpf/advanced/binding-markup-extension.md)或[DynamicResource 标记扩展](../../../../docs/framework/wpf/advanced/dynamicresource-markup-extension.md)。 有关详细信息，请参阅为提供的示例<xref:System.Windows.Setter.Value%2A?displayProperty=fullName>属性。  
  
 到目前为止，此概述仅介绍了使用 setter 设置属性值。 此外可以在样式中指定事件处理程序。 有关详细信息，请参阅<xref:System.Windows.EventSetter>。  
  
<a name="styling_datatemplates"></a>   
## <a name="data-templates"></a>数据模板  
 在此示例应用程序中，没有<xref:System.Windows.Controls.ListBox>控件绑定到的照片列表︰  
  
 [!code-xml[StylingIntroSnippet#UIListBox](../../../../samples/snippets/csharp/VS_Snippets_Wpf/StylingIntroSnippet/CS/window1.xaml#uilistbox)]  
  
 这<xref:System.Windows.Controls.ListBox>当前如下所示︰  
  
 ![应用模板之前的 ListBox](../../../../docs/framework/wpf/controls/media/stylingintro-listboxbefore.png "StylingIntro_ListBoxBefore")  
  
 大多数控件都具有某种类型的内容，并且该内容通常来自要绑定到的数据。 在此示例中，数据是照片列表。 在[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]，您使用<xref:System.Windows.DataTemplate>来定义数据的可视化表示。 基本上，什么不将放入<xref:System.Windows.DataTemplate>决定在呈现的应用程序中数据的外观。  
  
 在我们的示例应用程序，每个自定义`Photo`对象具有`Source`指定图像的文件路径的类型字符串的属性。 目前，照片对象显示为文件路径。  
  
 对于要显示为图像的照片，您创建<xref:System.Windows.DataTemplate>作为资源︰  
  
 [!code-xml[StylingIntroSnippet#Resources](../../../../samples/snippets/csharp/VS_Snippets_Wpf/StylingIntroSnippet/CS/window1.xaml#resources)]  
[!code-xml[StylingIntroSnippet#DataTemplate](../../../../samples/snippets/csharp/VS_Snippets_Wpf/StylingIntroSnippet/CS/window1.xaml#datatemplate)]  
[!code-xml[StylingIntroSnippet#Resources2](../../../../samples/snippets/csharp/VS_Snippets_Wpf/StylingIntroSnippet/CS/window1.xaml#resources2)]  
  
 请注意， <xref:System.Windows.DataTemplate.DataType%2A>属性是非常类似于<xref:System.Windows.Style.TargetType%2A>属性<xref:System.Windows.Style>。 如果您<xref:System.Windows.DataTemplate>时，可以在资源部分中，您指定<xref:System.Windows.DataTemplate.DataType%2A>属性设置为一种类型并不将其分配`x:Key`、 <xref:System.Windows.DataTemplate>只要该类型将出现应用。 您始终可以选择要分配<xref:System.Windows.DataTemplate>与`x:Key`并将其作为`StaticResource`的属性<xref:System.Windows.DataTemplate>类型，如<xref:System.Windows.Controls.ItemsControl.ItemTemplate%2A>属性或<xref:System.Windows.Controls.ContentControl.ContentTemplate%2A>属性。  
  
 从根本上来说， <xref:System.Windows.DataTemplate>在上面的示例中定义，只要有`Photo`对象，它应显示为<xref:System.Windows.Controls.Image>内<xref:System.Windows.Controls.Border>。 与此<xref:System.Windows.DataTemplate>，应用程序现在如下所示︰  
  
 ![照片图](../../../../docs/framework/wpf/controls/media/stylingintro-photosasimages.png "StylingIntro_PhotosAsImages")  
  
 数据模板化模型还提供其他功能。 例如，如果您要显示集合中包含数据，使用其他集合<xref:System.Windows.Controls.HeaderedItemsControl>键入如<xref:System.Windows.Controls.Menu>或<xref:System.Windows.Controls.TreeView>，没有<xref:System.Windows.HierarchicalDataTemplate>。 另一个数据模板化功能是<xref:System.Windows.Controls.DataTemplateSelector>，这样，您可以选择<xref:System.Windows.DataTemplate>用于根据自定义逻辑。 有关详细信息，请参阅[数据模板化概述](../../../../docs/framework/wpf/data/data-templating-overview.md)，它提供了不同的数据模板化功能的更深入讨论。  
  
<a name="styling_controltemplates"></a>   
## <a name="control-templates"></a>控件模板  
 在[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]、 <xref:System.Windows.Controls.ControlTemplate>的控件定义了该控件的外观。 可以通过定义一个新更改的结构和控件的外观<xref:System.Windows.Controls.ControlTemplate>控件。 许多情况下，这种方法都足够灵活，以便不需要编写您自己的自定义控件。 有关详细信息，请参阅[通过创建 ControlTemplate 自定义现有控件的外观](../../../../docs/framework/wpf/controls/customizing-the-appearance-of-an-existing-control.md)。  
  
<a name="styling_triggers"></a>   
## <a name="triggers"></a>触发器  
 触发器设置属性，或启动操作，如动画，或当属性值更改时将引发一个事件。 <xref:System.Windows.Style>， <xref:System.Windows.Controls.ControlTemplate>，和<xref:System.Windows.DataTemplate>都`Triggers`属性，它可以包含一组触发器。 有各种类型的触发器。  
  
### <a name="property-triggers"></a>属性触发器  
 一个<xref:System.Windows.Trigger>设置属性值，或启动基于属性的值的操作称为属性触发器。  
  
 为了演示如何使用属性触发器，可以将每个<xref:System.Windows.Controls.ListBoxItem>部分透明，除非它被选中。 下面的样式集<xref:System.Windows.UIElement.Opacity%2A>值<xref:System.Windows.Controls.ListBoxItem>到`0.5`。 当<xref:System.Windows.Controls.ListBoxItem.IsSelected%2A>属性是`true`，但<xref:System.Windows.UIElement.Opacity%2A>设置为`1.0`:  
  
 [!code-xml[StylingIntroSample_snippet#Triggers](../../../../samples/snippets/csharp/VS_Snippets_Wpf/StylingIntroSample_snippet/CSharp/Window1.xaml#triggers)]  
[!code-xml[StylingIntroSample_snippet#EndTriggers](../../../../samples/snippets/csharp/VS_Snippets_Wpf/StylingIntroSample_snippet/CSharp/Window1.xaml#endtriggers)]  
  
 此示例使用<xref:System.Windows.Trigger>若要设置的属性值，但请注意，<xref:System.Windows.Trigger>类还具有<xref:System.Windows.TriggerBase.EnterActions%2A>和<xref:System.Windows.TriggerBase.ExitActions%2A>启用触发器，以执行操作的属性。  
  
 请注意， <xref:System.Windows.FrameworkElement.MaxHeight%2A>属性<xref:System.Windows.Controls.ListBoxItem>设置为`75`。 下图中的第三项是选定的项︰  
  
 ![设置 ListView 样式](../../../../docs/framework/wpf/controls/media/stylingintro-triggers.png "StylingIntro_triggers")  
  
### <a name="eventtriggers-and-storyboards"></a>可以使用事件触发器和情节提要  
 触发器的另一种是<xref:System.Windows.EventTrigger>，从而启动一组基于事件的出现次数的操作。 例如，以下<xref:System.Windows.EventTrigger>对象指定当鼠标指针进入<xref:System.Windows.Controls.ListBoxItem>、 <xref:System.Windows.FrameworkElement.MaxHeight%2A>属性的值进行动画处理`90`通过`0.2`第二个句点。 当鼠标离开该项目时，该属性返回到原始值的一段`1`第二个。 请注意，它是不需要指定<xref:System.Windows.Media.Animation.DoubleAnimation.To%2A>值<xref:System.Windows.ContentElement.MouseLeave>动画。 这是因为动画能够跟踪的原始值。  
  
 [!code-xml[StylingIntroSample_snippet#EventTriggers](../../../../samples/snippets/csharp/VS_Snippets_Wpf/StylingIntroSample_snippet/CSharp/Window1.xaml#eventtriggers)]  
  
 有关详细信息，请参阅[演示图板概述](../../../../docs/framework/wpf/graphics-multimedia/storyboards-overview.md)。  
  
 在下图中，鼠标指向第三个项︰  
  
 ![样式示例屏幕快照](../../../../docs/framework/wpf/controls/media/stylingintro-eventtriggers.png "StylingIntro_EventTriggers")  
  
### <a name="multitriggers-datatriggers-and-multidatatriggers"></a>MultiTriggers、 数据触发器和 MultiDataTriggers  
 除了<xref:System.Windows.Trigger>和<xref:System.Windows.EventTrigger>，有其他类型的触发器。 <xref:System.Windows.MultiTrigger>允许您设置基于多个条件的属性值。 您使用<xref:System.Windows.DataTrigger>和<xref:System.Windows.MultiDataTrigger>时您的条件的属性是数据绑定。  
  
<a name="styling_themes"></a>   
## <a name="shared-resources-and-themes"></a>共享的资源和主题  
 典型[!INCLUDE[TLA#tla_wpf](../../../../includes/tlasharptla-wpf-md.md)]应用程序可能有多个应用于整个应用程序的用户界面 (UI) 资源。 总体来说，这组资源可被视为应用程序的主题。 [!INCLUDE[TLA#tla_wpf](../../../../includes/tlasharptla-wpf-md.md)]对于封装用户界面 (UI) 资源作为主题通过使用提供支持一个资源字典，其中封装为<xref:System.Windows.ResourceDictionary>类。  
  
 [!INCLUDE[TLA#tla_wpf](../../../../includes/tlasharptla-wpf-md.md)]主题定义通过使用样式和模板化机制，[!INCLUDE[TLA#tla_wpf](../../../../includes/tlasharptla-wpf-md.md)]公开用于自定义的任何元素的可视对象。  
  
 [!INCLUDE[TLA#tla_wpf](../../../../includes/tlasharptla-wpf-md.md)]主题资源存储在嵌入的资源字典中。 这些资源字典必须嵌入签名的程序集，并可以既可以嵌入在代码本身所在的程序集或中的并行程序集。 在 PresentationFramework.dll，包含的程序集的情况下[!INCLUDE[TLA#tla_wpf](../../../../includes/tlasharptla-wpf-md.md)]控件，主题资源是在一系列的并行程序集。  
  
 该主题将成为搜索元素的样式时的外观的最后一个位置。 通常情况下，搜索将首先向上遍历元素树搜索适当的资源，然后在应用程序资源集合中查找并最后在系统中查询。 这使应用程序开发人员有机会在到达主题之前重新定义树或应用程序级别的任何对象的样式。  
  
 您可以为单个文件，使您能够在多个应用程序之间重用主题定义资源字典。 此外可以通过定义多个资源字典以提供相同类型的资源，但使用不同的值来创建各种互换主题。 重新定义这些样式或其他资源的应用程序级别是设计应用程序外观的推荐的方法。  
  
 若要共享一组资源，跨应用程序，包括样式和模板，可以创建[!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)]文件并定义<xref:System.Windows.ResourceDictionary>。 例如，看一看下图显示的一部分[ControlTemplates 示例样式](http://go.microsoft.com/fwlink/?LinkID=160041):  
  
 ![控件模板示例](../../../../docs/framework/wpf/controls/media/stylingintro-controltemplateexamples.png "StylingIntro_ControlTemplateExamples")  
  
 如果您看一下[!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)]示例中的文件，您会注意到所有文件都包含以下︰  
  
 [!code-xml[ControlTemplateExamples#MergedDictionaries](../../../../samples/snippets/csharp/VS_Snippets_Wpf/ControlTemplateExamples/CS/resources/button.xaml#mergeddictionaries)]  
  
 就是共享`shared.xaml`，它定义<xref:System.Windows.ResourceDictionary> ，包含一组样式和画笔资源，使控件在该示例将具有一致的外观。  
  
 有关详细信息，请参阅[合并资源字典](../../../../docs/framework/wpf/advanced/merged-resource-dictionaries.md)。  
  
 如果要为您的自定义控件创建一个主题，请参阅的外部控件库部分[控件创作概述](../../../../docs/framework/wpf/controls/control-authoring-overview.md)。  
  
## <a name="see-also"></a>另请参阅  
 [在 WPF 中的 pack Uri](../../../../docs/framework/wpf/app-development/pack-uris-in-wpf.md)   
 [如何︰ 查找 ControlTemplate 生成的元素](../../../../docs/framework/wpf/controls/how-to-find-controltemplate-generated-elements.md)   
 [查找由 DataTemplate 生成的元素](../../../../docs/framework/wpf/data/how-to-find-datatemplate-generated-elements.md)