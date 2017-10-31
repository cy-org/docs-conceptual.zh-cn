---
title: "WPF 应用程序资源、内容和数据文件 | Microsoft Docs"
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
  - "应用程序开发 [WPF], 文件"
  - "应用程序管理 [WPF]"
  - "内容文件 [WPF]"
  - "嵌入的资源 [WPF]"
  - "文件 [WPF]"
  - "松散资源 [WPF]"
  - "引用应用程序文件 [WPF]"
  - "远程文件 [WPF]"
  - "资源文件 [WPF]"
  - "源站点文件 [WPF]"
  - "WPF 应用程序, 文件"
ms.assetid: 7ad2943b-3961-41d3-8fc6-1582d43f5d99
caps.latest.revision: 25
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 21
---
# WPF 应用程序资源、内容和数据文件
[!INCLUDE[TLA#tla_win](../../../../includes/tlasharptla-win-md.md)] 应用程序通常依赖包含不可执行数据的文件，如[!INCLUDE[TLA#tla_xaml](../../../../includes/tlasharptla-xaml-md.md)]、图像、视频和音频。  [!INCLUDE[TLA#tla_wpf](../../../../includes/tlasharptla-wpf-md.md)] 为配置、识别和使用这些类型的数据文件（称为应用程序数据文件）提供了特殊支持。  这种支持主要针对一组特定的应用程序数据文件类型，包括：  
  
-   **资源文件**：编译到可执行或库 [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] 程序集中的数据文件。  
  
-   **内容文件**：与可执行 [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] 程序集具有显式关联的独立数据文件。  
  
-   **源站点文件**：与可执行 [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] 程序集没有关联的独立数据文件。  
  
 这三种类型的文件之间的一个重要区别是：资源文件和内容文件在生成时是已知的；程序集明确地知道它们的存在。  但是对于源站点文件，程序集可能完全不知道它们，或者通过 pack [!INCLUDE[TLA#tla_uri](../../../../includes/tlasharptla-uri-md.md)] 引用知道它们的存在；在后一种情况下，不能保证被引用的源站点文件实际存在。  
  
 为了引用应用程序数据文件，[!INCLUDE[TLA#tla_wpf](../../../../includes/tlasharptla-wpf-md.md)] 使用 Pack [!INCLUDE[TLA#tla_uri](../../../../includes/tlasharptla-uri-md.md)] 方案，这将在 [WPF 中的 Pack URI](../../../../docs/framework/wpf/app-development/pack-uris-in-wpf.md)中详细介绍。  
  
 本主题介绍如何配置和使用应用程序数据文件。  
  
   
  
<a name="Resource_Files"></a>   
## 资源文件  
 如果应用程序数据文件必须始终可供某个应用程序使用，那么保证可用性的唯一方法是将其编译到应用程序的主可执行程序集中，或者它所引用的程序集中。  这种类型的应用程序数据文件称为“资源文件”。  
  
 应在以下情况下使用资源文件：  
  
-   在将资源文件编译到程序集中之后，不需要更新资源文件的内容。  
  
-   希望通过减少文件依赖项的数量来简化应用程序分发的复杂性。  
  
-   应用程序数据文件必须是可本地化的（请参见 [WPF 全球化和本地化概述](../../../../docs/framework/wpf/advanced/wpf-globalization-and-localization-overview.md)）。  
  
> [!NOTE]
>  本节描述的资源文件与资源文件不同描述在 [XAML 资源](../../../../docs/framework/wpf/advanced/xaml-resources.md) 和不同于在 [管理应用程序资源 \(.NET\)](../Topic/Managing%20Application%20Resources%20\(.NET\).md)描述的嵌入或链接的资源。  
  
### 配置资源文件  
 在 [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] 中，资源文件是作为 `Resource` 项包含在 [!INCLUDE[TLA#tla_msbuild](../../../../includes/tlasharptla-msbuild-md.md)] 项目中的文件。  
  
```  
<Project "xmlns=http://schemas.microsoft.com/developer/msbuild/2003" ... >  
  ...  
  <ItemGroup>  
    <Resource Include="ResourceFile.xaml" />  
  </ItemGroup>  
  ...  
</Project>  
```  
  
> [!NOTE]
>  在 [!INCLUDE[TLA#tla_visualstu](../../../../includes/tlasharptla-visualstu-md.md)] 中，可通过将一个文件添加到项目并将其 `Build Action` 设置为 `Resource` 来创建资源文件。  
  
 项目生成时，[!INCLUDE[TLA2#tla_msbuild](../../../../includes/tla2sharptla-msbuild-md.md)] 会将该资源编译到程序集中。  
  
### 使用资源文件  
 若要加载资源文件，可以调用 <xref:System.Windows.Application> 类的 <xref:System.Windows.Application.GetResourceStream%2A> 方法，同时传递标识所需资源文件的 pack [!INCLUDE[TLA2#tla_uri](../../../../includes/tla2sharptla-uri-md.md)]。  <xref:System.Windows.Application.GetResourceStream%2A> 将返回一个 <xref:System.Windows.Resources.StreamResourceInfo> 对象，该对象将该资源文件作为 <xref:System.IO.Stream> 公开，并描述其内容类型。  
  
 例如，下面的代码演示如何使用 <xref:System.Windows.Application.GetResourceStream%2A> 来加载 <xref:System.Windows.Controls.Page> 资源文件，并将其设置为 <xref:System.Windows.Controls.Frame> \(`pageFrame`\) 的内容：  
  
 [!code-csharp[WPFAssemblyResourcesSnippets#LoadAPageResourceFileManuallyCODE](../../../../samples/snippets/csharp/VS_Snippets_Wpf/WPFAssemblyResourcesSnippets/CSharp/ResourcesSample/ApplicationGetResourceStreamSnippetWindow.xaml.cs#loadapageresourcefilemanuallycode)]
 [!code-vb[WPFAssemblyResourcesSnippets#LoadAPageResourceFileManuallyCODE](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/WPFAssemblyResourcesSnippets/VisualBasic/ResourcesSample/ApplicationGetResourceStreamSnippetWindow.xaml.vb#loadapageresourcefilemanuallycode)]  
  
 虽然通过调用 <xref:System.Windows.Application.GetResourceStream%2A> 可以访问 <xref:System.IO.Stream>，但是需要进行一些额外的工作来将其转换为将要设置的属性的类型。  可以改为通过使用代码将资源文件直接加载到某个类型的属性，来让 [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] 负责打开和转换 <xref:System.IO.Stream>。  
  
 下面的示例演示如何使用代码将 <xref:System.Windows.Controls.Page> 直接加载到 <xref:System.Windows.Controls.Frame> \(`pageFrame`\)中。  
  
 [!code-csharp[WPFAssemblyResourcesSnippets#LoadPageResourceFileFromCODE](../../../../samples/snippets/csharp/VS_Snippets_Wpf/WPFAssemblyResourcesSnippets/CSharp/ResourcesSample/ApplicationGetResourceStreamSnippetWindow.xaml.cs#loadpageresourcefilefromcode)]
 [!code-vb[WPFAssemblyResourcesSnippets#LoadPageResourceFileFromCODE](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/WPFAssemblyResourcesSnippets/VisualBasic/ResourcesSample/ApplicationGetResourceStreamSnippetWindow.xaml.vb#loadpageresourcefilefromcode)]  
  
 下面的示例是与上例等效的标记。  
  
 [!code-xml[WPFAssemblyResourcesSnippets#LoadPageResourceFileFromXAML](../../../../samples/snippets/csharp/VS_Snippets_Wpf/WPFAssemblyResourcesSnippets/CSharp/ResourcesSample/ApplicationGetResourceStreamSnippetWindow.xaml#loadpageresourcefilefromxaml)]  
  
### 作为资源文件的应用程序代码文件  
 可以使用 pack [!INCLUDE[TLA2#tla_uri#plural](../../../../includes/tla2sharptla-urisharpplural-md.md)] 来引用一组特殊的 [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] 应用程序代码文件，包括窗口、页、流文档和资源词典。  例如，可以将 <xref:System.Windows.Application.StartupUri%2A?displayProperty=fullName> 属性设置为一个 pack [!INCLUDE[TLA2#tla_uri](../../../../includes/tla2sharptla-uri-md.md)]，该 URL 引用要在应用程序启动时加载的窗口或页。  
  
 [!code-xml[WPFAssemblyResourcesSnippets#SetApplicationStartupURI](../../../../samples/snippets/csharp/VS_Snippets_Wpf/WPFAssemblyResourcesSnippets/CSharp/ResourcesSample/App.xaml#setapplicationstartupuri)]  
  
 当 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] 文件作为一个 `Page` 项包含在 [!INCLUDE[TLA#tla_msbuild](../../../../includes/tlasharptla-msbuild-md.md)] 项目中时，可以进行此操作。  
  
```  
<Project xmlns="http://schemas.microsoft.com/developer/msbuild/2003" ... >  
  ...  
  <ItemGroup>  
    <Page Include="MainWindow.xaml" />  
  </ItemGroup>  
  ...  
</Project>  
```  
  
> [!NOTE]
>  在 [!INCLUDE[TLA2#tla_visualstu](../../../../includes/tla2sharptla-visualstu-md.md)] 中，可以将新的 <xref:System.Windows.Window>、<xref:System.Windows.Navigation.NavigationWindow>、<xref:System.Windows.Controls.Page>、<xref:System.Windows.Documents.FlowDocument> 或 <xref:System.Windows.ResourceDictionary> 添加到项目，标记文件的 `Build Action` 将默认为 `Page`。  
  
 在编译含有 `Page` 项的项目时，[!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] 项将转换为二进制格式，并编译到关联的程序集中。  因此，可以像使用典型的资源文件一样使用这些文件。  
  
> [!NOTE]
>  如果 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] 文件配置为 `Resource` 项，并且没有代码隐藏文件，则原始 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] 将编译到程序集中，而不是原始 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] 的二进制版本。  
  
<a name="Content_Files"></a>   
## 内容文件  
 内容文件是作为松散文件与可执行程序集一起分发的。  虽然它们不编译到程序集中，但编译程序集时所使用的元数据建立了与每个内容文件的关联。  
  
 如果应用程序需要一组特定的应用程序数据文件，并且您希望能够更新这些文件，而无需重新编译使用它们的程序集，则应该使用内容文件。  
  
### 配置内容文件  
 若要将内容文件添加到项目中，必须在 `Content` 项中包含一个应用程序数据文件。  此外，因为内容文件不直接编译到程序集中，所以需要设置 [!INCLUDE[TLA2#tla_msbuild](../../../../includes/tla2sharptla-msbuild-md.md)]```CopyToOutputDirectory` 元数据元素，以指定将内容文件复制到一个相对于生成的程序集的位置。  如果希望在每次生成项目时都将资源复制到生成输出文件夹，可将 `CopyToOutputDirectory` 元数据元素设置为 `Always` 值。  否则，可以使用 `PreserveNewest` 值来确保只有最新版本的资源才会复制到生成输出文件夹。  
  
 下面演示的是一个配置为内容文件的文件，只有在将新版本的资源添加到项目时，它才会复制到生成输出文件夹。  
  
```  
<Project xmlns="http://schemas.microsoft.com/developer/msbuild/2003" ... >  
  ...  
  <ItemGroup>  
    <Content Include="ContentFile.xaml">  
      <CopyToOutputDirectory>PreserveNewest</CopyToOutputDirectory>  
    </Content>  
  </ItemGroup>  
  ...  
</Project>  
```  
  
> [!NOTE]
>  在 [!INCLUDE[TLA2#tla_visualstu](../../../../includes/tla2sharptla-visualstu-md.md)] 中，可通过将一个文件添加到项目并将其 `Build Action` 设置为 `Content` 来创建内容文件，然后将其 `Copy to Output Directory` 设置为 `Copy always`（与 `Always` 相同）和 `Copy if newer`（与 `PreserveNewest` 相同）。  
  
 生成项目时，对于每一个内容文件，将有一个相应的 <xref:System.Windows.Resources.AssemblyAssociatedContentFileAttribute> 特性编译到程序集的元数据中。  
  
 `[assembly: AssemblyAssociatedContentFile("ContentFile.xaml")]`  
  
 <xref:System.Windows.Resources.AssemblyAssociatedContentFileAttribute> 的值表示内容文件相对于其在项目中的位置的路径。  例如，如果内容文件位于某个项目子文件夹中，则附加路径信息将合并到 <xref:System.Windows.Resources.AssemblyAssociatedContentFileAttribute> 值中。  
  
 `[assembly: AssemblyAssociatedContentFile("Resources/ContentFile.xaml")]`  
  
 <xref:System.Windows.Resources.AssemblyAssociatedContentFileAttribute> 值也是内容文件在生成输出文件夹中的路径的值。  
  
### 使用内容文件  
 若要加载内容文件，可以调用 <xref:System.Windows.Application> 类的 <xref:System.Windows.Application.GetContentStream%2A> 方法，同时传递标识所需内容文件的 pack [!INCLUDE[TLA2#tla_uri](../../../../includes/tla2sharptla-uri-md.md)]。  <xref:System.Windows.Application.GetContentStream%2A> 将返回一个 <xref:System.Windows.Resources.StreamResourceInfo> 对象，该对象将该内容文件作为 <xref:System.IO.Stream> 公开，并描述其内容类型。  
  
 例如，下面的代码演示如何使用 <xref:System.Windows.Application.GetContentStream%2A> 来加载 <xref:System.Windows.Controls.Page> 内容文件，并将其设置为 <xref:System.Windows.Controls.Frame> \(`pageFrame`\) 的内容：  
  
 [!code-csharp[WPFAssemblyResourcesSnippets#LoadAPageContentFileManuallyCODE](../../../../samples/snippets/csharp/VS_Snippets_Wpf/WPFAssemblyResourcesSnippets/CSharp/ResourcesSample/ApplicationGetContentStreamSnippetWindow.xaml.cs#loadapagecontentfilemanuallycode)]
 [!code-vb[WPFAssemblyResourcesSnippets#LoadAPageContentFileManuallyCODE](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/WPFAssemblyResourcesSnippets/VisualBasic/ResourcesSample/ApplicationGetContentStreamSnippetWindow.xaml.vb#loadapagecontentfilemanuallycode)]  
  
 虽然通过调用 <xref:System.Windows.Application.GetContentStream%2A> 可以访问 <xref:System.IO.Stream>，但是需要进行一些额外的工作来将其转换为将要设置的属性的类型。  可以改为通过使用代码将资源文件直接加载到某个类型的属性，来让 [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] 负责打开和转换 <xref:System.IO.Stream>。  
  
 下面的示例演示如何使用代码将 <xref:System.Windows.Controls.Page> 直接加载到 <xref:System.Windows.Controls.Frame> \(`pageFrame`\)中。  
  
 [!code-csharp[WPFAssemblyResourcesSnippets#LoadPageContentFileFromCODE](../../../../samples/snippets/csharp/VS_Snippets_Wpf/WPFAssemblyResourcesSnippets/CSharp/ResourcesSample/ApplicationGetContentStreamSnippetWindow.xaml.cs#loadpagecontentfilefromcode)]
 [!code-vb[WPFAssemblyResourcesSnippets#LoadPageContentFileFromCODE](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/WPFAssemblyResourcesSnippets/VisualBasic/ResourcesSample/ApplicationGetContentStreamSnippetWindow.xaml.vb#loadpagecontentfilefromcode)]  
  
 下面的示例是与上例等效的标记。  
  
 [!code-xml[WPFAssemblyResourcesSnippets#LoadPageContentFileFromXAML](../../../../samples/snippets/csharp/VS_Snippets_Wpf/WPFAssemblyResourcesSnippets/CSharp/ResourcesSample/ApplicationGetContentStreamSnippetWindow.xaml#loadpagecontentfilefromxaml)]  
  
<a name="Site_of_Origin_Files"></a>   
## 源站点文件。  
 资源文件与同其一起分发的程序集有显式关系，这一关系由 <xref:System.Windows.Resources.AssemblyAssociatedContentFileAttribute> 定义。  但是，有些情况下可能需要在程序集和应用程序数据文件之间建立隐式关系或不存在的关系，这些情况包括：  
  
-   编译时文件不存在。  
  
-   在运行之前您不知道程序集将需要哪些文件。  
  
-   您希望能够更新文件，而又无需重新编译与这些文件关联的程序集。  
  
-   应用程序使用大型数据文件，如音频和视频，并且您希望仅在用户选择下载时才下载这些文件。  
  
 使用传统的 [!INCLUDE[TLA2#tla_uri](../../../../includes/tla2sharptla-uri-md.md)] 方案可以加载这些类型的文件，如 file:\/\/\/ 和 http:\/\/ 方案。  
  
 [!code-xml[WPFAssemblyResourcesSnippets#AbsolutePackUriFileHttpReferenceXAML](../../../../samples/snippets/csharp/VS_Snippets_Wpf/WPFAssemblyResourcesSnippets/CSharp/ResourcesSample/AbsolutePackUriPage.xaml#absolutepackurifilehttpreferencexaml)]  
  
 但是，file:\/\/\/ 和 http:\/\/ 方案要求应用程序具有完全信任。  如果应用程序是从 Internet 或 Intranet 启动的 [!INCLUDE[TLA#tla_xbap](../../../../includes/tlasharptla-xbap-md.md)]，并且它请求的权限集只针对从这些位置启动的应用程序，则松散文件只能从应用程序的源站点（启动位置）加载。  这样的文件称为“源站点”文件。  
  
 虽然源站点文件并不仅限于部分可信应用程序，但它却是部分可信应用程序的唯一选择。  完全可信应用程序可能仍然需要加载它们在生成时所不知道的应用程序数据文件；但是完全可信应用程序可以使用 file:\/\/\/，应用程序数据文件很可能将安装在该应用程序集的同一个文件夹或其子文件夹中。  在此情况下，使用源站点引用比使用 file:\/\/\/ 更加容易，因为使用 file:\/\/\/ 需要找出文件的完整路径。  
  
> [!NOTE]
>  源站点文件不会与 [!INCLUDE[TLA#tla_xbap](../../../../includes/tlasharptla-xbap-md.md)] 一起缓存在客户端计算机上，而内容文件却会如此。  所以，只有在专门请求下载源站点文件时，才会下载它们。  如果 [!INCLUDE[TLA#tla_xbap](../../../../includes/tlasharptla-xbap-md.md)] 应用程序有大型媒体文件，则将这些文件配置为源站点文件意味着应用程序初始启动更快，并且这些文件只会按需下载。  
  
### 配置源站点文件  
 如果源站点文件在编译时不存在或未知，则需要使用传统部署机制来确保所需文件在运行时可用，包括使用 `XCopy` 命令行程序或 [!INCLUDE[TLA#tla_wininstall](../../../../includes/tlasharptla-wininstall-md.md)]。  
  
 如果在编译时您知道要放置于源站点的文件，但仍然希望避免显式依赖项，则可以将这些文件作为 `None` 项添加到 [!INCLUDE[TLA#tla_msbuild](../../../../includes/tlasharptla-msbuild-md.md)] 项目中。  与内容文件一样，需要设置 [!INCLUDE[TLA2#tla_msbuild](../../../../includes/tla2sharptla-msbuild-md.md)] `CopyToOutputDirectory` 特性来指定将源站点文件复制到一个相对于生成的程序集的位置（通过指定 `Always` 值或 `PreserveNewest` 值）。  
  
```  
<Project xmlns="http://schemas.microsoft.com/developer/msbuild/2003" ... >  
  ...  
  <None Include="PageSiteOfOriginFile.xaml">  
    <CopyToOutputDirectory>Always</CopyToOutputDirectory>  
  </None>  
  ...  
</Project>  
```  
  
> [!NOTE]
>  在 [!INCLUDE[TLA2#tla_visualstu](../../../../includes/tla2sharptla-visualstu-md.md)] 中，可通过将一个文件添加到项目，并将其 `Build Action` 设置为 `None` 来创建源站点文件。  
  
 在项目生成时，[!INCLUDE[TLA2#tla_msbuild](../../../../includes/tla2sharptla-msbuild-md.md)] 将指定文件复制到生成输出文件夹。  
  
### 使用源站点文件  
 若要原始文件的站点，可以调用 <xref:System.Windows.Application> 类的 <xref:System.Windows.Application.GetRemoteStream%2A> 方法，同时传递标识原始文件的所需站点的 pack [!INCLUDE[TLA2#tla_uri](../../../../includes/tla2sharptla-uri-md.md)]。  <xref:System.Windows.Application.GetRemoteStream%2A> 将返回一个 <xref:System.Windows.Resources.StreamResourceInfo> 对象，该对象将原始文件的该站点作为 <xref:System.IO.Stream> 公开，并描述其内容类型。  
  
 例如，下面的代码演示如何使用 <xref:System.Windows.Application.GetRemoteStream%2A> 来加载 <xref:System.Windows.Controls.Page> 源站点文件，并将其设置为 <xref:System.Windows.Controls.Frame> \(`pageFrame`\) 的内容。  
  
 [!code-csharp[WPFAssemblyResourcesSnippets#LoadAPageSOOFileManuallyCODE](../../../../samples/snippets/csharp/VS_Snippets_Wpf/WPFAssemblyResourcesSnippets/CSharp/ResourcesSample/SOOPage.xaml.cs#loadapagesoofilemanuallycode)]
 [!code-vb[WPFAssemblyResourcesSnippets#LoadAPageSOOFileManuallyCODE](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/WPFAssemblyResourcesSnippets/VisualBasic/ResourcesSample/SOOPage.xaml.vb#loadapagesoofilemanuallycode)]  
  
 虽然通过调用 <xref:System.Windows.Application.GetRemoteStream%2A> 可以访问 <xref:System.IO.Stream>，但是需要进行一些额外的工作来将其转换为将要设置的属性的类型。  可以改为通过使用代码将资源文件直接加载到某个类型的属性，来让 [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] 负责打开和转换 <xref:System.IO.Stream>。  
  
 下面的示例演示如何使用代码将 <xref:System.Windows.Controls.Page> 直接加载到 <xref:System.Windows.Controls.Frame> \(`pageFrame`\)中。  
  
 [!code-csharp[WPFAssemblyResourcesSnippets#LoadPageSOOFileFromCODE](../../../../samples/snippets/csharp/VS_Snippets_Wpf/WPFAssemblyResourcesSnippets/CSharp/ResourcesSample/SOOPage.xaml.cs#loadpagesoofilefromcode)]
 [!code-vb[WPFAssemblyResourcesSnippets#LoadPageSOOFileFromCODE](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/WPFAssemblyResourcesSnippets/VisualBasic/ResourcesSample/SOOPage.xaml.vb#loadpagesoofilefromcode)]  
  
 下面的示例是与上例等效的标记。  
  
 [!code-xml[WPFAssemblyResourcesSnippets#LoadPageSOOFileFromXAML](../../../../samples/snippets/csharp/VS_Snippets_Wpf/WPFAssemblyResourcesSnippets/CSharp/ResourcesSample/SOOPage.xaml#loadpagesoofilefromxaml)]  
  
<a name="Rebuilding_after_Changing_Build_Type"></a>   
## 更改生成类型后重新生成  
 在更改应用程序数据文件的生成类型后，需要重新生成整个应用程序以确保应用这些更改。  如果只生成应用程序，则不会应用更改。  
  
## 请参阅  
 [WPF 中的 Pack URI](../../../../docs/framework/wpf/app-development/pack-uris-in-wpf.md)