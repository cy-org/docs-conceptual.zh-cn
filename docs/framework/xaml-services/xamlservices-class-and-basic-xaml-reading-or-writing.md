---
title: "XAMLServices Class and Basic XAML Reading or Writing | Microsoft Docs"
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
  - "XAML [XAML Services], XamlServices class"
  - "XamlServices class [XAML Services], how to use"
ms.assetid: 6ac27fad-3687-4d7a-add1-3e90675fdfde
caps.latest.revision: 11
author: "wadepickett"
ms.author: "wpickett"
manager: "wpickett"
caps.handback.revision: 11
---
# XAMLServices Class and Basic XAML Reading or Writing
<xref:System.Xaml.XamlServices> 是由 .NET Framework XAML 服务提供的一个类，可用于解决无需对 XAML 节点流的特定访问权限的 XAML 方案，或从这些节点获取的 XAML 类型系统信息。<xref:System.Xaml.XamlServices> API 可总结如下：`Load` 或 `Parse` 用以支持 XAML 加载路径，`Save` 用以支持 XAML 保存路径，以及 `Transform`，用以提供联接加载路径和保存的技术。`Transform` 可用于从一个 XAML 架构更改为另一个。 本主题总结了每个 API 分类，并介绍了特定方法重载之间的差异。  
  
<a name="load"></a>   
## 加载  
 各种 <xref:System.Xaml.XamlServices.Load%2A> 重载实现了加载路径的完整逻辑。 加载路径以某种形式使用 XAML，并输出 XAML 节点流。 其中的大部分加载路径使用一种编码的 XML 文本文件格式的 XAML。 但是，你也可以加载常规流，或者加载已包含在另一个 <xref:System.Xaml.XamlReader> 实现中的预加载 XAML 源。  
  
 适用于大多数方案的最简单的重载是 <xref:System.Xaml.XamlServices.Load%28System.String%29>。 此重载具有 `fileName` 参数，它仅是文本文件的名称，该文件包含要加载的 XAML。 这适用于应用程序方案，如具有本地计算机之前序列化的状态或数据的完全信任应用程序。 这也对框架有用，你正在其中定义应用程序模型并想要加载一个标准文件，这些标准文件定义应用程序行为、启动 UI 或其他使用 XAML 的框架定义的功能。  
  
 <xref:System.Xaml.XamlServices.Load%28System.IO.Stream%29> 具有类似的方案。 如果你让用户选择要加载文件，此重载可能会很有用，因为 <xref:System.IO.Stream> 是其他可以访问文件系统的 <xref:System.IO> API 的常见输出。 或者，你可以通过异步下载或其他也提供流的网络技术来访问 XAML 源。 （从流或用户选择的源进行加载可能出现安全问题。 有关详细信息，请参阅 [XAML Security Considerations](../../../docs/framework/xaml-services/xaml-security-considerations.md)。）  
  
 <xref:System.Xaml.XamlServices.Load%28System.IO.TextReader%29> 和 <xref:System.Xaml.XamlServices.Load%28System.Xml.XmlReader%29> 是重载，依赖于上一版本的 .NET Framework 的格式的读取器。 若要使用这些重载，你应该已经创建了读取器实例并使用其 `Create` API 来加载相关形式 （文本或 XML）的 XAML。 如果你已经在其他读取器中移动了记录指针或对它们执行了其他操作，这就不重要了。<xref:System.Xaml.XamlServices.Load%2A> 的负载路径逻辑始终处理整个根下的 XAML 输入。 这些重载的方案可能包括以下内容：  
  
-   设计图面，其中你从现有的特定于 XML 的文本编辑器提供简单的 XAML 编辑功能。  
  
-   核心 <xref:System.IO> 方案的变体，你可以在其中使用专用的读取器打开文件或流。 你的逻辑在尝试将内容加载为 XAML 之前对其执行初步检查或处理。  
  
 你可以加载文件或流，或者可以加载 <xref:System.Xml.XmlReader>、<xref:System.IO.TextReader> 或 <xref:System.Xaml.XamlReader>，它们通过使用读取器的 API 进行加载来包装你的 XAML 输入。  
  
 在内部，每个前面的重载最终为 <xref:System.Xaml.XamlServices.Load%28System.Xml.XmlReader%29>，且传递的 <xref:System.Xml.XmlReader> 用于创建一个新的 <xref:System.Xaml.XamlXmlReader>。  
  
 为更高级方案提供的 `Load` 签名是 <xref:System.Xaml.XamlServices.Load%28System.Xaml.XamlReader%29>。 在以下情况之一，可以使用此签名：  
  
-   你已定义自己的 <xref:System.Xaml.XamlReader> 实现。  
  
-   你需要指定与默认设置不同的 <xref:System.Xaml.XamlReader> 设置。  
  
 非默认设置的示例设置后列任一项：<xref:System.Xaml.XamlReaderSettings.AllowProtectedMembersOnRoot%2A>；<xref:System.Xaml.XamlReaderSettings.BaseUri%2A>；<xref:System.Xaml.XamlReaderSettings.IgnoreUidsOnPropertyElements%2A>；<xref:System.Xaml.XamlReaderSettings.LocalAssembly%2A>；<xref:System.Xaml.XamlReaderSettings.ValuesMustBeString%2A>。<xref:System.Xaml.XamlServices> 的默认读取器是 <xref:System.Xaml.XamlXmlReader>。 如果你提供自己 <xref:System.Xaml.XamlXmlReader>，对于设置，以下是用以设置非默认 <xref:System.Xaml.XamlXmlReaderSettings> 的属性：<xref:System.Xaml.XamlXmlReaderSettings.CloseInput%2A>；<xref:System.Xaml.XamlXmlReaderSettings.SkipXmlCompatibilityProcessing%2A>；<xref:System.Xaml.XamlXmlReaderSettings.XmlLang%2A>；<xref:System.Xaml.XamlXmlReaderSettings.XmlSpacePreserve%2A>。  
  
<a name="parse"></a>   
## 分析  
 <xref:System.Xaml.XamlServices.Parse%2A> 就像 `Load`，因为它是从 XAML 输入创建 XAML 节点流的负载路径 API。 但是，在这种情况下，XAML 输入直接作为一个字符串提供，其中包含所有要加载的 XAML。<xref:System.Xaml.XamlServices.Parse%2A> 是一种轻量级方法，与框架方案相比更适合应用程序方案。 有关详细信息，请参阅<xref:System.Xaml.XamlServices.Parse%2A>。<xref:System.Xaml.XamlServices.Parse%2A> 实际上只是一个包装的 <xref:System.Xaml.XamlServices.Load%28System.Xml.XmlReader%29> 调用，内部涉及到 <xref:System.IO.StringReader>。  
  
<a name="save"></a>   
## 保存  
 各种 <xref:System.Xaml.XamlServices.Save%2A> 重载实现保存路径。 所有 <xref:System.Xaml.XamlServices.Save%2A> 方法都采用对象图作为输入，并生成流、文件或 <xref:System.Xml.XmlWriter>\/<xref:System.IO.TextWriter> 实例形式的输出。  
  
 输入对象预期为某些对象表示形式的根对象。 这可能是业务对象的单个根、UI 方案中页的对象树的根、设计工具的工作编辑界面或适用于方案的其他根对象概念。  
  
 在许多方案中，你保存的对象树与加载 XAML 的原始操作相关，该加载使用 <xref:System.Xaml.XamlServices.Load%2A> 或其他通过框架\/应用程序模型实现的 API 来执行。 可能会在对象树中捕获到差异，产生这些差异的原因可能是状态更改，可能是应用程序捕获来自用户的运行时设置处的更改，或者是 XAML 变更，因为你的应用程序是 XAML 设计界面等原因。无论是否有更改，从标记首次加载 XAML 然后再次将其保存并比较两个 XAML 标记形式，这整个概念有时会被称为 XAML 的往返过程表示形式。  
  
 保持和序列化以标记形式设置的复杂对象这一操作面临的挑战是实现完全表示形式而不丢失信息与减少导致 XAML 可读性降低的冗繁信息之间的平衡。 此外，XAML 的不同客户可能对应该如何实现这种平衡有不同的定义或期望。<xref:System.Xaml.XamlServices.Save%2A> API 表示这种平衡的一个定义。<xref:System.Xaml.XamlServices.Save%2A> API 使用可用的 XAML 架构上下文和 <xref:System.Xaml.XamlType>、<xref:System.Xaml.XamlMember> 的默认的基于 CLR 的特征以及其他 XAML 内部函数和 XAML 类型系统概念，以确定在将某些 XAML 节点流构造保存回标记时可以在何处优化它们。 例如，<xref:System.Xaml.XamlServices> 保存路径可使用基于 CLR 的默认 XAML 架构上下文来解析对象的 <xref:System.Xaml.XamlType>，这可以确定一个 <xref:System.Xaml.XamlType.ContentProperty%2A?displayProperty=fullName>，然后可以在属性元素标记将属性写入对象的 XAML 内容时将其省略。  
  
<a name="transform"></a>   
## 转换  
 通过链接一个加载路径或保存路径作为单个操作，<xref:System.Xaml.XamlServices.Transform%2A> 会转换或变换 XAML。 可以将不同的架构上下文或不同的后备类型系统用于 <xref:System.Xaml.XamlReader> 和 <xref:System.Xaml.XamlWriter>，这会影响如何转换产生的 XAML。 这非常适合广泛的转换操作。  
  
 对于依赖于检查 XAML 节点流中每个节点的操作，通常不使用 <xref:System.Xaml.XamlServices.Transform%2A>。 相反，你需要定义自己的加载路径\-保存路径操作系列并插入自己的逻辑。 在其中一个路径，在你自己的节点循环中使用 XAML 读取器\/XAML 编写器对。 例如，使用 <xref:System.Xaml.XamlXmlReader> 加载初始 XAML 并使用连续的 <xref:System.Xaml.XamlXmlReader.Read%2A> 调用单步执行节点。 在 XAML 节点流级别操作现在可以调整各个节点（类型、成员、其他节点）以应用转换，或将节点保持原样。 然后开始将节点发送到 <xref:System.Xaml.XamlObjectWriter> 的相关 `Write` API 并写出对象。 有关更多信息，请参见[Understanding XAML Node Stream Structures and Concepts](../../../docs/framework/xaml-services/understanding-xaml-node-stream-structures-and-concepts.md)。  
  
## 请参阅  
 <xref:System.Xaml.XamlObjectWriter>   
 <xref:System.Xaml.XamlServices>   
 [XAML Services](../../../docs/framework/xaml-services/index.md)