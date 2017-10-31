---
title: "WPF 中的文档 | Microsoft Docs"
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
  - "可使用浏览器查看的文档"
  - "文档, 可使用浏览器查看的"
  - "文档, 控件"
  - "文档, 打包"
  - "文档, 文本布局"
  - "文档, 类型"
  - "文档, XPS"
  - "文档打包"
  - "XPS 文档"
ms.assetid: 6e8db7bc-050a-4070-aa72-bb8c46e87ff8
caps.latest.revision: 36
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 35
---
# WPF 中的文档
[!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)] 提供一系列丰富的文档功能，与先前几代的 [!INCLUDE[TLA#tla_mswin](../../../../includes/tlasharptla-mswin-md.md)] 相比，可以创建旨在更方便地访问和读取的高保真内容文档。  除增强的功能和质量外，[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 还对文档显示、打包和安全性能提供集成服务。  本主题介绍了 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 文档类型和文档打包。  
  
   
  
<a name="types_of_documents"></a>   
## 文档类型  
 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 基于文档用途将文档分成两个大的类别；这些文档类别分别被称为“固定文档”和“流文档”。  
  
 固定文档适用于需要精确的[!INCLUDE[TLA#tla_wys](../../../../includes/tlasharptla-wys-md.md)]表示形式的应用程序，这与使用的显示器或打印机硬件无关。  固定文档的典型用途包括桌面发布、字处理和窗体布局，在这些情况下，遵循原始页面设计非常关键。  作为其布局的一部分，固定文档独立于所使用的显示或打印设备来对内容元素进行精确地定位安放。  例如，一个固定文档页面在 96 dpi 显示器上显示的效果与在 600 dpi 激光打印机或 4800 dpi 照相排字机上输出的效果是严格一样的。  虽然文档质量会根据每台设备的功能达到最优化，但是页面布局在所有情况下都保持不变。  
  
 比较而言，当易读性是文档的主要使用要求时，流文档旨在优化查看和可读性并得到最佳利用。  流文档根据运行时变量（例如，窗口大小、设备分辨率和可选的用户首选项）来动态调整和重新排列文档内容，而不是设置为一个预定义的布局。  网页就是流文档的一个简单示例，在网页上页面内容会动态调整格式以适应当前窗口。  流文档会基于运行时环境来优化用户的查看和阅读体验。  例如，在高分辨率的 19 英寸显示器上或小型 2x3 英寸 PDA 屏幕上，同一流文档会动态调整格式以达到最理想的可读性。  此外，流文档还具有很多内置功能，包括搜索、能够优化可读性的查看模式以及更改字体大小和外观的功能。  请参见[流文档概述](../../../../docs/framework/wpf/advanced/flow-document-overview.md)了解有关流文档的演示、示例和详细信息。  
  
<a name="document_viewer"></a>   
## 文档控件和文本布局  
 [!INCLUDE[TLA2#tla_avalonwinfx](../../../../includes/tla2sharptla-avalonwinfx-md.md)] 提供一组预建的控件，可以简化固定文档、流文档和应用程序内常规文本的使用。  固定文档内容的显示是由 <xref:System.Windows.Controls.DocumentViewer> 控件支持的。  流文档内容的显示是由以下三个不同的控件支持的：<xref:System.Windows.Controls.FlowDocumentReader>、<xref:System.Windows.Controls.FlowDocumentPageViewer> 和 <xref:System.Windows.Controls.FlowDocumentScrollViewer>，它们分别映射到不同的用户方案（请参见下面的小节）。  其他 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 控件提供简化的布局以支持常规文本使用（请参见下面的[用户界面中的文本](#text_in_the_user_interface)）。  
  
### 固定文档控件 \- DocumentViewer  
 <xref:System.Windows.Controls.DocumentViewer> 控件旨在显示 <xref:System.Windows.Documents.FixedDocument> 内容。  <xref:System.Windows.Controls.DocumentViewer> 控件提供一个直观的用户界面，为常见的操作（包括打印输出、复制到剪贴板、缩放和文本搜索功能）提供内置支持。  此控件提供常见的滚动机制，支持对页面内容的访问。  与所有 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 控件类似，<xref:System.Windows.Controls.DocumentViewer> 支持完整或部分样式调整，这使得控件可以在视觉效果方面几乎与任何应用程序或环境相集成。  
  
 <xref:System.Windows.Controls.DocumentViewer> 设计为以只读方式显示内容，不支持对内容进行编辑或修改。  
  
<a name="flow_document"></a>   
### 流文档控件  
 **注意：**有关流文档功能及如何创建流文档的更多详细信息，请参见[流文档概述](../../../../docs/framework/wpf/advanced/flow-document-overview.md)。  
  
 流文档内容的显示是由以下三个控件支持的：<xref:System.Windows.Controls.FlowDocumentReader>、<xref:System.Windows.Controls.FlowDocumentPageViewer> 和 <xref:System.Windows.Controls.FlowDocumentScrollViewer>。  
  
#### FlowDocumentReader  
 <xref:System.Windows.Controls.FlowDocumentReader> 包含一些功能，使用户能够动态地在各种查看模式之间进行选择，这些查看模式包括单页（一次一页）查看模式、一次两页（书本阅读格式）查看模式和连续滚动（无界限）查看模式。  有关这些查看模式的更多信息，请参见 <xref:System.Windows.Controls.FlowDocumentReaderViewingMode>。  如果您不需要在不同查看模式之间动态切换的功能，则可以使用 <xref:System.Windows.Controls.FlowDocumentPageViewer> 和 <xref:System.Windows.Controls.FlowDocumentScrollViewer>，它们提供了固定使用特定查看模式的轻量级流内容查看器。  
  
#### FlowDocumentPageViewer 和 FlowDocumentScrollViewer  
 <xref:System.Windows.Controls.FlowDocumentPageViewer> 以一次一页的查看模式显示内容，而 <xref:System.Windows.Controls.FlowDocumentScrollViewer> 以连续滚动模式显示内容。  <xref:System.Windows.Controls.FlowDocumentPageViewer> 和 <xref:System.Windows.Controls.FlowDocumentScrollViewer> 都固定使用特定查看模式。  与 <xref:System.Windows.Controls.FlowDocumentReader> 相比，后者包含一些功能，使用户能够动态地在各种查看模式（由 <xref:System.Windows.Controls.FlowDocumentReaderViewingMode> 枚举提供）之间进行选择，但代价是需要消耗比 <xref:System.Windows.Controls.FlowDocumentPageViewer> 或 <xref:System.Windows.Controls.FlowDocumentScrollViewer> 更多的资源。  
  
 默认情况下，总是显示垂直滚动条，而水平滚动条则在需要时显示。  <xref:System.Windows.Controls.FlowDocumentScrollViewer> 的默认 [!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)] 不包括工具栏；但是 <xref:System.Windows.Controls.FlowDocumentScrollViewer.IsToolBarVisible%2A> 属性可用于启用内置工具栏。  
  
<a name="text_in_the_user_interface"></a>   
### 用户界面中的文本  
 除了可以将文本添加到文档外，显然文本还可以用于应用程序 UI（如窗体）中。  [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 包括多个用于在屏幕中绘制文本的控件。  每个控件都面向不同的方案，并具有自己的功能和限制列表。  通常，当需要支持的文本有限（例如[!INCLUDE[TLA#tla_ui](../../../../includes/tlasharptla-ui-md.md)] 中的简短语句）时，应使用 <xref:System.Windows.Controls.TextBlock> 元素。  当需要支持文本极少时，可以使用 <xref:System.Windows.Controls.Label>。  有关更多信息，请参见[TextBlock 概述](../../../../docs/framework/wpf/controls/textblock-overview.md)。  
  
<a name="packaging"></a>   
## 文档打包  
 <xref:System.IO.Packaging> [!INCLUDE[TLA2#tla_api#plural](../../../../includes/tla2sharptla-apisharpplural-md.md)] 提供一种有效方式，在一个便于访问、可移植和易于分发的单一容器中组织应用程序数据、文档内容和相关资源。  ZIP 文件是 <xref:System.IO.Packaging.Package> 类型的一个示例，能够将多个对象保存为一个单元。  打包 [!INCLUDE[TLA2#tla_api#plural](../../../../includes/tla2sharptla-apisharpplural-md.md)] 提供一个默认的 <xref:System.IO.Packaging.ZipPackage> 实现，设计为在 XML 和 ZIP 文件结构中使用开放式打包约定标准。  [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 打包 [!INCLUDE[TLA2#tla_api#plural](../../../../includes/tla2sharptla-apisharpplural-md.md)] 使得创建包以及在包内存储和访问对象变得更为简单。  存储在 <xref:System.IO.Packaging.Package> 中的对象被称为 <xref:System.IO.Packaging.PackagePart>（“部分”）。  包还可能包括已签名的数字证书，这些证书可以用于标识部分的发信方以及验证尚未修改包的内容。  包还包括 <xref:System.IO.Packaging.PackageRelationship> 功能，允许将其他信息添加到包中，或在未实际修改现有部分内容的情况下与特定部分相关联。  包服务还支持 [!INCLUDE[TLA#tla_rm](../../../../includes/tlasharptla-rm-md.md)]。  
  
 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 包结构用作一系列关键技术的基础：  
  
-   [!INCLUDE[TLA2#tla_xps](../../../../includes/tla2sharptla-xps-md.md)] 文档符合 [!INCLUDE[TLA#tla_xps](../../../../includes/tlasharptla-xps-md.md)]。  
  
-   Microsoft Office "12" 开放式 XML 格式文档 \(.docx\)。  
  
-   用于个人应用程序设计的自定义存储格式。  
  
 基于打包 API，<xref:System.Windows.Xps.Packaging.XpsDocument> 是专为存储 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 固定内容文档而设计。  <xref:System.Windows.Xps.Packaging.XpsDocument> 是自包含文档，可以在查看器中打开、在 <xref:System.Windows.Controls.DocumentViewer> 控件中显示、路由到打印后台或直接输出到与 [!INCLUDE[TLA2#tla_xps](../../../../includes/tla2sharptla-xps-md.md)] 兼容的打印机。  
  
 以下小节提供有关 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 附带的 <xref:System.IO.Packaging.Package> 和 <xref:System.Windows.Xps.Packaging.XpsDocument> [!INCLUDE[TLA2#tla_api#plural](../../../../includes/tla2sharptla-apisharpplural-md.md)] 的更多信息。  
  
<a name="packages"></a>   
### 包组件  
 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 打包 API，应用程序数据和文档可以在一个可移植的单元中组织。  ZIP 文件是最常见的包类型，并且是 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 附带的默认包类型。  <xref:System.IO.Packaging.Package> 本身是一个抽象类，<xref:System.IO.Packaging.ZipPackage> 就是从中使用开放式标准 XML 和 ZIP 文件体系结构实现的。  <xref:System.IO.Packaging.Package.Open%2A> 方法默认使用 <xref:System.IO.Packaging.ZipPackage> 来创建和使用 ZIP 文件。  包可以包含三种基本类型的项：  
  
|||  
|-|-|  
|<xref:System.IO.Packaging.PackagePart>|应用程序内容、数据、文档和资源文件。|  
|<xref:System.IO.Packaging.PackageDigitalSignature>|[X.509 证书](GTMT)用于标识、身份验证和验证。|  
|<xref:System.IO.Packaging.PackageRelationship>|与包或特定部分相关的增加信息。|  
  
<a name="PackageParts"></a>   
#### PackagePart  
 <xref:System.IO.Packaging.PackagePart>（“部分”）是一个抽象类，是指存储在 <xref:System.IO.Packaging.Package> 中的一个对象。  在 ZIP 文件中，包的各个部分与存储在 ZIP 文件中的各个文件相对应。  <xref:System.IO.Packaging.ZipPackagePart> 为存储在 <xref:System.IO.Packaging.ZipPackage> 中的可序列化对象提供默认实现。  与文件系统类似，包中包含的部分存储在分层目录或“文件夹样式”组织中。  使用 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 打包 API，应用程序可以使用单一 ZIP 容器写入、存储和读取多个 <xref:System.IO.Packaging.PackagePart> 对象。  
  
<a name="PackageDigitalSignatures"></a>   
#### PackageDigitalSignature  
 为安全起见，<xref:System.IO.Packaging.PackageDigitalSignature>（“数字签名”）可以与包内的部分关联。  <xref:System.IO.Packaging.PackageDigitalSignature> 合并了 [509](GTMT)，提供以下两个功能：  
  
1.  标识部分的发信方并对其进行身份验证。  
  
2.  验证部件是否尚未被修改。  
  
 数字签名不会阻止部分被修改，但如果该部分已经以任何方式发生改变，则对该数字签名的验证检查将失败。  然后应用程序可采取适当的操作（例如，阻止部分打开，或通知用户该部分已修改，是不安全的）。  
  
<a name="PackageRelationships"></a>   
#### PackageRelationship  
 <xref:System.IO.Packaging.PackageRelationship>（“关系”）提供一种机制，用于将其他信息与包或包内的部分关联。  关系是一种包级别的设备，可以在未修改实际部分内容的情况下将其他信息与部分关联。  在许多情况下，直接向部分内容中插入新数据通常是不切实际的：  
  
-   部分及其内容架构的实际类型未知。  
  
-   即使已知，内容架构可能也不会提供添加新信息的方式。  
  
-   部分可能已进行数字签名或加密，不能进行修改。  
  
 包关系提供一种可检测到的方式，用于添加其他信息并将该信息与各个部分或整个包关联。  包关系用于两种主要功能：  
  
1.  定义一个部分与另一个部分之间的依赖关系。  
  
2.  定义添加注释或与部分相关的其他数据的信息关系。  
  
 <xref:System.IO.Packaging.PackageRelationship> 提供一个快速、可检测到的方式来定义依赖关系，并添加与包的部分或整个包相关联的其他信息。  
  
<a name="Dependency_Relationships"></a>   
##### 依赖关系  
 依赖关系用于描述一个部分对其他部分的依赖性。  例如，一个包可能包含包括一个或多个 \<img\> 图像标记的 HTML 部分。  此图像标记指的是作为其他包的内部部分或外部部分（可通过 Internet 访问）定位的图像。  创建与 HTML 文件关联的 <xref:System.IO.Packaging.PackageRelationship>，可以使查找和访问从属资源更加快速和方便。  浏览器或查看器应用程序可以直接访问部分关系，并立即在无需了解架构或未分析文档的情况下开始汇编从属资源。  
  
<a name="Information_Relationships"></a>   
##### 信息关系  
 与注释或批注类似，<xref:System.IO.Packaging.PackageRelationship> 还可以用于存储要与部分关联的其他类型的信息，而不必实际修改部分内容本身。  
  
<a name="XPS_Documents"></a>   
## XPS 文档  
 [!INCLUDE[TLA#tla_xps](../../../../includes/tlasharptla-xps-md.md)] 文档是一个包，其中包含一个或多个固定文档以及呈现操作所需的所有资源和信息。  [!INCLUDE[TLA2#tla_xps](../../../../includes/tla2sharptla-xps-md.md)] 还是 [!INCLUDE[TLA#tla_winvista](../../../../includes/tlasharptla-winvista-md.md)] 固有的后台打印文件格式。  <xref:System.Windows.Xps.Packaging.XpsDocument> 存储在标准 ZIP 数据集中，可以包括 XML 和二进制组件的组合，如图像和字体文件。[PackageRelationships](#PackageRelationships) 用于定义内容和完全呈现文档所需的资源之间的依赖关系。  <xref:System.Windows.Xps.Packaging.XpsDocument> 设计提供一种单一高保真文档解决方案，支持以下多种用途：  
  
-   将固定文档内容和资源读取、写入和存储为单个可移植且易于分发的文件。  
  
-   利用 [!INCLUDE[TLA2#tla_xps](../../../../includes/tla2sharptla-xps-md.md)] 查看器应用程序显示文档。  
  
-   以 [!INCLUDE[TLA#tla_winvista](../../../../includes/tlasharptla-winvista-md.md)] 的本机打印后台输出格式输出文档。  
  
-   将文档直接路由到与 [!INCLUDE[TLA2#tla_xps](../../../../includes/tla2sharptla-xps-md.md)] 兼容的打印机。  
  
## 请参阅  
 <xref:System.Windows.Documents.FixedDocument>   
 <xref:System.Windows.Documents.FlowDocument>   
 <xref:System.Windows.Xps.Packaging.XpsDocument>   
 <xref:System.IO.Packaging.ZipPackage>   
 <xref:System.IO.Packaging.ZipPackagePart>   
 <xref:System.IO.Packaging.PackageRelationship>   
 <xref:System.Windows.Controls.DocumentViewer>   
 [Text](../../../../docs/framework/wpf/advanced/optimizing-performance-text.md)   
 [流文档概述](../../../../docs/framework/wpf/advanced/flow-document-overview.md)   
 [打印概述](../../../../docs/framework/wpf/advanced/printing-overview.md)   
 [文档序列化和存储](../../../../docs/framework/wpf/advanced/document-serialization-and-storage.md)