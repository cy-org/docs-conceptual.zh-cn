---
title: "合并资源字典 | Microsoft Docs"
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
  - "合并资源字典"
  - "合并资源字典"
ms.assetid: d159531f-05d4-49fd-b951-c332de51e5bc
caps.latest.revision: 13
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 12
---
# 合并资源字典
[!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)]资源支持合并的资源字典功能。 此功能使您能够定义的资源部分[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]应用程序的外部编译[!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)]应用程序。 然后可以在应用程序之间共享资源并将也更方便地隔离进行本地化。  
  
## <a name="introducing-a-merged-resource-dictionary"></a>引入了合并的资源字典  
 在标记中，你可以使用以下语法将合并的资源字典引入到页面︰  
  
 [!code-xml[ResourceMergeDictionary#MergedXAML](../../../../samples/snippets/csharp/VS_Snippets_Wpf/ResourceMergeDictionary/CS/default.xaml#mergedxaml)]  
  
 请注意， <xref:System.Windows.ResourceDictionary>元素不具有[X:key 指令](../../../../docs/framework/xaml-services/x-key-directive.md)，这是通常所必需的资源集合中的所有项。 但另一个<xref:System.Windows.ResourceDictionary>内引用<xref:System.Windows.ResourceDictionary.MergedDictionaries%2A>集合是一种特殊情况，留待此合并的资源字典方案。 <xref:System.Windows.ResourceDictionary>引入了合并资源字典中不能有[X:key 指令](../../../../docs/framework/xaml-services/x-key-directive.md)。 通常情况下，每个<xref:System.Windows.ResourceDictionary>内<xref:System.Windows.ResourceDictionary.MergedDictionaries%2A>集合指定<xref:System.Windows.ResourceDictionary.Source%2A>属性。 值<xref:System.Windows.ResourceDictionary.Source%2A>应[!INCLUDE[TLA#tla_uri](../../../../includes/tlasharptla-uri-md.md)]可解析为要合并的资源文件的位置。 该目标[!INCLUDE[TLA2#tla_uri](../../../../includes/tla2sharptla-uri-md.md)]必须是另一个[!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)]文件中，与<xref:System.Windows.ResourceDictionary>作为其根元素。  
  
> [!NOTE]
>  它是合法定义内的资源<xref:System.Windows.ResourceDictionary>作为指定的替代方法指定为合并字典<xref:System.Windows.ResourceDictionary.Source%2A>，发送或同时从指定的源包含的资源的。 但是，这不是一种常见方案;合并的字典的主要方案是合并从外部文件位置的资源。 如果你想要指定某一页的标记内的资源，则应通常定义这些主<xref:System.Windows.ResourceDictionary>而不是在合并的字典。  
  
## <a name="merged-dictionary-behavior"></a>合并的字典的行为  
 合并的字典中的资源占用恰好在它们被合并到主资源字典中的作用域之后资源查找范围中的位置。 尽管资源键必须是在任何字典中是唯一的存在的密钥可以多次一对合并的字典。 在这种情况下，则返回该资源将来自按顺序在找到的最后一个字典<xref:System.Windows.ResourceDictionary.MergedDictionaries%2A>集合。 如果<xref:System.Windows.ResourceDictionary.MergedDictionaries%2A>集合中定义[!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)]，则集合中合并的字典的顺序是元素的顺序，在标记中所述。 如果主字典和一个字典，其中进行了合并，则未定义键，则返回该资源将来自主字典。 这些范围规则同样适用为静态资源引用和动态资源引用。  
  
### <a name="merged-dictionaries-and-code"></a>合并的字典和代码  
 合并的字典可以添加到`Resources`通过代码的字典。 默认情况下，最初为空<xref:System.Windows.ResourceDictionary>存在任何`Resources`属性都具有默认值，最初为空<xref:System.Windows.ResourceDictionary.MergedDictionaries%2A>集合属性。 若要添加的代码通过合并的字典，则获取到所需的主副本的引用<xref:System.Windows.ResourceDictionary>，获取其<xref:System.Windows.ResourceDictionary.MergedDictionaries%2A>属性值，然后调用`Add`泛型`Collection`中包含<xref:System.Windows.ResourceDictionary.MergedDictionaries%2A>。 您添加的对象必须是一个新<xref:System.Windows.ResourceDictionary>。 在代码中，您没有设置<xref:System.Windows.ResourceDictionary.Source%2A>属性。 相反，你必须获取<xref:System.Windows.ResourceDictionary>通过创建一个，或者加载其中一个对象。 加载现有值的一种方法<xref:System.Windows.ResourceDictionary>调用<xref:System.Windows.Markup.XamlReader.Load%2A?displayProperty=fullName>在现有[!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)]具有文件流<xref:System.Windows.ResourceDictionary>根，然后转换<xref:System.Windows.Markup.XamlReader.Load%2A?displayProperty=fullName>返回值为<xref:System.Windows.ResourceDictionary>。  
  
### <a name="merged-resource-dictionary-uris"></a>合并的资源字典 Uri  
 有几种技术来包括合并的资源字典，这由[!INCLUDE[TLA#tla_uri](../../../../includes/tlasharptla-uri-md.md)]将使用的格式。 概括地说，这些技术可以分为两个类别︰ 作为项目的一部分，编译的资源和不项目的一部分作为编译的资源。  
  
 对于编译为项目的一部分的资源，可以使用引用的资源位置的相对路径。 相对路径是在编译期间计算的。 所需的资源必须定义为资源生成操作作为项目的一部分。 如果在项目中作为资源包括资源.xaml 文件，不需要将资源文件复制到输出目录，该资源已包含在编译的应用程序。 此外可以使用内容的生成操作，但您必须再将文件复制到输出目录，并还将相同路径关系中的资源文件部署到可执行文件。  
  
> [!NOTE]
>  不要使用嵌入的资源生成操作。 该生成操作本身支持[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]应用程序，但是在解析<xref:System.Windows.ResourceDictionary.Source%2A>并未并入<xref:System.Resources.ResourceManager>，并因此无法分离从流的单个资源。 您仍可以使用嵌入的资源，出于其他目的，只要您也使用了<xref:System.Resources.ResourceManager>才能访问资源。  
  
 相关的方法是使用指向的 Pack URI[!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)]文件中，并把它作为源。 Pack URI 可实现对引用的程序集和其他技术的组件的引用。 Pack Uri 的详细信息，请参阅[WPF 应用程序资源、 内容和数据文件](../../../../docs/framework/wpf/app-development/wpf-application-resource-content-and-data-files.md)。  
  
 对于不项目的一部分作为编译的资源，URI 是在运行时计算的。 您可以使用一种常见的 URI 传输如文件: 或 http︰ 如果要引用的资源文件。 使用非资源方法的缺点是该文件︰ 访问需要额外的部署步骤和 http︰ 访问权限意味着 Internet 安全区域。  
  
### <a name="reusing-merged-dictionaries"></a>重用合并的字典  
 您可以重复使用或共享应用程序之间的合并的资源字典，因为可以通过任何引用要合并的资源字典有效[!INCLUDE[TLA#tla_uri](../../../../includes/tlasharptla-uri-md.md)]。 完全如何执行此操作将取决于您应用程序的部署策略和应用程序模型您遵循。 使用前面提到的 Pack URI 策略提供了一种方法通常将合并资源跨多个项目在开发过程中通过共享程序集引用。 在这种情况下，资源仍分发客户端，而且至少一个应用程序必须部署已引用程序集。 还有可能引用通过使用 http 协议的分布式 URI 合并的资源。  
  
 将合并的字典编写为本地应用程序文件或本地共享存储是另一个可能的合并的字典 / 应用程序部署方案。  
  
### <a name="localization"></a>本地化  
 如果需要本地化的资源隔离到的字典来合并到主字典的更多信息，而且保持为松散[!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)]，这些文件可以单独进行本地化。 这种方法是本地化的附属资源程序集的轻量替代。 有关详细信息，请参阅[WPF 全球化和本地化概述](../../../../docs/framework/wpf/advanced/wpf-globalization-and-localization-overview.md)。  
  
## <a name="see-also"></a>另请参阅  
 <xref:System.Windows.ResourceDictionary>   
 [XAML 资源](../../../../docs/framework/wpf/advanced/xaml-resources.md)   
 [资源和代码](../../../../docs/framework/wpf/advanced/resources-and-code.md)   
 [WPF 应用程序资源、 内容和数据文件](../../../../docs/framework/wpf/app-development/wpf-application-resource-content-and-data-files.md)