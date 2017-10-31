---
title: "数据绑定概述 | Microsoft Docs"
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
  - "绑定数据, 关于数据绑定"
  - "针对数据绑定进行的转换"
  - "Data Binding — 数据绑定, 关于数据绑定"
  - "针对绑定进行的数据转换"
ms.assetid: c707c95f-7811-401d-956e-2fffd019a211
caps.latest.revision: 78
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 75
---
# 数据绑定概述
[!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)] 数据绑定为应用程序提供了一种简单而一致的方法来显示数据以及与数据交互。  元素能够以 [!INCLUDE[TLA#tla_clr](../../../../includes/tlasharptla-clr-md.md)] 对象和 [!INCLUDE[TLA#tla_xml](../../../../includes/tlasharptla-xml-md.md)] 形式绑定到来自各种数据源的数据。  <xref:System.Windows.Controls.ContentControl>（如 <xref:System.Windows.Controls.Button>）和 <xref:System.Windows.Controls.ItemsControl>（如 <xref:System.Windows.Controls.ListBox> 和 <xref:System.Windows.Controls.ListView>）具有内置功能，使单个数据项或数据项集合可以进行灵活的样式设置。  可以在数据之上生成排序、筛选和分组视图。  
  
 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 中的数据绑定功能与传统模型相比具有一些优势，包括本质上支持数据绑定的各种属性、灵活的数据 [!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)] 表示形式，以及业务逻辑与 [!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)] 的完全分离。  
  
 本主题首先讨论 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 数据绑定的基本概念，然后详细介绍 <xref:System.Windows.Data.Binding> 类以及数据绑定的其他功能的用法。  
  
   
  
<a name="what_is_data_binding"></a>   
## 什么是数据绑定？  
 数据绑定是在应用程序 [!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)] 与业务逻辑之间建立连接的过程。  如果绑定具有正确设置并且数据提供正确通知，则当数据更改其值时，绑定到数据的元素会自动反映更改。  数据绑定可能还意味着如果元素中数据的外部表现形式发生更改，则基础数据可以自动更新以反映更改。  例如，如果用户编辑 <xref:System.Windows.Controls.TextBox> 元素中的值，则基础数据值会自动更新以反映该更改。  
  
 数据绑定的一种典型用法是将服务器或本地配置数据放置到窗体或其他 [!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)] 控件中。  在 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 中，此概念得到扩展，包括了大量属性与各种数据源的绑定。  在 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 中，元素的[依赖项属性](GTMT)可以绑定到 [!INCLUDE[TLA2#tla_clr](../../../../includes/tla2sharptla-clr-md.md)] 对象（包括 [!INCLUDE[TLA#tla_adonet](../../../../includes/tlasharptla-adonet-md.md)] 对象或与 Web 服务和 Web 属性相关联的对象）和 [!INCLUDE[TLA2#tla_xml](../../../../includes/tla2sharptla-xml-md.md)] 数据。  
  
 有关数据绑定的示例，请参见来自 [Data Binding Demo](http://go.microsoft.com/fwlink/?LinkID=163703)（数据绑定演示）的以下应用程序 [!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)]：  
  
 ![数据绑定示例屏幕快照](../../../../docs/framework/wpf/data/media/databinding-databindingdemo.png "DataBinding\_DataBindingDemo")  
  
 上面是显示拍卖项列表的应用程序 [!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)]。  该应用程序演示数据绑定的以下功能：  
  
-   <xref:System.Windows.Controls.ListBox> 的内容绑定到 *AuctionItem* 对象的集合。  *AuctionItem* 对象具有一些属性，如 *Description*、*StartPrice*、*StartDate*、*Category*、*SpecialFeatures*。  
  
-   <xref:System.Windows.Controls.ListBox> 中显示的数据（*AuctionItem* 对象）进行模板化，以便显示每个拍卖项的说明和当前价格。  这是使用一个 <xref:System.Windows.DataTemplate> 实现的。  此外，每个项的外观取决于要显示的 *AuctionItem* 的 *SpecialFeatures* 值。  如果 *AuctionItem* 的 *SpecialFeatures* 值为 *Color*，则该项具有蓝色边框。  如果该值为 *Highlight*，则该项具有橙色边框和一个星号。  [数据模板化](#data_templating)一节提供了有关数据模板化的信息。  
  
-   用户可以使用提供的 <xref:System.Windows.Controls.CheckBox> 对数据进行分组、筛选或排序。  在上面的图像中，选中了“Group by category”（按类别分组）和“Sort by category and date”（按类别和日期排序）<xref:System.Windows.Controls.CheckBox>。  您可能已经注意到数据是根据产品类别分组的，而且类别名称按字母顺序排序。  这些项在每个类别中也是按照起始日期排序的，虽然从该图像中很难注意到这一点。  这是使用*集合视图* 实现的。  [绑定到集合](#binding_to_collections)一节讨论了集合视图。  
  
-   当用户选中一个项时，<xref:System.Windows.Controls.ContentControl> 会显示选定项的详细信息。  这称为*主从方案*。  [主从方案](#master_detail_scenario)一节提供了有关此类型的绑定方案的信息。  
  
-   *StartDate* 属性的类型为 <xref:System.DateTime>，该类型返回一个日期，包括精确到毫秒的时间。  在此应用程序中，使用了一个自定义转换器，以便显示较短的日期字符串。  [数据转换](#data_conversion)一节提供了有关转换器的信息。  
  
 当用户单击*“Add Product”（添加产品）*按钮时，会出现下面的窗体：  
  
 ![“添加产品清单”页](../../../../docs/framework/wpf/data/media/databinding-demo-addproductlisting.png "DataBinding\_Demo\_AddProductListing")  
  
 用户可以编辑窗体中的字段，使用简略预览和详细预览窗格来预览产品清单，然后单击*“submit”（提交）*以添加新的产品清单。  任何现有的分组、筛选和排序功能都会应用于新项。  在这种特殊情况下，在上面图像中输入的项会作为 *Computer* 类别中的第二项显示。  
  
 *“Start Date”（起始日期）* <xref:System.Windows.Controls.TextBox> 中提供的验证逻辑未在此图像中显示。  如果用户输入一个无效日期（无效的格式或过去的日期），则会通过一个 <xref:System.Windows.Controls.ToolTip> 和 <xref:System.Windows.Controls.TextBox> 旁的一个红色感叹号来通知用户。  [数据验证](#data_validation)一节讨论了如何创建验证逻辑。  
  
 在详细介绍数据绑定的上述不同功能之前，我们会先在下一节中讨论一些对理解 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 数据绑定非常重要的基本概念。  
  
<a name="basic_data_binding_concepts"></a>   
## 基本数据绑定概念  
   
  
 不论要绑定什么元素，不论数据源的特性是什么，每个绑定都始终遵循下图所示的模型：  
  
 ![基本数据绑定示意图](../../../../docs/framework/wpf/data/media/databindingmostbasic.png "DataBindingMostBasic")  
  
 如上图所示，数据绑定实质上是[绑定目标](GTMT)与[绑定源](GTMT)之间的桥梁。  该图演示以下基本的 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 数据绑定概念：  
  
-   通常，每个绑定都具有四个组件：[绑定目标](GTMT)对象、目标属性、[绑定源](GTMT)，以及要使用的[绑定源](GTMT)中的值的路径。  例如，如果要将 <xref:System.Windows.Controls.TextBox> 的内容绑定到 *Employee* 对象的 *Name* 属性，则目标对象是 <xref:System.Windows.Controls.TextBox>，目标属性是 <xref:System.Windows.Controls.TextBox.Text%2A> 属性，要使用的值是 *Name*，源对象是 *Employee* 对象。  
  
-   目标属性必须为[依赖项属性](GTMT)。  大多数 <xref:System.Windows.UIElement> 属性都是[依赖项属性](GTMT)，而大多数[依赖项属性](GTMT)（除了只读属性）默认情况下都支持数据绑定。  （只有 <xref:System.Windows.DependencyObject> 类型可以定义[依赖项属性](GTMT)，所有 <xref:System.Windows.UIElement> 都派生自 <xref:System.Windows.DependencyObject>。）  
  
-   尽管图中并未指出，但请注意，[绑定源](GTMT) 对象并不限于自定义 [!INCLUDE[TLA2#tla_clr](../../../../includes/tla2sharptla-clr-md.md)] 对象。  [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 数据绑定支持 [!INCLUDE[TLA2#tla_clr](../../../../includes/tla2sharptla-clr-md.md)] 对象和 [!INCLUDE[TLA2#tla_xml](../../../../includes/tla2sharptla-xml-md.md)] 形式的数据。  举例来说，绑定源可以是 <xref:System.Windows.UIElement>、任何列表对象、与 [!INCLUDE[TLA#tla_adonet](../../../../includes/tlasharptla-adonet-md.md)] 数据或 Web 服务关联的 [!INCLUDE[TLA2#tla_clr](../../../../includes/tla2sharptla-clr-md.md)] 对象，也可以是包含 [!INCLUDE[TLA2#tla_xml](../../../../includes/tla2sharptla-xml-md.md)] 数据的 XmlNode。  有关更多信息，请参见[绑定源概述](../../../../docs/framework/wpf/data/binding-sources-overview.md)。  
  
 在阅读其他[!INCLUDE[TLA#tla_sdk](../../../../includes/tlasharptla-sdk-md.md)] 主题时，请务必记住一点：当您建立绑定时，您是将[绑定目标](GTMT)绑定*到* [绑定源](GTMT)。  例如，如果您要使用数据绑定在一个 <xref:System.Windows.Controls.ListBox> 中显示一些基础 [!INCLUDE[TLA2#tla_xml](../../../../includes/tla2sharptla-xml-md.md)] 数据，就是将 <xref:System.Windows.Controls.ListBox> 绑定到 [!INCLUDE[TLA2#tla_xml](../../../../includes/tla2sharptla-xml-md.md)] 数据。  
  
 若要建立绑定，请使用 <xref:System.Windows.Data.Binding> 对象。  本主题的剩余部分会讨论与 <xref:System.Windows.Data.Binding> 对象相关的许多概念以及该对象的一些属性和用法。  
  
<a name="direction_of_data_flow"></a>   
### 数据流的方向  
 正如上文所述和上图中箭头所示，绑定的数据流可以从[数据目标](GTMT)流向[数据源](GTMT)（例如，当用户编辑 <xref:System.Windows.Controls.TextBox> 的值时，源值会发生更改）和\/或（如果绑定源提供正确的通知）从[绑定源](GTMT)流向[绑定目标](GTMT)（例如，<xref:System.Windows.Controls.TextBox> 内容会随[绑定源](GTMT)中的更改而进行更新）。  
  
 您可能希望应用程序使用户可以更改数据并将数据传播回源对象。  或者，您可能不希望允许用户更新源数据。  您可以通过设置 <xref:System.Windows.Data.Binding> 对象的 <xref:System.Windows.Data.Binding.Mode%2A> 属性来对此进行控制。  下图演示不同类型的数据流：  
  
 ![数据绑定数据流](../../../../docs/framework/wpf/data/media/databinding-dataflow.png "DataBinding\_DataFlow")  
  
-   <xref:System.Windows.Data.BindingMode> 绑定导致对源属性的更改会自动更新目标属性，但是对目标属性的更改不会传播回源属性。  此绑定类型适用于绑定的控件为隐式只读控件的情况。  例如，您可能绑定到如股票行情自动收录器这样的源，或许目标属性没有用于进行更改的控件接口（如表的数据绑定背景色）。  如果无需监视目标属性的更改，则使用 <xref:System.Windows.Data.BindingMode> 绑定模式可避免 <xref:System.Windows.Data.BindingMode> 绑定模式的系统开销。  
  
-   <xref:System.Windows.Data.BindingMode> 绑定导致对源属性的更改会自动更新目标属性，而对目标属性的更改也会自动更新源属性。  此绑定类型适用于可编辑窗体或其他完全交互式 [!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)] 方案。  大多数属性都默认为 <xref:System.Windows.Data.BindingMode> 绑定，但是一些[依赖项属性](GTMT)（通常为用户可编辑的控件的属性，如 <xref:System.Windows.Controls.TextBox> 的 <xref:System.Windows.Controls.TextBox.Text%2A> 属性和 <xref:System.Windows.Controls.CheckBox> 的 <xref:System.Windows.Controls.Primitives.ToggleButton.IsChecked%2A> 属性）默认为 <xref:System.Windows.Data.BindingMode> 绑定。  确定[依赖项属性](GTMT)绑定在默认情况下是单向还是双向的编程方法是：使用 <xref:System.Windows.DependencyProperty.GetMetadata%2A> 获取属性的属性元数据，然后检查 <xref:System.Windows.FrameworkPropertyMetadata.BindsTwoWayByDefault%2A> 属性的布尔值。  
  
-   <xref:System.Windows.Data.BindingMode> 与 <xref:System.Windows.Data.BindingMode> 绑定相反；它在目标属性更改时更新源属性。  一个示例方案是您只需要从 [!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)] 重新计算源值的情况。  
  
-   <xref:System.Windows.Data.BindingMode> 绑定未在图中显示，该绑定会导致源属性初始化目标属性，但不传播后续更改。  这意味着，如果数据上下文发生了更改，或者数据上下文中的对象发生了更改，则更改不会反映在目标属性中。  此绑定类型适用于以下情况：使用当前状态的快照适合使用的或数据状态实际为静态的数据。  如果要从源属性初始化具有某个值的目标属性，并且事先不知道数据上下文，则也可以使用此绑定类型。  此绑定类型实质上是 <xref:System.Windows.Data.BindingMode> 绑定的简化形式，在源值不更改的情况下可以提供更好的性能。  
  
 请注意，若要检测源更改（适用于 <xref:System.Windows.Data.BindingMode> 和 <xref:System.Windows.Data.BindingMode> 绑定），则源必须实现一种合适的属性更改通知机制（如 <xref:System.ComponentModel.INotifyPropertyChanged>）。  有关 <xref:System.ComponentModel.INotifyPropertyChanged> 实现的示例，请参见[实现属性更改通知](../../../../docs/framework/wpf/data/how-to-implement-property-change-notification.md)。  
  
 <xref:System.Windows.Data.Binding.Mode%2A> 属性页提供有关绑定模式的更多信息，以及一个如何指定绑定方向的示例。  
  
<a name="what_triggers_source_updates"></a>   
### 触发源更新的原因  
 <xref:System.Windows.Data.BindingMode> 或 <xref:System.Windows.Data.BindingMode> 绑定侦听目标属性的更改，并将这些更改传播回源。  这称为更新源。  例如，可以编辑文本框中的文本以更改基础源值。  如上一节中所述，数据流的方向由绑定的 <xref:System.Windows.Data.Binding.Mode%2A> 属性的值确定。  
  
 但是，源值是在您编辑文本的同时进行更新，还是在您结束编辑文本并将鼠标指针从文本框移走后才进行更新呢？  绑定的 <xref:System.Windows.Data.Binding.UpdateSourceTrigger%2A> 属性确定触发源更新的原因。  下图中右箭头的点演示 <xref:System.Windows.Data.Binding.UpdateSourceTrigger%2A> 属性的角色：  
  
 ![UpdateSourceTrigger 示意图](../../../../docs/framework/wpf/data/media/databindingupdatesourcetrigger.png "DataBindingUpdateSourceTrigger")  
  
 如果 <xref:System.Windows.Data.Binding.UpdateSourceTrigger%2A> 值为 <xref:System.Windows.Data.UpdateSourceTrigger>，则 <xref:System.Windows.Data.BindingMode> 或 <xref:System.Windows.Data.BindingMode> 绑定的右箭头指向的值会在目标属性更改时立刻进行更新。  但是，如果 <xref:System.Windows.Data.Binding.UpdateSourceTrigger%2A> 值为 <xref:System.Windows.Data.UpdateSourceTrigger>，则仅当目标属性失去焦点时，该值才会使用新值进行更新。  
  
 与 <xref:System.Windows.Data.Binding.Mode%2A> 属性类似，不同的[依赖项属性](GTMT)具有不同的默认 <xref:System.Windows.Data.Binding.UpdateSourceTrigger%2A> 值。  大多数[依赖项属性](GTMT)的默认值都为 <xref:System.Windows.Data.UpdateSourceTrigger>，而 <xref:System.Windows.Controls.TextBox.Text%2A> 属性的默认值为 <xref:System.Windows.Data.UpdateSourceTrigger>。  这意味着，只要目标属性更改，源更新通常都会发生，这对于 <xref:System.Windows.Controls.CheckBox> 和其他简单控件很有用。  但对于文本字段，每次键击之后都进行更新会降低性能，用户也没有机会在提交新值之前使用退格键修改键入错误。  这就是为什么 <xref:System.Windows.Controls.TextBox.Text%2A> 属性的默认值是 <xref:System.Windows.Data.UpdateSourceTrigger> 而不是 <xref:System.Windows.Data.UpdateSourceTrigger> 的原因。  
  
 有关如何查找[依赖项属性](GTMT)的默认 <xref:System.Windows.Data.Binding.UpdateSourceTrigger%2A> 值的信息，请参见 <xref:System.Windows.Data.Binding.UpdateSourceTrigger%2A> 属性页。  
  
 下表使用 <xref:System.Windows.Controls.TextBox> 作为示例提供每个 <xref:System.Windows.Data.Binding.UpdateSourceTrigger%2A> 值的示例方案：  
  
|UpdateSourceTrigger 值|源值何时进行更新|文本框的示例方案|  
|---------------------------|--------------|--------------|  
|LostFocus（<xref:System.Windows.Controls.TextBox.Text%2A?displayProperty=fullName> 的默认值）|当 TextBox 控件失去焦点时|一个与验证逻辑（请参见“验证逻辑”一节）关联的 <xref:System.Windows.Controls.TextBox>|  
|PropertyChanged|当键入到 <xref:System.Windows.Controls.TextBox> 中时|聊天室窗口中的 <xref:System.Windows.Controls.TextBox> 控件|  
|Explicit|当应用程序调用 <xref:System.Windows.Data.BindingExpression.UpdateSource%2A> 时|可编辑窗体中的 <xref:System.Windows.Controls.TextBox> 控件（仅当用户单击提交按钮时才更新源值）|  
  
 有关示例，请参见[控制文本框文本更新源的时间](../../../../docs/framework/wpf/data/how-to-control-when-the-textbox-text-updates-the-source.md)。  
  
<a name="creating_a_binding"></a>   
## 创建绑定  
   
  
 前面几节中讨论的一些概念可以概括为：使用 <xref:System.Windows.Data.Binding> 对象建立绑定，每个绑定通常都具有四个组件：绑定目标、目标属性、绑定源、要使用的源值的路径。  本节讨论如何设置绑定。  
  
 请看下面的示例，其中的绑定源对象是一个名为 *MyData* 的类，该类在 *SDKSample* 命名空间中定义。  出于演示的目的，*MyData* 类具有一个名为 *ColorName* 的字符串属性，该属性的值设置为“Red”。  因此，此示例生成一个具有红色背景的按钮。  
  
 [!code-xml[BindNonTextProperty#1](../../../../samples/snippets/csharp/VS_Snippets_Wpf/BindNonTextProperty/CS/Page1.xaml#1)]  
  
 有关绑定声明语法的详尽信息以及如何在代码中设置绑定的示例，请参见[绑定声明概述](../../../../docs/framework/wpf/data/binding-declarations-overview.md)。  
  
 如果将此示例应用于基本关系图，则生成的图如下所示。  这是一个 <xref:System.Windows.Data.BindingMode> 绑定，因为 Background 属性在默认情况下支持 <xref:System.Windows.Data.BindingMode> 绑定。  
  
 ![数据绑定示意图](../../../../docs/framework/wpf/data/media/databindingbuttonbackgroundexample.png "DataBindingButtonBackgroundExample")  
  
 您可能会奇怪为什么会这样，即使 *ColorName* 属性为类型字符串，而 <xref:System.Windows.Controls.Control.Background%2A> 属性为 <xref:System.Windows.Media.Brush> 类型。  这是由于进行了默认类型转换，此类型转换在[数据转换](#data_conversion)一节中进行了讨论。  
  
<a name="specifying_the_binding_source"></a>   
### 指定绑定源  
 请注意，在上一个示例中，绑定源是通过设置 <xref:System.Windows.Controls.DockPanel> 元素上的 <xref:System.Windows.FrameworkElement.DataContext%2A> 属性来指定的。  <xref:System.Windows.Controls.Button> 随后从 <xref:System.Windows.Controls.DockPanel>（这是其父元素）继承 <xref:System.Windows.FrameworkElement.DataContext%2A> 值。  在这里重复一下，绑定源对象是绑定的四个必需组件之一。  因此，如果未指定绑定源对象，则绑定将没有任何作用。  
  
 可通过多种方法指定绑定源对象。  在将多个属性绑定到相同源时，可以使用父元素上的 <xref:System.Windows.FrameworkElement.DataContext%2A> 属性。  但是，在各个绑定声明上指定绑定源有时可能更为合适。  对于上一个示例，可以不使用 <xref:System.Windows.FrameworkElement.DataContext%2A> 属性，而是通过在按钮的绑定声明上直接设置 <xref:System.Windows.Data.Binding.Source%2A> 属性来指定绑定源，如下面的示例中所示：  
  
 [!code-xml[BindNonTextProperty#BackgroundBindingCompact](../../../../samples/snippets/csharp/VS_Snippets_Wpf/BindNonTextProperty/CS/Page2.xaml#backgroundbindingcompact)]  
  
 除了在元素上直接设置 <xref:System.Windows.FrameworkElement.DataContext%2A> 属性、从上级继承 <xref:System.Windows.FrameworkElement.DataContext%2A> 值（如第一个示例中的按钮）、通过设置 <xref:System.Windows.Data.Binding> 上的 <xref:System.Windows.Data.Binding.Source%2A> 属性来显式指定绑定源（如最后一个示例中的按钮），还可以使用 <xref:System.Windows.Data.Binding.ElementName%2A> 属性或 <xref:System.Windows.Data.Binding.RelativeSource%2A> 属性指定绑定源。  当绑定到应用程序中的其他元素时（例如在使用滑块调整按钮的宽度时），<xref:System.Windows.Data.Binding.ElementName%2A> 属性是很有用的。  当在 <xref:System.Windows.Controls.ControlTemplate> 或 <xref:System.Windows.Style> 中指定绑定时，<xref:System.Windows.Data.Binding.RelativeSource%2A> 属性是很有用的。  有关更多信息，请参见[指定绑定源](../../../../docs/framework/wpf/data/how-to-specify-the-binding-source.md)。  
  
<a name="specifying_the_path_to_the_value"></a>   
### 指定值的路径  
 如果绑定源是一个对象，则可使用 <xref:System.Windows.Data.Binding.Path%2A> 属性指定要用于绑定的值。  如果要绑定到 [!INCLUDE[TLA2#tla_xml](../../../../includes/tla2sharptla-xml-md.md)] 数据，则可使用 <xref:System.Windows.Data.Binding.XPath%2A> 属性指定该值。  在某些情况下，可以使用 <xref:System.Windows.Data.Binding.Path%2A> 属性，即使在数据为 [!INCLUDE[TLA2#tla_xml](../../../../includes/tla2sharptla-xml-md.md)] 时。  例如，如果要访问返回的 XmlNode（作为 XPath 查询的结果）的 Name 属性，则应使用 <xref:System.Windows.Data.Binding.Path%2A> 属性和 <xref:System.Windows.Data.Binding.XPath%2A> 属性。  
  
 有关语法信息和示例，请参见 <xref:System.Windows.Data.Binding.Path%2A> 和 <xref:System.Windows.Data.Binding.XPath%2A> 属性页。  
  
 请注意，虽然我们已强调要使用的值的 <xref:System.Windows.Data.Binding.Path%2A> 是绑定的四个必需组件之一，但在要绑定到整个对象的情况下，要使用的值会与[绑定源](GTMT)对象相同。  在这些情况下，不指定 <xref:System.Windows.Data.Binding.Path%2A> 比较合适。  请看下面的示例：  
  
 [!code-xml[MasterDetail#EmptyBinding](../../../../samples/snippets/csharp/VS_Snippets_Wpf/MasterDetail/CSharp/Page1.xaml#emptybinding)]  
  
 上面的示例使用空绑定语法：{Binding}。  在此情况下，<xref:System.Windows.Controls.ListBox> 从父 DockPanel 元素继承 DataContext（此示例中未演示）。  当未指定路径时，默认为绑定到整个对象。  换句话说，在此示例中路径已被省略，因为要将 <xref:System.Windows.Controls.ItemsControl.ItemsSource%2A> 属性绑定到整个对象。  （有关深入讨论，请参见[绑定到集合](#binding_to_collections)一节。）  
  
 除了绑定到集合以外，在希望绑定到整个对象，而不是仅绑定到对象的单个属性时，也可以使用此方案。  例如，在源对象为类型字符串，并且您仅仅希望绑定到该字符串本身时。  另一种常见情况是您希望将一个元素绑定到具有多个属性的一个对象。  
  
 请注意，您可能需要应用自定义逻辑，使数据对您的绑定目标属性有意义。  自定义逻辑的形式可以是自定义转换器（如果默认类型转换不存在）。  有关转换器的信息，请参见[数据转换](#data_conversion)。  
  
<a name="binding_bindingexpression"></a>   
### Binding 和 BindingExpression  
 在详细介绍数据绑定的其他功能和用法之前，介绍 <xref:System.Windows.Data.BindingExpression> 类会十分有用。  如前面几节所述，<xref:System.Windows.Data.Binding> 类是用于绑定声明的高级别类；<xref:System.Windows.Data.Binding> 类提供了很多属性，您可以利用这些类来指定绑定的特征。  相关类 <xref:System.Windows.Data.BindingExpression> 是维持源与目标之间的连接的基础对象。  一个绑定包含可以在多个绑定表达式之间共享的所有信息。  <xref:System.Windows.Data.BindingExpression> 是无法共享的实例表达式，其中包含有关 <xref:System.Windows.Data.Binding> 的所有实例信息。  
  
 例如，请看下面的示例，其中 *myDataObject* 是 *MyData* 类的实例，*myBinding* 是源 <xref:System.Windows.Data.Binding> 对象，*MyData* 类是包含一个名为 *MyDataProperty* 的字符串属性的已定义类。  此示例将 *mytext*（<xref:System.Windows.Controls.TextBlock> 的实例）的文本内容绑定到 *MyDataProperty*。  
  
 [!code-csharp[CodeOnlyBinding#1](../../../../samples/snippets/csharp/VS_Snippets_Wpf/CodeOnlyBinding/CSharp/binding.cs#1)]
 [!code-vb[CodeOnlyBinding#1](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/CodeOnlyBinding/VisualBasic/App.vb#1)]  
  
 您可以使用相同的 *myBinding* 对象来创建其他绑定。  例如，可以使用 *myBinding* 对象将复选框的文本内容绑定到 *MyDataProperty*。  在这种情况下，将有两个 <xref:System.Windows.Data.BindingExpression> 实例共享 *myBinding* 对象。  
  
 可以通过对数据绑定对象调用 <xref:System.Windows.Data.BindingOperations.GetBindingExpression%2A> 的返回值来获取 <xref:System.Windows.Data.BindingExpression> 对象。  以下主题演示 <xref:System.Windows.Data.BindingExpression> 类的一些用法：  
  
-   [从已绑定的目标属性获取绑定对象](../../../../docs/framework/wpf/data/how-to-get-the-binding-object-from-a-bound-target-property.md)  
  
-   [控制文本框文本更新源的时间](../../../../docs/framework/wpf/data/how-to-control-when-the-textbox-text-updates-the-source.md)  
  
<a name="data_conversion"></a>   
## 数据转换  
 在上面的示例中，按钮是红色的，因为其 <xref:System.Windows.Controls.Control.Background%2A> 属性绑定到一个值为“Red”的字符串属性。  可以这样做的原因是 <xref:System.Windows.Media.Brush> 类型上提供了一个类型转换器，可以将字符串值转换为 <xref:System.Windows.Media.Brush>。  
  
 要将此信息添加到[创建绑定](#creating_a_binding)一节的图中，关系图如下所示：  
  
 ![数据绑定示意图](../../../../docs/framework/wpf/data/media/databindingbuttondefaultconversion.png "DataBindingButtonDefaultConversion")  
  
 但是，如果绑定源对象不是具有类型字符串的属性，而是具有类型 <xref:System.Windows.Media.Color> 的 *Color* 属性，该怎么办？  在这种情况下，为了使绑定正常工作，您需要先将 *Color* 属性值转换为 <xref:System.Windows.Controls.Control.Background%2A> 属性所接受的值。  您需要通过实现 <xref:System.Windows.Data.IValueConverter> 接口来创建一个自定义转换器，如下面的示例中所示：  
  
 [!code-csharp[ColorPicker_snip#16](../../../../samples/snippets/csharp/VS_Snippets_Wpf/ColorPicker_snip/CSharp/ColorPickerLib/ColorPicker.cs#16)]
 [!code-vb[ColorPicker_snip#16](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/ColorPicker_snip/visualbasic/colorpickerlib/colorpicker.vb#16)]  
  
 <xref:System.Windows.Data.IValueConverter> 参考页提供了更多信息。  
  
 现在使用自定义转换器而不是默认转换，关系图如下所示：  
  
 ![数据绑定示意图](../../../../docs/framework/wpf/data/media/databindingconvertercolorexample.png "DataBindingConverterColorExample")  
  
 在这里重复一下，由于要绑定到的类型中提供了类型转换器，因而可以使用默认转换。  此行为取决于目标中可用的类型转换器。  如果无法确定，请创建您自己的转换器。  
  
 下面提供了一些典型方案，在这些方案中，实现数据转换器是非常有意义的：  
  
-   数据应根据区域性以不同方式显示。  例如，可能需要根据在特定区域性中使用的值或标准，来实现货币转换器或日历日期\/时间转换器。  
  
-   使用的数据不一定会更改属性的文本值，但会更改其他某个值（如图像的源，或显示文本的颜色或样式）。  在这种情况下，可以通过转换可能不合适的属性绑定（如将文本字段绑定到表单元格的 Background 属性）来使用转换器。  
  
-   将多个控件或控件的多个属性绑定到相同数据。  在这种情况下，主绑定可能仅显示文本，而其他绑定则处理特定的显示问题，但仍使用同一绑定作为源信息。  
  
-   到目前为止，我们尚未讨论 <xref:System.Windows.Data.MultiBinding>（其目标属性具有绑定集合）。  对于 <xref:System.Windows.Data.MultiBinding>，可以使用自定义 <xref:System.Windows.Data.IMultiValueConverter> 从绑定的值生成最终值。  例如，可以从红色、蓝色和绿色的值来计算颜色，这些值可以是来自于相同或不同绑定源对象的值。  有关示例和信息，请参见 <xref:System.Windows.Data.MultiBinding> 类页。  
  
<a name="binding_to_collections"></a>   
## 绑定到集合  
   
  
 绑定源对象可以视为其属性包含数据的单个对象，也可以视为通常组合在一起的多态对象的数据集合（如查询数据库的结果）。  到目前为止，我们仅讨论了绑定到单个对象，但是绑定到数据集合是一个常见方案。  例如，一个常见方案是使用 <xref:System.Windows.Controls.ItemsControl>（如 <xref:System.Windows.Controls.ListBox>、<xref:System.Windows.Controls.ListView> 或 <xref:System.Windows.Controls.TreeView>）来显示数据集合，如[什么是数据绑定？](#what_is_data_binding)一节中的应用程序。  
  
 幸运的是，基本关系图仍然适用。  如果要将 <xref:System.Windows.Controls.ItemsControl> 绑定到集合，则关系图如下所示：  
  
 ![数据绑定 ItemsControl 示意图](../../../../docs/framework/wpf/data/media/databindingitemscontrol.png "DataBindingItemsControl")  
  
 正如此图中所示，若要将 <xref:System.Windows.Controls.ItemsControl> 绑定到集合对象，应使用 <xref:System.Windows.Controls.ItemsControl.ItemsSource%2A> 属性。  可以将 <xref:System.Windows.Controls.ItemsControl.ItemsSource%2A> 属性视为 <xref:System.Windows.Controls.ItemsControl> 的内容。  请注意，绑定是 <xref:System.Windows.Data.BindingMode>，因为 <xref:System.Windows.Controls.ItemsControl.ItemsSource%2A> 属性默认情况下支持 <xref:System.Windows.Data.BindingMode> 绑定。  
  
<a name="how_to_implement_collections"></a>   
### 如何实现集合  
 可以枚举实现 <xref:System.Collections.IEnumerable> 接口的任何集合。  但是，若要设置动态绑定，以便集合中的插入或删除操作可以自动更新 [!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)]，则该集合必须实现 <xref:System.Collections.Specialized.INotifyCollectionChanged> 接口。  此接口公开一个事件，只要基础集合发生更改，都应该引发该事件。  
  
 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 提供 <xref:System.Collections.ObjectModel.ObservableCollection%601> 类，它是公开 <xref:System.Collections.Specialized.INotifyCollectionChanged> 接口的数据集合的内置实现。  请注意，为了完全支持将数据值从源对象传送到目标，支持可绑定属性的集合中的每个对象还必须实现 <xref:System.ComponentModel.INotifyPropertyChanged> 接口。  有关更多信息，请参见[绑定源概述](../../../../docs/framework/wpf/data/binding-sources-overview.md)。  
  
 在实现自己的集合之前，请先考虑使用 <xref:System.Collections.ObjectModel.ObservableCollection%601> 或一个现有的集合类，如 <xref:System.Collections.Generic.List%601>、<xref:System.Collections.ObjectModel.Collection%601> 和 <xref:System.ComponentModel.BindingList%601> 等。  如果您有高级方案并且希望实现自己的集合，请考虑使用 <xref:System.Collections.IList>，它提供可以按索引逐个访问的对象的非泛型集合，因而可提供最佳性能。  
  
<a name="collection_views"></a>   
### 集合视图  
 一旦 <xref:System.Windows.Controls.ItemsControl> 绑定到数据集合，您可能希望对数据进行排序、筛选或分组。  若要执行此操作，可以使用集合视图，这是实现 <xref:System.ComponentModel.ICollectionView> 接口的类。  
  
   
  
<a name="what_are_collection_views"></a>   
#### 什么是集合视图？  
 集合视图是位于绑定源集合顶部的一层，您可以通过它使用排序、筛选和分组查询来导航和显示源集合，而无需更改基础源集合本身。  集合视图还维护着一个指向集合中的当前项的指针。  如果源集合实现了 <xref:System.Collections.Specialized.INotifyCollectionChanged> 接口，则 <xref:System.Collections.Specialized.INotifyCollectionChanged.CollectionChanged> 事件引发的更改将传播到视图。  
  
 由于视图不会更改基础源集合，因此每个源集合可以有多个关联的视图。  例如，您可以有 *Task* 对象的集合。  通过使用视图，可以通过多种不同的方式来显示相同数据。  例如，您可能希望在页面左侧显示按优先级排序的任务，而在页面右侧显示按区域分组的任务。  
  
<a name="how_to_create_a_view"></a>   
#### 如何创建视图  
 创建和使用视图的一种方式是直接实例化视图对象并将其用作绑定源。  例如，请考虑在[什么是数据绑定？](#what_is_data_binding)一节中显示的 [Data Binding Demo](http://go.microsoft.com/fwlink/?LinkID=163703)（数据绑定演示）应用程序。  该应用程序的实现方式是将 <xref:System.Windows.Controls.ListBox> 绑定到数据集合上的视图，而不是直接绑定到数据集合。  下面的示例摘自 [Data Binding Demo](http://go.microsoft.com/fwlink/?LinkID=163703)（数据绑定演示）应用程序。  <xref:System.Windows.Data.CollectionViewSource> 类是继承自 <xref:System.Windows.Data.CollectionView> 的类的[!INCLUDE[TLA#tla_xaml](../../../../includes/tlasharptla-xaml-md.md)] 代理。  在此特定示例中，视图的 <xref:System.Windows.Data.CollectionViewSource.Source%2A> 绑定到当前应用程序对象的 *AuctionItems* 集合（类型为 <xref:System.Collections.ObjectModel.ObservableCollection%601>）。  
  
 [!code-xml[DataBindingLab#WindowResources1](../../../../samples/snippets/csharp/VS_Snippets_Wpf/DataBindingLab/CSharp/MainWindow.xaml#windowresources1)]  
[!code-xml[DataBindingLab#CollectionViewSource](../../../../samples/snippets/csharp/VS_Snippets_Wpf/DataBindingLab/CSharp/MainWindow.xaml#collectionviewsource)]  
[!code-xml[DataBindingLab#WindowResources2](../../../../samples/snippets/csharp/VS_Snippets_Wpf/DataBindingLab/CSharp/MainWindow.xaml#windowresources2)]  
  
 资源 *listingDataView* 随后用作应用程序中元素（如 <xref:System.Windows.Controls.ListBox>）的绑定源：  
  
 [!code-xml[DataBindingLab#Master1](../../../../samples/snippets/csharp/VS_Snippets_Wpf/DataBindingLab/CSharp/MainWindow.xaml#master1)]  
[!code-xml[DataBindingLab#Master2](../../../../samples/snippets/csharp/VS_Snippets_Wpf/DataBindingLab/CSharp/MainWindow.xaml#master2)]  
  
 若要为同一集合创建另一个视图，可以创建另一个 <xref:System.Windows.Data.CollectionViewSource> 实例并为其提供另一个 `x:Key` 名称。  
  
 下表显示了哪些视图数据类型是作为默认集合视图创建的或者是由 <xref:System.Windows.Data.CollectionViewSource> 根据源集合类型创建的。  
  
|源集合类型|集合视图类型|注释|  
|-----------|------------|--------|  
|<xref:System.Collections.IEnumerable>|基于 <xref:System.Windows.Data.CollectionView> 的内部类型|无法对项进行分组。|  
|<xref:System.Collections.IList>|<xref:System.Windows.Data.ListCollectionView>|最快。|  
|<xref:System.ComponentModel.IBindingList>|<xref:System.Windows.Data.BindingListCollectionView>||  
  
##### 使用默认视图  
 指定集合视图作为绑定源是创建和使用集合视图的一种方式。  WPF 还会为用作绑定源的每个集合创建一个默认集合视图。  如果您直接绑定到集合，则 WPF 会绑定到其默认视图。  请注意，此默认视图由到同一集合的所有绑定共享，因此一个绑定控件或代码对默认视图所做的更改（如排序或对当前项指针的更改，下文将对此进行讨论）会反映在到同一集合的所有其他绑定中。  
  
 若要获取默认视图，请使用 <xref:System.Windows.Data.CollectionViewSource.GetDefaultView%2A> 方法。  有关示例，请参见[获取数据集合的默认视图](../../../../docs/framework/wpf/data/how-to-get-the-default-view-of-a-data-collection.md)。  
  
##### 包含 ADO.NET 数据表的集合视图  
 为了提高性能，ADO.NET <xref:System.Data.DataTable> 或 <xref:System.Data.DataView> 对象的集合视图会将排序和筛选工作委托给 <xref:System.Data.DataView>。  这会导致排序和筛选工作由数据源的所有集合视图分担。  若要使每个集合视图都能独立进行排序和筛选，请用每个集合视图自己的 <xref:System.Data.DataView> 对象来初始化它。  
  
<a name="sorting"></a>   
#### 排序  
 如前所述，视图可以将排序顺序应用于集合。  如同在基础集合中一样，数据可能具有或不具有相关的固有顺序。  通过集合上的视图，您可以根据您提供的比较条件来应用顺序或更改默认顺序。  由于这是基于客户端的数据视图，因此一种常见情况是用户可能希望根据列对应的值，对多列表格数据进行排序。  通过使用视图，可以应用这种用户驱动的排序，而无需对基础集合进行任何更改，甚至不必再次查询集合内容。  有关示例，请参见[在单击标题时对 GridView 列进行排序](../../../../docs/framework/wpf/controls/how-to-sort-a-gridview-column-when-a-header-is-clicked.md)。  
  
 下面的示例演示[什么是数据绑定？](#what_is_data_binding)一节中的应用程序 [!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)] 的“按类别和日期排序”<xref:System.Windows.Controls.CheckBox> 的排序逻辑：  
  
 [!code-csharp[DataBindingLab#8](../../../../samples/snippets/csharp/VS_Snippets_Wpf/DataBindingLab/CSharp/MainWindow.xaml.cs#8)]
 [!code-vb[DataBindingLab#8](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/DataBindingLab/VisualBasic/MainWindow.xaml.vb#8)]  
  
<a name="filtering"></a>   
#### 筛选  
 视图还可以将筛选器应用于集合。  这意味着即使集合中可能存在一个项，此特定视图也仅用于显示整个集合的某个子集。  可以根据条件在数据中进行筛选。  例如，正如在[什么是数据绑定？](#what_is_data_binding)一节中的应用程序的工作方式那样，“仅显示成交商品”<xref:System.Windows.Controls.CheckBox> 包含了筛选出成交价为 25 美元或更高的项的逻辑。  执行下面的代码可以在选中该 <xref:System.Windows.Controls.CheckBox> 时将 *ShowOnlyBargainsFilter* 设置为 <xref:System.Windows.Data.CollectionViewSource.Filter> 事件处理程序：  
  
 [!code-csharp[DataBindingLab#10](../../../../samples/snippets/csharp/VS_Snippets_Wpf/DataBindingLab/CSharp/MainWindow.xaml.cs#10)]
 [!code-vb[DataBindingLab#10](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/DataBindingLab/VisualBasic/MainWindow.xaml.vb#10)]  
  
 *ShowOnlyBargainsFilter* 事件处理程序具有以下实现：  
  
 [!code-csharp[DataBindingLab#5](../../../../samples/snippets/csharp/VS_Snippets_Wpf/DataBindingLab/CSharp/MainWindow.xaml.cs#5)]
 [!code-vb[DataBindingLab#5](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/DataBindingLab/VisualBasic/MainWindow.xaml.vb#5)]  
  
 如果直接使用一个 <xref:System.Windows.Data.CollectionView> 类而不是 <xref:System.Windows.Data.CollectionViewSource>，则应使用 <xref:System.Windows.Data.CollectionView.Filter%2A> 属性来指定回调。  有关示例，请参见[筛选视图中的数据](../../../../docs/framework/wpf/data/how-to-filter-data-in-a-view.md)。  
  
<a name="grouping"></a>   
#### 分组  
 除了用来查看 <xref:System.Collections.IEnumerable> 集合的内部类之外，所有的集合视图都支持分组功能，用户可以利用此功能将集合视图中的集合划分成逻辑组。  这些组可以是显式的，其中的用户提供组列表，也可以是隐式的，其中的组依据数据动态生成。  
  
 下面的示例演示“Group by category”（按类别分组）<xref:System.Windows.Controls.CheckBox> 的逻辑：  
  
 [!code-csharp[DataBindingLab#6](../../../../samples/snippets/csharp/VS_Snippets_Wpf/DataBindingLab/CSharp/MainWindow.xaml.cs#6)]
 [!code-vb[DataBindingLab#6](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/DataBindingLab/VisualBasic/MainWindow.xaml.vb#6)]  
  
 有关其他分组示例，请参见[对实现 GridView 的 ListView 中的项进行分组](../../../../docs/framework/wpf/controls/how-to-group-items-in-a-listview-that-implements-a-gridview.md)。  
  
<a name="current_record_pointers"></a>   
#### 当前项指针  
 视图还支持当前项的概念。  可以在集合视图中的对象之间导航。  在导航时，您是在移动项指针，该指针可用于检索存在于集合中的特定位置的对象。  有关示例，请参见[在数据集合视图中的对象之间导航](../../../../docs/framework/wpf/data/how-to-navigate-through-the-objects-in-a-data-collectionview.md)。  
  
 由于 WPF 只通过使用视图（您指定的视图或集合的默认视图）绑定到集合，因此到集合的所有绑定都有一个当前项指针。  绑定到视图时，`Path` 值中的斜杠（“\/”）字符用于指定视图的当前项。  在下面的示例中，数据上下文是一个集合视图。  第一行绑定到集合。  第二行绑定到集合中的当前项。  第三行绑定到集合中的当前项的 `Description` 属性。  
  
```xaml  
<Button Content="{Binding }" />  
<Button Content="{Binding Path=/}" />  
<Button Content="{Binding Path=/Description}" />   
```  
  
 还可以连着使用斜杠和属性语法以遍历集合的层次结构。  下面的示例绑定到一个名为 `Offices` 的集合的当前项，此集合又是源集合的当前项的属性。  
  
```xaml  
<Button Content="{Binding /Offices/}" />  
```  
  
 当前项指针可能会受对集合应用的任何排序或筛选操作的影响。  排序操作将当前项指针保留在所选的最后一项上，但集合视图现在是围绕此指针重构的。  （或许所选项以前曾位于列表的开头，但现在所选项可能在中间的某个位置。）如果所选内容在筛选之后保留在视图中，则筛选操作会保留所选项。  否则，当前项指针会设置为经过筛选的集合视图的第一项。  
  
<a name="master_detail_scenario"></a>   
#### 主\-从绑定方案  
 当前项的概念不仅用于集合中项的导航，而且用于主\-从绑定方案。  再考虑一下[什么是数据绑定？](#what_is_data_binding)一节中的应用程序 [!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)]。  在该应用程序中，<xref:System.Windows.Controls.ListBox> 的所选内容决定了在 <xref:System.Windows.Controls.ContentControl> 中显示的内容。  换句话说，当选中一个 <xref:System.Windows.Controls.ListBox> 项时，<xref:System.Windows.Controls.ContentControl> 会显示选定项的详细信息。  
  
 通过将两个或更多控件绑定到同一视图可以轻松地实现主\-从方案。  下面来自 [Data Binding Demo](http://go.microsoft.com/fwlink/?LinkID=163703)（数据绑定演示）的示例演示在[什么是数据绑定？](#what_is_data_binding)一节中的应用程序 [!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)] 上看到的 <xref:System.Windows.Controls.ListBox> 和 <xref:System.Windows.Controls.ContentControl> 的标记：  
  
 [!code-xml[DataBindingLab#Master1](../../../../samples/snippets/csharp/VS_Snippets_Wpf/DataBindingLab/CSharp/MainWindow.xaml#master1)]  
[!code-xml[DataBindingLab#Master2](../../../../samples/snippets/csharp/VS_Snippets_Wpf/DataBindingLab/CSharp/MainWindow.xaml#master2)]  
[!code-xml[DataBindingLab#Detail](../../../../samples/snippets/csharp/VS_Snippets_Wpf/DataBindingLab/CSharp/MainWindow.xaml#detail)]  
  
 请注意，这两个控件都绑定到同一个源，即 *listingDataView* 静态资源（请参见[如何创建视图](#how_to_create_a_view)一节中的此资源的定义）。  可以这样做的原因是当单一实例对象（此示例中为 <xref:System.Windows.Controls.ContentControl>）绑定到一个集合视图时，该对象会自动绑定到该视图的 <xref:System.Windows.Data.CollectionView.CurrentItem%2A>。  请注意，<xref:System.Windows.Data.CollectionViewSource> 对象会自动同步货币与所选内容。  如果列表控件没有像示例中那样绑定到 <xref:System.Windows.Data.CollectionViewSource> 对象，则您需要将其 <xref:System.Windows.Controls.Primitives.Selector.IsSynchronizedWithCurrentItem%2A> 属性设置为 `true` 以达到此目的。  
  
 有关其他示例，请参见[绑定到集合并基于选择显示信息](../../../../docs/framework/wpf/data/how-to-bind-to-a-collection-and-display-information-based-on-selection.md)和[对分层数据使用主\-从模式](../../../../docs/framework/wpf/data/how-to-use-the-master-detail-pattern-with-hierarchical-data.md)。  
  
 您可能已经注意到上面的示例使用了一个模板。  实际上，如果不使用模板（由 <xref:System.Windows.Controls.ContentControl> 显式使用的模板以及由 <xref:System.Windows.Controls.ListBox> 隐式使用的模板），则数据不会按照我们希望的方式显示。  现在，我们开始介绍下一节中的数据模板化。  
  
<a name="data_templating"></a>   
## 数据模板化  
 如果不使用数据模板，则[什么是数据绑定？](#what_is_data_binding)一节中的应用程序 [!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)] 将如下所示：  
  
 ![没有数据模板的数据绑定演示](../../../../docs/framework/wpf/data/media/databindingdemotemplates.png "DataBindingDemoTemplates")  
  
 如上一节中的示例所示，<xref:System.Windows.Controls.ListBox> 控件和 <xref:System.Windows.Controls.ContentControl> 都绑定到 *AuctionItem* 的整个集合对象（更具体地说，是绑定到集合对象上的视图）。  如果没有有关如何显示数据集合的特定说明，则 <xref:System.Windows.Controls.ListBox> 会显示基础集合中的每个对象的字符串表示形式，而 <xref:System.Windows.Controls.ContentControl> 会显示绑定到的对象的字符串表示形式。  
  
 若要解决该问题，应用程序应定义 <xref:System.Windows.DataTemplate>。  如上一节中的示例所示，<xref:System.Windows.Controls.ContentControl> 显式使用 *detailsProductListingTemplate* <xref:System.Windows.DataTemplate>。  在显示集合中的 *AuctionItem* 对象时，<xref:System.Windows.Controls.ListBox> 控件隐式使用下面的 <xref:System.Windows.DataTemplate>：  
  
 [!code-xml[DataBindingLab#AuctionItemDataTemplate](../../../../samples/snippets/csharp/VS_Snippets_Wpf/DataBindingLab/CSharp/DataBindingLabApp.xaml#auctionitemdatatemplate)]  
  
 使用这两个 <xref:System.Windows.DataTemplate>，生成的 UI 如[什么是数据绑定？](#what_is_data_binding)一节中所示的 UI。  如屏幕快照所示，除了可以在控件中放置数据以外，使用 <xref:System.Windows.DataTemplate> 还可以为数据定义引人注目的视觉效果。  例如，上面的 <xref:System.Windows.DataTemplate> 中使用了 <xref:System.Windows.DataTrigger>，因而 *SpecialFeatures* 值为 *HighLight* 的 *AuctionItem* 会显示为带有橙色边框和一个星号。  
  
 有关数据模板的更多信息，请参见[数据模板化概述](../../../../docs/framework/wpf/data/data-templating-overview.md)。  
  
<a name="data_validation"></a>   
## 数据验证  
   
  
 接受用户输入的大多数应用程序都需要具有验证逻辑，以确保用户输入了需要的信息。  验证检查可以基于类型、范围、格式或其他应用程序特定的要求。  本节讨论了数据验证在 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 中的工作方式。  
  
<a name="validation_rules"></a>   
### 将验证规则与绑定关联  
 使用 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 数据绑定模型可以将 <xref:System.Windows.Data.Binding.ValidationRules%2A> 与 <xref:System.Windows.Data.Binding> 对象相关联。  例如，下面的示例将一个 <xref:System.Windows.Controls.TextBox> 绑定到名为 `StartPrice` 的属性并将一个 <xref:System.Windows.Controls.ExceptionValidationRule> 对象添加到 <xref:System.Windows.Data.Binding.ValidationRules%2A?displayProperty=fullName> 属性。  
  
 [!code-xml[DataBindingLab#DefaultValidation](../../../../samples/snippets/csharp/VS_Snippets_Wpf/DataBindingLab/CSharp/AddProductWindow.xaml#defaultvalidation)]  
  
 <xref:System.Windows.Controls.ValidationRule> 对象可检查属性的值是否有效。  [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 具有以下两种类型的内置 <xref:System.Windows.Controls.ValidationRule> 对象：  
  
-   <xref:System.Windows.Controls.ExceptionValidationRule> 检查在更新绑定源属性的过程中引发的异常。  在前面的示例中，`StartPrice` 为整数类型。  当用户输入的值无法转换为整数时，将引发异常，这会导致将绑定标记为无效。  用于显式设置 <xref:System.Windows.Controls.ExceptionValidationRule> 的可选语法是将 <xref:System.Windows.Data.Binding> 或 <xref:System.Windows.Data.MultiBinding> 对象上的 <xref:System.Windows.Data.Binding.ValidatesOnExceptions%2A> 属性设置为 `true`。  
  
-   <xref:System.Windows.Controls.DataErrorValidationRule> 对象检查由实现 <xref:System.ComponentModel.IDataErrorInfo> 接口的对象所引发的错误。  有关使用此验证规则的示例，请参见 <xref:System.Windows.Controls.DataErrorValidationRule>。  用于显式设置 <xref:System.Windows.Controls.DataErrorValidationRule> 的可选语法是将 <xref:System.Windows.Data.Binding> 或 <xref:System.Windows.Data.MultiBinding> 对象上的 <xref:System.Windows.Data.Binding.ValidatesOnDataErrors%2A> 属性设置为 `true`。  
  
 也可以通过从 <xref:System.Windows.Controls.ValidationRule> 类派生和实现 <xref:System.Windows.Controls.ValidationRule.Validate%2A> 方法来创建自己的验证规则。  下面的示例演示[什么是数据绑定？](#what_is_data_binding)一节中的*添加产品清单*“起始日期”<xref:System.Windows.Controls.TextBox> 使用的规则：  
  
 [!code-csharp[DataBindingLab#2](../../../../samples/snippets/csharp/VS_Snippets_Wpf/DataBindingLab/CSharp/FutureDateRule.cs#2)]
 [!code-vb[DataBindingLab#2](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/DataBindingLab/VisualBasic/FutureDateRule.vb#2)]  
  
 *StartDateEntryForm* <xref:System.Windows.Controls.TextBox> 使用此 *FutureDateRule*，如下面的示例中所示：  
  
 [!code-xml[DataBindingLab#CustomValidation](../../../../samples/snippets/csharp/VS_Snippets_Wpf/DataBindingLab/CSharp/AddProductWindow.xaml#customvalidation)]  
  
 请注意，由于 <xref:System.Windows.Data.Binding.UpdateSourceTrigger%2A> 值为 <xref:System.Windows.Data.UpdateSourceTrigger>，因此在每次键击时，绑定引擎都会更新源值，这意味着该引擎还会在每次键击时检查 <xref:System.Windows.Data.Binding.ValidationRules%2A> 集合中的每条规则。  我们会在“验证过程”一节中进行更深入的讨论。  
  
<a name="invalidation_feedback"></a>   
### 提供视觉反馈  
 如果用户输入的值无效，则您可能希望在应用程序 [!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)] 上提供一些有关错误的反馈。  提供这种反馈的一种方式是将 <xref:System.Windows.Controls.Validation.ErrorTemplate%2A?displayProperty=fullName> 附加属性设置为自定义 <xref:System.Windows.Controls.ControlTemplate>。  如上一小节中所示，*StartDateEntryForm* <xref:System.Windows.Controls.TextBox> 使用一个名为 *validationTemplate* 的 <xref:System.Windows.Controls.Validation.ErrorTemplate%2A>。  下面的示例显示 *validationTemplate* 的定义：  
  
 [!code-xml[DataBindingLab#1](../../../../samples/snippets/csharp/VS_Snippets_Wpf/DataBindingLab/CSharp/AddProductWindow.xaml#1)]  
  
 <xref:System.Windows.Controls.AdornedElementPlaceholder> 元素指定要装饰的控件应放置的位置。  
  
 此外，您可能还要使用 <xref:System.Windows.Controls.ToolTip> 显示错误消息。  *StartDateEntryForm* 和 *StartPriceEntryForm* <xref:System.Windows.Controls.TextBox> 都使用样式 *textStyleTextBox*，该样式创建一个显示错误消息的 <xref:System.Windows.Controls.ToolTip>。  下面的示例显示 *textStyleTextBox* 的定义。  当绑定元素的属性的一个或多个绑定发生错误时，[附加属性](GTMT) <xref:System.Windows.Controls.Validation.HasError%2A?displayProperty=fullName> 为 `true`。  
  
 [!code-xml[DataBindingLab#14](../../../../samples/snippets/csharp/VS_Snippets_Wpf/DataBindingLab/CSharp/DataBindingLabApp.xaml#14)]  
  
 使用自定义 <xref:System.Windows.Controls.Validation.ErrorTemplate%2A> 和 <xref:System.Windows.Controls.ToolTip>，*StartDateEntryForm* <xref:System.Windows.Controls.TextBox> 在发生验证错误时会如下所示：  
  
 ![数据绑定验证错误](../../../../docs/framework/wpf/data/media/databindingdemo-validation.png "DataBindingDemo\_Validation")  
  
 如果您的 <xref:System.Windows.Data.Binding> 具有关联验证规则，但是您未在绑定控件上指定 <xref:System.Windows.Controls.Validation.ErrorTemplate%2A>，则在出现验证错误时会使用默认 <xref:System.Windows.Controls.Validation.ErrorTemplate%2A> 来通知用户。  默认 <xref:System.Windows.Controls.Validation.ErrorTemplate%2A> 是一个在装饰器层中定义红色边框的控件模板。  使用默认 <xref:System.Windows.Controls.Validation.ErrorTemplate%2A> 和 <xref:System.Windows.Controls.ToolTip>，*StartPriceEntryForm* <xref:System.Windows.Controls.TextBox> 的 [!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)] 在发生验证错误时会如下所示：  
  
 ![数据绑定验证错误](../../../../docs/framework/wpf/data/media/databindingdemo-validationdefault.png "DataBindingDemo\_ValidationDefault")  
  
 有关如何提供逻辑以验证对话框中的所有控件的示例，请参见[对话框概述](../../../../docs/framework/wpf/app-development/dialog-boxes-overview.md)中的“自定义对话框”一节。  
  
<a name="validation_process"></a>   
### 验证过程  
 目标的值传输到绑定源属性时通常会发生验证。  这种情况发生在 <xref:System.Windows.Data.BindingMode> 和 <xref:System.Windows.Data.BindingMode> 绑定上。  在这里重复一下，导致源更新的原因取决于 <xref:System.Windows.Data.Binding.UpdateSourceTrigger%2A> 属性的值，如[触发源更新的原因](#what_triggers_source_updates)一节中所述。  
  
 下面描述了验证过程。  注意，如果在验证过程中的任何时候发生验证错误或者其他类型的错误，该过程将中断。  
  
1.  绑定引擎检查是否定义了任何自定义 <xref:System.Windows.Controls.ValidationRule> 对象（其 <xref:System.Windows.Controls.ValidationRule.ValidationStep%2A> 对于该 <xref:System.Windows.Data.Binding> 设置为 <xref:System.Windows.Controls.ValidationStep>），如果已经定义，绑定引擎会对每个 <xref:System.Windows.Controls.ValidationRule> 调用 <xref:System.Windows.Controls.ValidationRule.Validate%2A> 方法，直到其中一个规则出错或者全部规则都通过为止。  
  
2.  绑定引擎随后会调用转换器（如果存在）。  
  
3.  如果转换器成功，绑定引擎就会检查是否定义了任何自定义 <xref:System.Windows.Controls.ValidationRule> 对象（其 <xref:System.Windows.Controls.ValidationRule.ValidationStep%2A> 对于该 <xref:System.Windows.Data.Binding> 设置为 <xref:System.Windows.Controls.ValidationStep>），如果已经定义，绑定引擎会对每个将 <xref:System.Windows.Controls.ValidationRule.ValidationStep%2A> 设置为 <xref:System.Windows.Controls.ValidationStep> 的 <xref:System.Windows.Controls.ValidationRule> 调用 <xref:System.Windows.Controls.ValidationRule.Validate%2A> 方法，直到其中一个规则出错或者全部规则都通过为止。  
  
4.  绑定引擎设置源属性。  
  
5.  绑定引擎检查是否定义了任何自定义 <xref:System.Windows.Controls.ValidationRule> 对象（其 <xref:System.Windows.Controls.ValidationRule.ValidationStep%2A> 对于该 <xref:System.Windows.Data.Binding> 设置为 <xref:System.Windows.Controls.ValidationStep>），如果已经定义，绑定引擎会对每个将 <xref:System.Windows.Controls.ValidationRule.ValidationStep%2A> 设置为 <xref:System.Windows.Controls.ValidationStep> 的 <xref:System.Windows.Controls.ValidationRule> 调用 <xref:System.Windows.Controls.ValidationRule.Validate%2A> 方法，直到其中一个规则出错或者全部规则都通过为止。  如果 <xref:System.Windows.Controls.DataErrorValidationRule> 与某个绑定关联并且其 <xref:System.Windows.Controls.ValidationRule.ValidationStep%2A> 设置为默认值 <xref:System.Windows.Controls.ValidationStep>，则此时会检查 <xref:System.Windows.Controls.DataErrorValidationRule>。  此时还检查 <xref:System.Windows.Data.Binding.ValidatesOnDataErrors%2A> 设置为 `true` 的绑定。  
  
6.  绑定引擎检查是否定义了任何自定义 <xref:System.Windows.Controls.ValidationRule> 对象（其 <xref:System.Windows.Controls.ValidationRule.ValidationStep%2A> 对于该 <xref:System.Windows.Data.Binding> 设置为 <xref:System.Windows.Controls.ValidationStep>），如果已经定义，绑定引擎会对每个将 <xref:System.Windows.Controls.ValidationRule.ValidationStep%2A> 设置为 <xref:System.Windows.Controls.ValidationStep> 的 <xref:System.Windows.Controls.ValidationRule> 调用 <xref:System.Windows.Controls.ValidationRule.Validate%2A> 方法，直到其中一个规则出错或者全部规则都通过为止。  
  
 如果在此过程的任何时候某个 <xref:System.Windows.Controls.ValidationRule> 未通过，绑定引擎就会创建一个 <xref:System.Windows.Controls.ValidationError> 对象并将该对象添加到绑定元素的 <xref:System.Windows.Controls.Validation.Errors%2A?displayProperty=fullName> 集合中。  绑定引擎在任何给定步骤运行 <xref:System.Windows.Controls.ValidationRule> 对象之前，它会移除在该步骤中添加到绑定元素的 <xref:System.Windows.Controls.Validation.Errors%2A?displayProperty=fullName> [附加属性](GTMT)的任何 <xref:System.Windows.Controls.ValidationError>。  例如，如果某个 <xref:System.Windows.Controls.ValidationRule.ValidationStep%2A> 设置为 <xref:System.Windows.Controls.ValidationStep> 的 <xref:System.Windows.Controls.ValidationRule> 失败，则下一次进行验证过程时，绑定引擎会先移除该 <xref:System.Windows.Controls.ValidationError>，然后紧接着调用任何将 <xref:System.Windows.Controls.ValidationRule.ValidationStep%2A> 设置为 <xref:System.Windows.Controls.ValidationStep> 的 <xref:System.Windows.Controls.ValidationRule>。  
  
 当 <xref:System.Windows.Controls.Validation.Errors%2A?displayProperty=fullName> 不为空时，元素的 <xref:System.Windows.Controls.Validation.HasError%2A?displayProperty=fullName> [附加属性](GTMT)设置为 `true`。  此外，如果 <xref:System.Windows.Data.Binding> 的 <xref:System.Windows.Data.Binding.NotifyOnValidationError%2A> 属性设置为 `true`，则绑定引擎将在该元素上引发 <xref:System.Windows.Controls.Validation.Error?displayProperty=fullName> [附加事件](GTMT)。  
  
 还应注意，任何方向（目标到源或源到目标）的有效值传输操作都将清除 <xref:System.Windows.Controls.Validation.Errors%2A?displayProperty=fullName> [附加属性](GTMT)。  
  
 如果绑定具有与其关联的 <xref:System.Windows.Controls.ExceptionValidationRule> 或者其 <xref:System.Windows.Data.Binding.ValidatesOnExceptions%2A> 属性设置为 `true` 并且在绑定引擎设置源时引发一个异常，则绑定引擎会检查是否有 <xref:System.Windows.Data.Binding.UpdateSourceExceptionFilter%2A>。  您可以选择使用 <xref:System.Windows.Data.Binding.UpdateSourceExceptionFilter%2A> 回调来提供用于处理异常的自定义处理程序。  如果未对 <xref:System.Windows.Data.Binding> 指定 <xref:System.Windows.Data.Binding.UpdateSourceExceptionFilter%2A>，绑定引擎就会对异常创建 <xref:System.Windows.Controls.ValidationError> 并将其添加到绑定元素的 <xref:System.Windows.Controls.Validation.Errors%2A?displayProperty=fullName> 集合中。  
  
<a name="debugging_mechanism"></a>   
## 调试机制  
 可以在绑定相关对象上设置附加属性 <xref:System.Diagnostics.PresentationTraceSources.TraceLevel%2A?displayProperty=fullName> 以接收有关特定绑定的状态的信息。  
  
## 请参阅  
 <xref:System.Windows.Controls.DataErrorValidationRule>   
 [WPF 版本 4.5 的新增功能](../../../../docs/framework/wpf/getting-started/whats-new.md)   
 [绑定到 LINQ 查询的结果](../../../../docs/framework/wpf/data/how-to-bind-to-the-results-of-a-linq-query.md)   
 [数据绑定](../../../../docs/framework/wpf/advanced/optimizing-performance-data-binding.md)   
 [Data Binding Demo](http://go.microsoft.com/fwlink/?LinkID=163703)   
 [帮助主题](../../../../docs/framework/wpf/data/data-binding-how-to-topics.md)   
 [绑定到 ADO.NET 数据源](../../../../docs/framework/wpf/data/how-to-bind-to-an-ado-net-data-source.md)