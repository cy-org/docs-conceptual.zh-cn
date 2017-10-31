---
title: "将字体与应用程序一起打包 | Microsoft Docs"
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
  - "应用程序, 打包字体"
  - "字体, 与应用程序一起打包"
  - "将字体与应用程序一起打包"
  - "版式, 将字体与应用程序一起打包"
ms.assetid: db15ee48-4d24-49f5-8b9d-a64460865286
caps.latest.revision: 29
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 25
---
# 将字体与应用程序一起打包
本主题概述如何将字体随 [!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)] 应用程序一起打包。  
  
> [!NOTE]
>  正如大多数类型的软件一样，字体文件也不是出售的，而是授予其使用许可。  用来控制字体使用的许可证因供应商而异，但一般说来，大多数许可证（包括 [!INCLUDE[TLA#tla_ms#initcap](../../../../includes/tlasharptla-mssharpinitcap-md.md)] 随应用程序和 [!INCLUDE[TLA#tla_mswin](../../../../includes/tlasharptla-mswin-md.md)] 提供的字体的许可证）都不允许将字体嵌入应用程序中或以其他方式重新发布。  因此，作为开发人员，您需要确保自己对于嵌入到应用程序中或者以其他方式重新发布的任何字体拥有所需的许可权。  
  
   
  
<a name="introduction_to_packaging_fonts"></a>   
## 字体打包简介  
 可以很方便地将字体作为资源打包在 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 应用程序中，以显示用户界面文本和基于文本的其他类型的内容。  字体可以与应用程序的程序集文件分开，也可以嵌入到这些程序集文件中。  您还可以创建纯资源字体库以供应用程序引用。  
  
 [!INCLUDE[TLA#tla_opentype](../../../../includes/tlasharptla-opentype-md.md)] 和 [!INCLUDE[TLA#tla_truetype](../../../../includes/tlasharptla-truetype-md.md)] 字体包含一个类型标志 fsType，它指示字体的嵌入许可权。  但是，这个类型标志仅引用存储在文档中的嵌入字体，而不引用嵌入到应用程序中的字体。  可以通过创建 <xref:System.Windows.Media.GlyphTypeface> 对象并引用它的 <xref:System.Windows.Media.GlyphTypeface.EmbeddingRights%2A> 属性来检索字体的字体嵌入权。  有关 fsType 标志的更多信息，请参考 [OpenType Specification](http://www.microsoft.com/typography/otspec/os2.htm)（OpenType 规格）的“OS\/2 and Windows Metrics”（OS\/2 和 Windows 规格）部分。  
  
 [Microsoft Typography](http://www.microsoft.com/typography/links/)（Microsoft 版式）网站包括联系信息，这些信息可帮助您查找特定的字体供应商或者查找自定义作品的字体供应商。  
  
<a name="adding_fonts_as_content_items"></a>   
## 将字体作为内容项添加  
 您可以将字体作为项目内容项添加到应用程序中，这些项目内容项与应用程序的程序集文件是分开的。  这意味着内容项不会作为资源嵌入到程序集中。  下面的项目文件示例演示如何定义内容项。  
  
```  
<Project DefaultTargets="Build" xmlns="http://schemas.microsoft.com/developer/msbuild/2003">  
  <!-- Other project build settings ... -->  
  
  <ItemGroup>  
    <Content Include="Peric.ttf" />  
    <Content Include="Pericl.ttf" />  
  </ItemGroup>  
</Project>  
```  
  
 为了确保应用程序可以在运行时使用字体，这些字体必须能够从应用程序的部署目录中访问。  使用应用程序项目文件中的 `<CopyToOutputDirectory>` 元素，可以在生成过程中将字体自动复制到应用程序部署目录中。  下面的项目文件示例演示如何将字体复制到部署目录中。  
  
```  
<ItemGroup>  
  <Content Include="Peric.ttf">  
    <CopyToOutputDirectory>PreserveNewest</CopyToOutputDirectory>  
  </Content>  
  <Content Include="Pericl.ttf">  
    <CopyToOutputDirectory>PreserveNewest</CopyToOutputDirectory>  
  </Content>  
</ItemGroup>  
```  
  
 下面的代码示例演示如何将应用程序的字体作为内容项来引用，所引用的内容项必须与应用程序的程序集文件位于同一个目录中。  
  
 [!code-xml[FontSnippets#FontPackageSnippet8](../../../../samples/snippets/csharp/VS_Snippets_Wpf/FontSnippets/CSharp/FontPackageSnippets.xaml#fontpackagesnippet8)]  
  
<a name="adding_fonts_as_resource_items"></a>   
## 将字体作为资源项添加  
 您可以将字体作为项目资源项添加到应用程序中，这些项目资源项会嵌入到应用程序的程序集文件中。  对资源使用单独的子目录有助于对应用程序的项目文件进行组织。  下面的项目文件示例演示如何在一个单独的子目录中将字体定义为资源项。  
  
```  
<Project DefaultTargets="Build" xmlns="http://schemas.microsoft.com/developer/msbuild/2003">  
  <!-- Other project build settings ... -->  
  
  <ItemGroup>  
    <Resource Include="resources\Peric.ttf" />  
    <Resource Include="resources\Pericl.ttf" />  
  </ItemGroup>  
</Project>  
```  
  
> [!NOTE]
>  在将字体作为资源添加到您的应用程序中时，请确保您设置的是 `<Resource>` 元素，而不是应用程序项目文件中的 `<EmbeddedResource>` 元素。  不支持将 `<EmbeddedResource>` 元素用于生成操作。  
  
 下面的标记示例演示如何引用应用程序的字体资源。  
  
 [!code-xml[FontSnippets#FontPackageSnippet1](../../../../samples/snippets/csharp/VS_Snippets_Wpf/FontSnippets/CSharp/FontPackageSnippets.xaml#fontpackagesnippet1)]  
  
### 在代码中引用字体资源项  
 为了在代码中引用字体资源项，必须提供一个由两部分组成的字体资源引用：基本[!INCLUDE[TLA#tla_uri](../../../../includes/tlasharptla-uri-md.md)] 和字体位置引用。  这些值用作 <xref:System.Windows.Media.FontFamily.%23ctor%2A> 方法的参数。  下面的代码示例演示如何在名为 `resources` 的项目子目录中引用应用程序的字体资源。  
  
 [!code-csharp[FontSnippets#FontPackageSnippet2](../../../../samples/snippets/csharp/VS_Snippets_Wpf/FontSnippets/CSharp/FontPackageSnippets.xaml.cs#fontpackagesnippet2)]
 [!code-vb[FontSnippets#FontPackageSnippet2](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/FontSnippets/visualbasic/fontpackagesnippets.xaml.vb#fontpackagesnippet2)]  
  
 基本[!INCLUDE[TLA#tla_uri](../../../../includes/tlasharptla-uri-md.md)] 可以包括字体资源所在的应用程序子目录。  在这种情况下，字体位置引用将不需要指定目录，而必须包括一个前导“`./`”，该前缀指示字体资源位于由基本[!INCLUDE[TLA#tla_uri](../../../../includes/tlasharptla-uri-md.md)] 指定的目录中。  下面的代码示例演示了另一种引用字体资源项的方法，该示例与上面的代码示例等效。  
  
 [!code-csharp[FontSnippets#FontPackageSnippet5](../../../../samples/snippets/csharp/VS_Snippets_Wpf/FontSnippets/CSharp/FontPackageSnippets.xaml.cs#fontpackagesnippet5)]
 [!code-vb[FontSnippets#FontPackageSnippet5](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/FontSnippets/visualbasic/fontpackagesnippets.xaml.vb#fontpackagesnippet5)]  
  
### 在同一个应用程序子目录中引用字体  
 可以将应用程序内容和资源文件放在应用程序项目中由用户定义的同一个子目录中。  下面的项目文件示例显示了在同一个子目录中定义的内容页和字体资源。  
  
```  
<ItemGroup>  
  <Page Include="pages\HomePage.xaml" />  
</ItemGroup>  
<ItemGroup>  
  <Resource Include="pages\Peric.ttf" />  
  <Resource Include="pages\Pericl.ttf" />  
</ItemGroup>  
```  
  
 由于应用程序内容和字体位于同一个子目录中，因此字体引用是相对于应用程序内容的。  下面的示例演示当字体与应用程序在同一个目录中时，如何引用应用程序的字体资源。  
  
 [!code-xml[FontSnippets#FontPackageSnippet3](../../../../samples/snippets/csharp/VS_Snippets_Wpf/FontSnippets/CSharp/pages/HomePage.xaml#fontpackagesnippet3)]  
  
 [!code-csharp[FontSnippets#FontPackageSnippet4](../../../../samples/snippets/csharp/VS_Snippets_Wpf/FontSnippets/CSharp/pages/HomePage.xaml.cs#fontpackagesnippet4)]
 [!code-vb[FontSnippets#FontPackageSnippet4](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/FontSnippets/visualbasic/pages/homepage.xaml.vb#fontpackagesnippet4)]  
  
### 在应用程序中枚举字体  
 若要在应用程序中将字体作为资源项来枚举，应使用 <xref:System.Windows.Media.Fonts.GetFontFamilies%2A> 或 <xref:System.Windows.Media.Fonts.GetTypefaces%2A> 方法。  下面的示例演示如何使用 <xref:System.Windows.Media.Fonts.GetFontFamilies%2A> 方法从应用程序字体所在的位置返回 <xref:System.Windows.Media.FontFamily> 对象的集合。  在本示例中，应用程序包含一个名为“resources”的子目录。  
  
 [!code-csharp[FontSnippets#FontsSnippet3](../../../../samples/snippets/csharp/VS_Snippets_Wpf/FontSnippets/CSharp/FontFamilySnippets.xaml.cs#fontssnippet3)]
 [!code-vb[FontSnippets#FontsSnippet3](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/FontSnippets/visualbasic/fontfamilysnippets.xaml.vb#fontssnippet3)]  
  
 下面的示例演示如何使用 <xref:System.Windows.Media.Fonts.GetTypefaces%2A> 方法从应用程序字体所在的位置返回 <xref:System.Windows.Media.Typeface> 对象的集合。  在本示例中，应用程序包含一个名为“resources”的子目录。  
  
 [!code-csharp[FontSnippets#FontsSnippet7](../../../../samples/snippets/csharp/VS_Snippets_Wpf/FontSnippets/CSharp/FontFamilySnippets.xaml.cs#fontssnippet7)]
 [!code-vb[FontSnippets#FontsSnippet7](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/FontSnippets/visualbasic/fontfamilysnippets.xaml.vb#fontssnippet7)]  
  
<a name="creating_a_font_resource_library"></a>   
## 创建字体资源库  
 您可以创建仅包含字体的纯资源库，这种类型的库项目中没有任何代码。  创建纯资源库是将资源与使用它们的应用程序代码分开的一种常用方法。  这还使得库程序集可以包括在多个应用程序项目中。  下面的项目文件示例显示了纯资源库项目的关键部分。  
  
```  
<PropertyGroup>  
  <AssemblyName>FontLibrary</AssemblyName>  
  <OutputType>library</OutputType>  
  ...  
</PropertyGroup>  
...  
<ItemGroup>  
  <Resource Include="Kooten.ttf" />  
  <Resource Include="Pesca.ttf" />  
</ItemGroup  
```  
  
### 引用资源库中的字体  
 若要在应用程序中引用资源库中的字体，必须将库程序集的名称作为字体引用的前缀。  在本例中，字体资源程序集是“FontLibrary”。  若要将程序集名称与程序集内的引用分开，应使用“;”字符。  添加后跟字体名引用的“Component”关键字即完成字体库资源的完整引用。  下面的代码示例演示如何引用资源库程序集内的字体。  
  
 [!code-xml[OpenTypeFontsSample#OpenTypeFontsSample1](../../../../samples/snippets/csharp/VS_Snippets_Wpf/OpenTypeFontsSample/CS/Kootenay.xaml#opentypefontssample1)]  
  
> [!NOTE]
>  本 SDK 包含一组 [!INCLUDE[TLA#tla_opentype](../../../../includes/tlasharptla-opentype-md.md)] 字体示例，您可以在 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 应用程序中使用这些字体。  这些字体是在纯资源库中定义的。  有关更多信息，请参见[示例 OpenType 字体包](../../../../docs/framework/wpf/advanced/sample-opentype-font-pack.md)。  
  
<a name="limitations_on_font_usage"></a>   
## 字体的使用限制  
 下面介绍在 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 应用程序中对字体进行打包和使用时的几个限制：  
  
-   **字体嵌入权限位：** [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 应用程序不检查或实施任何字体嵌入权限位。  有关更多信息，请参见[Introduction\_to\_Packing Fonts](#introduction_to_packaging_fonts)一节。  
  
-   **源字体站点：** [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 应用程序不允许对 http 或 ftp [!INCLUDE[TLA#tla_uri](../../../../includes/tlasharptla-uri-md.md)] 进行字体引用。  
  
-   **使用 pack: 表示法的绝对 URI：** [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 应用程序不允许您将“pack:”用作字体的绝对[!INCLUDE[TLA#tla_uri](../../../../includes/tlasharptla-uri-md.md)] 引用的一部分，来以编程方式创建 <xref:System.Windows.Media.FontFamily> 对象。  例如，`"pack://application:,,,/resources/#Pericles Light"` 是无效的字体引用。  
  
-   **自动嵌入字体：**在设计时，不支持搜索应用程序对字体的使用情况，而且不支持自动在应用程序的资源中嵌入字体。  
  
-   **字体子集：** [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 应用程序不支持为非固定文档创建字体子集。  
  
-   如果存在不正确的引用，应用程序将回退到使用可用字体。  
  
## 请参阅  
 <xref:System.Windows.Documents.Typography>   
 <xref:System.Windows.Media.FontFamily>   
 [Microsoft Typography: Links, News, and Contacts](http://www.microsoft.com/typography/links/)   
 [OpenType Specification](http://www.microsoft.com/typography/otspec/)   
 [OpenType 字体功能](../../../../docs/framework/wpf/advanced/opentype-font-features.md)   
 [示例 OpenType 字体包](../../../../docs/framework/wpf/advanced/sample-opentype-font-pack.md)