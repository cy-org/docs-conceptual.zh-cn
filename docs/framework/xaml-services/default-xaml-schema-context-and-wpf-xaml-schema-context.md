---
title: "Default XAML Schema Context and WPF XAML Schema Context | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-wpf"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 04e06a15-09b3-4210-9bdf-9a64c2eccb83
caps.latest.revision: 7
author: "wadepickett"
ms.author: "wpickett"
manager: "wpickett"
caps.handback.revision: 7
---
# Default XAML Schema Context and WPF XAML Schema Context
XAML 架构上下文是限定使用特定 XAML 词汇的 XAML 生产如何与对象编写行为进行交互（包括类型映射如何解析，如何加载程序集，如何解释特定的读取器和编写器设置）的概念实体。  本主题介绍 .NET Framework XAML 服务的功能和基于 CLR 类型系统的关联默认 XAML 架构上下文。  本主题还介绍用于 WPF 的 XAML 架构上下文。  
  
## 默认 XAML 架构上下文  
 .NET Framework XAML 服务实现并使用默认 XAML 架构上下文。  默认 XAML 架构上下文行为在 <xref:System.Xaml.XamlSchemaContext> 类的 API 中并不总是完全可见。  不过，在许多情况下，默认 XAML 架构上下文所影响的行为可通过 XAML 类型系统的公共 API（如 <xref:System.Xaml.XamlMember> 或 <xref:System.Xaml.XamlType> 的成员）或通过在使用默认 XAML 架构上下文的 XAML 读取器和 XAML 编写器上公开的 API 进行观察。  
  
 可通过调用 <xref:System.Xaml.XamlSchemaContext> 构造函数来创建封装默认行为的 <xref:System.Xaml.XamlSchemaContext>。  这将显式创建默认 XAML 架构上下文。  如果使用未显式采用 <xref:System.Xaml.XamlSchemaContext> 输入参数的 API 来初始化 XAML 读取器或 XAML 编写器，则会隐式创建相同的默认 XAML 架构上下文。  
  
 默认 XAML 架构上下文依赖于 CLR 对其类型映射行为的反射。  这包括检查定义 CLR <xref:System.Type> 以及相关的 <xref:System.Reflection.PropertyInfo> 或 <xref:System.Reflection.MethodInfo>。  此外，还会使用针对类型或成员的 CLR 特性，以便填充使用 CLR 后备类型的 XAML 类型或 XAML 成员信息的具体信息。  默认 XAML 架构上下文不需要类型系统扩展技术（如 `Invoker` 模式），因为可从 CLR 类型系统获得必要信息。  
  
 对于程序集加载逻辑，默认 XAML 架构上下文主要依赖于在 XAML 命名空间映射中提供的任何程序集值。  此外，<xref:System.Xaml.XamlReaderSettings.LocalAssembly%2A> 还可以为方案（如加载内部类型）提示要加载的程序集。  
  
## WPF XAML 架构上下文  
 本主题介绍了 WPF XAML 架构上下文，因为 WPF 实现提供了可通过实现非默认 XAML 架构上下文引入的功能类型的有趣说明。  而且，在介绍 WPF XAML 的 WPF 文档中，没有深入讨论 XAML 架构上下文概念；仅当一并讨论默认 XAML 架构上下文的工作方式时，才可以完全理解 XAML 架构上下文所实现的行为。  WPF XAML 架构上下文实现以下行为。  
  
 **查找重写：**WPF 具有几个 XAML 内容模型，其中存在未经 <xref:System.Windows.Markup.ContentPropertyAttribute> 特性化而起作用的 XAML 内容属性。  针对 WPF 的 <xref:System.Xaml.XamlType.LookupContentProperty%2A> 重写可实现此行为。  
  
 **WPF 表达式延迟：**WPF 具有将值延迟到运行时上下文可用时为止的多个表达式类。  模板扩展也是依赖于延迟技术的一种运行时行为。  
  
 **类型系统查找优化：**WPF 具有广泛的 XAML 词汇和对象模型，包括继承到数以百计的 WPF 定义类的基类成员定义。  WPF 本身也分布到多个程序集中。  WPF 使用查找表和其他技术来优化其类型查找。  这样就会通过默认 XAML 架构上下文及其基于 CLR 的类型查找来提供性能改进。  当查找表中不存在类型时，该行为将使用与默认 XAML 架构上下文类似的 XAML 架构上下文技术。  
  
 **XamlType 和 XamlMember 扩展：**WPF 使用依赖项属性来扩展属性概念，并使用路由事件来扩展事件概念。  为了针对 XAML 处理操作为这些概念提供更高的可见性，WPF 扩展了 <xref:System.Xaml.XamlType> 和 <xref:System.Xaml.XamlMember>，并添加了报告依赖项属性和路由事件特征的内部属性。  
  
### 访问 WPF XAML 架构上下文  
 如果您使用基于 WPF <xref:System.Windows.Markup.XamlReader?displayProperty=fullName> 或 <xref:System.Windows.Markup.XamlWriter?displayProperty=fullName> 的 XAML 技术，则 WPF XAML 架构上下文已在这些 XAML 读取器和 XAML 编写器实现中使用。  
  
 如果您使用未通过 WPF XAML 架构上下文进行初始化的其他 XAML 读取器或 XAML 编写器实现，则可以从 <xref:System.Windows.Markup.XamlReader.GetWpfSchemaContext%2A?displayProperty=fullName> 获取工作 WPF XAML 架构上下文。  然后，可以使用此值作为使用 <xref:System.Xaml.XamlSchemaContext> 的其他 API 的初始化值。  例如，可以调用 <xref:System.Xaml.XamlXmlReader.%23ctor%2A> 以进行初始化，然后传递 WPF XAML 架构上下文。  或者，可以将 WPF XAML 架构上下文用于 XAML 类型系统操作。  这可能包括 <xref:System.Xaml.XamlType> 或 <xref:System.Xaml.XamlMember> 的构造初始化，或调用 <xref:System.Xaml.XamlSchemaContext.GetXamlType%2A?displayProperty=fullName>。  
  
 请注意，如果从单纯的 XAML 节点流角度来访问 WPF XAML 的某些方面，则某些 WPF 框架功能可能尚未起作用。  例如，尚未应用控件的 WPF 模板。  因此，如果您访问在运行时可能使用整个可视化树填充的属性，则可能只会看到引用某一模板的属性值。  如果为 WPF 标记扩展提供的服务上下文是从非运行时环境提供的，则该上下文也可能不准确，并可能导致在尝试写对象图时出现异常。  
  
## XAML 和程序集加载  
 XAML 和 .NET Framework XAML 服务的程序集加载与 CLR 定义的 <xref:System.AppDomain> 概念进行集成。  XAML 架构上下文解释如何基于 <xref:System.AppDomain> 的使用和其他因素在运行时或设计时加载程序集或查找类型。  该逻辑根据以下具体情况而稍有不同：该 XAML 对于 XAML 读取器是否是宽松 XAML，是否是由 `XamlBuildTask` 编译到 DLL 中的 XAML，或者是否是由 WPF 的 `PresentationBuildTask` 生成的 BAML。  
  
 WPF 的 XAML 架构上下文与 WPF 应用程序模型集成，而后者使用 <xref:System.AppDomain> 以及作为 WPF 实现详细信息的其他因素。  
  
#### XAML 读取器输入（宽松 XAML）  
  
1.  XAML 架构上下文循环访问应用程序的 <xref:System.AppDomain>，并从最新加载的程序集开始，查找与该名称的所有方面匹配的已加载程序集。  如果找到匹配的程序集，则将该程序集用于解析。  
  
2.  否则，将使用基于 CLR <xref:System.Reflection.Assembly> API 的以下技术之一来加载程序集：  
  
    -   如果该名称在映射中是限定名称，则对该限定名称调用 <xref:System.Reflection.Assembly.Load%28System.String%29?displayProperty=fullName>。  
  
    -   如果上一步失败，则使用短名称和公钥标记（如果存在）来调用 <xref:System.Reflection.Assembly.Load%28System.String%29?displayProperty=fullName>。  
  
    -   如果该名称在映射中是非限定名称，则调用 <xref:System.Reflection.Assembly.LoadWithPartialName%2A?displayProperty=fullName>。  
  
#### XamlBuildTask  
 `XamlBuildTask` 用于 [!INCLUDE[vsindigo](../../../includes/vsindigo-md.md)] 和 [!INCLUDE[TLA#tla_workflow](../../../includes/tlasharptla-workflow-md.md)]。  
  
 请注意，通过 `XamlBuildTask` 进行的程序集引用始终是完全限定引用。  
  
1.  对限定名称调用 <xref:System.Reflection.Assembly.Load%28System.String%29?displayProperty=fullName>。  
  
2.  如果上一步失败，则使用短名称和公钥标记（如果存在）来调用 <xref:System.Reflection.Assembly.Load%28System.String%29?displayProperty=fullName>。  
  
#### BAML \(PresentationBuildTask\)  
 BAML 的程序集加载分为两个方面：加载包含 BAML 的初始程序集作为组件，为由 BAML 生产引用的任何类型加载支持该类型的程序集。  
  
##### 初始标记的程序集加载：  
 对要从其加载标记的程序集的引用始终是非限定引用。  
  
1.  WPF XAML 架构上下文循环访问 WPF 应用程序的 <xref:System.AppDomain>，并从最新加载的程序集开始，查找与该名称的所有方面匹配的已加载程序集。  如果找到匹配的程序集，则将该程序集用于解析。  
  
2.  如果上一步失败，则使用短名称和公钥标记（如果存在）来调用 <xref:System.Reflection.Assembly.Load%28System.String%29?displayProperty=fullName>。  
  
##### 按 BAML 类型进行的程序集引用：  
 针对在 BAML 生产中使用的类型的程序集引用始终是完全限定引用（作为生成任务的一项输出）。  
  
1.  WPF XAML 架构上下文循环访问 WPF 应用程序的 <xref:System.AppDomain>，并从最新加载的程序集开始，查找与该名称的所有方面匹配的已加载程序集。  如果找到匹配的程序集，则将该程序集用于解析。  
  
2.  否则，将使用以下技术中之一来加载程序集：  
  
    -   对限定名称调用 <xref:System.Reflection.Assembly.Load%28System.String%29?displayProperty=fullName>。  
  
    -   如果短名称 \+ 公钥标记的组合与从其加载 BAML 的程序集匹配，则使用该程序集。  
  
    -   使用短名称 \+ 公钥标记来调用 <xref:System.Reflection.Assembly.Load%28System.String%29?displayProperty=fullName>。  
  
## 请参阅  
 [Understanding XAML Node Stream Structures and Concepts](../../../docs/framework/xaml-services/understanding-xaml-node-stream-structures-and-concepts.md)