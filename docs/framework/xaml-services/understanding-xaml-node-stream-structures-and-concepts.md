---
title: "Understanding XAML Node Stream Structures and Concepts | Microsoft Docs"
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
  - "XAML node streams [XAML Services]"
  - "nodes [XAML Services], XAML node stream"
  - "XAML [XAML Services], XAML node streams"
ms.assetid: 7c11abec-1075-474c-9d9b-778e5dab21c3
caps.latest.revision: 14
author: "wadepickett"
ms.author: "wpickett"
manager: "wpickett"
caps.handback.revision: 14
---
# Understanding XAML Node Stream Structures and Concepts
.NET Framework XAML 服务中实现的 XAML 读取器和 XAML 编写器基于 XAML 节点流的设计概念。 将一组 XAML 节点概念化就生成 XAML 节点流。 在此概念化中，XAML 处理器逐一浏览 XAML 中节点关系的结构。 一个打开的 XAML 节点流中始终只存在一个当前记录或当前位置，并且 API 的很多方面只报告此位置提供的信息。 XAML 节点流中的当前节点可描述为对象、成员或值。 通过将 XAML 视为 XAML 节点流，XAML 读取器可与 XAML 编写器通信；并且在涉及 XAML 的加载路径或保存路径操作过程中可启用程序查看、更改 XAML 节点流的内容或与它交互。 XAML 读取器和编写器 API 设计以及 XAML 节点流概念都类似于上一个相关的读取器和编写器设计和概念，如：[!INCLUDE[TLA#tla_xmldom](../../../includes/tlasharptla-xmldom-md.md)]以及 <xref:System.Xml.XmlReader> 和 <xref:System.Xml.XmlWriter> 类。 本主题阐述 XAML 节点流概念，并介绍如何编写在 XAML 节点级别上与 XAML 表示形式进行交互的例程。  
  
<a name="loading_into_a_xaml_reader"></a>   
## 将 XAML 加载到 XAML 读取器  
 基 <xref:System.Xaml.XamlReader> 类不会声明用于将初始 XAML 加载到 XAML 读取器的特定技术。 相反，派生类声明并实现加载技术，包括用于 XAML 的输入源的常规特性和约束。 例如，<xref:System.Xaml.XamlObjectReader> 从表示根或基的单个对象的输入源开始读取对象图。 然后，<xref:System.Xaml.XamlObjectReader> 从对象图中生成 XAML 节点流。  
  
 最卓越的 .NET Framework XAML 服务将 <xref:System.Xaml.XamlReader> 子类定义为 <xref:System.Xaml.XamlXmlReader>。<xref:System.Xaml.XamlXmlReader> 通过流或文件路径直接加载文件本件，或者通过相关的读取器类（如 <xref:System.IO.TextReader>）间接加载，从而加载初始 XAML。 加载后，可认为 <xref:System.Xaml.XamlReader> 包含整个 XAML 输入源。 但是，<xref:System.Xaml.XamlReader> 基 API 旨在使读取器与 XAML 的单节点进行交互。 首次加载时，遇到的第一个单节点就是 XAML 的根和它的启动对象。  
  
### XAML 节点流概念  
 如果你通常更熟悉根据 DOM、树隐喻或查询访问基于 XML 的技术的方法以下方法有助于概念化 XAML 节点流。 假设加载的 XAML 是一个 DOM 或树，其中每个可能的节点均始终展开，然后以线性方式表示。 通过这些节点时，你可能遇到遍历与 DOM 相关的“输入”或“输出”级别，但 XAML 节点流不会显式跟踪，因为这些级别概念与节点流无关。 节点流有一个“当前”位置，但当前节点位置以外的节点流的所有特性均不可见，除非你已手动将流的其他特性作为引用存储。  
  
 XAML 节点流概念具有显著优点，如果你浏览了整个节点流，系统保证你已处理整个 XAML 表示形式；你无需担心处理信息的查询、DOM 操作或一些其他非线性方法遗漏了完整 XAML 表达形式中的某个部分。 因此，XAML 节点流表示形式非常适合连接 XAML 读取器和 XAML 编写器，还适合于提供一个系统，用于插入在 XAML 处理操作的读取和编写阶段之间运行的进程。 在很多情况下，XAML 读取器针对顺序可能在源文本、二进制或对象图中显示的方式故意优化了 XAML 节点流中的节点顺序或故意重新进行了排序。 此行为旨在强制执行 XAML 处理体系结构，以使 XAML 编写器决不位于节点流中它们必须“后退”的位置。 理想情况下，所有 XAML 写入操作都应能够基于架构上下文和节点流的当前位置运行。  
  
<a name="a_basic_reading_node_loop"></a>   
## 基本读取节点循环  
 用于检查 XAML 节点流的基本读取节点循环包括以下概念。 为了在本主题中讨论节点循环，假定你正在使用 <xref:System.Xaml.XamlXmlReader> 读取基于文本、用户可读的 XAML 文件。 本节中的链接是指 <xref:System.Xaml.XamlXmlReader> 实现的特定 XAML 节点循环 API。  
  
-   确保你不在 XAML 节点流的末尾（检查 <xref:System.Xaml.XamlXmlReader.IsEof%2A> 或使用 <xref:System.Xaml.XamlXmlReader.Read%2A> 返回值）。 如果你在流的末尾，此处没有当前节点，你应该退出。  
  
-   通过调用 <xref:System.Xaml.XamlXmlReader.NodeType%2A> 检查 XAML 节点流中当前公开的节点类型。  
  
-   如果具有直接连接的关联 XAML 对象编写器，此时通常调用 <xref:System.Xaml.XamlWriter.WriteNode%2A>。  
  
-   根据报告为当前节点或当前记录的 <xref:System.Xaml.XamlNodeType>，调用下面的一个操作以获取节点内容的相关信息：  
  
    -   对于 <xref:System.Xaml.XamlNodeType> 或 <xref:System.Xaml.XamlNodeType> 的 <xref:System.Xaml.XamlXmlReader.NodeType%2A>，调用 <xref:System.Xaml.XamlXmlReader.Member%2A> 以获取成员的相关 <xref:System.Xaml.XamlMember> 信息。 请注意，成员可能为 <xref:System.Xaml.XamlDirective>，因此不一定是前一个对象中具有传统定义类型的成员。 例如，应用于对象的 `x:Name` 显示为 XAML 成员，其中 <xref:System.Xaml.XamlMember.IsDirective%2A> 为 true，成员的 <xref:System.Xaml.XamlMember.Name%2A> 为 `Name`，且其他属性指示此指令在 XAML 语言 XAML 命名空间下。  
  
    -   对于 <xref:System.Xaml.XamlNodeType> 或 <xref:System.Xaml.XamlNodeType> 的 <xref:System.Xaml.XamlXmlReader.NodeType%2A>，调用 <xref:System.Xaml.XamlXmlReader.Type%2A> 以获取对象的相关 <xref:System.Xaml.XamlType> 信息。  
  
    -   对于 <xref:System.Xaml.XamlNodeType> 的 <xref:System.Xaml.XamlXmlReader.NodeType%2A>，调用 <xref:System.Xaml.XamlXmlReader.Value%2A>。 只有节点为成员值的最简单表达式或者对象的初始化文本时，此节点才是一个值（但是，应注意本主题下一节中介绍的类型转换行为）。  
  
    -   对于 <xref:System.Xaml.XamlNodeType> 的 <xref:System.Xaml.XamlXmlReader.NodeType%2A>，调用 <xref:System.Xaml.XamlXmlReader.Namespace%2A>，以获取命名空间节点的命名空间信息。  
  
-   调用 <xref:System.Xaml.XamlXmlReader.Read%2A>，以使 XAML 读取器前进到 XAML 节点流中的下一个节点，然后重复步骤。  
  
 .NET Framework XAML 服务 XAML 读取器提供的 XAML 节点流始终提供所有潜在节点的完整深入的遍历。 XAML 节点循环的典型流控制技术包括在 `while (reader.Read())` 中定义正文，和在节点循环的每个节点上打开 <xref:System.Xaml.XamlXmlReader.NodeType%2A>。  
  
 如果节点流位于文件末尾，则当前节点为 null。  
  
 使用读取器和编写器的最简单的循环类似于以下示例。  
  
```  
XamlXmlReader xxr = new XamlXmlReader(new StringReader(xamlStringToLoad)); //where xamlStringToLoad is a string of well formed XAML XamlObjectWriter xow = new XamlObjectWriter(xxr.SchemaContext); while (xxr.Read()) { xow.WriteNode(xxr); }  
```  
  
 此基本示例显示加载路径 XAML 节点循环，以透明方式连接 XAML 读取器和 XAML 编写器，其操作方式与使用 <xref:System.Xaml.XamlServices.Parse%2A?displayProperty=fullName> 时完全相同。 但此基本结构已扩展为适用于读取或写入方案。 一些可能的方案如下所示：  
  
-   打开 <xref:System.Xaml.XamlXmlReader.NodeType%2A>。 执行不同的操作，具体取决于正在读取的节点类型。  
  
-   在任何情况下，都不要调用 <xref:System.Xaml.XamlWriter.WriteNode%2A>。 仅在某些 <xref:System.Xaml.XamlXmlReader.NodeType%2A> 情况下调用 <xref:System.Xaml.XamlWriter.WriteNode%2A>。  
  
-   在特定节点类型的逻辑中，分析此节点的详细信息并操作它。 例如，只能写入特定 XAML 命名空间的对象，然后删除或延迟其他 XAML 命名空间的任何对象。 或者，可以删除或重新处理你的 XAML 系统在处理成员时不支持的任何 XAML 指令。  
  
-   定义可重写 `Write*` 方法的自定义 <xref:System.Xaml.XamlObjectWriter>，它可能执行绕过 XAML 架构上下文的类型映射。  
  
-   构造 <xref:System.Xaml.XamlXmlReader> 以使用非默认的 XAML 架构上下文，以便 XAML 行为中的自定义差异可兼用于读取器和编写器。  
  
### 访问节点循环之外的 XAML 的概念  
 除了用作 XAML 节点循环，可能还有其他使用 XAML 表示形式的方式。 例如，可能有 XAML 读取器可以读取索引节点，或者特别是直接通过 `x:Name`、`x:Uid` 或其他标识符访问节点。 .NET framework XAML 服务不提供完整实现，而通过服务和支持类型提供一种建议模式。 有关详细信息，请参阅<xref:System.Xaml.IXamlIndexingReader>和<xref:System.Xaml.XamlNodeList>。  
  
> [!TIP]
>  Microsoft 也会生成称为 Microsoft XAML 工具包的带外版本。 此带外版本仍处于预发布阶段。 但是，如果你想使用预发布组件，Microsoft XAML 工具包会提供一些有关 XAML 工具和 XAML 静态分析的有趣资源。 Microsoft XAML 工具包包括 XAML DOM API、对 FxCop 分析的支持以及 Silverlight 的 XAML 架构上下文。 有关详细信息，请参阅 [Microsoft XAML 工具包](http://code.msdn.microsoft.com/XAML)。  
  
<a name="working_with_the_current_node"></a>   
## 使用当前代码  
 使用 XAML 节点循环的大多数方案不仅仅读取节点。 大多数方案逐一处理当前节点并将每个节点传递到 <xref:System.Xaml.XamlWriter> 的实现。  
  
 在典型的加载路径方案中，<xref:System.Xaml.XamlXmlReader> 生成 XAML 节点流；根据逻辑和 XAML 架构上下文处理 XAML 节点；并将节点传递到 <xref:System.Xaml.XamlObjectWriter>。 然后，将生成的对象图集成到应用程序或框架中。  
  
 在典型的保存路径方案中，<xref:System.Xaml.XamlObjectReader> 读取对象图，系统处理单个 XAML 节点，<xref:System.Xaml.XamlXmlWriter> 将序列化结果作为 XAML 文本文件输出。 重点在于路径和方案一次只处理一个 XAML 节点，且可在 XAML 类型系统和 .NET Framework XAML 服务 API 所定义的标准化方式中处理 XAML 节点。  
  
### 框架和作用域  
 XAML 节点循环以线性方式遍历 XAML 节点流。 节点流遍历对象以及包含其他对象的的成员等。 它通常可用于通过实现框架和堆栈概念跟踪 XAML 节点流内的作用域。 当你身处其中主动调整节点流时尤其如此。 如果在 XAML 节点结构被视为来自 DOM 透视时向下查看到此结构，作为节点循环逻辑的一部分而实现的框架和堆栈支持会计算 `StartObject`（或 `GetObject`）和 `EndObject` 作用域。  
  
<a name="traversing_and_entering_object_nodes"></a>   
## 遍历并进入对象节点  
 节点流中由 XAML 读取器打开时的第一个节点为根对象的启动对象节点。 根据定义，此对象始终是单个对象节点，没有对等节点。 在所有实际的 XAML 示例中，根对象均被定义为具有多个对象和成员节点的一个或多个属性。 而成员节点具有一个或多个对象节点，或者转而只有一个值节点。 根对象通常定义 XAML 名称范围，此范围在 XAML 文本标记中按语法分配为属性，但在 XAML 节点流表示形式中映射到 `Namescope` 节点类型。  
  
 请注意下面的 XAML 示例（此为 .NET Framework 的现有类型不支持的任意 XAML）。 假定在此对象模型中，`FavorCollection` 是 `Favor` 的 `List<T>`，`Balloon` 和 `NoiseMaker` 可分配给 `Favor`，`Color` 对象按类似于 WPF 将颜色定义为已知颜色名称的方式支持 `Balloon.Color` 属性，且 `Color` 支持属性语法的类型转换器。  
  
|XAML 标记|生成的 XAML 节点流|  
|-------------|------------------|  
|`<Party`|`Party` 的 `Namespace` 节点|  
|`xmlns="PartyXamlNamespace">`|`Party` 的 `StartObject` 节点|  
|`<Party.Favors>`|`Party.Favors` 的 `StartMember` 节点|  
||隐式 `FavorCollection` 的 `StartObject` 节点|  
||隐式 `FavorCollection` 项属性的 `StartMember` 节点。|  
|`<Balloon`|`Balloon` 的 `StartObject` 节点|  
|`Color="Red"`|`Color` 的 `StartMember` 节点<br /><br /> 属性值字符串 `"Red"` 的`Value` 节点<br /><br /> `Color` 的 `EndMember`|  
|`HasHelium="True"`|`HasHelium` 的 `StartMember` 节点<br /><br /> 属性值字符串 `"True"` 的`Value` 节点<br /><br /> `HasHelium` 的 `EndMember`|  
|`>`|`Balloon` 的 `EndObject`|  
|`<NoiseMaker>Loudest</NoiseMaker>`|`NoiseMaker` 的 `StartObject` 节点<br /><br /> `_Initialization` 的 `StartMember` 节点<br /><br /> 初始化值字符串 `"Loudest"` 的 `Value` 节点<br /><br /> `_Initialization` 的 `EndMember` 节点<br /><br /> `NoiseMaker` 的 `EndObject`|  
||隐式 `FavorCollection` 项属性的 `EndMember` 节点。|  
||隐式 `FavorCollection` 的 `EndObject` 节点|  
|`</Party.Favors>`|`Favors` 的 `EndMember`|  
|`</Party>`|`Party` 的 `EndObject`|  
  
 在 XAML 节点流中，可依赖以下行为：  
  
-   如果存在 `Namespace` 节点，将它添加到紧靠用 `xmlns` 声明 XAML 命名空间的 `StartObject` 的前面。 再次查看具有 XAML 和示例节点流的上表。 请注意 `StartObject` 和 `Namespace` 节点在文本标记中与其声明位置转置的方式。 此行为表示命名空间节点始终显示在它们在节点流中应用到的节点前面。 此设计是因为命名空间信息对于对象编写器至关重要，必须在对象编辑器尝试执行类型映射或转而处理对象之前进行了解。 将 XANL 命名空间信息置于节点流中其应用程序作用域之前，这使得更容易始终按显示的顺序处理节点流。  
  
-   由于上述考虑，它是你从头遍历时在大多数实际标记情况中首先读取一个或多个 `Namespace` 节点，而不是根的 `StartObject`。  
  
-   `StartObject` 节点可后接 `StartMember`、`Value`，或即时 `EndObject`。 决不可紧跟其他 `StartObject`。  
  
-   `StartMember` 可后接 `StartObject`、`Value`，或即时 `EndMember`。 可后接成员的 `GetObject`（其中值应来自父对象的现有值），而不是会实例化新值的 `StartObject`。 也可后接应用于下一个 `StartObject` 的`Namespace` 节点。 决不可紧跟其他 `StartMember`。  
  
-   `Value` 节点表示值本身；不存在“EndValue”。 后面只能接 `EndMember`。  
  
    -   对象的 XAML 初始化文本因可能用于构造而不会导致对象\-值结构。 相反，会创建名为 `_Initialization` 的成员的专用成员节点。 并且此成员节点包含初始化值字符串。 如果存在，`_Initialization` 始终为第一个 `StartMember`。 可使用 XAML 语言 XAML 名称范围在限某些 XAML 服务表示形式中限定 `_Initialization`，以阐明 `_Initialization` 不是后备类型中的定义属性。  
  
    -   成员\-值组合表示值的属性设置。 可能最终为处理此值时使用的值转换器，并且值为纯字符串。 但是，在 XAML 对象编写器处理此节点流后才会计算此值。 XAML 对象编写器处理必需的 XAML 架构上下文、类型系统映射和值转换器所需的其他支持。  
  
-   `EndMember` 节点可后接后续成员的 `StartMember` 节点或成员所有者的 `EndObject` 节点。  
  
-   `EndObject` 节点可后接 `EndMember` 节点。 在对象在集合的项中成对出现的情况中，还可后接 `StartObject` 节点。 或者，可后接应用于下一个 `StartObject` 的 `Namespace` 节点。  
  
    -   对于关闭整个节点流的独特情况，根的 `EndObject` 后面不接任何内容；此时读取器位于文件结尾，且<xref:System.Xaml.XamlReader.Read%2A> 返回 `false`。  
  
<a name="value_converters_and_the_xaml_node_stream"></a>   
## 值转换器和 XAML 节点流  
 值转换器是用于标记扩展、类型转换器（包括值序列化程序）或通过 XAML 类型系统报告为值转换器的其他专用类的常用术语。 在 XAML 节点流中，类型转换器用法和标记扩展用法的表示形式非常迥异。  
  
### XAML 节点流中的类型转换器  
 最终生成类型转换器用法的属性设置将在 XAML 节点流中报告为成员的值。 XAML 节点流不会尝试生成类型转换器实例对象，也不会将值传递给它。 若要使用类型转换器的转换实现，需要调用 XAML 架构上下文并将其用于映射类型。 甚至确定应使用哪个类型转换器类处理值也间接需要 XAML 架构上下文。 使用默认 XAML 架构上下文时，XAML 类型系统可提供此信息。 如果在连接到 XAML 编写器前需要 XAML 节点流级别的类型转换器类信息，可以从要设置的成员的 <xref:System.Xaml.XamlMember> 信息中获取。 否则，类型转换器输入应作为纯值保留在 XAML 节点流中，直到执行需要类型映射系统和 XAML 架构上下文的剩余操作（例如由 XAML 对象编写器创建对象）。  
  
 例如，请注意下面的类定义大纲和它的 XAML 用法：  
  
```  
public class BoardSizeConverter : TypeConverter { //converts from string to an int[2] by splitting on an "x" char } public class GameBoard { [TypeConverter(typeof(BoardSizeConverter))] public int[] BoardSize; //2x2 array, initialization not shown }  
```  
  
```  
<GameBoard BoardSize="8x8"/>  
```  
  
 此用法的 XAML 节点流的文本表示形式可如下所示：  
  
 `StartObject`，带有表示 `GameBoard` 的 <xref:System.Xaml.XamlType>  
  
 `StartMember`，带有表示 `BoardSize` 的 <xref:System.Xaml.XamlMember>  
  
 `Value` 节点，带有文本字符串“`8x8`”  
  
 `EndMember` 与 `BoardSize` 匹配  
  
 `EndObject` 与 `GameBoard` 匹配  
  
 请注意此节点流中没有任何类型转换器实例。 但可以通过调用 `BoardSize` 的 <xref:System.Xaml.XamlMember> 上的 <xref:System.Xaml.XamlMember.TypeConverter%2A?displayProperty=fullName> 获取类型转换器信息。 如果具有有效的 XAML 架构上下文，也可通过获取 <xref:System.Xaml.Schema.XamlValueConverter%601.ConverterInstance%2A> 中的实例来调用转换器方法。  
  
### XAML 节点流中的标记扩展  
 标记扩展用法在 XAML 节点流中报告为成员中的对象节点，其中对象表示标记扩展实例。 因此标记扩展用法在节点流表示形式中比类型转换器用法表示得更为显式，并且具备更多信息。<xref:System.Xaml.XamlMember> 信息不包含标记扩展的任何相关信息，因为用法因情况而定，在每个可能的标记情况中都有不同；它与类型转换器的情况不同，不专用于每个类型或成员，也不是隐式的。  
  
 即使在 XAML 文本标记的属性中生成标记扩展用法（通常如此），标记扩展中作为对象节点的节点流表示形式也是上述情况。 使用显式对象元素窗体的标记扩展用法以相同方式处理。  
  
 在标记扩展对象节点中，可能存在此标记扩展的成员。 无论此标记扩展的用法是位置参数用法还是具有显式命名参数的用法，XAML 节点流表示形式都会保留它。  
  
 对于位置参数用法，XAML 节点流包含一个 XAML 语言定义的记录用法的属性 `_PositionalParameters`。 此属性是带有 <xref:System.Object> 约束的泛型 <xref:System.Collections.Generic.List%601>。 此约束是对象而不是字符串，因为位置参数用法一定内含嵌套标记扩展用法。 若要从用法中访问位置参数，可以循环访问列表并使用单个列表值的索引器。  
  
 对于命名参数用法，每个命名参数表示为节点流中此名称的成员节点。 成员值不一定是字符串，因为可能存在嵌套标记扩展用法。  
  
 尚未调用标记扩展的 `ProvideValue`。 但是，如果连接了 XAML 读取器和 XAML 编写器则进行调用，以便在节点系统中检查它时在标记扩展节点上调用 `WriteEndObject`。 为此，通常需要提供与在加载路径上形成对象图时所用的 XAML 架构上下文相同的上下文。 否则，任何标记扩展的 `ProvideValue` 都可在此引发异常，因为它没有可用的预期服务。  
  
<a name="xaml_and_xml_languagedefined_members_in_the_xaml_node_stream"></a>   
## XAML 节点流中 XAML 和 XML 语言定义的成员  
 特定成员由于 XAML 读取器的解释和约定而引入到 XAML 节点流，而不是通过显式 <xref:System.Xaml.XamlMember> 查找或构造引入。 通常，这些成员均为 XAML 指令。 在某些情况下，它是读取 XAML 的操作，用于将指令引入 XAML 节点流。 换句话说，原始输入 XAML 文本未显式指定成员指令，但XAML 读取器插入指令以满足结构 XAML 约定并在此信息丢失前报告 XAML 节点流中的信息。  
  
 下表说明了应将 XAML 读取器引入指令 XAML 成员节点的所有情况，并介绍了在 .NET Framework XAML 服务实现中标识成员节点的方式。  
  
-   **对象节点的初始化文本：**此成员节点的名称是 `_Initialization`，它表示 XAML 指令，并且在 XAML 语言 XAML 命名空间中进行定义。 可从 <xref:System.Xaml.XamlLanguage.Initialization%2A> 中获取它的静态实体。  
  
-   **标记扩展的位置参数：**此成员节点的名称是 `_PositionalParameters`，并且它在 XAML 语言 XAML 命名空间中进行定义。 它始终包含对象的泛型列表，其中每个对象都是通过以输入 XAML 提供的 `,` 分隔符拆分而预先分隔的位置参数。 可从 <xref:System.Xaml.XamlLanguage.PositionalParameters%2A> 中获取位置参数指令的静态实体。  
  
-   **未知内容：**此成员节点的名称是 `_UnknownContent`。 严格地说，它是 <xref:System.Xaml.XamlDirective>，并且在 XAML 语言 XAML 命名空间中定义。 在 XAML 对象元素包含源 XAML 中的内容但当前可用的 XAML 架构上下文中无法确认任何内容属性的情况下，此指令用作 sentinel。 可通过检查名为 `_UnknownContent` 的成员，在 XAML 节点流中检测此类情况。 如果加载路径 XAML 节点流中未执行其他操作，在遇到任何对象的 `_UnknownContent` 成员时将在尝试的 `WriteEndObject` 上引发默认 <xref:System.Xaml.XamlObjectWriter>。 默认 <xref:System.Xaml.XamlXmlWriter> 不会引发，并将成员视为隐式。 可以从 <xref:System.Xaml.XamlLanguage.UnknownContent%2A> 中获取 `_UnknownContent` 的静态实体。  
  
-   **集合的集合属性：**虽然用于 XAML 的集合类的后备 CLR 类型通常包含具有集合项的专用命名属性，但后备类型解决方案之前的 XAML 类型系统不具有此属性。 相反，XAML 节点流引入 `Items` 占位符作为集合 XAML 类型的成员。 在 .NET Framework XAML 服务实现中，节点流中此指令\/成员的名称为 `_Items`。 可以从 <xref:System.Xaml.XamlLanguage.Items%2A> 中获取此指令的常量。  
  
     请注意，XAML 节点流可能包含具有根据后备类型解决方案和 XAML 架构上下文不可解析的项的项属性。 例如，  
  
-   **XML 定义的成员：**XML 定义的 `xml:base`、`xml:lang` 和 `xml:space` 成员在 .NET Framework XAML 服务实现中分别报告为名为 `base`、`lang` 和 `space` 的 XAML 指令。 这些成员的命名空间是指 XML 命名空间 `http://www.w3.org/XML/1998/namespace`。 其中每个成员的常量都可从 <xref:System.Xaml.XamlLanguage> 获取。  
  
## 节点顺序  
 在某些情况下，<xref:System.Xaml.XamlXmlReader> 会根据在标记中查看或处理为 XML 时节点显示的顺序更改 XAML 节点流中的 XAML 节点顺序。 这是为了对节点进行排序，以便 <xref:System.Xaml.XamlObjectWriter> 可以仅向前的方式处理节点流。  在 .NET Framework XAML 服务中，为了针对节点流的 XAML 对象编写器使用者提高性能，XAML 读取器会重新对节点排序，而不是将此任务留给 XAML 编写器。  
  
 某些指令专用于提供从对象元素创建对象所需的详细信息。 这些指令包括： `Initialization`、`PositionalParameters`、`TypeArguments`、`FactoryMethod`、`Arguments`。 .NET Framework XAML 服务 XAML 读取器尝试将这些指令作为首批成员放置在对象的 `StartObject` 后的节点流中，原因将在下一节中介绍。  
  
### XamlObjectWriter 行为和节点顺序  
 <xref:System.Xaml.XamlObjectWriter> 的 `StartObject` 不一定是指示 XAML 对象编写器立即构造对象实例的信号。 XAML 包括多种语言功能，使用户可以使用附加输入初始化对象，并且不完全靠调用默认构造函数（而仅通过设置属性）来生成初始对象。 这些功能包括：<xref:System.Windows.Markup.XamlDeferLoadAttribute>；初始化文本；[x:TypeArguments](../../../docs/framework/xaml-services/x-typearguments-directive.md)；标记扩展的位置参数；工厂方法和关联的 [x:arguments](../../../docs/framework/xaml-services/x-arguments-directive.md) 节点（XAML 2009 年）。 其中每种情况都会延迟实际对象构造，并且因为对节点流重新排序，无论何时遇到不特定为此对象类型的构造指令的启动成员时，XAML 对象编写器都可依赖于实际构造实例的行为。  
  
### GetObject  
 `GetObject` 表示 XAML 节点，其中 XAML 对象编写器应转而获取对象的包含属性的值，而不是构造新对象。 当包含属性在后备类型的对象模型中不是故意为只读时，在 XAML 节点流中遇到 `GetObject` 节点的一种典型情况是针对集合对象或字典对象。 在此情况中，通常由拥有类型的初始化逻辑创建和初始化（通常为空）集合或字典。  
  
## 请参阅  
 <xref:System.Xaml.XamlObjectReader>   
 [XAML Services](../../../docs/framework/xaml-services/index.md)   
 [XAML Namespaces](../../../docs/framework/xaml-services/xaml-namespaces-for-net-framework-xaml-services.md)