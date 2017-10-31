---
title: "XAML Namespaces for .NET Framework XAML Services | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-wpf"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: e4f15f13-c420-4c1e-aeab-9b6f50212047
caps.latest.revision: 3
author: "wadepickett"
ms.author: "wpickett"
manager: "wpickett"
caps.handback.revision: 3
---
# XAML Namespaces for .NET Framework XAML Services
XAML 命名空间是从 XML 命名空间定义扩展的概念。  与 XML 命名空间类似，可以在标记中使用 `xmlns` 特性定义 XAML 命名空间。  XAML 节点流和其他 XAML 服务 API 中也包含 XAML 命名空间。  本主题定义 XAML 命名空间概念，介绍如何定义 XAML 命名空间并将其用于 XAML 架构上下文以及 .NET Framework XAML 服务的其他方面。  
  
## XML 命名空间与 XAML 命名空间  
 XAML 命名空间是一种特殊的 XML 命名空间，就像 XAML 是 XML 的特殊形式一样，它使用基本的 XML 形式作为标记。  在标记中，通过对某一元素应用 `xmlns` 特性声明 XAML 命名空间及其映射。  可以对在其中声明了 XAML 命名空间的元素进行 `xmlns` 声明。  对某一元素进行的 XAML 命名空间声明对该元素、该元素的所有特性以及该元素的所有子级有效。  特性可以使用与包含该特性的元素不同的 XAML 命名空间，只要特性名本身在标记语言中将前缀作为其特性名部分引用即可。  
  
 XAML 命名空间与 XML 命名空间的区别在于，XML 命名空间可用来引用架构，或用来简单地区分实体。  对于 XAML，XAML 中使用的类型和成员最终必须解析为后备类型，而 XML 架构概念不能很好地应用于此功能。  XAML 命名空间包含 XAML 架构上下文执行此类型映射必需的信息。  
  
## XAML 命名空间组成  
 XAML 命名空间定义有两个组成部分：前缀和标识符。  在标记中声明 XAML 命名空间或在 XAML 类型系统中定义 XAML 命名空间时，会显示每个组成部分。  
  
 前缀可以是 [W3C Namespaces in XML 1.0 specification](http://go.microsoft.com/fwlink/?LinkID=161735)（XML 1.0 中的 W3C 命名空间规范）中允许的任何字符串。  依照惯例，前缀通常是非常短的字符串，因为在典型的标记文件中，前缀要重复很多次。  某些用于多个 XAML 实现的 XAML 命名空间使用专门的常规前缀。  例如，XAML 语言 XAML 命名空间通常使用前缀 `x` 进行映射。  您可以定义一个默认 XAML 命名空间，其前缀不是在定义中给定的，而是以一个空字符串表示（如果由 .NET Framework XAML 服务 API 定义或查询）。  通常，默认 XAML 命名空间的选择要慎重，以便通过 XAML 实现技术及其方案和词汇表最大程度地省略前缀标记。  
  
 标识符可以是 [W3C Namespaces in XML 1.0 specification](http://go.microsoft.com/fwlink/?LinkID=161735)（XML 1.0 中的 W3C 命名空间规范）中允许的任何字符串。  根据约定，XML 命名空间或 XAML 命名空间的标识符常常以 URI 形式给出，通常为协议限定的绝对 URI。  通常，定义特定 XAML 词汇的版本信息表示路径字符串的一部分。  除 XML URI 约定外，XAML 命名空间还添加了附加标识符约定。  对于 XAML 命名空间，标识符就 XAML 架构上下文解析在 XAML 命名空间下指定为元素的类型或将特性解析为成员所需的信息进行通信。  
  
 为将信息传递给 XAML 架构上下文，XAML 命名空间的标识符必须采用 URI 形式。  但是，在这种情况下，URI 也声明为一个特定程序集或程序集列表中的匹配标识符。  这是通过在程序集中为该程序集赋予 <xref:System.Windows.Markup.XmlnsDefinitionAttribute> 特性完成的。  .NET Framework XAML 服务中的默认 XAML 架构上下文支持这种标识 XAML 命名空间并支持特性程序集中基于 CLR 的类型解析行为的方法。  更一般地说，这种转换可用于 XAML 架构上下文合并 CLR 或基于默认 XAML 架构上下文的情况，这是从 CLR 程序集读取 CLR 特性所必需的。  
  
 XAML 命名空间也可以由 CLR 命名空间和类型定义程序集之间的通信约定进行标识。  此约定适用于包含类型的程序集中没有 <xref:System.Windows.Markup.XmlnsDefinitionAttribute> 特性的情况。  此约定可能比 URI 约定更复杂，还可能导致歧义和重复，这是因为有多种引用程序集的方法。  
  
 使用 CLR 命名空间和程序集约定的最基本的标识符形式如下：  
  
 `clr-namespace:` *clrnsName* `; assembly=` *assemblyShortName*  
  
 `clr-namespace:` 和 `; assembly=` 是语法的文本组成部分。  
  
 *clrnsName* 是标识 CLR 命名空间的字符串名称。  此字符串名称包括所有内部点字符 \(.\)，这些点字符就 CLR 命名空间及其与其他 CLR 命名空间的关系提供提示。  
  
 *assemblyShortName* 是一个程序集的字符串名称，该程序集定义在 XAML 中有用的类型。  要通过声明的 XAML 命名空间访问的类型应由程序集定义，并在 *clrnsName* 指定的 CLR 命名空间中明确声明。  通常，此字符串名称提供的信息与 <xref:System.Reflection.AssemblyName.Name%2A?displayProperty=fullName> 报告的信息类似。  
  
 下面是更完整的 CLR 命名空间和程序集约定定义：  
  
 `clr-namespace:` *clrnsName* `; assembly=` *assemblyName*  
  
 *assemblyName* 表示作为合法的 <xref:System.Reflection.Assembly.Load%28System.String%29?displayProperty=fullName> 输入的任意字符串。  此字符串可以包含区域性、公钥或版本信息（<xref:System.Reflection.Assembly> 参考主题中定义了这些概念的定义）。  COFF 格式和证据（由其他 <xref:System.Reflection.Assembly.Load%2A> 重载使用）与 XAML 程序集加载目的无关；所有负载信息都必须表示为一个字符串。  
  
 为程序集指定公钥是有用的 XAML 安全性方法，也可以消除用简单名称加载程序集时可能存在的歧义，或者之前在缓存或应用程序域中存在的歧义。  有关更多信息，请参见 [XAML Security Considerations](../../../docs/framework/xaml-services/xaml-security-considerations.md)。  
  
## XAML 服务 API 中的 XAML 命名空间声明  
 在 XAML 服务 API 中，XAML 命名空间声明由 <xref:System.Xaml.NamespaceDeclaration> 对象表示。  在代码中声明 XAML 命名空间时，需要调用 <xref:System.Xaml.NamespaceDeclaration.%23ctor%28System.String%2CSystem.String%29> 构造函数。  `ns` 和 `prefix` 参数指定为字符串，要为这些参数提供的输入对应于本主题前面介绍的 XAML 命名空间标识符和 XAML 命名空间前缀的定义。  
  
 如果作为 XAML 节点流的一部分或通过 XAML 类型系统的其他访问检查 XAML 命名空间信息，则 <xref:System.Xaml.NamespaceDeclaration.Namespace%2A?displayProperty=fullName> 报告 XAML 命名空间标识符，<xref:System.Xaml.NamespaceDeclaration.Prefix%2A?displayProperty=fullName> 报告 XAML 命名空间前缀。  
  
 在 XAML 节点流中，XAML 命名空间信息可显示为一个 XAML 节点，该节点位于其应用实体之前。  这包括 XAML 命名空间信息在 XAML 根元素的 `StartObject` 之前的情况。  有关更多信息，请参见[Understanding XAML Node Stream Structures and Concepts](../../../docs/framework/xaml-services/understanding-xaml-node-stream-structures-and-concepts.md)。  
  
 对于很多使用 .NET Framework XAML 服务 API 的方案来说，至少应该存在一个 XAML 命名空间声明，并且声明必须包含或引用 XAML 架构上下文需要的信息。  XAML 命名空间必须指定要加载的程序集或帮助解析 XAML 架构上下文已加载或已知的命名空间和程序集中的特定类型。  
  
 为生成 XAML 节点流，XAML 类型信息必须通过 XAML 架构上下文可用。  要确定 XAML 类型信息，必须先确定要创建的每个节点的相关 XAML 命名空间。  这时，尚未创建任何类型实例，但 XAML 架构上下文可能需要从定义程序集和后备类型查找信息。  例如，为了处理标记 `<Party><PartyFavor/></Party>`，XAML 架构上下文必须能够确定 `Party` 的 `ContentProperty` 的名称和类型，因而必须知道 `Party` 和 `PartyFavor` 的 XAML 命名空间信息。  在默认 XAML 架构上下文的情况下，静态反射会报告很多 XAML 类型系统信息，在节点流中生成 XAML 类型节点需要这些信息。  
  
 为从 XAML 节点流生成对象图，原始标记中的每个 XAML 前缀都必须存在相应的 XAML 命名空间声明并记录在 XAML 节点流中。  这时，将创建实例，发生真正的类型映射行为。  
  
 如果需要预填充 XAML 命名空间信息，而未在标记中定义 XAML 架构上下文要使用的 XAML 命名空间，则可以使用以下方法，即在 <xref:System.Xml.XmlReader> 的 <xref:System.Xml.XmlParserContext> 中声明 XML 命名空间声明。  然后使用 <xref:System.Xml.XmlReader> 作为 XAML 读取器构造函数或 <xref:System.Xaml.XamlServices.Load%28System.Xml.XmlReader%29?displayProperty=fullName> 的输入。  
  
 与 .NET Framework XAML 服务中的 XAML 命名空间处理相关的另外两个 API 是 <xref:System.Windows.Markup.XmlnsDefinitionAttribute> 和 <xref:System.Windows.Markup.XmlnsPrefixAttribute> 特性。  这些特性适用于程序集。  <xref:System.Windows.Markup.XmlnsDefinitionAttribute> 由 XAML 架构上下文用来解释包含 URI 的任意 XAML 命名空间声明。  <xref:System.Windows.Markup.XmlnsPrefixAttribute> 由发出 XAML 的工具使用，以便使用可预测前缀序列化特定的 XAML 命名空间。  有关更多信息，请参见[XAML\-Related CLR Attributes for Custom Types and Libraries](../../../docs/framework/xaml-services/xaml-related-clr-attributes-for-custom-types-and-libraries.md)。  
  
## 请参阅  
 [Understanding XAML Node Stream Structures and Concepts](../../../docs/framework/xaml-services/understanding-xaml-node-stream-structures-and-concepts.md)