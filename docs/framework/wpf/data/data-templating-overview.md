---
title: "数据模板化概述 | Microsoft Docs"
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
  - "数据绑定、 模板"
  - "将数据绑定模板"
  - "数据模板"
  - "数据模板"
ms.assetid: 0f4d9f8c-0230-4013-bd7b-e8e7fed01b4a
caps.latest.revision: 25
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 24
---
# 数据模板化概述
[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]数据模板化模型为您提供很大的灵活性来定义您的数据表示形式。 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]控件具有内置功能，可以支持的数据表示自定义。 本主题首先演示如何定义<xref:System.Windows.DataTemplate> ，然后介绍其他数据模板化功能，例如选择了模板基于自定义逻辑和显示分层数据的支持。  
  
   
  
<a name="Prerequisites"></a>   
## <a name="prerequisites"></a>先决条件  
 本主题重点介绍数据模板化功能，并不是数据绑定概念的介绍。 有关基本数据绑定概念的信息，请参阅[数据绑定概述](../../../../docs/framework/wpf/data/data-binding-overview.md)。  
  
 <xref:System.Windows.DataTemplate>是有关数据的表示形式，是由提供的众多功能之一[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]样式和模板化模型。 有关的介绍[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]样式和模板化模型，例如，如何使用<xref:System.Windows.Style>若要在控件上设置属性，请参阅[样式和模板化](../../../../docs/framework/wpf/controls/styling-and-templating.md)主题。  
  
 此外，务必了解`Resources`，它们实质上是什么使对象如<xref:System.Windows.Style>和<xref:System.Windows.DataTemplate>为了能够重新使用。 对资源的详细信息，请参阅[XAML 资源](../../../../docs/framework/wpf/advanced/xaml-resources.md)。  
  
<a name="DataTemplating_Basic"></a>   
## <a name="data-templating-basics"></a>数据模板化基础知识  
   
  
 为了演示原因<xref:System.Windows.DataTemplate>是重要的是，让我们看一下数据绑定示例。 在此示例中，我们有<xref:System.Windows.Controls.ListBox>绑定到的列表`Task`对象。 每个`Task`对象具有`TaskName`（字符串）、 `Description` （字符串）、 `Priority` (int) 和一个类型的属性`TaskType`，即`Enum`面额`Home`和`Work`。  
  
 [!code-xml[DataTemplatingIntro_snip#Resources](../../../../samples/snippets/csharp/VS_Snippets_Wpf/DataTemplatingIntro_snip/CSharp/Window1.xaml#resources)]  
[!code-xml[DataTemplatingIntro_snip#UI1](../../../../samples/snippets/csharp/VS_Snippets_Wpf/DataTemplatingIntro_snip/CSharp/Window1.xaml#ui1)]  
[!code-xml[DataTemplatingIntro_snip#UI2](../../../../samples/snippets/csharp/VS_Snippets_Wpf/DataTemplatingIntro_snip/CSharp/Window1.xaml#ui2)]  
  
<a name="without_a_datatemplate"></a>   
### <a name="without-a-datatemplate"></a>而无需 DataTemplate  
 而无需<xref:System.Windows.DataTemplate>，但我们<xref:System.Windows.Controls.ListBox>当前如下所示︰  
  
 ![数据模板示例屏幕快照](../../../../docs/framework/wpf/data/media/datatemplatingintro-fig1.png "DataTemplatingIntro_fig1")  
  
 发生了什么情况是，如果没有任何特殊说明<xref:System.Windows.Controls.ListBox>通过默认调用`ToString`时尝试显示集合中的对象。 因此，如果`Task`对象重写`ToString`方法，则<xref:System.Windows.Controls.ListBox>基础集合中显示的字符串表示形式的每个源对象。  
  
 例如，如果`Task`类重写`ToString`方法这种方式，其中`name`是字段`TaskName`属性︰  
  
 [!code-csharp[DataTemplatingIntro_snip#ToString](../../../../samples/snippets/csharp/VS_Snippets_Wpf/DataTemplatingIntro_snip/CSharp/Data.cs#tostring)]
 [!code-vb[DataTemplatingIntro_snip#ToString](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/DataTemplatingIntro_snip/visualbasic/data.vb#tostring)]  
  
 则<xref:System.Windows.Controls.ListBox>外观如下所示︰  
  
 ![数据模板示例屏幕快照](../../../../docs/framework/wpf/data/media/datatemplatingintro-fig2.png "DataTemplatingIntro_fig2")  
  
 但是，这是限制，并不灵活。 此外，如果将绑定到[!INCLUDE[TLA2#tla_xml](../../../../includes/tla2sharptla-xml-md.md)]数据，您将无法重写`ToString`。  
  
<a name="defining_simple_datatemplate"></a>   
### <a name="defining-a-simple-datatemplate"></a>定义简单 DataTemplate  
 解决方法是定义<xref:System.Windows.DataTemplate>。 若要做到这一点的一种方法是设置<xref:System.Windows.Controls.ItemsControl.ItemTemplate%2A>属性<xref:System.Windows.Controls.ListBox>到<xref:System.Windows.DataTemplate>。 在中指定您<xref:System.Windows.DataTemplate>变成您的数据对象的可视结构。 以下<xref:System.Windows.DataTemplate>相当简单。 我们将向每个项都显示为三个说明<xref:System.Windows.Controls.TextBlock>内的元素<xref:System.Windows.Controls.StackPanel>。 每个<xref:System.Windows.Controls.TextBlock>元素绑定到的属性`Task`类。  
  
 [!code-xml[DataTemplatingIntro_snip#Inline](../../../../samples/snippets/csharp/VS_Snippets_Wpf/DataTemplatingIntro_snip/CSharp/Window1.xaml#inline)]  
  
 本主题中的示例的基础数据是一套[!INCLUDE[TLA2#tla_clr](../../../../includes/tla2sharptla-clr-md.md)]对象。 如果将绑定到[!INCLUDE[TLA2#tla_xml](../../../../includes/tla2sharptla-xml-md.md)]数据，基本概念是相同的但没有语法之间的细微差别。 例如，而不是`Path=TaskName`，则会将设置<xref:System.Windows.Data.Binding.XPath%2A>到`@TaskName`(如果`TaskName`是一个属性您[!INCLUDE[TLA2#tla_xml](../../../../includes/tla2sharptla-xml-md.md)]节点)。  
  
 现在我们<xref:System.Windows.Controls.ListBox>外观如下所示︰  
  
 ![数据模板示例屏幕快照](../../../../docs/framework/wpf/data/media/datatemplatingintro-fig3.png "DataTemplatingIntro_fig3")  
  
<a name="defining_datatemplate_as_a_resource"></a>   
### <a name="creating-the-datatemplate-as-a-resource"></a>为资源创建 DataTemplate  
 在上述示例中，我们定义<xref:System.Windows.DataTemplate>内联。 它是更常见的是使其成为可重用的对象，如以下示例所示在资源部分中定义︰  
  
 [!code-xml[DataTemplatingIntro_snip#R1](../../../../samples/snippets/csharp/VS_Snippets_Wpf/DataTemplatingIntro_snip/CSharp/Window1.xaml#r1)]  
[!code-xml[DataTemplatingIntro_snip#AsResource](../../../../samples/snippets/csharp/VS_Snippets_Wpf/DataTemplatingIntro_snip/CSharp/Window1.xaml#asresource)]  
[!code-xml[DataTemplatingIntro_snip#R2](../../../../samples/snippets/csharp/VS_Snippets_Wpf/DataTemplatingIntro_snip/CSharp/Window1.xaml#r2)]  
  
 现在，你可以使用`myTaskTemplate`作为资源，如以下示例所示︰  
  
 [!code-xml[DataTemplatingIntro_snip#MyTaskTemplate](../../../../samples/snippets/csharp/VS_Snippets_Wpf/DataTemplatingIntro_snip/CSharp/Window1.xaml#mytasktemplate)]  
  
 因为`myTaskTemplate`是资源，你现在可以在具有一个属性，它将其他控件上使用它<xref:System.Windows.DataTemplate>类型。 如上所示，为<xref:System.Windows.Controls.ItemsControl>对象，如<xref:System.Windows.Controls.ListBox>，它是<xref:System.Windows.Controls.ItemsControl.ItemTemplate%2A>属性。 有关<xref:System.Windows.Controls.ContentControl>对象，它是<xref:System.Windows.Controls.ContentControl.ContentTemplate%2A>属性。  
  
<a name="Styling_DataType"></a>   
### <a name="the-datatype-property"></a>数据类型属性  
 <xref:System.Windows.DataTemplate>类具有<xref:System.Windows.DataTemplate.DataType%2A>属性都非常类似于<xref:System.Windows.Style.TargetType%2A>属性<xref:System.Windows.Style>类。 因此，而不是指定`x:Key`为<xref:System.Windows.DataTemplate>在上述示例中，您可以执行以下︰  
  
 [!code-xml[DataTemplatingIntro_snip#DataType](../../../../samples/snippets/csharp/VS_Snippets_Wpf/DataTemplatingIntro_snip/CSharp/Window1.xaml#datatype)]  
  
 这<xref:System.Windows.DataTemplate>获取自动应用于所有`Task`对象。 请注意，在这种情况下`x:Key`隐式设置。 因此，如果将此分配<xref:System.Windows.DataTemplate> `x:Key`值，您要重写的隐式`x:Key`和<xref:System.Windows.DataTemplate>不会自动应用。  
  
 如果你正在绑定<xref:System.Windows.Controls.ContentControl>到的集合`Task`对象， <xref:System.Windows.Controls.ContentControl>不使用上述<xref:System.Windows.DataTemplate>自动。 这是因为上的绑定<xref:System.Windows.Controls.ContentControl>需要更多信息来区分是你想要将绑定到整个集合或单个对象。 如果您<xref:System.Windows.Controls.ContentControl>正在跟踪的所选内容<xref:System.Windows.Controls.ItemsControl>类型，您可以设置<xref:System.Windows.Data.Binding.Path%2A>属性<xref:System.Windows.Controls.ContentControl>绑定到"`/`"以指示您感兴趣的当前项。 有关示例，请参阅[绑定到集合并显示基于所选内容的信息](../../../../docs/framework/wpf/data/how-to-bind-to-a-collection-and-display-information-based-on-selection.md)。 否则，您需要指定<xref:System.Windows.DataTemplate>显式通过设置<xref:System.Windows.Controls.ContentControl.ContentTemplate%2A>属性。  
  
 <xref:System.Windows.DataTemplate.DataType%2A>属性是特别有用，当您有<xref:System.Windows.Data.CompositeCollection>不同类型的数据对象。 有关示例，请参阅[实现 CompositeCollection](../../../../docs/framework/wpf/data/how-to-implement-a-compositecollection.md)。  
  
<a name="adding_more_to_datatemplate"></a>   
## <a name="adding-more-to-the-datatemplate"></a>添加更多到 DataTemplate  
 当前，数据显示必要的信息，但绝对改进之处。 让我们通过添加改善的表现<xref:System.Windows.Controls.Border>、<xref:System.Windows.Controls.Grid>，和一些<xref:System.Windows.Controls.TextBlock>描述所显示的数据的元素。  
  
 [!code-xml[DataTemplatingIntro#AddingMore](../../../../samples/snippets/xaml/VS_Snippets_Wpf/DataTemplatingIntro/xaml/window1.xaml#addingmore)]  
[!code-xml[DataTemplatingIntro#AddingMore2](../../../../samples/snippets/xaml/VS_Snippets_Wpf/DataTemplatingIntro/xaml/window1.xaml#addingmore2)]  
  
 以下屏幕快照显示<xref:System.Windows.Controls.ListBox>与此修改<xref:System.Windows.DataTemplate>:  
  
 ![数据模板示例屏幕快照](../../../../docs/framework/wpf/data/media/datatemplatingintro-fig4.png "DataTemplatingIntro_fig4")  
  
 我们可以设置<xref:System.Windows.Controls.Control.HorizontalContentAlignment%2A>到<xref:System.Windows.HorizontalAlignment>上<xref:System.Windows.Controls.ListBox>以确保项的宽度占用的整个空间︰  
  
 [!code-xml[DataTemplatingIntro_snip#Stretch](../../../../samples/snippets/csharp/VS_Snippets_Wpf/DataTemplatingIntro_snip/CSharp/Window1.xaml#stretch)]  
  
 与<xref:System.Windows.Controls.Control.HorizontalContentAlignment%2A>属性设置为<xref:System.Windows.HorizontalAlignment>、 <xref:System.Windows.Controls.ListBox>现在如下所示︰  
  
 ![数据模板示例屏幕快照](../../../../docs/framework/wpf/data/media/datatemplatingintro-fig5.png "DataTemplatingIntro_fig5")  
  
<a name="DataTrigger_to_Apply_Property_Values"></a>   
### <a name="use-datatriggers-to-apply-property-values"></a>使用数据触发器应用属性值  
 当前的演示文稿不会告诉我们是否`Task`是家庭任务还是 office 任务。 请记住，`Task`对象具有`TaskType`类型的属性`TaskType`，这是一个包含值的枚举`Home`和`Work`。  
  
 在下面的示例中， <xref:System.Windows.DataTrigger>设置<xref:System.Windows.Controls.Border.BorderBrush%2A>所指定元素的`border`到`Yellow`如果`TaskType`属性是`TaskType.Home`。  
  
 [!code-xml[DataTemplatingIntro#DT](../../../../samples/snippets/xaml/VS_Snippets_Wpf/DataTemplatingIntro/xaml/window1.xaml#dt)]  
[!code-xml[DataTemplatingIntro#DataTrigger](../../../../samples/snippets/xaml/VS_Snippets_Wpf/DataTemplatingIntro/xaml/window1.xaml#datatrigger)]  
[!code-xml[DataTemplatingIntro#AddingMore2](../../../../samples/snippets/xaml/VS_Snippets_Wpf/DataTemplatingIntro/xaml/window1.xaml#addingmore2)]  
  
 应用程序现在如下所示。 有一个黄色边框不会显示主任务并具有浅绿色边框不会显示 office 任务︰  
  
 ![数据模板示例屏幕快照](../../../../docs/framework/wpf/data/media/datatemplatingintro-fig6.png "DataTemplatingIntro_fig6")  
  
 在此示例中<xref:System.Windows.DataTrigger>使用<xref:System.Windows.Setter>用于设置属性值。 此触发器类还提供<xref:System.Windows.TriggerBase.EnterActions%2A>和<xref:System.Windows.TriggerBase.ExitActions%2A> ，你可以启动一组操作，例如动画的属性。 此外，还有<xref:System.Windows.MultiDataTrigger>类，它允许您将更改应用基于多个数据绑定属性值。  
  
 一种方法来获得同样的效果是将绑定<xref:System.Windows.Controls.Border.BorderBrush%2A>属性设置为`TaskType`属性和值转换器来返回颜色基于的使用`TaskType`值。 创建使用转换器上述效果可从性能方面稍有提高效率。 此外，创建您自己的转换器，可以更大的灵活性因为您提供您自己的逻辑。 从根本上讲，您选择的技术取决于你的方案和您的首选项。 有关如何编写转换器的信息，请参阅<xref:System.Windows.Data.IValueConverter>。  
  
<a name="what_belongs_in_datatemplate"></a>   
### <a name="what-belongs-in-a-datatemplate"></a>哪些内容属于一个在 DataTemplate 中？  
 在上例中，我们放置在触发器<xref:System.Windows.DataTemplate>使用<xref:System.Windows.DataTemplate>。<xref:System.Windows.DataTemplate.Triggers%2A>属性。 <xref:System.Windows.Setter>的触发器设置元素的属性的值 (<xref:System.Windows.Controls.Border>元素) 中<xref:System.Windows.DataTemplate>。 但是，如果属性，您`Setters`关心也不是在当前的元素的属性<xref:System.Windows.DataTemplate>，它可能更适合于要设置属性使用<xref:System.Windows.Style>对于就是<xref:System.Windows.Controls.ListBoxItem>类 (要绑定的控件是否<xref:System.Windows.Controls.ListBox>)。 例如，如果您希望您<xref:System.Windows.Trigger>进行动画处理<xref:System.Windows.UIElement.Opacity%2A>值的项时鼠标指向某一项，定义了触发器内的<xref:System.Windows.Controls.ListBoxItem>样式。 有关示例，请参阅[样式和模板化示例简介](http://go.microsoft.com/fwlink/?LinkID=160010)。  
  
 一般情况下，请记住， <xref:System.Windows.DataTemplate>会应用于每个生成<xref:System.Windows.Controls.ListBoxItem> (有关如何以及在何处实际应用的详细信息，请参阅<xref:System.Windows.Controls.ItemsControl.ItemTemplate%2A>页。)。 您<xref:System.Windows.DataTemplate>是关注的演示文稿和数据对象的外观。 在大多数情况下，所有其他方面的演示文稿，例如，项看起来像当选中时或如何<xref:System.Windows.Controls.ListBox>排列项，不属于的定义中的<xref:System.Windows.DataTemplate>。 有关示例，请参阅[样式和模板化 ItemsControl](#DataTemplating_ItemsControl)部分。  
  
<a name="Styling_StyleSelection"></a>   
## <a name="choosing-a-datatemplate-based-on-properties-of-the-data-object"></a>选择数据对象的属性所基于的 DataTemplate  
 在[DataType 属性](#Styling_DataType)部分中，我们将讨论您可以定义不同的数据对象的不同的数据模板。 这一点非常有用的如果您具有<xref:System.Windows.Data.CompositeCollection>的不同类型或具有不同类型的项的集合。 在[来应用属性值使用 Datatrigger](#DataTrigger_to_Apply_Property_Values)部分中，我们所介绍的是否有相同类型的数据对象的集合则可以创建<xref:System.Windows.DataTemplate> ，然后使用触发器应用基于每个数据对象的属性值的更改。 但是，触发器可用于将属性值应用或启动动画，但它们无法让您能够灵活地重新构造数据对象的结构。 某些情况下，可能需要创建其他<xref:System.Windows.DataTemplate>数据属于相同的对象类型，但具有不同的属性。  
  
 例如，当`Task`对象具有`Priority`值`1`，要为其提供完全不同的外观，用作您自己的警报。 在这种情况下，创建<xref:System.Windows.DataTemplate>高优先级的显示器`Task`对象。 让我们将以下代码添加<xref:System.Windows.DataTemplate>到资源部分︰  
  
 [!code-xml[DataTemplatingIntro_snip#ImportantTemplate](../../../../samples/snippets/csharp/VS_Snippets_Wpf/DataTemplatingIntro_snip/CSharp/Window1.xaml#importanttemplate)]  
  
 请注意，本示例使用<xref:System.Windows.DataTemplate>。<xref:System.Windows.FrameworkTemplate.Resources%2A>属性。 资源定义中共享该部分中的元素<xref:System.Windows.DataTemplate>。  
  
 若要提供逻辑来选择哪些<xref:System.Windows.DataTemplate>使用基于`Priority`值的数据对象中，创建一个子类<xref:System.Windows.Controls.DataTemplateSelector>并重写<xref:System.Windows.Controls.DataTemplateSelector.SelectTemplate%2A>方法。 在下面的示例中，<xref:System.Windows.Controls.DataTemplateSelector.SelectTemplate%2A>方法提供逻辑来返回适当的值所基于的模板`Priority`属性。 在封装的资源中找到要返回的模板<xref:System.Windows.Window>元素。  
  
 [!code-csharp[DataTemplatingIntro_snip#DTSClass](../../../../samples/snippets/csharp/VS_Snippets_Wpf/DataTemplatingIntro_snip/CSharp/TaskListDataTemplateSelector.cs#dtsclass)]
 [!code-vb[DataTemplatingIntro_snip#DTSClass](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/DataTemplatingIntro_snip/visualbasic/tasklistdatatemplateselector.vb#dtsclass)]  
  
 然后，我们可以声明`TaskListDataTemplateSelector`作为资源︰  
  
 [!code-xml[DataTemplatingIntro_snip#R1](../../../../samples/snippets/csharp/VS_Snippets_Wpf/DataTemplatingIntro_snip/CSharp/Window1.xaml#r1)]  
[!code-xml[DataTemplatingIntro_snip#DTS](../../../../samples/snippets/csharp/VS_Snippets_Wpf/DataTemplatingIntro_snip/CSharp/Window1.xaml#dts)]  
[!code-xml[DataTemplatingIntro_snip#R2](../../../../samples/snippets/csharp/VS_Snippets_Wpf/DataTemplatingIntro_snip/CSharp/Window1.xaml#r2)]  
  
 若要使用的模板选择器资源，将其分配给<xref:System.Windows.Controls.ItemsControl.ItemTemplateSelector%2A>属性<xref:System.Windows.Controls.ListBox>。 <xref:System.Windows.Controls.ListBox>调用<xref:System.Windows.Controls.DataTemplateSelector.SelectTemplate%2A>方法`TaskListDataTemplateSelector`为每个基础集合中的项。 调用将作为项参数传递的数据对象。 <xref:System.Windows.DataTemplate>返回该方法然后应用于该数据对象。  
  
 [!code-xml[DataTemplatingIntro_snip#ItemTemplateSelector](../../../../samples/snippets/csharp/VS_Snippets_Wpf/DataTemplatingIntro_snip/CSharp/Window1.xaml#itemtemplateselector)]  
  
 与模板选择器后， <xref:System.Windows.Controls.ListBox>现在显示，如下所示︰  
  
 ![数据模板示例屏幕快照](../../../../docs/framework/wpf/data/media/datatemplatingintro-fig7.png "DataTemplatingIntro_fig7")  
  
 到此为止，我们在此示例中的讨论。 有关完整的示例，请参阅[简介数据模板示例](http://go.microsoft.com/fwlink/?LinkID=160009)。  
  
<a name="DataTemplating_ItemsControl"></a>   
## <a name="styling-and-templating-an-itemscontrol"></a>样式和模板化 ItemsControl  
 即使<xref:System.Windows.Controls.ItemsControl>不是唯一可以使用的控件类型<xref:System.Windows.DataTemplate> ，它是非常常见的方案将绑定<xref:System.Windows.Controls.ItemsControl>到集合。 在[哪些内容属于 DataTemplate](#what_belongs_in_datatemplate)我们讨论了部分的定义您<xref:System.Windows.DataTemplate>只应关心数据的表示形式。 为了知道何时不适合用于<xref:System.Windows.DataTemplate>务必了解由提供的不同样式和模板属性<xref:System.Windows.Controls.ItemsControl>。 下面的示例旨在阐释了这两个属性的函数。 <xref:System.Windows.Controls.ItemsControl>在此示例中绑定到同一`Tasks`如前面的示例所示的集合。 有关演示用途、 样式和模板在此示例中均声明为内联。  
  
 [!code-xml[DataTemplatingIntro_snip#ItemsControlProperties](../../../../samples/snippets/csharp/VS_Snippets_Wpf/DataTemplatingIntro_snip/CSharp/Window1.xaml#itemscontrolproperties)]  
  
 下面是在呈现时的示例屏幕快照︰  
  
 ![ItemsControl 示例屏幕快照](../../../../docs/framework/wpf/data/media/databinding-itemscontrolproperties.png "DataBinding_ItemsControlProperties")  
  
 请注意，而不是使用<xref:System.Windows.Controls.ItemsControl.ItemTemplate%2A>，您可以使用<xref:System.Windows.Controls.ItemsControl.ItemTemplateSelector%2A>。 请参阅上一节的一个示例。 同样，而不是使用<xref:System.Windows.Controls.ItemsControl.ItemContainerStyle%2A>，您可以选择要使用<xref:System.Windows.Controls.ItemsControl.ItemContainerStyleSelector%2A>。  
  
 其他两个与样式有关的属性的<xref:System.Windows.Controls.ItemsControl> ，不会显示如下<xref:System.Windows.Controls.ItemsControl.GroupStyle%2A>和<xref:System.Windows.Controls.ItemsControl.GroupStyleSelector%2A>。  
  
<a name="DataTemplating_HeirarchicalDataTemplate"></a>   
## <a name="support-for-hierarchical-data"></a>对分层数据的支持  
 到目前为止，我们仅讨论了如何将绑定到显示单个集合。 有时，您必须包含其他集合的集合。 <xref:System.Windows.HierarchicalDataTemplate>类旨在用于<xref:System.Windows.Controls.HeaderedItemsControl>要显示此类数据的类型。 在下面的示例中，`ListLeagueList`是一份`League`对象。 每个`League`对象具有`Name`和一系列`Division`对象。 每个`Division`具有`Name`和一系列`Team`对象以及每个`Team`对象具有`Name`。  
  
 [!code-xml[HierarchicalDataTemplateSnippet#HDT](../../../../samples/snippets/csharp/VS_Snippets_Wpf/HierarchicalDataTemplateSnippet/CS/window1.xaml#hdt)]  
  
 该示例演示使用<xref:System.Windows.HierarchicalDataTemplate>，您可以轻松地显示包含其他列表的列表数据。 下面是该示例的屏幕快照。  
  
 ![HierarchicalDataTemplate 示例屏幕快照](../../../../docs/framework/wpf/data/media/databinding-hierarchicaldatatemplate.png "DataBinding_HierarchicalDataTemplate")  
  
## <a name="see-also"></a>另请参阅  
 [数据绑定](../../../../docs/framework/wpf/advanced/optimizing-performance-data-binding.md)   
 [查找由 DataTemplate 生成的元素](../../../../docs/framework/wpf/data/how-to-find-datatemplate-generated-elements.md)   
 [样式和模板化](../../../../docs/framework/wpf/controls/styling-and-templating.md)   
 [数据绑定概述](../../../../docs/framework/wpf/data/data-binding-overview.md)   
 [GridView 列标题的样式和模板概述](../../../../docs/framework/wpf/controls/gridview-column-header-styles-and-templates-overview.md)