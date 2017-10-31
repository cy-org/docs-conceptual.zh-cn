---
title: "标记扩展和 WPF XAML | Microsoft Docs"
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
  - "*扩展类"
  - "绑定标记扩展"
  - "大括号字符"
  - "字符, 大括号"
  - "类, MarkupExtension"
  - "大括号字符 ({})"
  - "DynamicResource 标记扩展"
  - "文本大括号字符 ({})"
  - "标记扩展"
  - "MarkupExtension 类"
  - "嵌套扩展语法"
  - "RelativeSource 标记扩展"
  - "StaticResource 标记扩展"
  - "TemplateBinding 标记扩展"
  - "XAML, 标记扩展"
ms.assetid: 618dc745-8b14-4886-833f-486d2254bb78
caps.latest.revision: 26
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 23
---
# 标记扩展和 WPF XAML
本主题介绍 XAML 的标记扩展概念，包括其语法规则、用途以及底层的类对象模型。  标记扩展是 XAML 语言以及 XAML 服务的 .NET 实现的常规功能。  本主题专门详细论述了用于 WPF XAML 的标记扩展。  
  
   
  
<a name="XAML_Processors_and_Markup_Extensions"></a>   
## XAML 处理器和标记扩展  
 通常，XAML 分析器可将特性值解释为可转换成基元的文本字符串，或可通过某种方法将特性值转换为对象。  其中一种方法是引用类型转换器；详情请参见主题 [TypeConverters 和 XAML](../../../../docs/framework/wpf/advanced/typeconverters-and-xaml.md)。  不过，也存在要求其他行为的情况。  例如，可以指示 XAML 处理器，特性的值不应在对象图中生成新对象。  特性应生成引用对象图另一部分中的已构造对象或引用静态对象的对象图。  另一种情况是，可以指示 XAML 处理器使用向对象构造函数提供非默认参数的语法。在这些类型的情况中，标记扩展可以提供解决方案。  
  
<a name="Basic_Markup_Extension_Syntax"></a>   
## 基本标记扩展语法  
 可以实现标记扩展以便为特性用法中的属性和\/或属性元素用法中的属性提供值。  
  
 当用于提供特性值时，将标记扩展序列与 XAML 处理器区分开的语法就是左右大括号（{ 和 }）。  然后，由紧跟在左大括号后面的字符串标记来标识标记扩展的类型。  
  
 当用在属性元素语法中时，标记扩展在外观上与其他任何用于提供属性元素值的元素相同，即：一个将标记扩展类作为一个元素引用并以尖括号 \(\<\>\) 括起的 XAML 元素声明。  
  
<a name="XAML_Defined_Markup_Extensions"></a>   
## XAML 定义的标记扩展  
 有几个标记扩展并非是 XAML 的 WPF 实现所特有的，而是语言形式的 XAML 的内部函数或功能实现。  这些标记扩展在 System.Xaml 程序集中作为常规 .NET Framework XAML 服务的一部分而实现，并且位于 XAML 语言 XAML 命名空间中。  就常见标记用法而言，这些标记扩展通常可由用法中的 `x:` 前缀标识。  <xref:System.Windows.Markup.MarkupExtension> 基类（也在 System.Xaml 中定义）提供了所有标记扩展均应使用的模式，以便在 XAML 读取器和 XAML 编写器中得到支持（包括在 WPF XAML 中得到支持）。  
  
-   `x:Type` 为命名类型提供 <xref:System.Type> 对象。  此工具最常用于样式和模板。  有关详细信息，请参见 [x:Type 标记扩展](../../../../docs/framework/xaml-services/x-type-markup-extension.md)。  
  
-   `x:Static` 生成静态值。  这些值来自不直接是目标属性值的类型、但可以计算为该类型的值类型代码实体。  有关详细信息，请参见 [x:Static 标记扩展](../../../../docs/framework/xaml-services/x-static-markup-extension.md)。  
  
-   `x:Null` 将 `null` 指定为属性的值，可用于特性或属性元素值。  有关详细信息，请参见 [x:Null 标记扩展](../../../../docs/framework/xaml-services/x-null-markup-extension.md)。  
  
-   在特意不使用 WPF 基元素和控件模型提供的集合支持的情况下，`x:Array` 为 XAML 语法中常规数组的创建提供支持。  有关详细信息，请参见 [x:Array 标记扩展](../../../../docs/framework/xaml-services/x-array-markup-extension.md)。  
  
> [!NOTE]
>  `x:` 前缀在 XAML 文件或生产的根元素中用于 XAML 语言内部函数的典型 XAML 命名空间映射。  例如，WPF 应用程序的 [!INCLUDE[vs_current_short](../../../../includes/vs-current-short-md.md)] 模板会使用此 `x:` 映射启动 XAML 文件。  您可以在自己的 XAML 命名空间映射中选择不同的前缀标记，但本文档将采用默认的 `x:` 映射，并通过它来标识属于 XAML 语言的 XAML 命名空间已定义部分的那些实体，这与 WPF 默认命名空间或与特定框架不相关的其他 XAML 命名空间相反。  
  
<a name="WPF_Specific_Markup_Extensions"></a>   
## 特定于 WPF 的标记扩展  
 WPF 编程中最常用的标记扩展是支持资源引用的标记扩展（`StaticResource` 和 `DynamicResource`）以及支持数据绑定的标记扩展 \(`Binding`\)。  
  
-   `StaticResource` 通过替换已定义资源的值来为属性提供值。  `StaticResource` 计算最终在 XAML 加载时进行，并且在运行时没有访问对象图的权限。有关详细信息，请参见 [StaticResource 标记扩展](../../../../docs/framework/wpf/advanced/staticresource-markup-extension.md)。  
  
-   `DynamicResource` 通过将值推迟为对资源的运行时引用来为属性提供值。  动态资源引用强制在每次访问此类资源时都进行新查找，并在运行时有权访问对象图。  为了获取此访问权限，WPF 属性系统中的依赖项属性和计算出的表达式支持 `DynamicResource` 概念。  因此，对于依赖项属性目标，您只能使用 `DynamicResource`。  有关详细信息，请参见 [DynamicResource 标记扩展](../../../../docs/framework/wpf/advanced/dynamicresource-markup-extension.md)。  
  
-   `Binding` 使用在运行时应用于父对象的数据上下文来为属性提供数据绑定值。  此标记扩展相对复杂，因为它会启用大量内联语法来指定数据绑定。  有关详细信息，请参见 [绑定标记扩展](../../../../docs/framework/wpf/advanced/binding-markup-extension.md)。  
  
-   `RelativeSource` 为可以在运行时对象树中定位若干可能关系的 <xref:System.Windows.Data.Binding> 提供源信息。  对于在多用途模板中创建的绑定，或在未充分了解周围的对象树的情况下以代码创建的绑定，上述标记扩展会提供专用源。  有关详细信息，请参见 [RelativeSource MarkupExtension](../../../../docs/framework/wpf/advanced/relativesource-markupextension.md)。  
  
-   通过 `TemplateBinding`，控件模板可以使用来自要利用该模板的类的对象模型定义属性中的模板化属性的值。  换言之，模板定义中的属性可访问仅在应用了模板之后才存在的上下文。  有关详细信息，请参见 [TemplateBinding 标记扩展](../../../../docs/framework/wpf/advanced/templatebinding-markup-extension.md)。  有关 `TemplateBinding` 的实际使用的更多信息，请参见 [Styling with ControlTemplates Sample](http://go.microsoft.com/fwlink/?LinkID=160041)（使用 ControlTemplates 设置样式的示例）。  
  
-   `ColorConvertedBitmap` 支持相对高级的映像方案。  有关详细信息，请参见 [ColorConvertedBitmap 标记扩展](../../../../docs/framework/wpf/advanced/colorconvertedbitmap-markup-extension.md)。  
  
-   `ComponentResourceKey` 和 `ThemeDictionary` 支持资源查找的各个方面，特别是支持查找与自定义控件打包在一起的资源和主题。  有关更多信息，请参见[ComponentResourceKey 标记扩展](../../../../docs/framework/wpf/advanced/componentresourcekey-markup-extension.md)、[ThemeDictionary 标记扩展](../../../../docs/framework/wpf/advanced/themedictionary-markup-extension.md)或 [控件创作概述](../../../../docs/framework/wpf/controls/control-authoring-overview.md)。  
  
<a name="StarExtension"></a>   
## \*Extension 类  
 对于常规 XAML 语言和特定于 WPF 的标记扩展，每个标记扩展的行为都会通过从 <xref:System.Windows.Markup.MarkupExtension> 派生的 `*Extension` 类通知给 XAML 处理器，并提供 <xref:System.Windows.Markup.StaticExtension.ProvideValue%2A> 方法的实现。  每个扩展上的此方法都会提供在计算标记扩展时返回的对象。  通常会基于传递给标记扩展的各个字符串标记来计算返回的对象。  
  
 例如，<xref:System.Windows.StaticResourceExtension> 类提供实际资源查找的图面实现，以便其 <xref:System.Windows.Markup.MarkupExtension.ProvideValue%2A> 实现返回请求的对象，该特定实现的输入是用于按其 `x:Key` 查找资源的字符串。  如果您使用的是现有标记扩展，则其中的大部分实现详细信息都无关紧要。  
  
 某些标记扩展不使用字符串标记参数。  这是因为它们会返回静态值或一致的值，或者因为可通过使用 `serviceProvider` 参数传递的服务之一来获得应返回何种值的上下文。  
  
 提供 `*Extension` 命名模式的目的是为了获得便捷性和一致性。  XAML 处理器不必将该类标识为支持标记扩展。  只要基本代码包含 System.Xaml 并使用 .NET Framework XAML 服务实现，所有需要识别为 XAML 标记扩展的内容就都会从 <xref:System.Windows.Markup.MarkupExtension> 派生并支持构造语法。  WPF 定义的启用标记扩展的类不遵循 `*Extension` 命名模式，例如 <xref:System.Windows.Data.Binding>。  原因通常是该类支持纯标记扩展支持以外的方案。  对于 <xref:System.Windows.Data.Binding>，该类支持针对与 XAML 无关的方案在运行时访问对象的方法和属性。  
  
### 初始化文本的扩展类解释  
 跟在标记扩展名称后面且仍在括号内的字符串标记由 XAML 处理器通过以下方式之一解释：  
  
-   逗号始终代表各个标记的分隔符。  
  
-   如果各个分隔的标记不包含任何等号，则每个标记都将被视为构造函数参数。  每个构造函数参数都必须按该签名所期望的类型给出，并按照该签名所期望的顺序排列。  
  
    > [!NOTE]
    >  XAML 处理器必须调用与对的数量这一参数计数匹配的构造函数。  因此，如果要实现自定义标记扩展，请不要提供具有相同实参计数的多个形参。  XAML 处理器在多个标记扩展构造函数路径具有相同数量的参数时的行为方式尚未定义，但您应预计到如果这种情况存在于标记扩展类型定义中，则会允许 XAML 处理器引发有关使用情况的异常。  
  
-   如果各个分隔的标记包含等号，则 XAML 处理器会首先为标记扩展调用默认构造函数。  之后，每个“名称\=值”对都会被解释为标记扩展上存在的属性名称以及赋给该属性的值。  
  
-   如果在标记扩展中的构造函数行为与属性设置行为之间存在并行结果，则您使用哪个行为都无关紧要。  较常见的用法是将“*属性*`=`*值*”对用于具有多个可设置属性的标记扩展，因为这可令您的标记意图性更强，并减小意外转置构造函数参数的可能性。  （当指定“属性\=值”对时，这些属性可以为任意顺序。）另外，无法保证标记扩展提供设置每个可设置属性的构造函数参数。  例如，<xref:System.Windows.Data.Binding> 是一个标记扩展，具有多个可以通过“*属性*`=`*值*”形式的扩展来设置的属性，但 <xref:System.Windows.Data.Binding> 仅支持两个构造函数，即默认构造函数和一个设置初始路径的构造函数。  
  
-   文本逗号在未转义的情况下无法传递给标记扩展。  
  
<a name="EscapeSequences"></a>   
## 转义序列和标记扩展  
 XAML 处理器中的特性处理使用大括号作为标记扩展序列的指示符。  必要时，还可以使用后面跟文本大括号的空大括号对来输入转义序列，从而生成文本大括号字符特性值。  请参见 [{} 转义序列\/标记扩展](../../../../docs/framework/xaml-services/escape-sequence-markup-extension.md)。  
  
<a name="Nesting"></a>   
## XAML 用法中的嵌套标记扩展  
 支持多个标记扩展的嵌套，并且将首先计算每个标记扩展的最里层。  例如，考虑下面的用法：  
  
```  
<Setter Property="Background"  
  Value="{DynamicResource {x:Static SystemColors.ControlBrushKey}}" />  
  
```  
  
 在此用法中，`x:Static` 语句将首先计算并返回字符串。  该字符串随后用作 `DynamicResource` 的参数。  
  
## 标记扩展和属性元素语法  
 当用作填写属性元素值的对象元素时，标记扩展类在外观上与可用在 XAML 中的典型基于类型的对象元素没有区别。  典型对象元素与标记扩展之间的实际差异是，标记扩展计算为类型化值或延迟为表达式。  因此，标记扩展的属性值的任何可能类型错误的机制都将是不同的，这与后期绑定属性在其他编程模型中的处理方式类似。  将针对分析 XAML 时设置的目标属性，为类型匹配来计算普通对象元素。  
  
 当用在对象元素语法中以填充属性元素时，大部分标记扩展都不会包含内容或任何进一步的属性元素语法。  这样您就可以关闭对象元素标记，而不提供任何子元素。  不论何时 XAML 处理器遇到任何对象元素，都会调用该类的构造函数来实例化从已分析元素创建的对象。  标记扩展类也一样：如果您希望自己的标记扩展可在对象元素语法中使用，就必须提供默认构造函数。  有些现有标记扩展至少具有一个必需属性值，为了使初始化有效，必须指定该属性值。  如果是这样，通常会将该属性值作为对象元素的属性特性来指定。  在 [XAML 命名空间 \(x:\) 语言功能](../../../../docs/framework/xaml-services/xaml-namespace-x-language-features.md)和 [WPF XAML 扩展](../../../../docs/framework/wpf/advanced/wpf-xaml-extensions.md)参考页中，将指出具有必需属性的标记扩展（以及必需属性的名称）。  参考页还将指出特定标记扩展是否禁止使用对象元素语法或特性语法。  一个值得注意的情况是 [x:Array 标记扩展](../../../../docs/framework/xaml-services/x-array-markup-extension.md)，它无法支持特性语法，因为该数组的内容必须指定为标记中的内容。  数组内容的处理方式与常规对象一样，因此特性可以没有默认的类型转换器。  另外，[x:Array 标记扩展](../../../../docs/framework/xaml-services/x-array-markup-extension.md)需要 `type` 参数。  
  
## 请参阅  
 [XAML 概述 \(WPF\)](../../../../docs/framework/wpf/advanced/xaml-overview-wpf.md)   
 [XAML 命名空间 \(x:\) 语言功能](../../../../docs/framework/xaml-services/xaml-namespace-x-language-features.md)   
 [WPF XAML 扩展](../../../../docs/framework/wpf/advanced/wpf-xaml-extensions.md)   
 [StaticResource 标记扩展](../../../../docs/framework/wpf/advanced/staticresource-markup-extension.md)   
 [绑定标记扩展](../../../../docs/framework/wpf/advanced/binding-markup-extension.md)   
 [DynamicResource 标记扩展](../../../../docs/framework/wpf/advanced/dynamicresource-markup-extension.md)   
 [x:Type 标记扩展](../../../../docs/framework/xaml-services/x-type-markup-extension.md)