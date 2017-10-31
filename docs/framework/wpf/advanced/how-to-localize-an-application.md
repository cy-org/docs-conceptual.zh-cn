---
title: "如何：对应用程序进行本地化 | Microsoft Docs"
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
  - "应用程序, 本地化"
  - "Localization — 本地化, 应用程序"
  - "LocBaml 工具"
ms.assetid: 5001227e-9326-48a4-9dcd-ba1b89ee6653
caps.latest.revision: 37
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 33
---
# 如何：对应用程序进行本地化
本教程介绍如何通过使用 LocBaml 工具创建本地化应用程序。  
  
> [!NOTE]
>  LocBaml 工具不是可直接用于生产的应用程序。  它表示为一个示例，该示例使用某些本地化 API 并演示编写一个本地化工具的方法。  
>   
>    
  
<a name="Introduction"></a>   
## 概述  
 本讨论提供逐步实现本地化应用程序的方法。  首先，你要准备应用程序，以便可以提取将被翻译的文本。  相关文本翻译后，你要将翻译的文本合并到原始应用程序的新副本中。  
  
<a name="Requirements"></a>   
## 要求  
 在此讨论过程中，你将使用 [!INCLUDE[TLA#tla_msbuild](../../../../includes/tlasharptla-msbuild-md.md)]，这是一个从命令行运行的编译器。  
  
 此外，还会指导你使用项目文件。  有关如何使用 [!INCLUDE[TLA2#tla_msbuild](../../../../includes/tla2sharptla-msbuild-md.md)] 和项目文件的说明，请参阅[生成和部署](../../../../docs/framework/wpf/app-development/building-and-deploying-wpf-applications.md)。  
  
 在此讨论中的所有示例都使用 zh\-CN（中文\-中国）作为区域设置。  这使你能够而无需安装另一种语言就能完成这些示例的步骤。  
  
<a name="create_sample_app"></a>   
## 创建一个简单的应用程序  
 在此步骤中，你将准备要用于本地化的应用程序。  [!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)] 示例提供了 HelloApp 示例，将用于本讨论中的代码示例。  如果要使用此示例，请从 [LocBaml 工具示例](http://go.microsoft.com/fwlink/?LinkID=160016)下载 [!INCLUDE[TLA#tla_xaml](../../../../includes/tlasharptla-xaml-md.md)] 文件。  
  
1.  将应用程序开发到想要开始进行本地化的位置。  
  
2.  在项目文件中指定开发语言，以便 [!INCLUDE[TLA2#tla_msbuild](../../../../includes/tla2sharptla-msbuild-md.md)] 生成主程序集和附属程序集（具有 .resources.dll 扩展的文件）以包含非特定语言资源。  HelloApp 示例中的项目文件是 HelloApp.csproj。  在该文件中，你将找到标识如下的开发语言：  
  
     `<UICulture>en-US</UICulture>`  
  
3.  将 Uid 添加到你的 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] 文件。  Uid 用于跟踪对文件的更改并标识必须翻译的项。  若要将 Uid 添加到文件，请在你的项目文件上运行 **updateuid**：  
  
     **msbuild \/t:updateuid helloapp.csproj**  
  
     若要验证没有缺少或重复的 Uid，请运行 **checkuid**：  
  
     **msbuild \/t:checkuid helloapp.csproj**  
  
     运行 **updateuid** 之后，你的文件应包含 Uid。  例如，在 HelloApp 的 Pane1.xaml 文件中，你应能找到下列内容：  
  
     `<StackPanel x:Uid="StackPanel_1">`  
  
     `<TextBlock x:Uid="TextBlock_1">Hello World</TextBlock>`  
  
     `<TextBlock x:Uid="TextBlock_2">Goodbye World</TextBlock>`  
  
     `</StackPanel>`  
  
<a name="create_dll"></a>   
## 创建非特定语言资源附属程序集  
 将应用程序配置为生成非特定语言资源附属程序集后，则可生成应用程序。  这会生成主应用程序程序集，以及 LocBaml 本地化所需的非特定语言资源附属程序集。  若要生成应用程序：  
  
1.  编译 HelloApp 以创建一个 [!INCLUDE[TLA#tla_dll](../../../../includes/tlasharptla-dll-md.md)]：  
  
     **msbuild helloapp.csproj**  
  
2.  新创建的主应用程序程序集 HelloApp.exe 创建在下列文件夹中：  
  
     `C:\HelloApp\Bin\Debug\`  
  
3.  新创建的非特定语言资源附属程序集 HelloApp.resources.dll 创建在下列文件夹中：  
  
     `C:\HelloApp\Bin\Debug\en-US\`  
  
<a name="build_locbaml"></a>   
## 生成 LocBaml 工具  
  
1.  生成 LocBaml 所需的所有文件都位于 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 示例中。  从 [LocBaml 工具示例](http://go.microsoft.com/fwlink/?LinkID=160016)下载 [!INCLUDE[TLA#tla_lhcshrp](../../../../includes/tlasharptla-lhcshrp-md.md)] 文件。  
  
2.  从命令行运行项目文件 \(locbaml.csproj\) 来生成该工具：  
  
     **msbuild locbaml.csproj**  
  
3.  转到 Bin\\Release 目录以查找新创建的可执行文件 \(locbaml.exe\)。  示例：C:\\LocBaml\\Bin\\Release\\locbaml.exe。  
  
4.  运行 LocBaml 时可指定下列选项：  
  
    -   **parse** 或 **\-p:** 分析 Baml、资源或 [!INCLUDE[TLA2#tla_dll](../../../../includes/tla2sharptla-dll-md.md)] 文件以生成 .csv 或 .txt 文件。  
  
    -   **generate** 或 **\-g:** 通过使用翻译的文件生成本地化的二进制文件。  
  
    -   **out** 或 **\-o** \[*filedirectory*\]**:** 输出文件的名称。  
  
    -   **culture** 或 **\-cul** \[*culture*\]**:** 输出程序集的区域设置。  
  
    -   **translation** 或 **\-trans** \[*translation.csv*\]**:** 经过翻译或本地化的文件。  
  
    -   **asmpath** 或 **\-asmpath:** \[*filedirectory*\]**:** 如果你的 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] 代码包含自定义控件，则必须为自定义控件程序集提供 **asmpath**。  
  
    -   **nologo:** 显示没有徽标或版权信息。  
  
    -   **verbose:** 显示详细模式信息。  
  
    > [!NOTE]
    >  如果在运行该工具时需要选项列表，则键入 **LocBaml.exe** 然后按 ENTER。  
  
<a name="parse_dll"></a>   
## 使用 LocBaml 分析文件  
 由于已创建 LocBaml 工具，就可使用它来分析 HelloApp.resources.dll，从而提取将进行本地化的文本内容。  
  
1.  将 LocBaml.exe 复制到应用程序的 bin\\debug 文件夹，这也是创建主应用程序程序集的位置。  
  
2.  若要分析附属程序集文件并将输出存储为 .csv 文件，请使用下列命令：  
  
     **LocBaml.exe \/parse HelloApp.resources.dll \/out:Hello.csv**  
  
    > [!NOTE]
    >  如果输入文件 HelloApp.resources.dll 不在 LocBaml.exe 所在的同一目录中，请移动其中一个文件以使两个文件都位于同一目录中。  
  
3.  当运行 LocBaml 来分析文件时，输出包含由逗号（.csv 文件）或制表符（.txt 文件）分隔的七个字段。  下面显示了 HelloApp.resources.dll 的已分析的 .csv 文件：  
  
    ||  
    |-|  
    |HelloApp.g.en\-US.resources:window1.baml,Stack1:System.Windows.Controls.StackPanel.$Content,Ignore,FALSE, FALSE,,\#Text1;\#Text2;|  
    |HelloApp.g.en\-US.resources:window1.baml,Text1:System.Windows.Controls.TextBlock.$Content,None,TRUE, TRUE,,Hello World|  
    |HelloApp.g.en\-US.resources:window1.baml,Text2:System.Windows.Controls.TextBlock.$Content,None,TRUE, TRUE,,Goodbye World|  
  
     这七个字段是：  
  
    1.  **BAML Name**。  与源语言附属程序集相关的 BAML 资源的名称。  
  
    2.  **Resource Key**。  本地化的资源标识符。  
  
    3.  **Category**。  值类型。  请参阅[本地化特性和注释](../../../../docs/framework/wpf/advanced/localization-attributes-and-comments.md)。  
  
    4.  **Readability**。  值是否可以由本地化人员读取。  请参阅[本地化特性和注释](../../../../docs/framework/wpf/advanced/localization-attributes-and-comments.md)。  
  
    5.  **Modifiability**。  值是否可以由本地化人员修改。  请参阅[本地化特性和注释](../../../../docs/framework/wpf/advanced/localization-attributes-and-comments.md)。  
  
    6.  **Comments**。  值的附加说明，用于确定值被本地化的方式。  请参阅[本地化特性和注释](../../../../docs/framework/wpf/advanced/localization-attributes-and-comments.md)。  
  
    7.  **Value**。  要翻译为所需区域性设置的文本值。  
  
     下表显示了这些字段映射到 .csv 文件的分隔值的方式：  
  
    |BAML 名称|资源键|类别|可读性|可修改性|注释|值|  
    |-------------|---------|--------|---------|----------|--------|-------|  
    |HelloApp.g.en\-US.resources:window1.baml|Stack1:System.Windows.Controls.StackPanel.$Content|忽略|FALSE|FALSE||\#Text1;\#Text2|  
    |HelloApp.g.en\-US.resources:window1.baml|Text1:System.Windows.Controls.TextBlock.$Content|无|TRUE|TRUE||Hello World|  
    |HelloApp.g.en\-US.resources:window1.baml|Text2:System.Windows.Controls.TextBlock.$Content|无|TRUE|TRUE||Goodbye World|  
  
     请注意，所有 **Comments** 字段的值不包含任何值；如果字段没有值，则为空。  此外请注意第一行中的项既不可读也不可修改，并且拥有“Ignore”作为其 **Category** 值，这些都指示该值不可本地化。  
  
4.  为了便于发现已分析文件中的可本地化项（特别是在大型文件中），可以通过 **Category**、**Readability** 和 **Modifiability** 对这些项进行排序或筛选。  例如，你可以筛选出不可读且不可修改的值。  
  
<a name="translate_loc_content"></a>   
## 翻译可本地化的内容  
 使用任何你可用的工具翻译提取的内容。  执行此操作的一个好办法是将这些资源写入 .csv 文件，并在 [!INCLUDE[TLA#tla_xl](../../../../includes/tlasharptla-xl-md.md)] 中查看它们，对最后一列（值）作出翻译更改。  
  
<a name="merge_translations"></a>   
## 使用 LocBaml 生成新的 .resources.dll 文件  
 通过使用 LocBaml 分析 HelloApp.resources.dll 而标识的内容已被翻译，且必须合并回原始应用程序。  使用 **generate** 或 **\-g** 选项生成一个新的 .resources.dll 文件。  
  
1.  使用下列语法来生成新的 HelloApp.resources.dll 文件。  将区域性标记为 zh\-CN \(\/cul:zh\-CN\)。  
  
     **LocBaml.exe \/generate HelloApp.resources.dll \/trans:Hello.csv \/out:c:\\ \/cul:en\-US**  
  
    > [!NOTE]
    >  如果输入文件 Hello.csv 与可执行文件 LocBaml.exe 不在的同一目录中，请移动其中一个文件以使两个文件都位于同一目录中。  
  
2.  使用新创建的 HelloApp.resources.dll 文件替换 C:\\HelloApp\\Bin\\Debug\\en\-US\\HelloApp.resources.dll 目录中的旧 HelloApp.resources.dll 文件。  
  
3.  应在你的应用程序中将“Hello World”和“Goodbye World”翻译过来。  
  
4.  若要翻译到不同的区域性设置，请使用目标语言的区域设置。  下列示例演示了如何翻译为加拿大法语：  
  
     **LocBaml.exe \/generate HelloApp.resources.dll \/trans:Hellofr\-CA.csv \/out:c:\\ \/cul:fr\-CA**  
  
5.  在主应用程序程序集所在的程序集，创建一个新的特定于区域性的文件夹，以容纳新的附属程序集。  对于加拿大法语，该文件夹将为 fr\-CA。  
  
6.  将生成的附属程序集复制到新建文件夹。  
  
7.  若要测试新的附属程序集，你需要更改应用程序将在其下运行的区域性设置。  可以通过两种方法执行此操作：  
  
    -   更改操作系统的区域设置（“启动”                    &#124; **控制面板** &#124; “区域和语言选项”）。  
  
    -   在你的应用程序中，将下列代码添加到 App.xaml.cs 中：  
  
         [!code-xml[LocBamlChangeCultureSnippets#LocBamlChangeCultureMARKUP](../../../../samples/snippets/csharp/VS_Snippets_Wpf/LocBamlChangeCultureSnippets/CSharp/App.xaml#locbamlchangeculturemarkup)]  
  
         [!code-csharp[LocBamlChangeCultureSnippets#LocBamlChangeCultureCODEBEHIND](../../../../samples/snippets/csharp/VS_Snippets_Wpf/LocBamlChangeCultureSnippets/CSharp/App.xaml.cs#locbamlchangeculturecodebehind)]
         [!code-vb[LocBamlChangeCultureSnippets#LocBamlChangeCultureCODEBEHIND](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/LocBamlChangeCultureSnippets/VisualBasic/Application.xaml.vb#locbamlchangeculturecodebehind)]  
  
<a name="Some_Tips_for_Using_LocBaml"></a>   
## 使用 LocBaml 的一些提示  
  
-   所有定义自定义控件的依赖程序集必须复制到 LocBaml 的本地目录，或安装到 GAC。  这是必要的，因为本地化 API 在读取 [!INCLUDE[TLA#tla_baml](../../../../includes/tlasharptla-baml-md.md)] 时必须具有对依赖程序集的访问权限。  
  
-   如果主程序集已签名，则生成的资源 DLL 也必须签名以进行加载。  
  
-   本地化的资源 DLL 的版本需与主程序集进行同步。  
  
<a name="Whats_Next"></a>   
## 下一步  
 现在，你应该对如何使用 LocBaml 工具有了一个基本的了解。  你应该能够制作包含 Uid 的文件。  通过使用 LocBaml 工具，你应该能够分析文件以提取可本地化的内容，并且在内容翻译后，你应该能够生成一个合并已翻译内容的 resources.dll 文件。  本主题不包括每个可能的细节，但现在你已经掌握了使用 LocBaml 对应用程序进行本地化的必要知识。  
  
## 请参阅  
 [WPF 的全球化](../../../../docs/framework/wpf/advanced/globalization-for-wpf.md)   
 [使用自动布局概述](../../../../docs/framework/wpf/advanced/use-automatic-layout-overview.md)