---
title: "Defining Custom Types for Use with .NET Framework XAML Services | Microsoft Docs"
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
  - "defining custom types [XAML Services]"
ms.assetid: c2667cbd-2f46-4a7f-9dfc-53696e35e8e4
caps.latest.revision: 11
author: "wadepickett"
ms.author: "wpickett"
manager: "wpickett"
caps.handback.revision: 11
---
# Defining Custom Types for Use with .NET Framework XAML Services
如果要定义自定义类型，它们是业务对象或是对特定框架没有依赖项的类型，则可以遵循 XAML 的某些最佳做法。  如果您遵循这些做法，则 .NET Framework XAML 服务及其 XAML 读取器和 XAML 编写器可以发现类型中的 XAML 特征，并且使用 XAML 类型系统在 XAML 节点流中为其提供适当的表示形式。  本主题介绍类型定义、成员定义以及类型或成员的 CLR 特性化的最佳做法。  
  
## XAML 的构造函数模式和类型定义  
 为了能够实例化为 XAML 中的对象元素，自定义类必须满足以下要求：  
  
-   自定义类必须是公共的并且必须公开默认（无参数）公共构造函数。  （有关结构的说明，请参见以下各节。）  
  
-   自定义类不得是嵌套类。  全名路径中额外的“点”使得类命名空间区分不明确，并且妨碍了其他 XAML 功能（如附加属性）。  
  
 如果某个对象可以实例化为对象元素，则创建的对象可以填充任何属性（这些属性将该对象作为其基础类型）的属性元素形式。  
  
 如果启用了值转换器，您仍然可以为不符合这些条件的类型提供对象值。  有关更多信息，请参见 [Type Converters and Markup Extensions for XAML](../../../docs/framework/xaml-services/type-converters-and-markup-extensions-for-xaml.md)。  
  
### 结构  
 在 XAML 中，始终能够通过 CLR 定义来构造结构。  这是因为 CLR 编译器为结构隐式创建默认构造函数。  此构造函数将所有属性值初始化为它们的默认值。  
  
 在某些情况下，结构的默认构造行为不适用。  这可能是因为该结构在概念上作为一个联合同时用于填充值和函数。  作为一个联合，所含的值可能有互斥的解释，因此其属性都是不可设置的。  例如，WPF 词汇中的一个这类结构为 <xref:System.Windows.GridLength>。  这种结构应该实现类型转换器，以便可以使用为结构值创建不同解释或模式的字符串约定以特性形式表示值。  该结构还应通过非默认构造函数为代码构造公开类似的行为。  
  
### 接口  
 可以将接口用作成员的基础类型。  XAML 类型系统检查可赋值列表，并且期望作为值提供的对象可以赋值给接口。  接口必须表示为 XAML 类型的方式没有概念，只要相关可赋值类型支持 XAML 构造要求即可。  
  
### 工厂方法  
 工厂方法是 XAML 2009 功能。  这些方法修改了对象必须拥有默认构造函数的 XAML 原则。  本主题中不对工厂方法进行介绍。  请参见 [x:FactoryMethod Directive](../../../docs/framework/xaml-services/x-factorymethod-directive.md)。  
  
## 枚举  
 枚举具有 XAML 本机类型转换行为。  针对基础枚举类型解析 XAML 中指定的枚举常量名称，并将枚举值返回给 XAML 对象编写器。  
  
 XAML 通过应用 <xref:System.FlagsAttribute> 支持枚举的标志样式用法。  有关更多信息，请参见 [XAML 语法详述](../../../ocs/framework/wpf/advanced/xaml-syntax-in-detail.md)。  （[XAML 语法详述](../../../ocs/framework/wpf/advanced/xaml-syntax-in-detail.md) 是为 WPF 用户而编写，但该主题中的大部分信息与 XAML 相关，并不针对某个特定的实现框架。）  
  
## 成员定义  
 类型可定义用于 XAML 用法的成员。  类型可以定义 XAML 可用的成员，虽然特定类型不是 XAML 可用的。  这是由于存在 CLR 继承。  只要继承成员的某个类型支持 XAML 用法作为一个类型，并且该成员支持将 XAML 用法用于基础类型或具有可用的本机 XAML 语法，该成员就是 XAML 可用的。  
  
### 属性  
 如果使用典型 CLR `get` 和 `set` 访问器模式及适合于语言的关键字将属性定义为公共 CLR 属性，则 XAML 类型系统可以使用为 <xref:System.Xaml.XamlMember> 属性（如 <xref:System.Xaml.XamlMember.IsReadPublic%2A> 和 <xref:System.Xaml.XamlMember.IsWritePublic%2A>）提供的相应信息将属性报告为成员。  
  
 特定属性可以通过应用 <xref:System.ComponentModel.TypeConverterAttribute> 来启用文本语法。  有关更多信息，请参见 [Type Converters and Markup Extensions for XAML](../../../docs/framework/xaml-services/type-converters-and-markup-extensions-for-xaml.md)。  
  
 如果没有文本语法或本机 XAML 转换，并且没有进一步间接寻址（如标记扩展用法），则属性的类型（XAML 类型系统中的 <xref:System.Xaml.XamlMember.TargetType%2A>）必须能够通过将目标类型视为 CLR 类型而将实例返回给 XAML 对象编写器。  
  
 如果使用 XAML 2009，在不属于上述注意事项的情况下可以使用 [x:Reference Markup Extension](../../../docs/framework/xaml-services/x-reference-markup-extension.md) 来提供值；但这样与其说是类型定义问题，不如说是用法问题。  
  
### 事件  
 如果将事件定义为公共 CLR 事件，则 XAML 类型系统可以将事件报告为成员，同时 <xref:System.Xaml.XamlMember.IsEvent%2A> 为 `true`。  连接事件处理程序不在 .NET Framework XAML 服务功能的范围之内；这留给特定框架和实现。  
  
### 方法  
 方法的内联代码不是默认的 XAML 功能。  大多数情况下并不直接引用 XAML 中的方法成员，XAML 中的方法只是起到为特定 XAML 模式提供支持的作用。  [x:FactoryMethod Directive](../../../docs/framework/xaml-services/x-factorymethod-directive.md) 是一个异常。  
  
### 字段  
 CLR 设计原则不鼓励使用非静态字段。  对于静态字段来说，只能通过 [x:Static Markup Extension](../../../docs/framework/xaml-services/x-static-markup-extension.md) 来访问静态字段值；在这种情况下，不需在 CLR 定义中进行任何特殊操作来为 [x:Static](../../../docs/framework/xaml-services/x-static-markup-extension.md) 用法公开字段。  
  
## 可附加成员  
 可附加成员通过定义类型上的访问器方法模式向 XAML 公开。  作为一个对象，定义类型本身不需要是 XAML 可用的。  实际上，常见模式是声明一个服务类，其角色是拥有可附加成员并实现相关行为，但是不为任何其他功能（如 UI 表示形式）提供服务。  下文中的占位符*属性名*表示可附加成员的名称。  该名称在 [XamlName 语法](../../../docs/framework/xaml-services/xamlname-grammar.md)中必须有效。  
  
 请注意这些模式和类型的其他方法之间的名称冲突。  如果存在与其中一个模式匹配的成员，则 XAML 处理器可将该成员解释为一个可附加成员用法路径，即使这并不是您的意图。  
  
#### Get属性名 访问器  
 `Get` *属性名* 访问器的签名必须是：  
  
 `public static object Get` *PropertyName* `(object`  `target` `)`  
  
-   在实现中可以将 `target` 对象指定为更具体的类型。  可以使用它来限定可附加成员的使用范围；在所需范围之外使用将引发无效的强制转换异常，然后由 XAML 分析错误来呈现这些异常。  参数名不必非用 `target`，但在大多数实现中按照惯例命名为 `target`。  
  
-   可以在实现中将返回值指定为更具体的类型。  
  
 为了支持启用 <xref:System.ComponentModel.TypeConverter> 的文本语法用于可附加成员的特性用法，将 <xref:System.ComponentModel.TypeConverterAttribute> 应用于 `Get`*属性名* 访问器。  应用于 `get` 而不是 `set` 可能看起来不太直观；但是此约定可以支持可序列化的只读可附加成员的概念，这对于设计器方案非常有用。  
  
#### Set属性名 访问器  
 Set*属性名* 访问器的签名必须是：  
  
 `public static void Set` *PropertyName* `(object`  `target` `, object`  `value` `)`  
  
-   在实现中可以将 `target` 对象指定为更具体的类型，逻辑和结果与上节所述相同。  
  
-   在实现中可以将 `value` 对象指定为更具体的类型。  
  
 请记住，此方法的值是来自 XAML 用法的输入，通常采用特性形式。  在特性形式中，必须有针对文本语法的值转换器支持，并且要对 `Get`*属性名* 访问器进行特性化。  
  
### 可附加成员存储  
 访问器方法通常无法将可附加成员值放入对象图，也无法从对象图中检索出值并正确地序列化这些值。  为了提供此功能，以前的访问器签名中的 `target` 对象必须能够存储值。  存储机制应与可附加成员原则（即，成员可附加到成员列表中不包含该可附加成员的目标）一致。  .NET Framework XAML 服务通过 API <xref:System.Xaml.IAttachedPropertyStore> 和 <xref:System.Xaml.AttachablePropertyServices> 为可附加成员存储提供了一种实现方法。  <xref:System.Xaml.IAttachedPropertyStore> 由 XAML 编写器用于发现存储实现，应对作为访问器的 `target` 的类型实现。  静态 <xref:System.Xaml.AttachablePropertyServices> API 在访问器体中使用，并通过可附加成员的 <xref:System.Xaml.AttachableMemberIdentifier> 引用该成员。  
  
## 与 XAML 有关的 CLR 特性  
 为了向 .NET Framework XAML 服务报告 XAML 类型系统信息，正确地特性化类型、成员和程序集是非常重要的。  这与您是否希望直接基于.NET Framework XAML 服务 XAML 读取器和 XAML 编写器将类型用于 XAML 系统有关，或者与您是否基于这些 XAML 读取器和 XAML 编写器定义或使用利用 XAML 的框架有关。  
  
 有关与自定义类型的 XAML 支持有关的每个 XAML 相关特性的列表，请参见[XAML\-Related CLR Attributes for Custom Types and Libraries](../../../docs/framework/xaml-services/xaml-related-clr-attributes-for-custom-types-and-libraries.md)。  
  
## 用法  
 使用自定义类型要求标记作者必须映射包含自定义类型的程序集和 CLR 命名空间的前缀。  本主题中不对此过程进行介绍。  
  
## 访问级别  
 XAML 提供一种方式来加载和实例化具有 `internal` 访问级别的类型。  提供此功能是为了使用户代码可以定义自己的类型，然后从也属于该用户代码范围的标记实例化这些类。  
  
 来自 WPF 的一个示例是只要用户代码定义具有以下特点的 <xref:System.Windows.Controls.UserControl> 时：旨在用作重构 UI 行为的方式，但不属于任何可以通过使用 `public` 访问级别声明支持类来暗示的可能扩展机制。  如果后备代码编译为它从其引用为 XAML 类型的相同程序集，则可以使用 `internal` 访问声明这样一个 <xref:System.Windows.Controls.UserControl>。  
  
 对于在完全信任下加载 XAML 并使用 <xref:System.Xaml.XamlObjectWriter> 的应用程序，始终启用 `internal` 访问级别的类加载。  
  
 对于在部分信任下加载 XAML 的应用程序，可以使用 <xref:System.Xaml.Permissions.XamlAccessLevel> API 控制访问级别特征。  此外，延迟机制（如 WPF 模板系统）必须能够传播任何访问级别权限并为最终运行时计算保留这些权限；这是通过传递 <xref:System.Xaml.Permissions.XamlAccessLevel> 信息在内部处理的。  
  
### WPF 实现  
 如果 BAML 在部分信任下加载，则会将访问限制到作为 BAML 源的程序集的 <xref:System.Xaml.Permissions.XamlAccessLevel.AssemblyAccessTo%2A>，在这种情况下，WPF XAML 使用部分信任访问模型。  对于延迟，WPF 使用 <xref:System.Xaml.IXamlObjectWriterFactory.GetParentSettings%2A?displayProperty=fullName> 作为传递访问级别信息的机制。  
  
 在 WPF XAML 术语中，内部类型指还包含引用 XAML 的程序集所定义的类型。  这类类型可以通过有意省略映射的 assembly\= 部分的 XAML 命名空间（例如 `xmlns:local="clr-namespace:WPFApplication1"`）进行映射。  如果 BAML 引用一个内部类型，并且该类型具有 `internal` 访问级别，则会为程序集生成 `GeneratedInternalTypeHelper` 类。  如果要避免 `GeneratedInternalTypeHelper`，则必须使用 `public` 访问级别，或必须将相关类包含在单独的程序集中并使该程序集相关。  
  
## 请参阅  
 [XAML\-Related CLR Attributes for Custom Types and Libraries](../../../docs/framework/xaml-services/xaml-related-clr-attributes-for-custom-types-and-libraries.md)   
 [XAML Services](../../../docs/framework/xaml-services/index.md)