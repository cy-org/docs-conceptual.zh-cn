---
title: "XAML 语法详述 | Microsoft Docs"
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
  - "XML 命名空间"
  - "XAML 中，特性分析"
  - "特性分析"
  - "XAML 中，标记扩展"
  - "附加属性"
  - "标记语法 [XAML]"
  - "标记扩展"
  - "XAML 对象元素语法"
  - "XAML 中，语法术语"
  - "附加事件"
  - "查找语义"
  - "XAML 中，附加事件"
  - "XAML 中，内容语法"
  - "XAML 中，查找语义"
  - "内容语法"
  - "对象元素语法"
  - "语法术语 [XAML]"
  - "XAML 中，附加属性"
  - "特性 [XAML] 分析"
  - "XAML 中，标记语法"
  - "XAML 中，特性语法"
  - "属性元素语法"
  - "术语 [XAML]"
  - "命名空间的 XML"
  - "特性语法 [XAML]"
  - "XAML 属性元素语法"
ms.assetid: 67cce290-ca26-4c41-a797-b68aabc45479
caps.latest.revision: 26
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 26
---
# XAML 语法详述
本主题定义用于描述 XAML 语法的各个元素的术语。 这些条款本文档中，同时用于 WPF 文档的其余专门和其他使用 XAML 或由 XAML 语言支持 System.Xaml 级别启用的基本 XAML 概念的框架经常使用。 本主题扩展了该主题中引入的基本术语[XAML 概述 (WPF)](../../../../docs/framework/wpf/advanced/xaml-overview-wpf.md)。  
  

  
<a name="the_xaml_language_specification"></a>   
## <a name="the-xaml-language-specification"></a>XAML 语言规范  
 此处定义的 XAML 语法术语还定义或在 XAML 语言规范中引用。 XAML 是一种基于 XML 的语言并遵循或 XML 结构规则进行了扩展。 某些术语从共享或基于常用情况是描述 XML 语言或 XML 文档对象模型的术语。  
  
 有关 XAML 语言规范的详细信息，请下载[ \[MS-XAML\] ](http://go.microsoft.com/fwlink/?LinkId=114525)从 Microsoft 下载中心获得。  
  
<a name="xaml_and_clr"></a>   
## <a name="xaml-and-clr"></a>XAML 和 CLR  
 XAML 是一种标记语言。 [!INCLUDE[TLA#tla_clr](../../../../includes/tlasharptla-clr-md.md)]、 按其名称，启用运行时执行暗示的保证。 XAML 是不本身直接由 CLR 运行时的常见语言之一。 相反，您可以将 XAML 视为支持其自己的类型系统。 WPF 使用特定 XAML 分析系统构建在 CLR 和 CLR 类型系统。 XAML 类型映射到 CLR 类型时要实例化的运行的时表示为 WPF XAML 进行解析。 出于此原因，本文档中讨论的其余部分将包含对 CLR 类型系统中，引用，即使在 XAML 语言规范中的等效的语法讨论不这样做也是如此。 （每 XAML 语言规范级别，XAML 类型可以映射到任何其他类型的系统，它不必是 CLR，但这需要创建和使用不同的 XAML 分析器。）  
  
#### <a name="members-of-types-and-class-inheritance"></a>类型和类继承的成员  
 属性和事件时出现的 XAML 成员[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]类型通常继承自基类型。 例如，请看以下示例︰ `<Button Background="Blue" .../>`。 <xref:System.Windows.Controls.Control.Background%2A>属性不是立即声明的属性上<xref:System.Windows.Controls.Button>类，如果您要查看类定义、 反射结果或文档。 相反，<xref:System.Windows.Controls.Control.Background%2A>从基类继承<xref:System.Windows.Controls.Control>类。  
  
 类继承行为的[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]XAML 元素是大的不同之处，从 XML 标记的架构上强制实施的解释。 类继承可能非常复杂，特别是当中间基类为抽象类，或当涉及到接口。 这是一个难以代表准确而完整地使用架构类型的 XAML 元素和其允许的属性集，则通常用于原因[!INCLUDE[TLA2#tla_xml](../../../../includes/tla2sharptla-xml-md.md)]编程详细信息，如 DTD 或 XSD 格式。 另一个原因是可扩展性和 XAML 语言本身的类型映射功能阻止的任何固定表示形式的允许的类型和成员的完整性。  
  
<a name="object_element_syntax"></a>   
## <a name="object-element-syntax"></a>对象元素语法  
 *对象元素语法*是通过声明一个 XML 元素中实例化 CLR 类或结构的 XAML 标记语法。 此语法类似于 HTML 等其他标记语言的元素语法。 对象元素语法开头左的尖括号 （\<), followed immediately by the type name of the class or structure being instantiated. followed="" immediately="" by="" the="" type="" name="" of="" the="" class="" or="" structure="" being="">\</), followed immediately by the type name of the class or structure being instantiated.> 类型名称，后面可以有零个或多个空格和零个或多个属性还可以声明 object 元素，并用一个或多个空格来分隔每个特性名称 ="值"对。 最后，必须是以下项之一，则返回 true:  
  
-   由正斜杠 （/） 后紧跟右尖括号 (>)，必须关闭的元素和标记。  
  
-   必须是右尖括号 (>) 完成的开始标记。 其他对象元素、 属性元素或内部文本，可以按照开始标记。 可能会在此处包含哪些内容的确切通常会受到该元素的对象模型。 Object 元素的结束标记的等效项也必须存在，但在正确的嵌套，并与其他开始和结束标记对平衡。  
  
 由.NET 实现的 XAML 具有一组映射到类型，为属性或事件，以及 XAML 命名空间到 CLR 命名空间和程序集的属性的对象元素的规则。 对于 WPF 和.NET Framework 中，XAML 对象元素映射到[!INCLUDE[TLA#tla_net](../../../../includes/tlasharptla-net-md.md)]中定义的类型引用的程序集，并将属性映射到这些类型的成员。 在引用 XAML 中的 CLR 类型时，您有权访问该类型的继承成员。  
  
 例如，下面的示例是实例化的新实例的对象元素语法<xref:System.Windows.Controls.Button>类，并且还指定<xref:System.Windows.FrameworkElement.Name%2A>属性和该属性的值︰  
  
 [!code-xml[XAMLOvwSupport#SyntaxOE](../../../../samples/snippets/csharp/VS_Snippets_Wpf/XAMLOvwSupport/CSharp/Page1.xaml#syntaxoe)]  
  
 下面的示例是对象元素语法，它还包括 XAML 内容属性语法。 中包含的内部文本将用于设置<xref:System.Windows.Controls.TextBox> XAML 内容属性<xref:System.Windows.Controls.TextBox.Text%2A>。  
  
 [!code-xml[XAMLOvwSupport#ThisIsATextBox](../../../../samples/snippets/csharp/VS_Snippets_Wpf/XAMLOvwSupport/CSharp/Page1.xaml#thisisatextbox)]  
  
### <a name="content-models"></a>内容模型  
 一个类可能作为 XAML 对象元素语法中，根据支持一种用法，但该元素将仅在中正常工作的应用程序或页放在一个整体内容模型或元素树的预期位置。 例如， <xref:System.Windows.Controls.MenuItem>通常只能放置作为的子级<xref:System.Windows.Controls.Primitives.MenuBase>派生类，例如<xref:System.Windows.Controls.Menu>。 内容模型的特定元素编写为的类的控件和其他页上备注一部分[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]可作为 XAML 元素的类。  
  
<a name="properties_of_object_elements"></a>   
## <a name="properties-of-object-elements"></a>对象元素的属性  
 设置的各种可能的语法的在 XAML 中的属性。 根据您正在设置的属性的基础类型系统特征，可以为特定属性使用哪种语法会有所不同。  
  
 通过设置属性的值，您添加功能或特性对对象因为它们存在于运行的时对象图。 从对象元素创建的对象的初始状态取决于默认构造函数行为。 通常情况下，您的应用程序将使用以外的任何给定对象的完全默认实例。  
  
<a name="attribute_syntax_properties"></a>   
## <a name="attribute-syntax-properties"></a>特性语法 （属性）  
 特性语法是通过将属性声明在现有的对象元素上设置属性的值的 XAML 标记语法。 属性名称必须与支持相关对象元素的类的属性的 CLR 成员名称匹配。 属性名称后跟赋值运算符 （=）。 属性值必须是括在引号内的字符串。  
  
> [!NOTE]
>  可以使用替代引号将文本引号在特性中。 对于实例可以作为一种方式使用单引号来声明包含其中的双引号字符的字符串。 是否使用单引号或双引号时，应使用一对匹配用于打开和关闭的属性值字符串。 也有转义序列或其他技术可用于解决规定任何特定 XAML 语法的字符限制。 请参阅[XML 字符实体和 XAML](../../../../docs/framework/xaml-services/xml-character-entities-and-xaml.md)。  
  
 为了通过属性语法进行设置，属性必须是公共的并且必须是可写。 后备类型系统中的属性的值必须是值类型，或者必须引用类型可以实例化或引用由 XAML 处理器，当访问相关的后备类型。  
  
 对于 WPF XAML 事件，属性名称作为引用的事件必须是公共的并具有公共委托。  
  
 属性或事件必须是类或结构，它包含的对象元素通过实例化的成员。  
  
### <a name="processing-of-attribute-values"></a>属性值的处理  
 由 XAML 处理器进行处理的开始和结束引号内包含的字符串值。 对于属性，默认处理行为则取决于基础的 CLR 属性的类型。  
  
 属性值的内容由以下一项，使用此处理顺序︰  
  
1.  如果 XAML 处理器遇到一个大括号或派生自 object 元素<xref:System.Windows.Markup.MarkupExtension>、 然后引用的标记扩展而不是处理为字符串，值首先计算和标记扩展返回的对象用作的值。 在许多情况下返回的标记扩展的对象将对现有对象或表达式，用于将计算推迟到运行时，而不是新实例化的对象的引用。  
  
2.  如果该属性声明与特性化<xref:System.ComponentModel.TypeConverter>，或声明该属性的值类型与特性化<xref:System.ComponentModel.TypeConverter>、 该属性的字符串值提交到用作转换输入的类型转换器和转换器将返回一个新的对象实例。  
  
3.  如果没有任何<xref:System.ComponentModel.TypeConverter>，尝试直接转换为属性类型。 最后一个级别是在 XAML 语言基元类型或检查枚举 （分析器随后将访问匹配的值） 中的已命名常数名称之间的分析器本机值直接转换。  
  
#### <a name="enumeration-attribute-values"></a>枚举属性值  
 XAML 中的枚举由 XAML 分析器处理本质上，并且应通过指定其中一个枚举的已命名常数的字符串名称来指定枚举的成员。  
  
 无标志枚举值，对于本机行为是处理属性值的字符串，并将其解析为枚举值之一。 您不指定格式中的枚举*枚举*。*值*，这一点与您在代码中。 相反，您指定仅*值*，和*枚举*由您设置的属性的类型推断。 如果指定中的一个属性*枚举*。*值*窗体中，它将无法正确解析。  
  
 对于按标志枚举，该行为基于<xref:System.Enum.Parse%2A?displayProperty=fullName>方法。 用逗号分隔每个值，可以指定多个标志的枚举值。 但是，不能合并不按标志的枚举值。 例如，不能使用逗号语法以尝试创建<xref:System.Windows.Trigger>作用于无标志枚举的多个条件︰  
  
```  
<!--This will not compile, because Visibility is not a flagwise enumeration.-->  
...  
<Trigger Property="Visibility" Value="Collapsed,Hidden">  
  <Setter ... />  
</Trigger>  
...  
```  
  
 支持在 XAML 中设置的属性的按标志枚举很少在 WPF 中出现。 但是，这样的一个枚举是<xref:System.Windows.Media.StyleSimulations>。 例如，可以使用以逗号分隔标志特性语法要修改的备注中提供的示例<xref:System.Windows.Documents.Glyphs>类;`StyleSimulations = "BoldSimulation"`可能会变得`StyleSimulations = "BoldSimulation,ItalicSimulation"`。 <xref:System.Windows.Input.KeyBinding.Modifiers%2A?displayProperty=fullName>是另一个属性，可以指定多个枚举值的位置。 但是，此属性恰巧是一种特殊情况，因为<xref:System.Windows.Input.ModifierKeys>枚举支持其自己的类型转换器。 修饰符的类型转换器使用加号 （+） 作为分隔符，而不是逗号 （，）。 此转换支持更传统的语法来表示在 Microsoft Windows 编程中，如"Ctrl + Alt 键的组合键。  
  
### <a name="properties-and-event-member-name-references"></a>属性和事件成员名称引用  
 当指定特性时，可以引用任何属性或作为包含的对象元素对进行实例化 CLR 类型的成员存在的事件。  
  
 或者，可以引用一个附加的属性或附加事件，独立于包含的对象元素。 （下一节讨论是附加的属性）。  
  
 您还可以命名是通过使用可通过默认的命名空间访问的任何对象中的任何事件*typeName*。*事件*部分限定的名称; 这种语法支持附加路由事件的处理程序用于处理子元素，但父元素中的事件路由处理程序还没有该事件在其成员表中。 此语法类似于附加的事件语法，但此处该事件不是真正的附加的事件。 相反，所引用的限定名称的事件。 有关详细信息，请参阅[路由事件概述](../../../../docs/framework/wpf/advanced/routed-events-overview.md)。  
  
 在某些情况下，属性名称有时提供作为一个属性，而不是属性名称的值。 该属性名称还可以包括限定符，例如窗体中指定的属性*所有者类型*。*依赖项属性名称*。 在 XAML 中写入样式或模板时，此方案中很常见。 处理规则的属性值形式提供的属性名称不相同，并且通过所设置的属性的类型或特定 WPF 子系统的行为控制。 有关详细信息，请参阅[样式和模板化](../../../../docs/framework/wpf/controls/styling-and-templating.md)。  
  
 属性值均描述属性之间的关系时，另一个使用属性名。 此功能用于数据绑定和演示图板目标，以及是否启用<xref:System.Windows.PropertyPath>类，其类型转换器。 查找语义的更完整说明，请参阅[PropertyPath XAML 语法](../../../../docs/framework/wpf/advanced/propertypath-xaml-syntax.md)。  
  
<a name="property_element_syntax"></a>   
## <a name="property-element-syntax"></a>属性元素语法  
 *属性元素语法*是一种与元素的基本 XML 语法规则略有不同的语法。 在 XML 中，属性的值是一个实际的字符串，唯一可能的变化是正在使用哪种字符串编码格式。 在 XAML 中，您可以分配其他对象元素的属性的值。 通过属性元素语法来启用此功能。 而不是指定为元素标记内的特性的属性，该属性使用指定的开始元素标记在*元素类型名称*。*propertyName*窗体中，指定的属性的值，然后关闭属性元素。  
  
 具体而言，该语法以左的尖括号 （\<), followed immediately by the type name of the class or structure that the property element syntax is contained within. followed="" immediately="" by="" the="" type="" name="" of="" the="" class="" or="" structure="" that="" the="" property="" element="" syntax="" is="" contained="">\</), followed immediately by the type name of the class or structure that the property element syntax is contained within.> 这被紧跟由单个句点 （.），然后属性的名称，然后是右尖括号 (>)。 与特性语法中，该属性必须存在于指定类型的已声明的公共成员。 要分配给属性的值包含在属性元素中。 通常，给出的值为一个或多个 object 元素，因为对象指定为值是该方案属性元素语法旨在介绍。 最后，指定相同的等效的结束标记*元素类型名称*。*propertyName*组合必须提供，并正确的嵌套和与其他元素标记的平衡。  
  
 例如，以下是有关的属性元素语法<xref:System.Windows.FrameworkElement.ContextMenu%2A>属性<xref:System.Windows.Controls.Button>。  
  
 [!code-xml[XAMLOvwSupport#ContextMenu](../../../../samples/snippets/csharp/VS_Snippets_Wpf/XAMLOvwSupport/CSharp/Page1.xaml#contextmenu)]  
  
 属性元素中的值可以还提供内部文本的情况下，所指定的属性类型的基元值类型，如<xref:System.String>，或指定了名称的枚举。 这两种用法是略为稀少，因为每个这种情况下也可以使用简单的特性语法。 用字符串填充的属性元素的一个方案是不是 XAML 内容属性，但仍然用于 UI 文本表示形式的属性，必须在该 UI 文本中出现特定的空白元素 （如换行符）。 特性语法不能保留换行符，但是属性元素语法可以前提是有意义的空白保留处于活动状态 (有关详细信息，请参阅[中 XAML 的空白处理](../../../../docs/framework/xaml-services/whitespace-processing-in-xaml.md))。 另一个方案是，以便[X:uid 指令](../../../../docs/framework/xaml-services/x-uid-directive.md)可以应用于 property 元素，并因此将标记内的值，作为一个值，应在 WPF 中本地化输出 BAML 或通过其他技术。  
  
 属性元素不出现在 WPF 逻辑树。 Property 元素是只是一种特定的语法，来设置属性，并不是由实例或对象支持的元素。 (有关逻辑树概念的详细信息，请参阅[WPF 中的树](../../../../docs/framework/wpf/advanced/trees-in-wpf.md)。)  
  
 对于特性和属性元素语法支持的位置的属性，这两种语法通常具有相同的结果，虽然微妙之处，例如空格处理之间的语法略有不同。  
  
<a name="collection_syntax"></a>   
## <a name="collection-syntax"></a>集合语法  
 XAML 规范要求 XAML 处理器实现来标识的属性的值类型是集合。 在.NET 中的普通的 XAML 处理器实现基于托管的代码和 CLR，并且它标识集合类型通过以下项之一︰  
  
-   类型实现<xref:System.Collections.IList>。  
  
-   类型实现<xref:System.Collections.IDictionary>。  
  
-   类型派生自<xref:System.Array>(有关在 XAML 中的数组的详细信息，请参阅[X:array 标记扩展](../Topic/x:Array%20Markup%20Extension.md)。)  
  
 如果属性的类型是一个集合，然后不需要为对象元素标记中指定推断的集合类型。 相反，旨在成为该集合中的项的元素被指定为一个或多个属性元素的子元素。 在加载期间对对象计算每个此类项并将其添加到集合中通过调用`Add`隐含集合的方法。 例如，<xref:System.Windows.Style.Triggers%2A>属性<xref:System.Windows.Style>采用专用的集合类型<xref:System.Windows.TriggerCollection>，该类实现<xref:System.Collections.IList>。 不需要实例化<xref:System.Windows.TriggerCollection>对象标记中的元素。 相反，您可以指定一个或多个<xref:System.Windows.Trigger>项中的元素作为`Style.Triggers`属性元素中，其中<xref:System.Windows.Trigger>（或派生的类） 是强类型化和隐式为项类型所需的类型<xref:System.Windows.TriggerCollection>。  
  
 [!code-xml[XAMLOvwSupport#SyntaxPECollection](../../../../samples/snippets/csharp/VS_Snippets_Wpf/XAMLOvwSupport/CSharp/Page1.xaml#syntaxpecollection)]  
  
 一个属性可能是集合类型和该类型的 XAML 内容属性和派生类型，对其进行讨论在本主题的下一节中。  
  
 隐式集合元素中的逻辑树表示形式中，创建的成员，即使它不显示在标记中的某个元素也是如此。 父类型的构造函数通常是一个其属性的集合执行实例化并最初为空集合将成为对象树的一部分。  
  
> [!NOTE]
>  泛型列表和词典接口 (<xref:System.Collections.Generic.IList%601>和<xref:System.Collections.Generic.IDictionary%602>) 不支持集合检测。\</TKey, TValue> 但是，您可以使用<xref:System.Collections.Generic.List%601>类作为基类，因为它实现了<xref:System.Collections.IList>直接或<xref:System.Collections.Generic.Dictionary%602>用作基类，因为它实现了<xref:System.Collections.IDictionary>直接。\</TKey, TValue>  
  
 在.NET 参考页的集合类型中，此语法与特意省略的对象元素的集合会偶尔记录中的 XAML 语法章节作为隐式集合语法。  
  
 除了根元素，作为另一个元素的子元素嵌套了 XAML 文件中的每个对象元素实际上是一个或两个以下情况下的元素︰ 其父元素或指定的父元素 (XAML 内容属性将在下一节中讨论) 的 XAML 内容属性的值的元素的隐式集合属性的成员。 换而言之，父元素和标记页面中的子元素的关系实际上是根位置，单个对象，它对根下的每个对象元素是用于提供其父级的属性值的单个实例或某一集合中也是集合类型属性值的父项。 此单根概念通常是使用 XML 中，并且还在如加载 XAML 的 Api 的行为经常进一步巩固<xref:System.Windows.Markup.XamlReader.Load%2A>。  
  
 下面的示例是集合的对象元素语法 (<xref:System.Windows.Media.GradientStopCollection>) 显式指定。  
  
```xaml  
<LinearGradientBrush>  
  <LinearGradientBrush.GradientStops>  
    <GradientStopCollection>  
      <GradientStop Offset="0.0" Color="Red" />  
      <GradientStop Offset="1.0" Color="Blue" />  
    </GradientStopCollection>  
  </LinearGradientBrush.GradientStops>  
</LinearGradientBrush>  
```  
  
 请注意，它并不总是能够显式声明集合。 例如，尝试声明<xref:System.Windows.TriggerCollection>中前面所示显式<xref:System.Windows.Style.Triggers%2A>示例将失败。 显式声明集合要求的集合类必须支持默认构造函数，和<xref:System.Windows.TriggerCollection>没有默认构造函数。  
  
<a name="xaml_content_properties"></a>   
## <a name="xaml-content-properties"></a>XAML 内容属性  
 XAML 内容语法是一种语法，仅在指定的类上启用<xref:System.Windows.Markup.ContentPropertyAttribute>作为它们的类声明的一部分。 <xref:System.Windows.Markup.ContentPropertyAttribute>引用该类型的元素 （包括派生的类） 的 content 属性的属性名称。 通过 XAML 处理器处理时，将分配的任何子元素或找到的开始和结束标记的 object 元素之间的内部文本，该对象的 XAML 内容属性的值。 允许你指定显式属性元素的内容的属性，但.NET 参考中的 XAML 语法章节中一般不介绍这种用法。 显式/详细的方法具有特殊的价值使标记清晰明确或作为一种标记样式，但通常内容属性的目的是简化标记，以便可以直接嵌套直观相关的父-子元素。 上一个元素的其他属性的属性元素标记不分配为"内容"每个严格的 XAML 语言定义;它们的先前处理 XAML 分析器处理顺序，并且不被视为是"内容"。  
  
### <a name="xaml-content-property-values-must-be-contiguous"></a>必须是连续的 XAML 内容属性值  
 XAML 内容属性的值必须在该对象元素完全之前或之后的任何其他属性元素指定。 是否指定了 XAML 内容属性的值作为一个字符串，或一个或多个对象，也是如此。 例如，不解析以下标记︰  
  
```  
<Button>I am a   
  <Button.Background>Blue</Button.Background>  
  blue button</Button>  
```  
  
 这是非法的实质上是因为如果这种语法未使用的内容属性的属性元素语法进行显式，内容的属性将设置两次︰  
  
```  
<Button>  
  <Button.Content>I am a </Button.Content>  
  <Button.Background>Blue</Button.Background>  
  <Button.Content> blue button</Button.Content>  
</Button>  
```  
  
 如果内容的属性是一个集合，并且子元素穿插属性元素，将是一个类似的非法示例︰  
  
```  
<StackPanel>  
  <Button>This example</Button>  
  <StackPanel.Resources>  
    <SolidColorBrush x:Key="BlueBrush" Color="Blue"/>  
  </StackPanel.Resources>  
  <Button>... is illegal XAML</Button>  
</StackPanel>  
```  
  
<a name="content_properties_and_collection_syntax_combined"></a>   
## <a name="content-properties-and-collection-syntax-combined"></a>内容属性和集合语法组合  
 多个单个对象元素作为内容，才能接受内容的类型具体而言必须是属性的集合类型。 与集合类型的属性元素语法类似，XAML 处理器必须确定是集合类型的类型。 如果元素具有 XAML 内容属性，并且 XAML 内容属性的类型是一个集合，然后不需要为对象元素标记中指定隐含的集合类型并不需要指定为属性元素的 XAML 内容属性。 因此在标记中明显的内容模型现在可以具有多个分配作为内容的子元素。 下面是有关内容语法<xref:System.Windows.Controls.Panel>派生的类。 所有<xref:System.Windows.Controls.Panel>派生的类建立 XAML 内容属性为<xref:System.Windows.Controls.Panel.Children%2A>，这要求类型的值<xref:System.Windows.Controls.UIElementCollection>。  
  
 [!code-xml[XAMLOvwSupport#SyntaxContent](../../../../samples/snippets/csharp/VS_Snippets_Wpf/XAMLOvwSupport/CSharp/page5.xaml#syntaxcontent)]  
  
 请注意，对于既不在属性元素<xref:System.Windows.Controls.Panel.Children%2A>，也不为元素<xref:System.Windows.Controls.UIElementCollection>需要在标记中。 这是 XAML 设计功能，以便以递归方式包含元素，用于定义[!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)]更直观地表示为嵌套元素直接父-子元素间的关系，而无需干预属性元素标记或集合对象的树。 事实上， <xref:System.Windows.Controls.UIElementCollection>不能指定显式标记中作为对象元素设计使然。 因为使用它的唯一目的是作为隐式的集合， <xref:System.Windows.Controls.UIElementCollection>不会公开公共默认构造函数，因此不能实例化对象的某个元素。  
  
### <a name="mixing-property-elements-and-object-elements-in-an-object-with-a-content-property"></a>混合使用属性元素和具有内容的属性的对象中的对象元素  
 XAML 规范声明用于填充 XAML 对象元素中的内容属性的对象元素必须是连续的并且不能混合 XAML 处理器可强制实施。 针对混合使用属性元素和内容的此限制强制执行由[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]XAML 处理器。  
  
 您可以将子对象元素作为对象元素中的第一个立即标记。 然后可以引入属性元素。 或者，您可以指定一个或多个属性元素的内容，然后多个属性元素。 但是，一旦某一属性元素后面跟的内容，您不能进一步引入任何内容，则可以仅添加属性元素。  
  
 此内容 / 属性元素顺序要求并不适用于作为内容的内部文本。 但是，它仍是要保留的内部文本连续的因为有意义的空白将很难判断以可视方式在标记中属性元素穿插内部文本的不错的标记样式。  
  
<a name="xaml_namespaces"></a>   
## <a name="xaml-namespaces"></a>XAML 命名空间  
 上面的语法示例中未指定默认 XAML 命名空间之外的 XAML 命名空间。 在典型[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]应用程序中，默认的 XAML 命名空间指定为[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]命名空间。 您可以指定默认 XAML 命名空间之外的 XAML 命名空间，而且仍使用类似的语法。 但然后，任意位置其中一个类，名为无法访问默认 XAML 命名空间内，则该类名开头必须是以 XAML 命名空间前缀映射到相应的 CLR 命名空间。 例如，`<custom:Example/>`是对象元素语法来实例化的实例`Example`类，其中包含此类 （和可能包含后备类型的外部程序集信息） 的 CLR 命名空间之前曾映射到`custom`前缀。  
  
 有关 XAML 命名空间的详细信息，请参阅[XAML 命名空间和 Namespace 映射 WPF XAML 的](../../../../docs/framework/wpf/advanced/xaml-namespaces-and-namespace-mapping-for-wpf-xaml.md)。  
  
<a name="markup_extensions"></a>   
## <a name="markup-extensions"></a>标记扩展  
 XAML 定义了一个标记扩展编程实体，使从字符串特性值或对象元素的普通 XAML 处理器处理转义符并将推迟到后备类处理。 标识 XAML 处理器的标记扩展时使用的特性语法是左大括号 （{}） 后, 跟右大括号 （}） 以外的任何字符的字符。 第一个左大括号后面的字符串必须引用提供了特定的扩展行为，其中该引用可以省略子字符串"Extension"如果此子字符串是真正的类名的一部分的类。 此后，可能会出现一个空格，而则每个后续字符用作输入的扩展插件实现中，直到遇到的右大括号。  
  
 .NET XAML 实现使用<xref:System.Windows.Markup.MarkupExtension>作为所有受支持的标记扩展的基础的抽象类[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]以及其他框架或技术。 标记扩展的[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]特定实现通常用于提供一种方式来引用其他现有对象，或使将在运行时计算的对象的延迟的引用。 例如，通过简单的 WPF 数据绑定指定`{Binding}`标记扩展来代替通常将采用的特定属性的值。 许多 WPF 标记扩展特性语法的允许其中的特性语法通常不是可能的属性。 例如，<xref:System.Windows.Style>对象是一个相对复杂类型，包含一系列嵌套的对象和属性。 通常将在 WPF 中样式定义中的资源为<xref:System.Windows.ResourceDictionary>，然后通过一个请求资源的两个 WPF 标记扩展引用。 标记扩展将推迟到查找资源的属性值的计算，并使提供的值<xref:System.Windows.FrameworkElement.Style%2A>属性，采用类型<xref:System.Windows.Style>，请在特性语法如以下示例所示︰  
  
 `<Button Style="{StaticResource MyStyle}">My button</Button>`  
  
 在这里，`StaticResource`标识<xref:System.Windows.StaticResourceExtension>类，提供标记扩展实现。 下一个字符串`MyStyle`作为输入用于非默认<xref:System.Windows.StaticResourceExtension>构造函数中，从扩展字符串提取的参数声明请求<xref:System.Windows.ResourceKey>。 `MyStyle`预期为[X:key](../../../../docs/framework/xaml-services/x-key-directive.md)值<xref:System.Windows.Style>定义为资源。 [StaticResource 标记扩展](../../../../docs/framework/wpf/advanced/staticresource-markup-extension.md)用法要求使用的资源，以提供<xref:System.Windows.Style>静态资源查找逻辑在加载时通过属性值。  
  
 有关标记扩展的详细信息，请参阅[标记扩展和 WPF XAML](../../../../docs/framework/wpf/advanced/markup-extensions-and-wpf-xaml.md)。 有关标记扩展和编程功能在常规的.NET XAML 实现中启用其他 XAML 参考，请参阅[XAML Namespace （x:）语言功能](../../../../docs/framework/xaml-services/xaml-namespace-x-language-features.md)。 有关特定于 WPF 的标记扩展，请参阅[WPF XAML 扩展](../../../../docs/framework/wpf/advanced/wpf-xaml-extensions.md)。  
  
<a name="attached_properties"></a>   
## <a name="attached-properties"></a>附加属性  
 附加的属性是在 XAML 中属性可以拥有和某个特定类型定义，由此引入了一个编程概念但设置为特性或属性元素的任何元素上。 主要方案附加的属性为了的是，而无需在所有元素之间的广泛共享的对象模型允许向父元素报告信息标记结构中的子元素。 相反，报表信息传递到子元素的父元素可以使用附加的属性。 用途的附加的属性以及如何创建您自己的详细信息的附加属性，请参阅[附加属性概述](../../../../docs/framework/wpf/advanced/attached-properties-overview.md)。  
  
 附加的属性使用的语法，表面上类似于属性元素语法中，您还指定*typeName*。*propertyName*组合。 有两个重要的差异：  
  
-   您可以使用*typeName*。*propertyName*甚至在设置属性的语法通过附加的属性的组合。 附加的属性是唯一的情况，其中限定属性名称是特性语法中的要求。  
  
-   此外可以附加属性来使用属性元素语法。 但是，对于典型的属性元素语法*typeName*指定是包含属性的元素的对象元素。 如果您引用的是附加属性，则*typeName*是定义附加的属性不包含的对象元素的类。  
  
<a name="attached_events"></a>   
## <a name="attached-events"></a>附加事件  
 附加的事件也是另一个位置可通过特定类型定义事件，但处理程序可能会附加到任何对象元素的 XAML 中引入的编程概念。 在 WOF 实现中，通常定义的附加的事件的类型是定义的服务的静态类型和公开服务的类型中的路由的事件别名有时公开这些附加的事件。 附加事件的处理程序是通过属性语法指定的。 如附加事件的特性语法进行了扩展针对附加的事件，以允许*typeName*。*eventName*使用情况，其中*typeName*是提供的类`Add`和`Remove`事件处理程序，为附加的事件基础结构的访问器和*eventName*是事件名称。  
  
<a name="anatomy_of_a_xaml_page_root_element"></a>   
## <a name="anatomy-of-a-xaml-root-element"></a>XAML 根元素的剖析  
 下表显示了一个典型 XAML 根元素细分它们，显示的根元素的特定属性︰  
  
|||  
|-|-|  
|`<Page`|打开对象的根元素的元素|  
|`xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"`|默认值 ([!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]) 的 XAML 命名空间|  
|`xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"`|在 XAML 语言 XAML 命名空间|  
|`x:Class="ExampleNamespace.ExampleCode"`|将标记连接到任何代码隐藏的分部类声明为分部类定义|  
|`>`|元素末尾的对象的根。 对象已不关闭尚未，因为该元素包含子元素|  
  
<a name="optional_and_nonrecommended_xaml_usages"></a>   
## <a name="optional-and-nonrecommended-xaml-usages"></a>可选的和非建议的 XAML 用法  
 下列各节描述，从技术上讲支持由 XAML 处理器，但详细级别或剩余用户可读的 XAML 文件会干扰其他美学问题的产生的 XAML 用法您开发的应用程序包含 XAML 源。  
  
### <a name="optional-property-element-usages"></a>可选属性元素用法  
 可选属性元素的用法包括显式写出元素内容属性 XAML 处理器视为隐式。 例如，当声明的内容<xref:System.Windows.Controls.Menu>，您可以选择显式声明<xref:System.Windows.Controls.ItemsControl.Items%2A>的集合<xref:System.Windows.Controls.Menu>作为`<Menu.Items>`属性元素标记，并将每个<xref:System.Windows.Controls.MenuItem>内`<Menu.Items>`，而不是使用隐式的 XAML 处理器行为的所有子元素<xref:System.Windows.Controls.Menu>必须<xref:System.Windows.Controls.MenuItem>并放入<xref:System.Windows.Controls.ItemsControl.Items%2A>集合。 有时可选用法可以帮助以可视方式阐明对象结构，按标记中的表示形式。 或者有时的显式属性元素用法可以避免从技术上讲功能，但在视觉混乱，如嵌套的标记扩展的特性值中的标记。  
  
### <a name="full-typenamemembername-qualified-attributes"></a>完全限定的类型属性  
 The *typeName*.*memberName*窗体属性的工作方式实际上比仅仅使用路由的事件的情况更为普遍。 但在其他情况下该窗体是多余的应避免它，如果只是为了实现标记样式和可读性。 在以下示例中，这三个对引用<xref:System.Windows.Controls.Control.Background%2A>属性是完全等效︰  
  
 [!code-xml[XAMLOvwSupport#TypeNameProp](../../../../samples/snippets/csharp/VS_Snippets_Wpf/XAMLOvwSupport/CSharp/page8.xaml#typenameprop)]  
  
 `Button.Background`有效，因为该属性的限定的查找<xref:System.Windows.Controls.Button>成功 (<xref:System.Windows.Controls.Control.Background%2A>从 Control 继承) 和<xref:System.Windows.Controls.Button>是对象元素的类或其基类。 `Control.Background`有效，因为<xref:System.Windows.Controls.Control>类实际上定义<xref:System.Windows.Controls.Control.Background%2A>和<xref:System.Windows.Controls.Control>是<xref:System.Windows.Controls.Button>基类。  
  
 但是，以下*typeName*。*memberName*窗体示例不起作用，因此显示为注释︰  
  
 [!code-xml[XAMLOvwSupport#TypeNameBadProp](../../../../samples/snippets/csharp/VS_Snippets_Wpf/XAMLOvwSupport/CSharp/page8.xaml#typenamebadprop)]  
  
 <xref:System.Windows.Controls.Label>作为另一个派生的类的<xref:System.Windows.Controls.Control>，并且如果已指定`Label.Background`内<xref:System.Windows.Controls.Label>object 元素，这种用法会起作用。 但是，由于<xref:System.Windows.Controls.Label>不是类或类的基类<xref:System.Windows.Controls.Button>，然后处理指定的 XAML 处理器行为是`Label.Background`作为附加属性。 `Label.Background`不是可用的附加的属性，并且这种用法中无法正常工作。  
  
### <a name="basetypenamemembername-property-elements"></a>baseTypeName.memberName 属性元素  
 如何以类似方式*typeName*。*memberName*窗体适用于特性语法*基类型名称*。*memberName*语法适用于属性元素语法。 例如，下面的语法适用︰  
  
 [!code-xml[XAMLOvwSupport#GoofyPE](../../../../samples/snippets/csharp/VS_Snippets_Wpf/XAMLOvwSupport/CSharp/page8.xaml#goofype)]  
  
 在这里，形式提供 property 元素`Control.Background`即使属性元素中包含`Button`。  
  
 但是，正如*typeName*。*memberName*的属性，窗体*基类型名称*。*memberName*是在标记中，较差的样式，您应避免使用它。  
  
## <a name="see-also"></a>另请参阅  
 [XAML 概述 (WPF)](../../../../docs/framework/wpf/advanced/xaml-overview-wpf.md)   
 [XAML Namespace （x:）语言功能](../../../../docs/framework/xaml-services/xaml-namespace-x-language-features.md)   
 [WPF XAML 扩展](../../../../docs/framework/wpf/advanced/wpf-xaml-extensions.md)   
 [依赖项属性概述](../../../../docs/framework/wpf/advanced/dependency-properties-overview.md)   
 [TypeConverters 和 XAML](../../../../docs/framework/wpf/advanced/typeconverters-and-xaml.md)   
 [XAML 和 wpf 自定义类](../../../../docs/framework/wpf/advanced/xaml-and-custom-classes-for-wpf.md)