---
title: "文档序列化和存储 | Microsoft Docs"
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
  - "文档, Serialization — 序列化"
  - "文档, storage"
  - "文档序列化"
  - "文档存储"
ms.assetid: 4839cd87-e206-4571-803f-0200098ad37b
caps.latest.revision: 24
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 23
---
# 文档序列化和存储
[!INCLUDE[TLA#tla_winfx](../../../../includes/tlasharptla-winfx-md.md)]为创建和显示高质量的文档提供了一个强大环境。  增强功能可支持固定文档和流文档以及高级查看控件，这些增强功能与强大的二维和三维图形功能结合在一起，提高了 [!INCLUDE[TLA2#tla_winfx](../../../../includes/tla2sharptla-winfx-md.md)] 应用程序的质量水平，增强了用户体验。  [!INCLUDE[TLA2#tla_winfx](../../../../includes/tla2sharptla-winfx-md.md)] 的主要功能是能够灵活管理文档的内存中表现形式，而几乎每个应用程序都需要能够高效保存和加载数据存储区中的文档。  将文档从内部的内存中表现形式转换为外部数据存储区的过程称为[序列化](GTMT)。  反之，读取数据存储区并重新创建原始内存中实例的过程则称为反序列化。  
  
   
  
<a name="AboutSerialization"></a>   
## 关于文档序列化  
 理论上，对于应用程序来说，从内存中[序列化](GTMT)文档和将文档反序列到原来的内存中都是透明的。  应用程序调用序列化程序“write”方法来保存文档，而反序列化程序“read”方法则访问数据存储区并在内存中重新创建原始实例。  对于应用程序来说，只要序列化和反序列化进程将文档重新创建为其原始格式，数据存储的特定格式通常无关紧要。  
  
 应用程序通常可提供多个序列化选项，用户可以使用这些选项将文档保存到不同的媒体或保存为不同格式。  例如，应用程序可提供“另存为”选项将文档存储到磁盘文件、数据库或 Web 服务。  同样，不同的序列化程序可将文档存储为不同格式，例如 HTML、RTF、XML、XPS 或第三方格式。  对于应用程序，序列化定义了一个接口，该接口可以隔离每个特定序列化程序的实现内部的存储媒体的详细信息。  除封装存储详细信息这个优点之外，[!INCLUDE[TLA2#tla_winfx](../../../../includes/tla2sharptla-winfx-md.md)] <xref:System.Windows.Documents.Serialization> [!INCLUDE[TLA2#tla_api#plural](../../../../includes/tla2sharptla-apisharpplural-md.md)] 还提供了多个其他重要功能。  
  
### .NET Framework 3.0 文档序列化程序的功能  
  
-   通过直接访问高级别文档对象（[逻辑树](GTMT)和可视化对象），可以有效存储已分页的内容、二维\/三维元素、图像、媒体、超链接、批注以及其他支持内容。  
  
-   [同步](GTMT)和[异步](GTMT)操作。  
  
-   支持具有以下增强功能的插件序列化程序：  
  
    -   供所有 [!INCLUDE[TLA2#tla_winfx](../../../../includes/tla2sharptla-winfx-md.md)] 应用程序使用的系统级访问。  
  
    -   简单应用程序插件的发现功能。  
  
    -   第三方自定义插件的简单部署、安装和更新。  
  
    -   对自定义运行时设置和选项的用户界面支持。  
  
### XPS 打印路径  
 [!INCLUDE[TLA#tla_winfx](../../../../includes/tlasharptla-winfx-md.md)] [!INCLUDE[TLA2#tla_xps](../../../../includes/tla2sharptla-xps-md.md)] 打印路径还通过打印输出为编写文档提供了一种可扩展机制。  [!INCLUDE[TLA2#tla_xps](../../../../includes/tla2sharptla-xps-md.md)] 可以作为文档文件格式，也可以作为 [!INCLUDE[TLA#tla_winvista](../../../../includes/tlasharptla-winvista-md.md)] 的本机后台打印格式。  [!INCLUDE[TLA2#tla_xps](../../../../includes/tla2sharptla-xps-md.md)] 文档可直接发送到与 [!INCLUDE[TLA2#tla_xps](../../../../includes/tla2sharptla-xps-md.md)] 兼容的打印机，而无需转换为中间格式。  有关打印路径输出选项和功能的其他信息，请参见[打印概述](../../../../docs/framework/wpf/advanced/printing-overview.md)。  
  
<a name="PluginSerializers"></a>   
## 插件序列化程序  
 <xref:System.Windows.Documents.Serialization> API 可对以下各项提供支持：与应用程序分开安装、在运行时绑定并使用 <xref:System.Windows.Documents.Serialization.SerializerProvider> 发现机制访问的插件序列化程序和链接序列化程序。  插件序列化程序提供了增强功能，可以简化部署和系统范围的使用。  还可针对无法在其中访问插件序列化程序的[部分可信](GTMT)环境（例如 [!INCLUDE[TLA#tla_xbap#plural](../../../../includes/tlasharptla-xbapsharpplural-md.md)]）实现链接序列化程序。  链接序列化程序基于 <xref:System.Windows.Documents.Serialization.SerializerWriter> 类的派生的实现，将被编译并直接链接到应用程序。  插件序列化程序和链接序列化程序都是通过相同的公共方法和事件来运行的，这样可以方便地在同一应用程序中使用其中一种或两种序列化程序。  
  
 插件序列化程序对应用程序开发人员很有帮助：它向新的存储设计和文件格式提供扩展性，而无需在生成时对每种潜在的格式进行直接编码。  插件序列化程序还通过为自定义或专有文件格式提供部署、安装和更新系统可访问插件的标准方法，使第三方开发人员受益匪浅。  
  
### 使用插件序列化程序  
 插件序列化程序易于使用。  <xref:System.Windows.Documents.Serialization.SerializerProvider> 类为系统上安装的每个插件枚举一个 <xref:System.Windows.Documents.Serialization.SerializerDescriptor> 对象。  <xref:System.Windows.Documents.Serialization.SerializerDescriptor.IsLoadable%2A> 属性根据当前配置筛选已安装的插件，并验证应用程序是否可以加载和使用序列化程序。  <xref:System.Windows.Documents.Serialization.SerializerDescriptor> 还提供了其他属性（如 <xref:System.Windows.Documents.Serialization.SerializerDescriptor.DisplayName%2A> 和 <xref:System.Windows.Documents.Serialization.SerializerDescriptor.DefaultFileExtension%2A>），应用程序可以使用这些属性来提示用户选择可用输出格式的序列化程序。  [!INCLUDE[TLA2#tla_xps](../../../../includes/tla2sharptla-xps-md.md)] 的默认插件序列化程序随 [!INCLUDE[TLA2#tla_winfx](../../../../includes/tla2sharptla-winfx-md.md)] 一起提供，并会始终进行枚举。  用户选择输出格式之后，将使用 <xref:System.Windows.Documents.Serialization.SerializerProvider.CreateSerializerWriter%2A> 方法创建特定格式的 <xref:System.Windows.Documents.Serialization.SerializerWriter>。  然后可以调用 <xref:System.Windows.Documents.Serialization.SerializerWriter>.<xref:System.Windows.Documents.Serialization.SerializerWriter.Write%2A> 方法将文档流输出到数据存储区。  
  
 下面的示例阐释在“PlugInFileFilter”属性中使用 <xref:System.Windows.Documents.Serialization.SerializerProvider> 方法的应用程序。  PlugInFileFilter 枚举已安装的插件，并使用 <xref:Microsoft.Win32.SaveFileDialog> 的可用文件选项生成筛选器字符串。  
  
 [!code-csharp[DocumentSerialize#DocSerializeFileFilter](../../../../samples/snippets/csharp/VS_Snippets_Wpf/DocumentSerialize/CSharp/ThumbViewer.cs#docserializefilefilter)]  
  
 用户选择输出文件名之后，下面的示例阐释如何使用 <xref:System.Windows.Documents.Serialization.SerializerProvider.CreateSerializerWriter%2A> 方法以指定格式存储给定文档。  
  
 [!code-csharp[DocumentSerialize#DocSerializePlugIn](../../../../samples/snippets/csharp/VS_Snippets_Wpf/DocumentSerialize/CSharp/ThumbViewer.cs#docserializeplugin)]  
  
<a name="InstallingPluginSerializers"></a>   
### 安装插件序列化程序  
 <xref:System.Windows.Documents.Serialization.SerializerProvider> 类为插件序列化程序的发现和访问提供高级别应用程序接口。  <xref:System.Windows.Documents.Serialization.SerializerProvider> 为应用程序查找和提供系统上已安装并可访问的序列化程序的列表。  已安装序列化程序的具体信息通过注册表设置来定义。  使用 <xref:System.Windows.Documents.Serialization.SerializerProvider.RegisterSerializer%2A> 方法可向注册表添加插件序列化程序；或者如果尚未安装 [!INCLUDE[TLA2#tla_winfx](../../../../includes/tla2sharptla-winfx-md.md)]，插件安装脚本自身则可以直接设置注册表值。  使用 <xref:System.Windows.Documents.Serialization.SerializerProvider.UnregisterSerializer%2A> 方法可以移除以前已安装的插件，或者类似地通过卸载脚本来重置注册表设置。  
  
### 创建插件序列化程序  
 插件序列化程序和链接序列化程序使用同一公开的公共方法和事件，并且类似地可将其设计为以[同步](GTMT)或[异步](GTMT)方式运行。  创建插件序列化程序通常应执行下列三个基本步骤：  
  
1.  首先以链接序列化程序的形式实现和调试序列化程序。  开始时通过创建直接编译和链接到测试应用程序的序列化程序，可以提供对断点以及其他有助于测试的调试服务的完全访问权限。  
  
2.  完全测试序列化程序之后，会添加一个 <xref:System.Windows.Documents.Serialization.ISerializerFactory> 界面以创建插件。  <xref:System.Windows.Documents.Serialization.ISerializerFactory> 界面允许对所有 [!INCLUDE[TLA2#tla_winfx](../../../../includes/tla2sharptla-winfx-md.md)] 对象进行完全访问，包括逻辑树、<xref:System.Windows.UIElement> 对象、<xref:System.Windows.Documents.IDocumentPaginatorSource> 和 <xref:System.Windows.Media.Visual> 元素。  此外，<xref:System.Windows.Documents.Serialization.ISerializerFactory> 提供的同步和异步方法和事件与链接序列化程序使用的方法和事件相同。  由于输出大型文档需要一定时间，因此推荐使用异步操作以维持响应用户交互，并在数据存储区出现问题时提供“取消”选项。  
  
3.  创建插件序列化程序之后，将实现安装脚本以分发和安装（以及卸载）插件（请参见上面的“[安装插件序列化程序](#InstallingPluginSerializers)”）。  
  
## 请参阅  
 <xref:System.Windows.Documents.Serialization>   
 <xref:System.Windows.Xps.XpsDocumentWriter>   
 <xref:System.Windows.Xps.Packaging.XpsDocument>   
 [WPF 中的文档](../../../../docs/framework/wpf/advanced/documents-in-wpf.md)   
 [打印概述](../../../../docs/framework/wpf/advanced/printing-overview.md)   
 [XML Paper Specification: Overview](http://go.microsoft.com/fwlink?LinkID=106246)