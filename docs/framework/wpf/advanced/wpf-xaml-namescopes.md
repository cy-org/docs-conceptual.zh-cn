---
title: "WPF XAML 名称范围 | Microsoft Docs"
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
  - "API, 与名称相关的"
  - "类, FrameworkContentElement"
  - "类, FrameworkElement"
  - "类, RegisterName"
  - "FrameworkContentElement 类"
  - "FrameworkElement 类"
  - "与名称相关的 API"
  - "名称范围"
  - "寄存器名类"
  - "样式, 名称范围"
  - "模板, 名称范围"
  - "XAML, 名称范围"
ms.assetid: 52bbf4f2-15fc-40d4-837b-bb4c21ead7d4
caps.latest.revision: 19
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 18
---
# WPF XAML 名称范围
XAML 名称范围是用于标识在 XAML 定义的对象的概念。  XAML 名称范围中的名称可以用于在对象的 XAML 定义名称以及其在对象树中的实例等效项之间建立关系。  通常，[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 托管代码中的 XAML 名称范围在为 XAML 应用程序加载各个 XAML 页的根时进行创建。  作为编程对象的 XAML 名称范围由 <xref:System.Windows.Markup.INameScope> 接口定义，并且还由实际类 <xref:System.Windows.NameScope> 实现。  
  
   
  
<a name="Namescopes_in_Loaded_XAML_Applications"></a>   
## 加载的 XAML 应用程序中的名称范围  
 在更广阔的编程或计算机科学环境中，编程概念一般都会遵守一个原则：即具备可用于访问对象的唯一标识符或名称。  对于使用标识符或名称的系统，名称范围用于定义边界，过程或技术将在边界内搜索是否请求了该名称的对象，或在边界之内强制标识名称具有唯一性。  这些一般原则适用于 XAML 名称范围。  在 WPF 中，当加载 XAML 页时，会在该页的根元素上创建 XAML 名称范围。  从页的根开始，XAML 页中指定的每个名称都将添加到相关的 XAML 名称范围内。  
  
 在 WPF XAML 中，XAML 名称范围始终由作为常见根元素的元素（如 <xref:System.Windows.Controls.Page> 和 <xref:System.Windows.Window>）进行控制。  如果在标记中某个元素（例如 <xref:System.Windows.FrameworkElement> 或 <xref:System.Windows.FrameworkContentElement>）是页的根元素，则 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] 处理器将隐式添加一个 <xref:System.Windows.Controls.Page> 根元素，以使 <xref:System.Windows.Controls.Page> 可以提供工作 XAML 范围。  
  
> [!NOTE]
>  即使在 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] 标记中的任何元素上都没有定义 `Name` 或 `x:Name` 特性，WPF 生成操作也会为 XAML 生产创建 XAML 名称范围。  
  
 如果尝试在任意 XAML 名称范围中两次使用同一个名称，则会引发异常。  对于采用代码隐藏技术并且是已编译的应用程序一部分的 WPF XAML，如果在标记的初始编译过程中创建页的已生成类，WPF 生成操作将在生成时引发该异常。  对于不是由任何生成操作进行标记编译的 XAML，在加载该 XAML 时可能会引发与 XAML 名称范围相关的异常。  XAML 设计人员也可以在设计时预测 XAML 名称范围问题。  
  
### 向运行时对象树添加对象  
 XAML 的分析时间表示 WPF XAML 名称范围的创建和定义时间。  如果在对生成对象树的 XAML 进行分析后的某一时刻向树中添加对象，则新对象的 `Name` 或 `x:Name` 值不会自动更新 XAML 名称范围内的信息。  若要在加载 XAML 后将对象的名称添加到 WPF XAML 名称范围中，必须对定义 XAML 名称范围的对象（通常为 XAML 页的根）调用相应的 <xref:System.Windows.Markup.INameScope.RegisterName%2A> 实现。  如果该名称未注册，则无法通过 <xref:System.Windows.FrameworkElement.FindName%2A> 这类方法按名称引用添加的对象，并且无法将该名称用于动画目标。  
  
 对于应用程序开发人员最常见的方案是将使用 <xref:System.Windows.FrameworkElement.RegisterName%2A> 将名称注册到页面当前根元素的 XAML 名称范围中。  <xref:System.Windows.FrameworkElement.RegisterName%2A> 是用于确定动画目标对象的演示图板的重要方案的一部分。  有关更多信息，请参见[演示图板概述](../../../../docs/framework/wpf/graphics-multimedia/storyboards-overview.md)。  
  
 如果对定义 XAML 名称范围的对象以外的对象调用 <xref:System.Windows.FrameworkElement.RegisterName%2A>，则名称仍将注册到保存调用对象的 XAML 名称范围，就像对定义对象的 XAML 名称范围调用 <xref:System.Windows.FrameworkElement.RegisterName%2A> 一样。  
  
### 代码中的 XAML 名称范围  
 可以在代码中创建并使用 XAML 名称范围。  即使对于纯代码使用，XAML 名称范围创建中涉及的 API 和概念也是一样，因为 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 的 XAML 处理器在处理 XAML 本身时使用这些 API 和概念。  存在这些概念和 API 主要是为了能够在对象树（通常是部分或全部在 XAML 中定义的）中按名称查找对象。  
  
 对于以编程方式创建（而不是来自所加载的 XAML）的应用程序，定义 XAML 名称范围的对象必须实现 <xref:System.Windows.Markup.INameScope> 或者必须是 <xref:System.Windows.FrameworkElement> 或 <xref:System.Windows.FrameworkContentElement> 派生类，才能支持对其实例创建 XAML 名称范围。  
  
 此外，对于不是由 XAML 处理器加载和处理的任何元素，默认情况下不会创建或初始化对象的 XAML 名称范围。  必须为随后要向其中注册名称的任何对象显式创建新的 XAML 名称范围。  若要创建 XAML 名称范围，请调用静态 <xref:System.Windows.NameScope.SetNameScope%2A> 方法。  指定该名称范围所属的对象作为 `dependencyObject` 参数，并指定新的 <xref:System.Windows.NameScope.%23ctor%2A> 构造函数调用作为 `value` 参数。  
  
 如果作为 <xref:System.Windows.NameScope.SetNameScope%2A> 的 `dependencyObject` 提供的对象不是 <xref:System.Windows.Markup.INameScope> 实现，也不是 <xref:System.Windows.FrameworkElement> 或 <xref:System.Windows.FrameworkContentElement>，那么，对任何子元素调用 <xref:System.Windows.FrameworkElement.RegisterName%2A> 均无效。  如果未能显式创建新的 XAML 名称范围，则调用 <xref:System.Windows.FrameworkElement.RegisterName%2A> 将引发异常。  
  
 有关在代码中使用 XAML 名称范围 API 的示例，请参见[定义名称范围](../../../../docs/framework/wpf/graphics-multimedia/how-to-define-a-name-scope.md)。  
  
<a name="Namescopes_in_Styles_and_Templates"></a>   
## 样式和模板中的 XAML 名称范围  
 通过 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 中的样式和模板可以简单方式重复使用和重新应用内容。  但是，样式和模板可能还包括具有在模板级别定义的 XAML 名称的元素。  同一个模板可能在某个页中被多次重复使用。  因此，样式和模板都定义其自身的 XAML 名称范围，而与在从中应用样式或模板的对象树中的位置无关。  
  
 请看下面的示例：  
  
 [!code-xml[XamlOvwSupport#NameScopeTemplates](../../../../samples/snippets/csharp/VS_Snippets_Wpf/XAMLOvwSupport/CSharp/page6.xaml#namescopetemplates)]  
  
 此处，同一个模板被应用到两个不同的按钮。  如果模板没有独立的 XAML 名称范围，则该模板中用到的 `TheBorder` 名称会在 XAML 名称范围内导致名称冲突。  模板的每个实例化都有其自已的 XAML 名称范围，因此在本示例中每个实例化模板的 XAML 名称范围都只包含一个名称。  
  
 样式也会定义其自身的 XAML 名称范围，这样大多数情况下都会向演示图板的各个部分分配特定名称。  即使模板重新定义为控件自定义项的一部分，这些名称也会启用以具有此名称的元素为目标的控件特定行为。  
  
 由于 XAML 名称范围是独立的，因此在模板中查找命名元素与在页面中查找非模板化命名元素相比更加困难。  首先需要确定所应用的模板，方法是获取该模板所应用到的控件的 <xref:System.Windows.Controls.Control.Template%2A> 属性值。  然后，调用 <xref:System.Windows.FrameworkTemplate.FindName%2A> 的模板版本，将模板所应用到的控件作为第二个参数进行传递。  
  
 如果您是控件作者，您要生成一个约定，即所应用的模板中的特定命名元素是控件本身所定义的行为的目标，则可以在控件实现代码中使用 <xref:System.Windows.FrameworkElement.GetTemplateChild%2A> 方法。  由于 <xref:System.Windows.FrameworkElement.GetTemplateChild%2A> 方法是受保护的，因此只有控件作者才可以访问它。  
  
 如果正在使用模板，并且需要涉及从中应用该模板的 XAML 名称范围，则请获取 <xref:System.Windows.FrameworkElement.TemplatedParent%2A> 的值，然后从那里调用 <xref:System.Windows.FrameworkElement.FindName%2A>。  举一个使用模板的例子：您正在编写事件处理程序实现，其中该事件将从所应用的模板中的元素被引发。  
  
<a name="Namescopes_and_Name_related_APIs"></a>   
## XAML 名称范围和与名称相关的 API  
 <xref:System.Windows.FrameworkElement> 具有 <xref:System.Windows.FrameworkElement.FindName%2A>、<xref:System.Windows.FrameworkElement.RegisterName%2A> 和 <xref:System.Windows.FrameworkElement.UnregisterName%2A> 方法。  如果对其调用这些方法的对象拥有 XAML 名称范围，则这些方法将调入相关 XAML 名称范围的方法。  否则，会对父元素进行检查，看它是否拥有一个 XAML 名称范围，此过程递归继续，直到找到一个 XAML 名称范围（因为 XAML 处理器行为，确定根中有一个 XAML 名称范围）。  <xref:System.Windows.FrameworkContentElement> 具有类似的行为，所不同的是 <xref:System.Windows.FrameworkContentElement> 绝不会拥有 XAML 名称范围。  在 <xref:System.Windows.FrameworkContentElement> 上存在上述方法，因此这些调用最终可以转发到 <xref:System.Windows.FrameworkElement> 父元素。  
  
 <xref:System.Windows.NameScope.SetNameScope%2A> 用于将新的 XAML 名称范围映射到现有的对象。  多次调用 <xref:System.Windows.NameScope.SetNameScope%2A> 可以重置或清除 XAML 名称范围，但这种方法并不常用。  此外，通常不通过代码使用 <xref:System.Windows.NameScope.GetNameScope%2A>。  
  
### XAML 名称范围实现  
 下面的类直接实现 <xref:System.Windows.Markup.INameScope>：  
  
-   <xref:System.Windows.NameScope>  
  
-   <xref:System.Windows.Style>  
  
-   <xref:System.Windows.ResourceDictionary>  
  
-   <xref:System.Windows.FrameworkTemplate>  
  
 <xref:System.Windows.ResourceDictionary> 不使用 XAML 名称或名称范围，而是使用键，因为它是一种字典实现。  <xref:System.Windows.ResourceDictionary> 实现 <xref:System.Windows.Markup.INameScope> 的唯一原因就是它因此可以向用户代码引发异常，从而有助于阐明真正的 XAML 名称范围与 <xref:System.Windows.ResourceDictionary> 处理键的方式之间的区别，并且还可以保证父元素不会将 XAML 名称范围应用于 <xref:System.Windows.ResourceDictionary>。  
  
 <xref:System.Windows.FrameworkTemplate> 和 <xref:System.Windows.Style> 通过显式接口定义实现 <xref:System.Windows.Markup.INameScope>。  显式实现允许这些 XAML 名称范围在通过 <xref:System.Windows.Markup.INameScope> 接口被访问时做出常规反应，这是 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 内部进程传达 XAML 名称范围的方式。  但是，显式接口定义不是 <xref:System.Windows.FrameworkTemplate> 和 <xref:System.Windows.Style> 的常规 API 图面的一部分，原因是几乎不需要对 <xref:System.Windows.FrameworkTemplate> 和 <xref:System.Windows.Style> 直接调用 <xref:System.Windows.Markup.INameScope> 方法，而是要使用如 <xref:System.Windows.FrameworkElement.GetTemplateChild%2A> 的其他 API。  
  
 下面的各个类定义其自身的 XAML 名称范围，具体方法是使用 <xref:System.Windows.NameScope?displayProperty=fullName> 帮助器类并通过 <xref:System.Windows.NameScope.NameScope%2A?displayProperty=fullName> 附加属性连接到其 XAML 名称范围实现：  
  
-   <xref:System.Windows.FrameworkElement>  
  
-   <xref:System.Windows.FrameworkContentElement>  
  
## 请参阅  
 [WPF XAML 的 XAML 命名空间和命名空间映射](../../../../docs/framework/wpf/advanced/xaml-namespaces-and-namespace-mapping-for-wpf-xaml.md)   
 [x:Name 指令](../../../../docs/framework/xaml-services/x-name-directive.md)