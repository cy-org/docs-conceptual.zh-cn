---
title: "WPF 中的树 | Microsoft Docs"
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
  - "元素树"
  - "Logical Tree — 逻辑树"
  - "Visual Tree — 可视化树"
ms.assetid: e83f25e5-d66b-4fc7-92d2-50130c9a6649
caps.latest.revision: 20
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 19
---
# WPF 中的树
在许多技术中，元素和组件都按树结构的形式组织。在这种结构中，开发人员可以直接操作树中的对象节点来影响应用程序的呈现或行为。  [!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)] 也使用了若干树结构形式来定义程序元素之间的关系。  多数情况下，WPF 开发人员可以用代码创建应用程序，也可以用 XAML 定义应用程序的组成部分。与此同时，他们在概念层面上考虑对象树形式，但却要调用具体的 API 或使用特定的标记来实现对象树，而不是像在 XML DOM 中那样，使用某些常规对象树操作 API。  WPF 公开两个提供树形式视图的帮助器类：<xref:System.Windows.LogicalTreeHelper> 和 <xref:System.Windows.Media.VisualTreeHelper>。  WPF 文档中还使用了“可视化树”和“逻辑树”两个术语，它们有助于理解某些关键 WPF 功能的行为。  本主题定义可视化树和逻辑树的含义，讨论这些树与总体对象树概念之间的关系，并介绍 <xref:System.Windows.LogicalTreeHelper> 和 <xref:System.Windows.Media.VisualTreeHelper>。  
  
   
  
<a name="element_tree"></a>   
## WPF 中的树  
 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 中，最完整的树结构是对象树。  如果在 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] 中定义一个应用程序页，然后加载该 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)]，那么将根据标记中元素之间的嵌套关系来创建树结构。  如果使用代码定义应用程序或应用程序的一部分，则将根据为属性（实现给定对象的内容模型）指定属性值的方式来创建树结构。  在 [!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)] 中，完整的对象树可通过两种方式进行概念化并报告给其公共 API：作为逻辑树和作为可视化树。  逻辑树与可视化树之间的区别并不始终很重要，但在某些 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 子系统中它们可能会偶尔导致问题，并影响您对标记或代码的选择。  
  
 尽管我们不总是直接操作逻辑树或可视化树，但它们有助于理解与树的交互方式有关的概念，进而从技术角度了解 WPF。  若要理解 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 中属性继承和事件路由的工作原理，将 WPF 视为某种树形式也是一大要点。  
  
> [!NOTE]
>  因为对象树更像是概念，而不是实际 API，所以还可以将此概念视为对象图。  实际上，在运行时，对象之间的某些关系不能由树形式表示。  尽管如此，树形式的适用性还是很强，尤其是对于 XAML 定义的 UI。因此，大多数 WPF 文档在提及这个常规概念时，仍使用术语“对象树”。  
  
<a name="logical_tree"></a>   
## 逻辑树  
 在 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 中，通过为支持 UI 元素的对象设置属性，可以向这些 UI 元素添加内容。  例如，通过操作 <xref:System.Windows.Controls.ListBox> 控件的 <xref:System.Windows.Controls.ItemsControl.Items%2A> 属性，可以将项添加到该控件。  通过这种方法，可以将项放入用作 <xref:System.Windows.Controls.ItemsControl.Items%2A> 属性值的 <xref:System.Windows.Controls.ItemCollection> 中。  同样，通过操作 <xref:System.Windows.Controls.DockPanel> 的 <xref:System.Windows.Controls.Panel.Children%2A> 属性值，可以将对象添加到该控件中。  此时，您实际上是将对象添加到 <xref:System.Windows.Controls.UIElementCollection> 中。  有关代码示例，请参见 [Add an Element Dynamically](http://msdn.microsoft.com/zh-cn/d00f258a-7973-4de7-bc54-a3fc1f638419)。  
  
 在[!INCLUDE[TLA#tla_xaml](../../../../includes/tlasharptla-xaml-md.md)] 中，当在 <xref:System.Windows.Controls.ListBox> 中放置列表项，或在 <xref:System.Windows.Controls.DockPanel> 中放置控件或其他 UI 元素时，还会显式或隐式用到 <xref:System.Windows.Controls.ItemsControl.Items%2A> 和 <xref:System.Windows.Controls.Panel.Children%2A> 属性，如下例所示。  
  
 [!code-xml[TreeOvwsSupport#AllCode](../../../../samples/snippets/csharp/VS_Snippets_Wpf/TreeOvwsSupport/CS/page1.xaml#allcode)]  
  
 如果此 XAML 是作为符合文档对象模型的 XML 来处理的，且已包含了作为隐式项注释掉的标记（可能本是合法的），那么得到的 XML DOM 树应已包含表示 `<ListBox.Items>` 以及其他隐式项的元素。  但是，当您读取标记和写入对象时，XAML 不会这样处理，得到的对象图不会明确包含 `ListBox.Items`。  不过，它确实有一个名为 `Items` 的 <xref:System.Windows.Controls.ListBox> 属性，其中包含一个 <xref:System.Windows.Controls.ItemCollection>，并且在处理 <xref:System.Windows.Controls.ListBox> XAML 时，该 <xref:System.Windows.Controls.ItemCollection> 将初始化，但是为空。  然后，作为 <xref:System.Windows.Controls.ListBox> 的内容而存在的每个子对象元素，都将通过对 `ItemCollection.Add` 的分析器调用，添加到 <xref:System.Windows.Controls.ItemCollection> 中。  这个示例将 XAML 处理成对象树，目前看起来，该示例创建的对象树基本上是逻辑树。  
  
 不过，即使不考虑 XAML 隐式语法项，该逻辑树也不是应用程序 UI 在运行时存在的整个对象图。  之所以出现这种情况，主要是因为可视化对象和模板。  例如，请考虑 <xref:System.Windows.Controls.Button>。  在逻辑树中，可以看到 <xref:System.Windows.Controls.Button> 对象及其字符串 `Content`。  但在运行时对象树中，此按钮还有更多内容。  具体而言，该按钮在屏幕上仅显示为现在这样，是因为它应用了特定的 <xref:System.Windows.Controls.Button> 控件模板。  在逻辑树中，看不到来自所应用模板的可视化对象，如可视化按钮四周由模板定义的深灰色 <xref:System.Windows.Controls.Border>。即使在运行时过程中查看逻辑树（例如，处理来自可见 UI 的输入事件，然后读取逻辑树），也看不到。  若要查找模板可视化对象，需要改为检查可视化树。  
  
 有关 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] 语法与所创建对象图之间的映射关系，以及 XAML 中隐式语法的更多信息，请参见 [XAML 语法详述](../../../../docs/framework/wpf/advanced/xaml-syntax-in-detail.md)或 [XAML 概述 \(WPF\)](../../../../docs/framework/wpf/advanced/xaml-overview-wpf.md)。  
  
<a name="tree_property_inheritance_event_routing"></a>   
### 逻辑树用途  
 有了逻辑树的存在，内容模型可以方便地循环访问其潜在子对象，因而可以得到扩展。  此外，逻辑树还为某些通知提供框架，例如在加载逻辑树中的所有对象之后。  从根本上说，逻辑树是框架级别的近似运行时对象图（排除了可视化对象），但其足以用于对您自己的运行时应用程序成分执行多种查询操作。  
  
 此外，静态和动态资源引用有着相同的解析过程：针对最初发出请求的对象，沿逻辑树向上查找 <xref:System.Windows.FrameworkElement.Resources%2A> 集合，然后沿逻辑树继续向上，检查每一个 <xref:System.Windows.FrameworkElement> 或 <xref:System.Windows.FrameworkContentElement>，查找另一个包含 <xref:System.Windows.ResourceDictionary>（因而可能包含该键）的 `Resources` 值。  当同时存在逻辑树和可视化树时，将使用逻辑树进行资源查找。  有关资源字典和查找的更多信息，请参见[XAML 资源](../../../../docs/framework/wpf/advanced/xaml-resources.md)。  
  
<a name="composition"></a>   
### 逻辑树的构成  
 逻辑树在 [WPF 框架级别](GTMT)定义。这意味着，与逻辑树操作关系最密切的 WPF 基元素是 <xref:System.Windows.FrameworkElement> 或 <xref:System.Windows.FrameworkContentElement>。  但是可以看出，如果实际使用 <xref:System.Windows.LogicalTreeHelper> API，则逻辑树有时会包含既不是 <xref:System.Windows.FrameworkElement>，也不是 <xref:System.Windows.FrameworkContentElement> 的节点。  例如，在逻辑树中可以看到 <xref:System.Windows.Controls.TextBlock> 的 <xref:System.Windows.Controls.TextBlock.Text%2A> 值，该值是一个字符串。  
  
<a name="override_logical_tree"></a>   
### 重写逻辑树  
 有经验的控件作者会重写若干 [!INCLUDE[TLA2#tla_api#plural](../../../../includes/tla2sharptla-apisharpplural-md.md)]，用于定义常规对象或内容模型如何在逻辑树中添加或移除对象，这样可以重写逻辑树。  有关如何重写逻辑树的示例，请参见[重写逻辑树](../../../../docs/framework/wpf/advanced/how-to-override-the-logical-tree.md)。  
  
<a name="pvi"></a>   
### 属性值继承  
 属性值继承通过混合树操作。  包含用于启用属性继承的 <xref:System.Windows.FrameworkPropertyMetadata.Inherits%2A> 属性的实际元数据是 [WPF 框架级别](GTMT) <xref:System.Windows.FrameworkPropertyMetadata> 类。  因此，持有原始值的父对象和继承该值的子对象都必须是 <xref:System.Windows.FrameworkElement> 或 <xref:System.Windows.FrameworkContentElement>，且都必须属于某个逻辑树。  但是，对于支持属性继承的现有 WPF 属性，属性值的继承能够通过逻辑树中没有的中介对象永久存在。  这主要适用于以下情况：让模板元素使用在应用了模板的实例上设置的所有继承属性值，或者使用在更高级别的页级成分（因此在逻辑树中也位于更高位置）中设置的所有继承属性值。  为了使属性值的继承在这两种情况下保持一致，继承属性必须注册为附加属性。如果要定义具有属性继承行为的自定义依赖属性，则应采用这种方式。  通过帮助器类实用工具方法无法完全预测属性继承确切使用的树，即使在运行时也一样。  有关更多信息，请参见[属性值继承](../../../../docs/framework/wpf/advanced/property-value-inheritance.md)。  
  
<a name="two_trees"></a>   
## 可视化树  
 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 中除了逻辑树的概念，还存在[可视化树](GTMT)的概念。  可视化树描述由 <xref:System.Windows.Media.Visual> 基类表示的可视化对象的结构。  为控件编写模板时，将定义或重新定义适用于该控件的可视化树。  对于出于性能和优化原因想要对绘图进行较低级别控制的开发人员来说，他们也会对可视化树感兴趣。  在传统 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 应用程序编程中，也会用到可视化树：[路由事件](GTMT)的事件路由大多遍历可视化树而非逻辑树。  这种微妙的路由事件行为可能不会很明显，除非您是控件作者。  对于在可视化级别实现构成的控件，如果沿可视化树路由事件，该控件将能够处理事件或创建事件 setter。  
  
<a name="trees_content"></a>   
## 树、内容元素和内容宿主  
 内容元素（从 <xref:System.Windows.ContentElement> 派生的类）不是可视化树的一部分；内容元素不从 <xref:System.Windows.Media.Visual> 继承并且没有可视化表示形式。  若要完全显示在 UI 中，<xref:System.Windows.ContentElement> 必须承载在既属于 <xref:System.Windows.Media.Visual>，又属于逻辑树的内容宿主中。  这样的对象通常会是 <xref:System.Windows.FrameworkElement>。  您可以使用概念说明，内容宿主有点类似于内容的“浏览器”，它选择要在该宿主控制的屏幕区域中显示内容的方式。  承载内容时，可以使内容成为通常与可视化树关联的某些树进程的参与者。  通常，<xref:System.Windows.FrameworkElement> 宿主类包括实现代码，该代码用于通过内容逻辑树的子节点将任何已承载的 <xref:System.Windows.ContentElement> 添加到事件路由，即使承载内容不是真实可视化树的一部分时也将如此。  这样做是必要的，以便 <xref:System.Windows.ContentElement> 可以为路由到除其自身之外的任何元素的路由事件提供来源。  
  
<a name="tree_traversal"></a>   
## 树遍历  
 <xref:System.Windows.LogicalTreeHelper> 类为逻辑树遍历提供 <xref:System.Windows.LogicalTreeHelper.GetChildren%2A>、<xref:System.Windows.LogicalTreeHelper.GetParent%2A> 和 <xref:System.Windows.LogicalTreeHelper.FindLogicalNode%2A> 方法。  在大多数情况下，不需要遍历现有控件的逻辑树，因为这些控件几乎总是将其逻辑子元素公开为一个专用集合属性，这种属性支持集合访问，如 `Add`、索引器等等。  对于不选择从预期控件模式（例如已定义了集合属性的 <xref:System.Windows.Controls.ItemsControl> 或 <xref:System.Windows.Controls.Panel>）派生以及打算提供其自己的集合属性支持的控件作者，树遍历主要是他们使用的一种方案。  
  
 可视化树还支持用于可视化树遍历的帮助器类 <xref:System.Windows.Media.VisualTreeHelper>。  无法通过控件特定的属性方便地公开可视化树，因此，如果您的编程方案必须遍历可视化树，建议您使用 <xref:System.Windows.Media.VisualTreeHelper> 类。  有关更多信息，请参见[WPF 图形呈现疑难解答](../../../../docs/framework/wpf/graphics-multimedia/wpf-graphics-rendering-overview.md)。  
  
> [!NOTE]
>  有时，有必要检查所应用模板的可视化树。  执行此操作时应谨慎。  即便是遍历定义有模板的控件的可视化树，该控件的使用者仍可以通过设置实例的 <xref:System.Windows.Controls.Control.Template%2A> 属性随时更改模板，甚至最终用户也可以通过更改系统主题来影响所应用的模板。  
  
<a name="routes"></a>   
## “树”形式路由事件的路由  
 如前所述，对于任何给定的路由事件，其路由都沿着一条预定的树路径进行，这棵树是可视化树和逻辑树表示形式的混合体。  事件路由可在树中向上或向下进行，具体取决于该事件是隧道路由事件还是冒泡路由事件。  事件路由概念没有直接支持的帮助器类，因此当出现引发实际路由的事件时，无法使用这种类来遍历事件路由。  存在表示路由的类 <xref:System.Windows.EventRoute>，但该类的方法通常仅供内部使用。  
  
<a name="resourcesandtrees"></a>   
## 资源字典和树  
 对页中定义的所有 `Resources` 进行资源字典查找时，基本上是在遍历逻辑树。  逻辑树之外的对象可以引用键控资源，但资源查找顺序将从该对象与逻辑树的连接处开始。  在 WPF 中，只有逻辑树节点可以有包含 <xref:System.Windows.ResourceDictionary> 的 `Resources` 属性，因此，通过遍历可视化树从 <xref:System.Windows.ResourceDictionary> 中查找键控资源并无益处。  
  
 但是，资源查找也可以超出直接逻辑树。  对于应用程序标记，资源查找可向前继续进行到应用程序级资源字典，然后再到作为静态属性或键进行引用的主题支持和系统值。  如果资源引用是动态的，则主题本身也可以引用主题逻辑树之外的系统值。  有关资源字典和查找逻辑的更多信息，请参见[XAML 资源](../../../../docs/framework/wpf/advanced/xaml-resources.md)。  
  
## 请参阅  
 [输入概述](../../../../docs/framework/wpf/advanced/input-overview.md)   
 [WPF 图形呈现疑难解答](../../../../docs/framework/wpf/graphics-multimedia/wpf-graphics-rendering-overview.md)   
 [路由事件概述](../../../../docs/framework/wpf/advanced/routed-events-overview.md)   
 [不在对象树中的对象元素的初始化](../../../../docs/framework/wpf/advanced/initialization-for-object-elements-not-in-an-object-tree.md)   
 [WPF 体系结构](../../../../docs/framework/wpf/advanced/wpf-architecture.md)