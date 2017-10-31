---
title: "XAML 概述 (WPF) | Microsoft Docs"
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
  - "特性语法 [XAML]"
  - "基类 [XAML]"
  - "类 [XAML]"
  - "代码隐藏文件 [WPF], XAML"
  - "集合属性 [XAML]"
  - "内容模型 [XAML]"
  - "事件 [XAML]"
  - "可扩展应用程序标记语言（请参见 XAML）"
  - "属性元素 [XAML]"
  - "根元素 [XAML]"
  - "路由事件"
  - "用户界面 [XAML]"
  - "XAML [WPF], 关于 XAML"
ms.assetid: a80db4cd-dd0f-479f-a45f-3740017c22e4
caps.latest.revision: 57
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 50
---
# XAML 概述 (WPF)
本主题介绍 XAML 语言的功能，并演示如何使用 XAML 编写 [!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)] 应用程序。  本主题专门介绍 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 实现的 XAML。  XAML 本身是一个比 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 大的语言概念。  
  
   
  
<a name="what_is_xaml"></a>   
## 什么是 XAML？  
 XAML 是一种声明性标记语言。  如同应用于 [!INCLUDE[TLA2#tla_winfx](../../../../includes/tla2sharptla-winfx-md.md)] 编程模型一样，XAML 简化了为 [!INCLUDE[TLA2#tla_winfx](../../../../includes/tla2sharptla-winfx-md.md)] 应用程序创建 [!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)] 的过程。  您可以在声明性 XAML 标记中创建可见的 [!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)] 元素，然后使用代码隐藏文件（通过分部类定义与标记相连接）将 [!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)] 定义与运行时逻辑相分离。  XAML 直接以程序集中定义的一组特定后备类型表示对象的实例化。这与大多数其他标记语言不同，后者通常是与后备类型系统没有此类直接关系的解释语言。  XAML 实现了一个工作流，通过此工作流，各方可以采用不同的工具来处理应用程序的 [!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)] 和逻辑。  
  
 以文本表示时，XAML 文件是通常具有 `.xaml` 扩展名的 XML 文件。  可通过任何 XML 编码对文件进行编码，但通常编码为 UTF\-8。  
  
 下面的示例演示如何创建作为 [!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)] 一部分的按钮。  此示例的目的仅在于供您初步了解 XAML 是如何表示常用 [!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)] 编程形式的（它不是一个完整的示例）。  
  
 [!code-xml[XAMLOvwSupport#DirtSimple](../../../../samples/snippets/csharp/VS_Snippets_Wpf/XAMLOvwSupport/CSharp/page2.xaml#dirtsimple)]  
  
<a name="xaml_syntax_in_brief"></a>   
## XAML 语法概述  
 下面的章节介绍 XAML 语法的基本形式，并提供一个简短的标记示例。  这些章节并不提供每个语法形式的完整信息，例如这些语法如何在后备类型系统中表示。  有关本主题中介绍的每种语法形式在 XAML 语法中的详情的更多信息，请参见 [XAML 语法详述](../../../../docs/framework/wpf/advanced/xaml-syntax-in-detail.md)。  
  
 如果您以前熟悉 XML 语言，则下面几节中的很多材料对您而言都是基础知识。  这是 XAML 的其中一个基本设计原则的结果。  XAML 语言定义它自己的概念，但这些概念在 XML 语言和标记形式内发挥作用。  
  
### XAML 对象元素  
 对象元素通常声明类型的实例。  该类型在为以 XAML 为语言的技术提供后备类型的程序集中定义。  
  
 对象元素语法始终以左尖括号 \(\<\) 开头，  后跟要创建实例的类型的名称。  （该名称可能包含前缀，前缀的概念会在后面解释。）在此之后，您可以选择声明该对象元素的特性。  要完成对象元素标记，请以右尖括号 \(\>\) 结尾。  您也可以使用不含任何内容的自结束形式，方法是用一个正斜杠后接一个右尖括号 \(\/\>\) 来完成标记。  例如，请再次查看前面演示的标记代码段：  
  
 [!code-xml[XAMLOvwSupport#DirtSimple](../../../../samples/snippets/csharp/VS_Snippets_Wpf/XAMLOvwSupport/CSharp/page2.xaml#dirtsimple)]  
  
 此示例指定了两个对象元素：`<StackPanel>`（含有内容，后面有一个结束标记）和 `<Button .../>`（自结束形式，包含几个特性）。  对象元素 `StackPanel` 和 `Button` 各映射到一个类名，这些类由 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 定义并且是 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 程序集的一部分。  指定对象元素标记时会创建一条 XAML 处理指令来创建一个新实例。  每个实例都是在分析和加载 XAML 时通过调用基础类型的默认构造函数来创建的。  
  
### 特性语法（属性）  
 对象的属性通常可表示为对象元素的特性。  特性语法命名在特性语法中设置的属性，后跟赋值运算符 \(\=\)。  特性的值始终以包含在引号中的字符串的形式进行指定。  
  
 特性语法是最简单有效的属性设置语法，并且对于曾使用过标记语言的开发人员而言在使用中是最直观的语法。  例如，以下标记将创建一个具有红色文本和蓝色背景的按钮，还将创建指定为 `Content` 的显示文本。  
  
 [!code-xml[XAMLOvwSupport#BlueRedButton](../../../../samples/snippets/csharp/VS_Snippets_Wpf/XAMLOvwSupport/CSharp/Page1.xaml#blueredbutton)]  
  
### 属性元素语法  
 对于对象元素的某些属性，特性语法是不可能实现的，因为无法在特性语法的引号和字符串限制内充分地表达提供属性值所必需的对象或信息。  对于这些情况，可以使用另一个语法，即属性元素语法。  
  
 属性元素开始标记的语法为 `<`*类型名称*`.`*属性名称*`>`。  通常，该标记的内容是类型的一个对象元素，属性会将该元素作为其值。  指定内容之后，必须用一个结束标记结束属性元素。  结束标记的语法为 `</`*类型名称*`.`*属性名称*`>`。  
  
 如果可以使用特性语法，那么使用特性语法通常更为方便，且能够实现更为精简的标记，但这通常只是一个风格的问题，而不属于技术限制。  下面的示例演示了在前面的特性语法示例中设置的相同属性，但这次对 `Button` 的所有属性使用了属性元素语法。  
  
 [!code-xml[XAMLOvwSupport#BlueRedButtonPE](../../../../samples/snippets/csharp/VS_Snippets_Wpf/XAMLOvwSupport/CSharp/Page1.xaml#blueredbuttonpe)]  
  
### 集合语法  
 XAML 语言包含一些优化，可以生成可读性更好的标记。  其中的一项优化是：如果某个特定属性采用集合类型，则您在标记中声明为该属性的值内的子元素的项将成为集合的一部分。  在这种情况下，子对象元素的集合是设置为集合属性的值。  
  
 下面的示例演示为 <xref:System.Windows.Media.GradientBrush.GradientStops%2A> 属性设置值的集合语法：  
  
```xaml  
<LinearGradientBrush>  
  <LinearGradientBrush.GradientStops>  
    <!-- no explicit new GradientStopCollection, parser knows how to find or create -->  
    <GradientStop Offset="0.0" Color="Red" />  
    <GradientStop Offset="1.0" Color="Blue" />  
  </LinearGradientBrush.GradientStops>  
</LinearGradientBrush>  
```  
  
### XAML 内容属性  
 XAML 指定了一个语言功能，通过该功能，一个类可以指定它的一个且仅一个属性为 XAML 内容属性。  该对象元素的子元素用于设置该内容属性的值。  换言之，仅对内容属性而言，您可以在 XAML 标记中设置该属性时省略属性元素，并在标记中生成更直观的父级\/子级形式。  
  
 例如，<xref:System.Windows.Controls.Border> 指定内容属性 <xref:System.Windows.Controls.Decorator.Child%2A>。  系统处理下面两个 <xref:System.Windows.Controls.Border> 元素的方式相同。  第一个元素利用了内容属性语法而省略了 `Border.Child` 属性元素。  第二个元素显式标明 `Border.Child`。  
  
```xaml  
<Border>  
  <TextBox Width="300"/>  
</Border>  
<!--explicit equivalent-->  
<Border>  
  <Border.Child>  
    <TextBox Width="300"/>  
  </Border.Child>  
</Border>  
```  
  
 作为 XAML 语言的规则，XAML 内容属性的值必须完全在该对象元素的其他任何属性元素之前或之后指定。  例如，下面的标记无法进行编译：  
  
```  
<Button>I am a   
  <Button.Background>Blue</Button.Background>  
  blue button</Button>  
```  
  
 有关 XAML 内容属性的此项限制的更多信息，请参见 [XAML 语法详述](../../../../docs/framework/wpf/advanced/xaml-syntax-in-detail.md)的“XAML 内容属性”一节。  
  
### 文本内容  
 有少量 XAML 元素可直接将文本作为其内容来处理。  若要实现此功能，必须满足以下条件之一：  
  
-   类必须声明一个内容属性，并且该内容属性必须是可赋值给字符串的类型（该类型可以是 <xref:System.Object>）。  例如，任何 <xref:System.Windows.Controls.ContentControl> 都将 <xref:System.Windows.Controls.ContentControl.Content%2A> 用作其内容属性，并且其类型为 <xref:System.Object>，这样就支持实际的 <xref:System.Windows.Controls.ContentControl>（例如，<xref:System.Windows.Controls.Button>）上的如下用法：`<Button>Hello</Button>`。  
  
-   类型必须声明一个类型转换器，该类型转换器将文本内容用作其初始化文本。  例如，`<Brush>Blue</Brush>`。  这种情况实际上并不常见。  
  
-   类型必须为已知的 XAML 语言基元。  
  
### 内容属性和集合语法组合  
 请看以下示例：  
  
```xaml  
<StackPanel>  
  <Button>First Button</Button>  
  <Button>Second Button</Button>  
</StackPanel>  
```  
  
 此例中，每个 <xref:System.Windows.Controls.Button> 都是 <xref:System.Windows.Controls.StackPanel> 的一个子元素。  这是一个简单直观的标记，其中出于两个不同的原因省略了两个标记。  
  
-   **省略的 StackPanel.Children 属性元素：** <xref:System.Windows.Controls.StackPanel> 从 <xref:System.Windows.Controls.Panel> 派生。  <xref:System.Windows.Controls.Panel> 将 <xref:System.Windows.Controls.Panel.Children%2A?displayProperty=fullName> 定义为其 XAML 内容属性。  
  
-   **省略的 UIElementCollection 对象元素：** <xref:System.Windows.Controls.Panel.Children%2A?displayProperty=fullName> 属性采用类型 <xref:System.Windows.Controls.UIElementCollection>，该类型实现 <xref:System.Collections.IList>。  根据处理集合（例如 <xref:System.Collections.IList>）的 XAML 规则，集合的元素标记可以省略。  （在这种情况下，<xref:System.Windows.Controls.UIElementCollection> 实际无法实例化，因为它没有公开默认构造函数，这就是 <xref:System.Windows.Controls.UIElementCollection> 对象元素以注释形式出现的原因。）  
  
```xaml  
<StackPanel>  
  <StackPanel.Children>  
    <!--<UIElementCollection>-->  
    <Button>First Button</Button>  
    <Button>Second Button</Button>  
    <!--</UIElementCollection>-->  
  </StackPanel.Children>  
</StackPanel>  
```  
  
### 特性语法（事件）  
 特性语法还可用于事件成员，而不仅限于属性成员。  在这种情况下，特性的名称为事件的名称。  在 XAML 事件的 WPF 实现中，特性的值是实现该事件的委托的处理程序的名称。  例如，以下标记将 <xref:System.Windows.Controls.Primitives.ButtonBase.Click> 事件的一个处理程序指定给在标记中创建的 <xref:System.Windows.Controls.Button>：  
  
 [!code-xml[XAMLOvwSupport#ButtonWithCodeBehind](../../../../samples/snippets/csharp/VS_Snippets_Wpf/XAMLOvwSupport/CSharp/page3.xaml#buttonwithcodebehind)]  
  
 除此特性语法示例外，还有更多关于 WPF 中的事件和 XAML 的内容。  例如，您可能希望了解此处引用的 `ClickHandler` 表示什么，以及它是如何定义的。  这将在本主题中后面的一节中解释。  
  
<a name="case_and_whitespace_in_xaml"></a>   
## XAML 中的大小写和空白  
 XAML 通常区分大小写。  出于解析后备类型的目的，WPF XAML 按照 CLR 区分大小写的相同规则区分大小写。  按名称与程序集中的基础类型进行比较或者与类型的成员进行比较时，对象元素、属性元素和特性名称均必须使用区分大小写的形式指定。  XAML 语言关键字和基元也区分大小写。  值并不总是区分大小写。  值是否区分大小写将取决于与采用该值的属性关联的类型转换器行为，或取决于属性值类型。  例如，采用 <xref:System.Boolean> 类型的属性可以采用 `true` 或 `True` 作为等效值，但只是因为将字符串转换为 <xref:System.Boolean> 的本机 WPF XAML 分析器类型转换已经允许将这些值作为等效值。  
  
 WPF XAML 处理器和序列化程序将忽略或删除所有无意义的空白，并规范化任何有意义的空白。  这与 XAML 规范的默认空白行为建议一致。  通常，只有当您在 XAML 内容属性中指定字符串时，此行为的重要性才会体现出来。  简言之，XAML 将空格、换行符和制表符转化为空格，如果它们出现在一个连续字符串的任一端，则保留一个空格。  有关 XAML 空白处理的完整说明不属于本主题的讨论范围。  有关详细信息，请参见 [XAML 中的空白处理](../../../../docs/framework/xaml-services/whitespace-processing-in-xaml.md)。  
  
<a name="markup_extensions"></a>   
## 标记扩展  
 标记扩展是一个 XAML 语言概念。  当用于提供特性语法的值时，大括号（`{` 和 `}`）表示标记扩展用法。  此用法指示 XAML 处理系统不要像通常那样将特性值视为一个文本字符串或者可转换为字符串的值。  
  
 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 应用程序编程中最常用的标记扩展是 [Binding](../../../../docs/framework/wpf/advanced/binding-markup-extension.md)（用于数据绑定表达式）以及资源引用 [StaticResource](../../../../docs/framework/wpf/advanced/staticresource-markup-extension.md) 和 [DynamicResource](../../../../docs/framework/wpf/advanced/dynamicresource-markup-extension.md)。  通过使用标记扩展，即使属性通常不支持特性语法，也可以使用特性语法为属性提供值。  标记扩展经常使用中间表达式类型实现一些功能，例如，推迟值或引用仅在运行时才存在的其他对象。  
  
 例如，下面的标记使用特性语法设置 <xref:System.Windows.FrameworkElement.Style%2A> 属性的值。  <xref:System.Windows.FrameworkElement.Style%2A> 属性采用了 <xref:System.Windows.Style> 类的一个实例，该实例默认情况下未能用特性语法字符串实例化。  但在本例中，特性引用了特定的标记扩展 [StaticResource](../../../../docs/framework/wpf/advanced/staticresource-markup-extension.md)。  当处理该标记扩展时，它返回对以前在资源字典中作为键控资源进行实例化的某个样式的引用。  
  
<!-- TODO: review snippet reference  [!CODE [FEResourceSH#XAMLOvwShortResources](FEResourceSH#XAMLOvwShortResources)]  -->  
<!-- TODO: review snippet reference [!CODE [FEResourceSH#XAMLOvwShortResources2](FEResourceSH#XAMLOvwShortResources2)]  -->  
<!-- TODO: review snippet reference [!CODE [FEResourceSH#XAMLOvwShortResources3](FEResourceSH#XAMLOvwShortResources3)]  -->  
  
 有关特定在 WPF 中实现的所有 XAML 标记扩展的参考列表，请参见 [WPF XAML 扩展](../../../../docs/framework/wpf/advanced/wpf-xaml-extensions.md)。  有关由 System.Xaml 定义并且可更广泛用于 .NET Framework XAML 实现的标记扩展的参考列表，请参见 [XAML 命名空间 \(x:\) 语言功能](../../../../docs/framework/xaml-services/xaml-namespace-x-language-features.md)。  有关标记扩展概念的更多信息，请参见[标记扩展和 WPF XAML](../../../../docs/framework/wpf/advanced/markup-extensions-and-wpf-xaml.md)。  
  
<a name="type_converters"></a>   
## 类型转换器  
 在一节中，曾提到特性值必须能够使用字符串进行设置。  对字符串如何转换为其他对象类型或基元值的基本本机处理取决于 <xref:System.String> 类型本身，以及对某些类型（如 <xref:System.DateTime> 或 <xref:System.Uri>）的本机处理。  但是很多 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 类型或这些类型的成员扩展了基本字符串特性处理行为，因此可以指定更复杂的对象类型的实例作为字符串和特性。  
  
 <xref:System.Windows.Thickness> 结构是一个类型示例，该类型拥有可使用 XAML 的类型转换。  <xref:System.Windows.Thickness> 指示嵌套矩形中的度量并用作一些属性（如 <xref:System.Windows.FrameworkElement.Margin%2A>）的值。  通过对 <xref:System.Windows.Thickness> 设置类型转换器，所有使用 <xref:System.Windows.Thickness> 的属性都可以更容易地在 XAML 中指定，因为它们可指定为特性。  下面的示例使用类型转换和特性语法来为 <xref:System.Windows.FrameworkElement.Margin%2A> 提供值：  
  
 [!code-xml[XAMLOvwSupport#MarginTCE](../../../../samples/snippets/csharp/VS_Snippets_Wpf/XAMLOvwSupport/CSharp/page7.xaml#margintce)]  
  
 上面的特性语法示例与下面更为详细的语法示例等效，但在下面的示例中，<xref:System.Windows.FrameworkElement.Margin%2A> 改为通过包含 <xref:System.Windows.Thickness> 对象元素的属性元素语法进行设置。  而且设置 <xref:System.Windows.Thickness> 的四个关键属性作为新实例的特性：  
  
 [!code-xml[XAMLOvwSupport#MarginVerbose](../../../../samples/snippets/csharp/VS_Snippets_Wpf/XAMLOvwSupport/CSharp/page7.xaml#marginverbose)]  
  
> [!NOTE]
>  还有少数对象只能通过类型转换这种公开方式在不涉及到子类的情况下为该类型设置属性，因为类型本身并没有默认构造函数。  一个示例是 <xref:System.Windows.Input.Cursor>。  
  
 有关如何支持类型转换及其在特性语法上的应用的更多信息，请参见 [TypeConverters 和 XAML](../../../../docs/framework/wpf/advanced/typeconverters-and-xaml.md)。  
  
<a name="xaml_root_elements_and_xaml_namespaces"></a>   
## XAML 根元素和 XAML 命名空间  
 一个 XAML 文件只能有一个根元素，这样才能同时成为格式正确的 [!INCLUDE[TLA2#tla_xml](../../../../includes/tla2sharptla-xml-md.md)] 文件和有效的 XAML 文件。  对于典型的 WPF 方案，将使用在 WPF 应用程序模型中具有重要意义的根元素（例如，为页使用 <xref:System.Windows.Window> 或 <xref:System.Windows.Controls.Page>，为外部字典使用 <xref:System.Windows.ResourceDictionary> 或为应用程序定义使用 <xref:System.Windows.Application>）。  下面的示例演示 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 页的典型 XAML 文件的根元素，此根元素为 <xref:System.Windows.Controls.Page>。  
  
 [!code-xml[XAMLOvwSupport#RootOnly](../../../../samples/snippets/csharp/VS_Snippets_Wpf/XAMLOvwSupport/CSharp/page2.xaml#rootonly)]  
[!code-xml[XAMLOvwSupport#RootOnly2](../../../../samples/snippets/csharp/VS_Snippets_Wpf/XAMLOvwSupport/CSharp/page2.xaml#rootonly2)]  
  
 根元素还包含特性 `xmlns` 和 `xmlns:x`。  这些特性向 XAML 处理器指明哪些 XAML 命名空间包含标记将要作为元素引用的后备类型的类型定义。  `xmlns` 特性明确指示默认的 XAML 命名空间。  在默认的 XAML 命名空间中，可以不使用前缀指定标记中的对象元素。  对于大多数 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 应用程序方案以及 [!INCLUDE[TLA2#tla_sdk](../../../../includes/tla2sharptla-sdk-md.md)] 的 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 部分中给出的几乎所有示例，默认的 XAML 命名空间均映射到为 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 命名空间 [!INCLUDE[TLA#tla_wpfxmlnsv1](../../../../includes/tlasharptla-wpfxmlnsv1-md.md)]。  `xmlns:x` 特性指示另外一个 XAML 命名空间，该命名空间映射 XAML 语言命名空间 [!INCLUDE[TLA#tla_xamlxmlnsv1](../../../../includes/tlasharptla-xamlxmlnsv1-md.md)]。  
  
 使用 `xmlns` 定义用法范围和名称范围映射的做法符合 XML 1.0 规范。  XAML 名称范围与 XML 名称范围的不同仅在于：XAML 名称范围还包含有关进行类型解析和分析 XAML 时名称范围的元素如何受类型支持的信息。  
  
 请注意，只有在每个 XAML 文件的根元素上，`xmlns` 特性才是绝对必需的。  `xmlns` 定义将适用于根元素的所有子代元素（此行为也符合 `xmlns` 的 XML 1.0 规范）。同时允许根以下的其他元素上具有 `xmlns` 特性，这些特性将适用于定义元素的任何子代元素。  但是，频繁定义或重新定义 XAML 命名空间可能会导致 XAML 标记样式难以阅读。  
  
 其 XAML 处理器的 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 实现包括可识别 WPF 核心程序集的基础结构。  已知 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 核心程序集包含支持 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 到默认 XAML 命名空间的映射的类型。  这是通过属于项目生成文件以及 WPF 生成和项目系统一部分的配置来实现的。  因此，为了引用来自 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 程序集的 XAML 元素，只需将默认 XAML 命名空间声明为默认 `xmlns`。  
  
### x: 前缀  
 在上面的根元素示例中，前缀 `x:` 用于映射 XAML 命名空间 [!INCLUDE[TLA#tla_xamlxmlnsv1](../../../../includes/tlasharptla-xamlxmlnsv1-md.md)]，该命名空间是支持 XAML 语言构造的专用 XAML 命名空间。  在这整个 [!INCLUDE[TLA2#tla_sdk](../../../../includes/tla2sharptla-sdk-md.md)] 的项目模板、示例以及文档中，此 `x:` 前缀用于映射该 XAML 命名空间。  XAML 语言的 XAML 命名空间包含多个将在 XAML 中频繁用到的编程构造。  下面列出了将用到的最常见的 `x:` 前缀编程构造：  
  
-   [x:Key](../../../../docs/framework/xaml-services/x-key-directive.md)：为 <xref:System.Windows.ResourceDictionary>（或其他框架中的类似字典概念）中的每个资源设置唯一的键。  在典型的 WPF 应用程序标记中的所有 `x:` 用法中，`x:Key` 将可能占到 90%。  
  
-   [x:Class](../../../../docs/framework/xaml-services/x-class-directive.md)：向为 XAML 页提供代码隐藏的类指定 [!INCLUDE[TLA2#tla_clr](../../../../includes/tla2sharptla-clr-md.md)] 命名空间和类名。  必须具有这样一个类才能支持每个 WPF 编程模型的代码隐藏，而正是因此，即使没有资源，也几乎总是能看到映射的 `x:`。  
  
-   [x:Name](../../../../docs/framework/xaml-services/x-name-directive.md)：处理对象元素后，为运行时代码中存在的实例指定运行时对象名称。  通常，您将为 [x:Name](../../../../docs/framework/xaml-services/x-name-directive.md) 经常使用 WPF 定义的等效属性。  此类属性特定映射到 CLR 后备属性，因此更便于进行应用程序编程，在应用程序编程中，您经常使用运行时代码从初始化的 XAML 中查找命名元素。  最常见的此类属性是 <xref:System.Windows.FrameworkElement.Name%2A?displayProperty=fullName>。  在特定类型中不支持等效的 [WPF 框架级](GTMT) <xref:System.Windows.FrameworkElement.Name%2A> 属性时，仍然可以使用 [x:Name](../../../../docs/framework/xaml-services/x-name-directive.md)。  某些动画方案中会发生这种情况。  
  
-   [x:Static](../../../../docs/framework/xaml-services/x-static-markup-extension.md)：启用一个返回静态值的引用，该静态值只能是一个 XAML 兼容属性。  
  
-   [x:Type](../../../../docs/framework/xaml-services/x-type-markup-extension.md)：根据类型名称构造一个 <xref:System.Type> 引用。  它用于指定采用 <xref:System.Type>（例如 <xref:System.Windows.Style.TargetType%2A?displayProperty=fullName>）的特性，但属性经常具有本机的字符串到 <xref:System.Type> 的转换功能，因此使用 [x:Type](../../../../docs/framework/xaml-services/x-type-markup-extension.md) 标记扩展用法是可选的。  
  
 `x:` 前缀\/XAML 命名空间中还有其他一些不太常见的编程构造。  有关详细信息，请参见 [XAML 命名空间 \(x:\) 语言功能](../../../../docs/framework/xaml-services/xaml-namespace-x-language-features.md)。  
  
<a name="custom_prefixes_and_custom_types_in_xaml"></a>   
## XAML 中的自定义前缀和自定义类型  
 对于您自己的自定义程序集或 PresentationCore、PresentationFramework 和 WindowsBase 的 WPF 核心以外的程序集，可以将该程序集指定为自定义 `xmlns` 映射的一部分。  只要该类型能够正确地实现以支持您所尝试的 XAML 用法，就可以在 XAML 中引用该程序集中的类型。  
  
 下面是一个说明自定义前缀如何在 XAML 标记中工作的基本示例。  前缀 `custom` 在根元素标记中定义，并映射为随应用程序一同打包并可用于该应用程序的一个特定程序集。  此程序集包含 `NumericUpDown` 类型，实现该类型的目的是在支持常规 XAML 用法之外，还可以使用允许在 WPF XAML 内容模型的此特定点执行插入的类继承。  通过使用该前缀，此 `NumericUpDown` 控件的一个实例声明为对象元素，以便 XAML 分析器可找到包含该类型的 XAML 命名空间，从而找到包含该类型定义的后备程序集的位置。  
  
```  
<Page  
    xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"   
    xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"   
    xmlns:custom="clr-namespace:NumericUpDownCustomControl;assembly=CustomLibrary"  
    >  
  <StackPanel Name="LayoutRoot">  
    <custom:NumericUpDown Name="numericCtrl1" Width="100" Height="60"/>  
...  
  </StackPanel>  
</Page>  
```  
  
 有关 XAML 中自定义类型的更多信息，请参见 [XAML 及 WPF 的自定义类](../../../../docs/framework/wpf/advanced/xaml-and-custom-classes-for-wpf.md)。  
  
 有关 XML 命名空间与程序集中后备代码的命名空间如何相关的更多信息，请参见 [WPF XAML 的 XAML 命名空间和命名空间映射](../../../../docs/framework/wpf/advanced/xaml-namespaces-and-namespace-mapping-for-wpf-xaml.md)。  
  
<a name="events_and_xaml_codebehind"></a>   
## 事件和 XAML 代码隐藏  
 大多数 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 应用程序既包括 XAML 标记，也包括代码隐藏。  在一个项目中，XAML 编写为 `.xaml` 文件，而 [!INCLUDE[TLA2#tla_clr](../../../../includes/tla2sharptla-clr-md.md)] 语言（如 [!INCLUDE[TLA#tla_visualb](../../../../includes/tlasharptla-visualb-md.md)] 或 [!INCLUDE[TLA#tla_cshrp](../../../../includes/tlasharptla-cshrp-md.md)]）用于编写代码隐藏文件。  在 WPF 编程和应用程序模型中对 XAML 文件进行标记编译时，XAML 文件的 XAML 代码隐藏文件的位置是通过如下方式来标识的：以 XAML 的根元素的 `x:Class` 特性形式指定一个命名空间和类。  
  
 在目前已介绍的示例中，您已看到几个按钮，但还没有一个按钮具有任何关联的逻辑行为。  为对象元素添加行为的主要应用程序级机制是使用元素类的现有事件，并为在运行时引发该事件时调用的该事件编写特定的处理程序。  事件名称以及要使用的处理程序的名称在标记中指定，而实现处理程序的代码在代码隐藏中定义。  
  
 [!code-xml[XAMLOvwSupport#ButtonWithCodeBehind](../../../../samples/snippets/csharp/VS_Snippets_Wpf/XAMLOvwSupport/CSharp/page3.xaml#buttonwithcodebehind)]  
  
 [!code-csharp[XAMLOvwSupport#ButtonWithCodeBehindHandler](../../../../samples/snippets/csharp/VS_Snippets_Wpf/XAMLOvwSupport/CSharp/page3.xaml.cs#buttonwithcodebehindhandler)]
 [!code-vb[XAMLOvwSupport#ButtonWithCodeBehindHandler](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/XAMLOvwSupport/VisualBasic/Page1.xaml.vb#buttonwithcodebehindhandler)]  
  
 请注意，代码隐藏文件使用 CLR 命名空间 `ExampleNamespace` 并将 `ExamplePage` 声明为该命名空间内的一个分部类。  这相当于在标记根中提供的 `ExampleNamespace`.`ExamplePage` 的 `x:Class` 特性值。  WPF 标记编译器将通过从根元素类型派生一个类，为编译的任何 XAML 文件创建一个分部类。  当您提供也会定义同一分部类的代码隐藏时，将在与编译的应用程序相同的命名空间和类中组合生成的代码。  
  
 有关 WPF 中代码隐藏编程要求的更多信息，请参见[WPF 中的代码隐藏和 XAML](../../../../docs/framework/wpf/advanced/code-behind-and-xaml-in-wpf.md) 中的“代码隐藏、事件处理程序和分部类要求”一节。  
  
 如果您不想创建一个单独的代码隐藏文件，还可以将代码内联到 XAML 文件中。  但是，内联代码是一种缺少多样性的方法，有很多的限制。  有关详细信息，请参见[WPF 中的代码隐藏和 XAML](../../../../docs/framework/wpf/advanced/code-behind-and-xaml-in-wpf.md)。  
  
### 路由事件  
 [路由事件](GTMT)是一个特殊的事件功能，该功能是 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 的基础。  路由事件使一个元素可以处理另一个元素引发的事件，前提是这些元素通过树关系连接在一起。  使用 XAML 特性指定事件处理时，可以对任何元素（包括未在类成员表中列出路由事件的元素）侦听和处理该路由事件。  这是通过以所属类名限定事件名特性来实现的。  例如，在当前所讨论的 `StackPanel` \/ `Button` 示例中，父 `StackPanel` 可以通过在 `StackPanel` 对象元素上指定特性 `Button.Click`，并使用处理程序名作为特性值，为子元素按钮的 <xref:System.Windows.Controls.Primitives.ButtonBase.Click> 事件注册一个处理程序。  有关路由事件如何工作的更多信息，请参见[路由事件概述](../../../../docs/framework/wpf/advanced/routed-events-overview.md)。  
  
<a name="x_name_and_xaml_named_elements"></a>   
## XAML 命名元素  
 默认情况下，通过处理 XAML 对象元素在对象图中创建的对象实例没有唯一标识符或对象引用。  相反，如果在代码中调用构造函数，则几乎总是使用构造函数结果为构造的实例设置一个变量，以便以后在代码中引用该实例。  为了对通过标记定义创建的对象提供标准化访问，XAML 定义了 [x:Name 特性](../../../../docs/framework/xaml-services/x-name-directive.md)。  您可以在任何对象元素上设置 `x:Name` 特性的值。  在代码隐藏中，您选择的标识符等效于引用所构造的实例的实例变量。  在任何方面，命名元素都像它们是对象实例一样工作（此名称引用该实例），并且代码隐藏可以引用该命名元素来处理应用程序内的运行时交互。  实例和变量之间的这种连接是由 WPF XAML 标记编译器实现的，并且更具体涉及到功能和模式，例如本主题中将不详细讨论的 <xref:System.Windows.Markup.IComponentConnector.InitializeComponent%2A>。  
  
 [WPF 框架级](GTMT) XAML 元素继承 <xref:System.Windows.FrameworkElement.Name%2A> 属性，该属性等效于 XAML 定义的 `x:Name` 特性。  其他某些类也为 `x:Name`（通常也定义为 `Name` 属性）提供属性级等效项。  一般而言，如果您在所选元素\/类型的成员表中找不到 `Name` 属性，则可以改用 `x:Name`。  `x:Name` 值将通过特定子系统或通过诸如 <xref:System.Windows.FrameworkElement.FindName%2A> 等实用工具方法，为可在运行时使用的 XAML 元素提供标识符。  
  
 下面的示例在 <xref:System.Windows.Controls.StackPanel> 元素上设置 <xref:System.Windows.FrameworkElement.Name%2A>。  然后，该 <xref:System.Windows.Controls.StackPanel> 中的 <xref:System.Windows.Controls.Button> 上的处理程序通过由 <xref:System.Windows.FrameworkElement.Name%2A> 设置的实例引用 `buttonContainer` 来引用 <xref:System.Windows.Controls.StackPanel>。  
  
 [!code-xml[XAMLOvwSupport#NamedE](../../../../samples/snippets/csharp/VS_Snippets_Wpf/XAMLOvwSupport/CSharp/page7.xaml#namede)]  
[!code-xml[XAMLOvwSupport#NamedE2](../../../../samples/snippets/csharp/VS_Snippets_Wpf/XAMLOvwSupport/CSharp/page7.xaml#namede2)]  
  
 [!code-csharp[XAMLOvwSupport#NameCode](../../../../samples/snippets/csharp/VS_Snippets_Wpf/XAMLOvwSupport/CSharp/page7.xaml.cs#namecode)]
 [!code-vb[XAMLOvwSupport#NameCode](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/XAMLOvwSupport/VisualBasic/Page1.xaml.vb#namecode)]  
  
 就像变量一样，实例的 XAML 名称受范围概念的控制，因此可以在可预测的某个范围内强制名称唯一。  定义页面的主标记表示一个唯一的 XAML 名称范围，而该 XAML 名称范围的边界就是该页面的根元素。  但是，其他标记源（如样式或样式中的模板）可以在运行时与页面交互，这种标记源常常具有自己的 XAML 名称范围，这些名称范围不一定与页面的 XAML 名称范围相关联。  有关 `x:Name` 和 XAML 名称范围的更多信息，请参见 <xref:System.Windows.FrameworkElement.Name%2A>、[x:Name 指令](../../../../docs/framework/xaml-services/x-name-directive.md) 或 [WPF XAML 名称范围](../../../../docs/framework/wpf/advanced/wpf-xaml-namescopes.md)。  
  
<a name="attached_properties_and_attached_events"></a>   
## 附加属性和附加事件  
 XAML 指定了一个语言功能，该功能允许对任何元素指定某些属性或事件，而不管要设置属性或事件的元素的类型定义中是否存在该属性或事件。  该功能的属性版本称为[附加属性](GTMT)，事件版本称为[附加事件](GTMT)。  从概念上讲，可以将附加属性和附加事件视为可以在任何 XAML 元素\/对象实例上设置的全局成员。  但是，元素\/类或更大的基础结构必须支持附加值的后备属性存储。  
  
 通常通过特性语法来使用 XAML 中的附加属性。  在特性语法中，您可以采用“*所有者类型*.*属性名*”的形式指定附加属性。  
  
 表面上，这与属性元素用法类似，但在这种情况下，您指定的“*所有者类型*”始终是一种与从中要设置附加属性的对象元素不同的类型。  “*所有者类型*”这种类型提供 XAML 处理器为获取或设置附加属性值所需要的访问器方法。  
  
 使用附加属性的最常见方案是使子元素能够向其父元素报告属性值。  
  
 下面的示例演示了 <xref:System.Windows.Controls.DockPanel.Dock%2A?displayProperty=fullName> 附加属性。  <xref:System.Windows.Controls.DockPanel> 类为 <xref:System.Windows.Controls.DockPanel.Dock%2A?displayProperty=fullName> 定义访问器，因此拥有附加属性。  <xref:System.Windows.Controls.DockPanel> 类还包括一个逻辑，该逻辑迭代其子元素并具体检查每个元素是否具有 <xref:System.Windows.Controls.DockPanel.Dock%2A?displayProperty=fullName> 设置值。  如果找到一个值，将在布局过程中使用该值定位子元素。  使用 <xref:System.Windows.Controls.DockPanel.Dock%2A?displayProperty=fullName> 附加属性和这种定位功能事实上是 <xref:System.Windows.Controls.DockPanel> 类的激动人心的一面。  
  
 [!code-xml[XAMLOvwSupport#DockAP](../../../../samples/snippets/csharp/VS_Snippets_Wpf/XAMLOvwSupport/CSharp/page8.xaml#dockap)]  
  
 在 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 中，大部分或所有附加属性还作为[依赖项属性](GTMT)来实现。  有关详细信息，请参见[附加属性概述](../../../../docs/framework/wpf/advanced/attached-properties-overview.md)。  
  
 附加事件使用类似的“*所有者类型*.*事件名*”特性语法形式。  就像非附加事件一样，XAML 中的附加事件的特性值指定对元素处理事件时调用的处理程序方法的名称。  在 WPF XAML 中使用附加事件并不常见。  有关更多信息，请参见[附加事件概述](../../../../docs/framework/wpf/advanced/attached-events-overview.md)。  
  
<a name="base_classes_and_xaml"></a>   
## 基类型和 XAML  
 基础 WPF XAML 及其 XAML 命名空间是类型的一个集合，这些类型对应于 [!INCLUDE[TLA2#tla_clr](../../../../includes/tla2sharptla-clr-md.md)] 对象以及 XAML 的标记元素。  但是，并不是所有的类都能映射到元素。  抽象类（如 <xref:System.Windows.Controls.Primitives.ButtonBase>）和某些非抽象基类在 [!INCLUDE[TLA2#tla_clr](../../../../includes/tla2sharptla-clr-md.md)] 对象模型中用于继承。  基类（包括抽象类）对于 XAML 开发仍然很重要，因为每个具体的 XAML 元素都从其层次结构中的某个基类继承成员。  通常，这些成员包括可以设置为元素特性的属性或者可以处理的事件。  <xref:System.Windows.FrameworkElement> 是 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 在 [WPF 框架级](GTMT)的具体 [!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)] 基类。  设计 [!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)] 时，您将使用各种形状、面板、修饰器或控件类，它们全部从 <xref:System.Windows.FrameworkElement> 派生而来。  有一个相关的基类 <xref:System.Windows.FrameworkContentElement>，它使用可在 <xref:System.Windows.FrameworkElement> 中特意镜像 [!INCLUDE[TLA2#tla_api#plural](../../../../includes/tla2sharptla-apisharpplural-md.md)] 的 [!INCLUDE[TLA2#tla_api#plural](../../../../includes/tla2sharptla-apisharpplural-md.md)]，支持适合流布局表示形式的面向文档的元素。  元素级的特性和 [!INCLUDE[TLA2#tla_clr](../../../../includes/tla2sharptla-clr-md.md)] 对象模型的组合提供了一组通用的属性，这些属性可以在大多数具体的 XAML 元素上设置，而不管具体的 XAML 元素类型及其基础类型是什么。  
  
<a name="xaml_security"></a>   
## XAML 安全性  
 XAML 是一种直接表示对象实例化和执行的标记语言。  因此，在 XAML 中创建的元素能够像等效的生成代码那样与系统资源（如网络访问、文件系统 IO）进行交互。  
  
 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 支持 [!INCLUDE[net_v40_short](../../../../includes/net-v40-short-md.md)] 安全框架[!INCLUDE[TLA#tla_cas](../../../../includes/tlasharptla-cas-md.md)]。  这意味着在 Internet 区域中运行的 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 内容具有更少的执行权限。"  “宽松 XAML”（由 XAML 查看器在加载时解释的非编译 XAML 的页面）和 [!INCLUDE[TLA#tla_xbap](../../../../includes/tlasharptla-xbap-md.md)] 通常在此 Internet 区域中运行，并且使用相同的权限集。  但是，加载到完全受信任的应用程序中的 XAML 与承载应用程序具有相同的系统资源访问权限。  有关更多信息，请参见 [WPF 部分信任安全](../../../../docs/framework/wpf/wpf-partial-trust-security.md)。  
  
<a name="loading_xaml_from_code"></a>   
## 从代码中加载 XAML  
 XAML 可用于定义整个 UI，但有时也适合在 XAML 中定义 UI 的一部分。  此功能可用于实现部分自定义，在本地存储信息，使用 XAML 提供业务对象或者各种可能的方案。  这些方案的关键是 <xref:System.Windows.Markup.XamlReader> 类及其 <xref:System.Windows.Markup.XamlReader.Load%2A> 方法。  输入是一个 XAML 文件，而输出是一个对象，表示从该标记创建的整个运行时对象树。  然后您可以插入该对象，作为应用程序中已存在的另一个对象的属性。  只要该属性在具有最终显示功能并且将通知执行引擎已向应用程序中添加新内容的内容模型中是一个合适的属性，就可以通过载入 XAML 非常轻松地修改正在运行的应用程序的内容。  请注意，通常只在完全受信任的应用程序中使用此功能，因为将文件加载到正在运行的应用程序中会带来明显的安全隐患。  
  
<a name="whats_next"></a>   
## 接下来的内容  
 本主题简单介绍了适用于 WPF 的 XAML 语法概念和术语。  有关本文使用的术语的更多信息，请参见 [XAML 语法详述](../../../../docs/framework/wpf/advanced/xaml-syntax-in-detail.md)。  
  
 如果尚未做过 [演练：开始使用 WPF](../../../../docs/framework/wpf/getting-started/walkthrough-my-first-wpf-desktop-application.md)教程主题中的练习，请试做。  当您创建该教程中介绍的以标记为中心的应用程序时，其中的练习将帮助您巩固本主题中介绍的许多概念。  
  
 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 使用一个特定的应用程序模型，该模型基于 <xref:System.Windows.Application> 类。  有关详细信息，请参见[应用程序管理概述](../../../../docs/framework/wpf/app-development/application-management-overview.md)。  
  
 [生成 WPF 应用程序](../../../../docs/framework/wpf/app-development/building-a-wpf-application-wpf.md) 为您详细介绍了如何通过命令行以及使用 [!INCLUDE[TLA#tla_visualstu](../../../../includes/tlasharptla-visualstu-md.md)] 生成包含 XAML 的应用程序。  
  
 [依赖项属性概述](../../../../docs/framework/wpf/advanced/dependency-properties-overview.md)详细介绍了 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 中属性的多样性，并介绍了[依赖项属性](GTMT)的概念。  
  
## 请参阅  
 [XAML 语法详述](../../../../docs/framework/wpf/advanced/xaml-syntax-in-detail.md)   
 [XAML 及 WPF 的自定义类](../../../../docs/framework/wpf/advanced/xaml-and-custom-classes-for-wpf.md)   
 [XAML 命名空间 \(x:\) 语言功能](../../../../docs/framework/xaml-services/xaml-namespace-x-language-features.md)   
 [WPF XAML 扩展](../../../../docs/framework/wpf/advanced/wpf-xaml-extensions.md)   
 [基元素概述](../../../../docs/framework/wpf/advanced/base-elements-overview.md)   
 [WPF 中的树](../../../../docs/framework/wpf/advanced/trees-in-wpf.md)