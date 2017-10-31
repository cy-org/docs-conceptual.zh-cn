---
title: "XAML Services | Microsoft Docs"
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
  - "XAML [XAML Services], System.Xaml concepts"
  - "XAML Services in WPF [XAML Services]"
  - "System.Xaml [XAML Services], conceptual documentation"
ms.assetid: 0e11f386-808c-4eae-9ba6-029ad7ba2211
caps.latest.revision: 13
author: "wadepickett"
ms.author: "wpickett"
manager: "wpickett"
caps.handback.revision: 13
---
# XAML Services
本主题介绍称为 .NET Framework XAML 服务的技术集的功能。  描述的服务和 API 大多数都位于程序集 System.Xaml 中，该程序集是随 .NET 核心程序集的 [!INCLUDE[net_v40_short](../../../includes/net-v40-short-md.md)] 集一起引入的。  这些服务包括读取器和编写器、架构类、架构支持、工厂、类的特性化、XAML 语言内部函数支持以及其他 XAML 语言功能。  
  
## 本文档相关信息  
 .NET Framework XAML 服务的概念文档假定您以前使用过 XAML 语言，并且知道如何将其应用于特定框架（例如 [!INCLUDE[TLA#tla_winclient](../../../includes/tlasharptla-winclient-md.md)] 或 [!INCLUDE[TLA#tla_workflow](../../../includes/tlasharptla-workflow-md.md)]）或者应用于特定技术功能区域（例如，<xref:Microsoft.Build.Framework.XamlTypes> 中的生成自定义功能）。  本文档不介绍 XAML 作为一种标记语言的基础知识、XAML 语法术语或其他介绍性材料。  而本文档专门介绍如何使用在 System.Xaml 程序集库中启用的 .NET Framework XAML 服务。  这些 API 大多数都针对 XAML 语言集成和扩展性方案。  这可能包括以下几方面：  
  
-   扩展基本 XAML 读取器或 XAML 编写器的功能（直接处理 XAML 节点流；派生自己的 XAML 读取器或 XAML 编写器）。  
  
-   定义 XAML 可用的自定义类型（这些类型没有特定的框架依赖项），并将这些类型特性化以将其 XAML 类型系统特性传递给 .NET Framework XAML 服务。  
  
-   承载 XAML 读取器或 XAML 编写器以作为应用程序的组件，如 XAML 标记源的可视化设计器或交互式编辑器。  
  
-   编写 XAML 值转换器（标记扩展；自定义类型的类型转换器）。  
  
-   定义自定义 XAML 架构上下文（使用用于后备类型源的备用程序集加载技术；使用类型已知的查找技术而不是始终反射程序集；使用加载的程序集概念，这些概念不使用 CLR `AppDomain` 及其关联的安全模型）。  
  
-   扩展基本 XAML 类型系统。  
  
-   使用 `Lookup` 或 `Invoker` 技术影响 XAML 类型系统以及计算类型后备的方式。  
  
 如果您正在查找有关 XAML 作为一种语言的介绍性材料，则可尝试参见 [XAML 概述 \(WPF\)](../../../ocs/framework/wpf/advanced/xaml-overview-wpf.md)。  该主题为不熟悉 [!INCLUDE[TLA#tla_winclient](../../../includes/tlasharptla-winclient-md.md)] 也不会使用 XAML 标记和 XAML 语言功能的用户介绍 XAML。  另一个有用的文档为 [XAML 语言规范](http://go.microsoft.com/fwlink/?LinkId=114525)中的介绍性材料。  
  
## .NET 结构中的 .NET Framework XAML 服务和 System.Xaml  
 在以前版本的 [!INCLUDE[TLA#tla_netframewk](../../../includes/tlasharptla-netframewk-md.md)] 中，对 XAML 语言功能的支持是由在 [!INCLUDE[TLA#tla_netframewk](../../../includes/tlasharptla-netframewk-md.md)]（[!INCLUDE[TLA#tla_winclient](../../../includes/tlasharptla-winclient-md.md)]、[!INCLUDE[TLA#tla_workflow](../../../includes/tlasharptla-workflow-md.md)] 和 [!INCLUDE[vsindigo](../../../includes/vsindigo-md.md)]）上生成的框架实现的，因此其行为以及使用的 API 因您所使用的具体框架而有所不同。  这包括 XAML 分析器及其对象图创建机制、XAML 语言内部函数、序列化支持等。  
  
 在 [!INCLUDE[net_v40_long](../../../includes/net-v40-long-md.md)]中，.NET Framework XAML 服务和 System.Xaml 程序集定义了支持 XAML 语言功能所需的大部分内容。  这包括 XAML 读取器和 XAML 编写器的基类。  向 .NET Framework XAML 服务中添加的最重要功能（任何框架特定 XAML 实现中没有的功能）是 XAML 的类型系统表示形式。  该类型系统表示形式以面向对象的方式表示 XAML，该方式侧重于 XAML 功能，而不依赖于框架的特定功能。  
  
 XAML 类型系统不受 XAML 来源的标记形式或运行时特定信息的限制，也不受任何特定后备类型系统的限制。  XAML 类型系统包括类型、成员、XAML 架构上下文、XML 级别的概念以及其他 XAML 语言概念或 XAML 内部函数的对象表示形式。  使用或扩展 XAML 类型系统，可以从像 XAML 读取器和 XAML 编写器这样的类派生，并且可以将 XAML 表示形式的功能扩展到由使用或发出 XAML 的框架、技术或应用程序启用的特定功能中。  XAML 架构上下文的概念支持通过 XAML 对象编写器实现、通过上下文中程序集信息进行通信的某种技术的后备类型系统以及 XAML 节点源的组合编写实际对象图。  有关 XAML 架构概念的更多信息，  请参见 [Default XAML Schema Context and WPF XAML Schema Context](../../../docs/framework/xaml-services/default-xaml-schema-context-and-wpf-xaml-schema-context.md)。  
  
## XAML 节点流、XAML 读取器和 XAML 编写器  
 若要了解 .NET Framework XAML 服务在 XAML 语言与将 XAML 用作语言的特定技术之间的关系中发挥的作用，了解 XAML 节点流的概念以及该概念形成 API 和术语的方式会非常有用。  XAML 节点流是介于 XAML 语言表示形式与 XAML 表示或定义的对象图之间的中间概念。  
  
-   XAML 读取器是以某种形式处理 XAML 并生成 XAML 节点流的实体。  在 API 中，XAML 读取器由基类 <xref:System.Xaml.XamlReader> 表示。  
  
-   XAML 编写器是处理 XAML 节点流并生成其他内容的实体。  在 API 中，XAML 编写器由基类 <xref:System.Xaml.XamlWriter> 表示。  
  
 涉及 XAML 的两个最常见情况是加载 XAML 以实例化对象图，以及保存来自某个应用程序或工具的对象图并生成 XAML 表示形式（通常以标记形式保存为文本文件）。  在本文档中，加载 XAML 和创建对象图通常称为加载路径。  在本文档中，将现有对象图保存或序列化为 XAML 通常称为保存路径。  
  
 最常见的加载路径类型如下所述：  
  
-   从 XAML 表示形式开始，再到采用 UTF 编码的 XML 格式并保存为文本文件。  
  
-   将该 XAML 加载到 <xref:System.Xaml.XamlXmlReader> 中。  <xref:System.Xaml.XamlXmlReader> 是 <xref:System.Xaml.XamlReader> 子类。  
  
-   结果是 XAML 节点流。  使用 <xref:System.Xaml.XamlXmlReader> \/ <xref:System.Xaml.XamlReader> API 可访问 XAML 节点流的各个节点。  此处最典型的操作是在 XAML 节点流中向前推进，从而使用“当前记录”形式处理每个节点。  
  
-   将生成的节点从 XAML 节点流传递给 <xref:System.Xaml.XamlObjectWriter> API。  <xref:System.Xaml.XamlObjectWriter> 是 <xref:System.Xaml.XamlWriter> 子类。  
  
-   <xref:System.Xaml.XamlObjectWriter> 根据通过源 XAML 节点流的进度写入对象图，每次写入一个对象。  该操作在 XAML 架构上下文以及可以访问后备类型系统和框架的程序集和类型的实现的协助下完成。  
  
-   在 XAML 节点流的末尾调用 <xref:System.Xaml.XamlObjectWriter.Result%2A> 以获取对象图的根对象。  
  
 最常见的保存路径类型如下所述：  
  
-   从整个应用程序运行时的对象图开始，再到运行时的 UI 内容和状态或运行时整个应用程序对象表示形式的较小分段。  
  
-   从逻辑起始对象（如应用程序根或文档根），将对象加载到 <xref:System.Xaml.XamlObjectReader> 中。  <xref:System.Xaml.XamlObjectReader> 是 <xref:System.Xaml.XamlReader> 子类。  
  
-   结果是 XAML 节点流。  可使用 <xref:System.Xaml.XamlObjectReader> 和 <xref:System.Xaml.XamlReader> API 来访问 XAML 节点流的各个节点。  此处最典型的操作是在 XAML 节点流中向前推进，从而使用“当前记录”形式处理每个节点。  
  
-   将生成的节点从 XAML 节点流传递给 <xref:System.Xaml.XamlXmlWriter> API。  <xref:System.Xaml.XamlXmlWriter> 是 <xref:System.Xaml.XamlWriter> 子类。  
  
-   <xref:System.Xaml.XamlXmlWriter> 采用 XML UTF 编码编写 XAML。  可以将其另存为文本文件、流或其他形式。  
  
-   调用 <xref:System.Xaml.XamlXmlWriter.Flush%2A> 以获取最终输出。  
  
 有关 XAML 节点流概念的更多信息，请参见[Understanding XAML Node Stream Structures and Concepts](../../../docs/framework/xaml-services/understanding-xaml-node-stream-structures-and-concepts.md)。  
  
### XamlServices 类  
 并不总是需要处理 XAML 节点流。  如果您需要基本加载路径或基本保存路径，则可以在 <xref:System.Xaml.XamlServices> 类中使用 API。  
  
-   <xref:System.Xaml.XamlServices.Load%2A> 的各种签名实现加载路径。  通过使用该读取器的 API 进行加载，可以加载文件或流，也可以加载包装您的 XAML 输入的 <xref:System.Xml.XmlReader>、<xref:System.IO.TextReader> 或 <xref:System.Xaml.XamlReader>。  
  
-   <xref:System.Xaml.XamlServices.Save%2A> 的各种签名保存对象图并以流、文件或 <xref:System.Xml.XmlWriter>\/<xref:System.IO.TextWriter> 实例的形式生成输出。  
  
-   <xref:System.Xaml.XamlServices.Transform%2A> 通过以单个操作的形式链接加载路径和保存路径来转换 XAML。  可以对 <xref:System.Xaml.XamlReader> 和 <xref:System.Xaml.XamlWriter> 使用不同的架构上下文或不同的后备类型系统，这会影响所得到的 XAML 的转换方式。  
  
 有关如何使用 <xref:System.Xaml.XamlServices>的更多信息，请参见[XAMLServices Class and Basic XAML Reading or Writing](../../../docs/framework/xaml-services/xamlservices-class-and-basic-xaml-reading-or-writing.md)。  
  
## XAML 类型系统  
 XAML 类型系统提供使用 XAML 节点流的给定单个节点所需的 API。  
  
 <xref:System.Xaml.XamlType> 是某个对象的表示形式 \- 是介于起始对象节点和结束对象节点之间处理的内容。  
  
 <xref:System.Xaml.XamlMember> 是某个对象成员的表示形式 \- 是介于起始成员节点和结束成员节点之间处理的内容。  
  
 API（如 <xref:System.Xaml.XamlType.GetAllMembers%2A>、<xref:System.Xaml.XamlType.GetMember%2A> 和 <xref:System.Xaml.XamlMember.DeclaringType%2A>）报告 <xref:System.Xaml.XamlType> 和 <xref:System.Xaml.XamlMember> 之间的关系。  
  
 由 .NET Framework XAML 服务实现的 XAML 类型系统的默认行为基于公共语言运行时 \(CLR\) 以及使用反射对程序集中的 CLR 类型进行的静态分析。  因此，对于特定的 CLR 类型，XAML 类型系统的默认实现可以公开该类型及其成员的 XAML 架构，并根据 XAML 类型系统进行报告。  在默认的 XAML 类型系统中，类型可分配性的概念映射到 CLR 继承上，并且实例和值类型等的概念也映射到 CLR 的支持行为和功能。  
  
## XAML 语言功能参考  
 为了支持 XAML，.NET Framework XAML 服务提供了为 XAML 语言 XAML 命名空间定义的 XAML 语言概念的特定实现。  将以特定参考页的形式对这些内容进行描述。  我们是从由 XAML 读取器或 XAML 编写器（由 .NET Framework XAML 服务定义）处理时这些语言功能的行为方式的角度来描述这些语言功能的。  有关更多信息，请参见 [XAML Namespace \(x:\) Language Features](../../../docs/framework/xaml-services/xaml-namespace-x-language-features.md)。