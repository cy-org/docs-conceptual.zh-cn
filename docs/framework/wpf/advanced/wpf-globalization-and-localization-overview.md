---
title: "WPF 全球化和本地化概述 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-wpf"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "Globalization — 全球化, 关于全球化"
  - "Localization — 本地化, 关于本地化"
ms.assetid: 56e5a5c8-6c96-4d19-b8e1-a5be1dc564af
caps.latest.revision: 39
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 34
---
# WPF 全球化和本地化概述
当您将自己的产品限制为只能通过一种语言使用时，您便将潜在的客户群限制为全球 65 亿人口中的一小部分。  如果您想让自己的应用程序被全球用户所接受，那么对产品进行经济而有效的本地化将是赢得更多客户的最好、最经济的方法。  
  
 本概述介绍 [!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)] 中的全球化和本地化。  全球化是指设计和开发在多个地点执行的应用程序。  例如，全球化支持适用于不同区域性用户的本地化用户界面和区域数据。  [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 提供全球化设计功能，包括自动布局、附属程序集以及本地化特性和注释。  
  
 本地化是针对应用程序所支持的特定区域性将应用程序资源转换为本地化版本的过程。  在 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 中进行本地化时，可使用 <xref:System.Windows.Markup.Localizer> 命名空间中的 API。这些 API 实现 [LocBaml Tool Sample](http://go.microsoft.com/fwlink/?LinkID=160016)（LocBaml 工具示例）命令行工具。  有关如何生成和使用 LocBaml 的信息，请参见[对应用程序进行本地化](../../../../docs/framework/wpf/advanced/how-to-localize-an-application.md)。  
  
   
  
## 在 WPF 中进行全球化和本地化的最佳做法  
 按照本节提供的与 UI 设计和本地化相关的提示操作，可以最大限度地利用 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 中内置的大部分全球化和本地化功能。  
  
### WPF UI 设计的最佳做法  
 当您设计基于 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 的 [!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)] 时，请考虑实施下列最佳做法：  
  
-   在 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] 中编写 [!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)]；避免在代码中创建 [!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)]。  当您使用 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] 创建 [!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)] 时，应通过内置的本地化 API 来对其进行公开。  
  
-   避免使用绝对位置和固定大小来对内容进行布局；相反，应使用相对位置或自动大小调整。  
  
    -   使用 <xref:System.Windows.Window.SizeToContent%2A>；并将宽度和高度设置为 `Auto`。  
  
    -   避免使用 <xref:System.Windows.Controls.Canvas> 对 [!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)] 进行布局。  
  
    -   使用 <xref:System.Windows.Controls.Grid> 及其大小共享功能。  
  
-   在边距中提供额外的空间，因为本地化文本通常需要更多的空间。  额外空间为可能会延伸的字符预留了余地。  
  
-   启用 <xref:System.Windows.Controls.TextBlock> 上的 <xref:System.Windows.Controls.TextBlock.TextWrapping%2A> 以避免剪裁。  
  
-   设置 **xml:lang** 特性。  此特性描述特定元素及其子元素的区域性。  此属性的值可更改 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 中几种功能的行为。例如，它可以更改断字、拼写检查、数字替换、复杂字符造型和字体回退的行为。  有关设置 [XAML 中 xml:lang 的处理](../../../../docs/framework/xaml-services/xml-lang-handling-in-xaml.md)的更多信息，请参见 [WPF 的全球化](../../../../docs/framework/wpf/advanced/globalization-for-wpf.md)。  
  
-   创建自定义的复合字体，以更好地控制用于不同语言的字体。  默认情况下，[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 使用“Windows\\Fonts”目录中的 GlobalUserInterface.composite 字体。  
  
-   当您创建的导航应用程序可能在以从右到左的格式显示文本的区域性中进行本地化时，请显式设置每个页的 <xref:System.Windows.FlowDirection> 以确保该页不从 <xref:System.Windows.Navigation.NavigationWindow> 继承 <xref:System.Windows.FlowDirection>。  
  
-   当您创建在浏览器之外承载的独立导航应用程序时，请将初始应用程序的 <xref:System.Windows.Application.StartupUri%2A> 设置为 <xref:System.Windows.Navigation.NavigationWindow> 而不是页面（例如，`<Application StartupUri="NavigationWindow.xaml">`）。  此设计使您可以更改窗口和导航栏的 <xref:System.Windows.FlowDirection>。  有关更多信息和示例，请参见 [Globalization Homepage Sample](http://go.microsoft.com/fwlink/?LinkID=159990)（全球化主页示例）。  
  
### WPF 本地化的最佳做法  
 当您对基于 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 的应用程序进行本地化时，请考虑实施下列最佳做法：  
  
-   使用本地化注释为本地化人员提供额外的上下文。  
  
-   使用本地化特性控制本地化，而不是选择性地省略元素上的 <xref:System.Windows.Markup.Localizer.BamlLocalizableResourceKey.Uid%2A> 属性。  有关更多信息，请参见[本地化特性和注释](../../../../docs/framework/wpf/advanced/localization-attributes-and-comments.md)。  
  
-   使用 **msbuild \/t:updateuid** 和 **\/t:checkuid** 在 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] 中添加和检查 <xref:System.Windows.Markup.Localizer.BamlLocalizableResourceKey.Uid%2A> 属性。  使用 <xref:System.Windows.Markup.Localizer.BamlLocalizableResourceKey.Uid%2A> 属性跟踪开发和本地化之间的更改。<xref:System.Windows.Markup.Localizer.BamlLocalizableResourceKey.Uid%2A> 属性可以帮助您对新的开发更改进行本地化。  如果将 <xref:System.Windows.Markup.Localizer.BamlLocalizableResourceKey.Uid%2A> 属性手动添加到 [!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)]，则任务通常会比较繁重并且缺乏准确性。  
  
    -   开始进行本地化之后，请不要编辑或更改 <xref:System.Windows.Markup.Localizer.BamlLocalizableResourceKey.Uid%2A> 属性。  
  
    -   不要使用重复的 <xref:System.Windows.Markup.Localizer.BamlLocalizableResourceKey.Uid%2A> 属性（当您使用“复制并粘贴”命令时，请记住此提示）。  
  
    -   在 AssemblyInfo.\* 中设置 `UltimateResourceFallback` 位置以指定合适的回退语言（例如，`[assembly: NeutralResourcesLanguage("en-US",   UltimateResourceFallbackLocation.Satellite)]`）。  
  
         如果您决定通过在项目文件中省略 `<UICulture>` 标记来在主程序集中包括源语言，请将 `UltimateResourceFallback` 位置设置为主程序集而不是附属程序集（例如，`[assembly: NeutralResourcesLanguage("en-US", UltimateResourceFallbackLocation.MainAssembly)]`）。  
  
<a name="workflow_to_localize"></a>   
## 对 WPF 应用程序进行本地化  
 当您对 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 应用程序进行本地化时，有多种选择。  例如，您可以将应用程序中的可本地化资源绑定到 [!INCLUDE[TLA2#tla_xml](../../../../includes/tla2sharptla-xml-md.md)] 文件，在 resx 表中存储可本地化的文本，或者让本地化人员使用 [!INCLUDE[TLA#tla_xaml](../../../../includes/tlasharptla-xaml-md.md)] 文件。  本节介绍使用 XAML 的 BAML 形式的本地化工作流，该工作流有以下几个好处：  
  
-   可以在生成之后进行本地化。  
  
-   可以通过本地化从较低版本 XAML 的 BAML 形式更新到更高版本 XAML 的 BAML 形式，以便在开发的同时进行本地化。  
  
-   因为 XAML 的 BAML 形式是 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] 的已编译形式，所以可以在编译时验证原始源元素和语义。  
  
### 本地化生成过程  
 开发 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 应用程序时，本地化的生成过程如下：  
  
-   开发人员创建并全球化 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 应用程序。  在项目文件中，开发人员设置 `<UICulture>en-US</UICulture>`，以便在编译应用程序时生成一个非特定语言主程序集。此程序集具有一个附属 .resources.dll 文件，该文件包含所有可本地化的资源。因为我们的本地化 [!INCLUDE[TLA2#tla_api#plural](../../../../includes/tla2sharptla-apisharpplural-md.md)] 支持从主程序集进行提取，所以可选择在主程序集中保留源语言。  
  
-   在将文件编译到生成中时，会将 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] 转换为 XAML 的 BAML 形式。  非特定区域性的 `MyDialog.exe` 和区域相关的（英语）`MyDialog.resources.dll` 文件将发布到说英语的客户手中。  
  
### 本地化工作流  
 在生成未本地化的 `MyDialog.resources.dll` 文件之后，本地化过程便开始了。  使用 <xref:System.Windows.Markup.Localizer> 下的 [!INCLUDE[TLA2#tla_api#plural](../../../../includes/tla2sharptla-apisharpplural-md.md)] 将原始 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] 中的 [!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)] 元素和属性从 XAML 的 BAML 形式提取为键\/值对。  本地化人员使用键\/值对来对应用程序进行本地化。  在本地化完成之后，您可以从新值生成一个新的 .resource.dll。  
  
 键\/值对的键是开发人员放置在原始 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] 中的 `x:Uid` 值。  [!INCLUDE[TLA2#tla_api](../../../../includes/tla2sharptla-api-md.md)] 可以使用这些 `x:Uid` 值来跟踪和合并在本地化过程中发生在开发人员与本地化人员之间的更改。  例如，如果在本地化人员开始进行本地化之后，开发人员更改了 [!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)]，则您可以将开发更改与已经完成的本地化工作进行合并，以便使损失的翻译工作达到最少。  
  
 下图显示了一个基于 XAML 的 BAML 形式的典型本地化工作流。  此关系图假设开发人员用英语编写应用程序。  开发人员创建 WPF 应用程序并将其全球化。  在项目文件中，开发人员设置 `<UICulture>en-US</UICulture>`，以便在生成时会生成一个非特定语言的主程序集，并使该程序集具有一个包含所有可本地化资源的附属 .resources.dll。  或者，因为 WPF 本地化 API 支持从主程序集进行提取，所以还可以保留主程序集中的源语言。  生成过程结束之后，XAML 会被编译为 BAML。  非特定区域性的 MyDialog.exe.resources.dll 将被发布到说英语的客户手中。  
  
 ![本地化工作流](../../../../docs/framework/wpf/advanced/media/localizationworkflow.png "LocalizationWorkflow")  
  
 ![未本地化的工作流](../../../../docs/framework/wpf/advanced/media/localizationworkflow2.png "LocalizationWorkflow2")  
  
<a name="examples_of_localization"></a>   
## WPF 本地化示例  
 本节包含几个本地化应用程序示例，以帮助您了解如何生成和本地化 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 应用程序。  
  
#### “运行”对话框示例  
 下图显示**“运行”**对话框示例的输出。  
  
 **：**  
  
 ![“运行”对话框](../../../../docs/framework/wpf/advanced/media/rundialogenglish.png "RunDialogEnglish")  
  
 **德语：**  
  
 ![德语的“运行”对话框](../../../../docs/framework/wpf/advanced/media/rundialoggerman.png "RunDialogGerman")  
  
 **设计一个全球化“运行”对话框**  
  
 此示例使用 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 和 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] 生成一个**“运行”**对话框。  此对话框与 [!INCLUDE[TLA#tla_win](../../../../includes/tlasharptla-win-md.md)]“开始”菜单中包含的**“运行”**对话框等效。  
  
 生成全球化对话框的一些要点包括：  
  
 **Automatic Layout**  
  
 *在 Window1.xaml 中：*  
  
 `<Window SizeToContent="WidthAndHeight">`  
  
 以前的 Window 属性会根据内容的大小自动调整窗口的大小。  此属性可以防止窗口切断在本地化之后增加大小的内容；它还可以在内容由于本地化而减小大小时移除不必要的空格。  
  
 `<Grid x:Uid="Grid_1">`  
  
 为了使 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 本地化 [!INCLUDE[TLA2#tla_api#plural](../../../../includes/tla2sharptla-apisharpplural-md.md)] 可以正确运行，需要使用 <xref:System.Windows.Markup.Localizer.BamlLocalizableResourceKey.Uid%2A> 属性。  
  
 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 本地化 [!INCLUDE[TLA2#tla_api#plural](../../../../includes/tla2sharptla-apisharpplural-md.md)] 使用这些属性来跟踪[!INCLUDE[TLA#tla_ui](../../../../includes/tlasharptla-ui-md.md)] 的开发和本地化之间的更改。  <xref:System.Windows.Markup.Localizer.BamlLocalizableResourceKey.Uid%2A> 属性使您可以将 [!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)] 的较新版本与 [!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)] 的较早本地化合并起来。  通过在命令 shell 中运行 **msbuild \/t:updateuid RunDialog.csproj**，可以添加 <xref:System.Windows.Markup.Localizer.BamlLocalizableResourceKey.Uid%2A> 属性。  因为手动添加 <xref:System.Windows.Markup.Localizer.BamlLocalizableResourceKey.Uid%2A> 属性通常比较费时并且准确性较差，所以建议使用此方法来添加这些属性。  可以通过运行 **msbuild \/t:checkuid RunDialog.csproj** 来检查是否正确设置了 <xref:System.Windows.Markup.Localizer.BamlLocalizableResourceKey.Uid%2A> 属性。  
  
 使用 <xref:System.Windows.Controls.Grid> 控件可以构造 [!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)]，该控件对利用 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 中的自动布局很有用处。  请注意，对话框被拆分成三行五列。  没有一个行和列定义具有固定大小；因此，位于每个单元格中的 [!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)] 元素能够在本地化过程中适应大小的增加和减小。  
  
 [!code-xml[GlobalizationRunDialog#GridColumnDef](../../../../samples/snippets/csharp/VS_Snippets_Wpf/GlobalizationRunDialog/CS/Window1.xaml#gridcolumndef)]  
  
 放置**“Open:”（打开）**标签和 <xref:System.Windows.Controls.ComboBox> 的前两列占了 [!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)] 总宽度的 10%。  
  
 [!code-xml[GlobalizationRunDialog#GridColumnDef2](../../../../samples/snippets/csharp/VS_Snippets_Wpf/GlobalizationRunDialog/CS/Window1.xaml#gridcolumndef2)]  
  
 请注意，此示例使用了 <xref:System.Windows.Controls.Grid> 的共享大小调整功能。  最后三列通过将自身放置在相同的 <xref:System.Windows.Controls.DefinitionBase.SharedSizeGroup%2A> 中利用此功能。  正如您可以从属性的名称中看出的那样，此属性使不同的列可以采用相同的大小。  因此，在将“Browse…”本地化为更长的字符串“Durchsuchen…”时，所有按钮的宽度都会增加，而不是显示一个小的“OK”按钮和一个大得不相称的“Durchsuchen…”按钮。  
  
 **Xml:lang**  
  
 `Xml:lang="en-US"`  
  
 请注意放置在 [!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)] 的根元素中的 [XAML 中 xml:lang 的处理](../../../../docs/framework/xaml-services/xml-lang-handling-in-xaml.md)。  此属性描述给定元素及其子元素的区域性。  [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 中的多项功能都使用此值，在本地化过程中应对此值进行相应的更改。  此值会更改在断字以及对字词进行拼写检查时所使用的字典。  它还会影响数字的显示以及字体回退系统选择所用字体的方式。  最后，该属性会影响数值的显示方式以及用复杂字母书写的文本的造型方式。  默认值为“en\-US”。  
  
 **Building a Satellite Resource Assembly**  
  
 *在 .csproj 中：*  
  
 `<UICulture>en-US</UICulture>`  
  
 请注意，增加了 `UICulture` 值。  如果将此属性设置为有效的 <xref:System.Globalization.CultureInfo> 值（例如，“en\-US”），生成项目时会产生一个包含所有可本地化的资源的附属程序集。  
  
 `<Resource Include="RunIcon.JPG">`  
  
 `<Localizable>False</Localizable>`  
  
 `</Resource>`  
  
 由于 `RunIcon.JPG` 对所有区域性都应具有同样的外观，因此不需要对其进行本地化。  `Localizable` 设置为 `false`，以使其保留在非特定语言主程序集而不是附属程序集中。  所有不可编译资源的默认 `Localizable` 值都设置为 `true`。  
  
 **对“运行”对话框进行本地化**  
  
 **Parse**  
  
 生成应用程序之后，对其进行本地化的第一步是将可本地化的资源从附属程序集中分析出来。  为了演示本主题，请使用 [LocBaml Tool Sample](http://go.microsoft.com/fwlink/?LinkID=160016) 上的示例 LocBaml 工具。  请注意，LocBaml 只是一个示例工具，其目的是帮助您了解有关如何生成适合您的本地化过程的本地化工具的入门知识。  使用 LocBaml 可以运行下面的命令以进行分析：**LocBaml \/parse RunDialog.resources.dll \/out:**，从而生成“RunDialog.resources.dll.CSV”文件。  
  
 **Localize**  
  
 使用您所选的支持 Unicode 的 CSV 编辑器来编辑此文件。  筛选掉本地化类别为“None”的所有项。  您应看到下面的项：  
  
||||  
|-|-|-|  
|资源键|本地化类别|值|  
|Button\_1:System.Windows.Controls.Button.$Content|Button|确定|  
|Button\_2:System.Windows.Controls.Button.$Content|Button|取消|  
|Button\_3:System.Windows.Controls.Button.$Content|Button|Browse...|  
|ComboBox\_1:System.Windows.Controls.ComboBox.$Content|ComboBox||  
|TextBlock\_1:System.Windows.Controls.TextBlock.$Content|Text|Type the name of a program, folder, document, or Internet resource, and Windows will open it for you.|  
|TextBlock\_2:System.Windows.Controls.TextBlock.$Content|Text|Open:|  
|Window\_1:System.Windows.Window.Title|标题|Run|  
  
 将该应用程序本地化为德语版本需要进行下面的翻译：  
  
||||  
|-|-|-|  
|资源键|本地化类别|值|  
|Button\_1:System.Windows.Controls.Button.$Content|Button|确定|  
|Button\_2:System.Windows.Controls.Button.$Content|Button|Abbrechen|  
|Button\_3:System.Windows.Controls.Button.$Content|Button|Durchsuchen…|  
|ComboBox\_1:System.Windows.Controls.ComboBox.$Content|ComboBox||  
|TextBlock\_1:System.Windows.Controls.TextBlock.$Content|Text|Geben Sie den Namen eines Programms, Ordners, Dokuments oder einer Internetresource an.|  
|TextBlock\_2:System.Windows.Controls.TextBlock.$Content|Text|Öffnen:|  
|Window\_1:System.Windows.Window.Title|标题|Run|  
  
 **Generate**  
  
 本地化的最后一步涉及到创建新近本地化的附属程序集。  可以使用下面的 LocBaml 命令完成此操作：  
  
 **LocBaml.exe \/generate RunDialog.resources.dll \/trans:RunDialog.resources.dll.CSV \/out: .  \/cul:de\-DE**  
  
 在德语版 [!INCLUDE[TLA#tla_mswin](../../../../includes/tlasharptla-mswin-md.md)] 上，如果此 resources.dll 被放置在主程序集旁边的“de\-DE”文件夹中，则会自动加载此资源而不是“en\-US”文件夹中的资源。  如果没有德语版的 [!INCLUDE[TLA#tla_mswin](../../../../includes/tlasharptla-mswin-md.md)] 以测试这种情况，请将区域性设置为您所使用的 [!INCLUDE[TLA#tla_mswin](../../../../includes/tlasharptla-mswin-md.md)] 的区域性（例如，  en\-US），并替换原始的 resources.dll。  
  
 **Satellite Resource Loading**  
  
|MyDialog.exe|en\-US\\MyDialog.resources.dll|de\-DE\\MyDialog.resources.dll|  
|------------------|------------------------------------|------------------------------------|  
|代码|原始英语 BAML|本地化 BAML|  
|非特定区域性资源|其他英语资源|其他被本地化到德语的资源|  
  
 .NET framework 根据应用程序的 `Thread.CurrentThread.CurrentUICulture` 自动选择要加载的附属资源程序集。  其默认设置为您的 [!INCLUDE[TLA#tla_mswin](../../../../includes/tlasharptla-mswin-md.md)] 操作系统的区域性。  因此，如果您使用的是德语版 [!INCLUDE[TLA#tla_mswin](../../../../includes/tlasharptla-mswin-md.md)]，则会加载 de\-DE\\MyDialog.resources.dll；如果您使用的是英语版 [!INCLUDE[TLA#tla_mswin](../../../../includes/tlasharptla-mswin-md.md)]，则会加载 en\-US\\MyDialog.resources.dll。  通过在项目的 AssemblyInfo.\* 中指定 NeutralResourcesLanguage，可以设置应用程序的最终回退资源。  例如，如果您指定：  
  
 `[assembly: NeutralResourcesLanguage("en-US", UltimateResourceFallbackLocation.Satellite)]`  
  
 则如果 de\-DE\\MyDialog.resources.dll 和 de\\MyDialog.resources.dll 都不可用，则德语版 Windows 将使用 en\-US\\MyDialog.resources.dll。  
  
### Microsoft 沙特阿拉伯主页  
 下图显示了英语和阿拉伯语主页。  有关生成这些图形的完整示例，请参见 [Globalization Homepage Sample](http://go.microsoft.com/fwlink/?LinkID=159990)（全球化主页示例）。  
  
 **：**  
  
 ![英语页面](../../../../docs/framework/wpf/advanced/media/englishhomepage.png "EnglishHomepage")  
  
 **阿拉伯语：**  
  
 ![“阿拉伯语”页](../../../../docs/framework/wpf/advanced/media/arabichomepage.png "ArabicHomepage")  
  
### 设计全球 Microsoft 主页  
 Microsoft 沙特阿拉伯网站的这个实体模型阐释了针对 RightToLeft 语言提供的全球化功能。  诸如希伯来语和阿拉伯语之类的语言具有从右到左的阅读顺序，因此 [!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)] 的布局方式通常必须与英语等从左到右的语言中的布局方式不同。  从左右方向的语言本地化到右左方向的语言或者反之可能相当困难。  [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 旨在使此类本地化工作变得更容易。  
  
 **FlowDirection**  
  
 *Homepage.xaml：*  
  
 [!code-xml[GlobalizationHomepage#Homepage](../../../../samples/snippets/csharp/VS_Snippets_Wpf/GlobalizationHomepage/CS/Homepage.xaml#homepage)]  
  
 请注意 <xref:System.Windows.Controls.Page> 上的 <xref:System.Windows.FrameworkElement.FlowDirection%2A> 属性。  将此属性更改为 <xref:System.Windows.FlowDirection> 将更改 <xref:System.Windows.Controls.Page> 及其子元素的 <xref:System.Windows.FrameworkElement.FlowDirection%2A>，以使此 [!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)] 的布局如阿拉伯语用户所期望的那样变为从右到左。  可以通过在任何元素上指定显式的 <xref:System.Windows.FrameworkElement.FlowDirection%2A> 来重写继承行为。  <xref:System.Windows.FrameworkElement.FlowDirection%2A> 属性对所有 <xref:System.Windows.FrameworkElement> 或文档相关元素都可用，并且具有隐式值 <xref:System.Windows.FlowDirection>。  
  
 请注意，当根 <xref:System.Windows.FrameworkElement.FlowDirection%2A> 发生更改时，甚至连背景渐变画笔都进行了正确的翻转：  
  
 **FlowDirection\="LeftToRight"**  
  
 ![从左到右显示](../../../../docs/framework/wpf/advanced/media/lefttoright.png "LeftToRight")  
  
 **FlowDirection\="RightToLeft"**  
  
 ![从右向左显示](../../../../docs/framework/wpf/advanced/media/righttoleft.png "RightToLeft")  
  
 **避免对面板和控件使用固定维度**  
  
 请浏览一下 Homepage.xaml，您会注意到，除了为顶级 <xref:System.Windows.Controls.DockPanel> 上的整个 [!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)] 指定的固定宽度和高度之外，没有其他固定维度。  请避免使用固定尺寸，以防系统裁剪可能比源文本长的本地化文本。  [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 面板和控件将根据其所包含的内容自动调整大小。  大多数控件还具有最小和最大尺寸，设置这些尺寸可以加强控制（例如  MinWidth\= "20"）。  通过 <xref:System.Windows.Controls.Grid>，还可以使用“\*”设置相对宽度和高度（例如  Width\= "0.25\*"），或使用该控件的单元格大小共享功能。  
  
 **本地化注释**  
  
 在很多情况下，内容可能不太明确，难以翻译。  开发人员或设计人员能够通过本地化注释为本地化人员提供额外的上下文和注释。  例如，下面的 Localization.Comments 阐明了字符“&#124;”的用法。  
  
 [!code-xml[GlobalizationHomepage#LocalizationComment](../../../../samples/snippets/csharp/VS_Snippets_Wpf/GlobalizationHomepage/CS/Homepage.xaml#localizationcomment)]  
  
 此注释与 TextBlock\_1 的内容相关联，并且在使用 LocBaml 工具（请参见[对应用程序进行本地化](../../../../docs/framework/wpf/advanced/how-to-localize-an-application.md)）时，可以在输出 .csv 文件的 TextBlock\_1 行的第六列看到此注释：  
  
|||||||  
|-|-|-|-|-|-|  
|资源键|类别|可读性|可修改性|注释|值|  
|TextBlock\_1:System.Windows.Controls.TextBlock.$Content|Text|TRUE|TRUE|此字符被用作装饰性规则。|&#124;|  
  
 使用下面的语法可以将注释放置在任何元素的内容或属性上：  
  
 [!code-xml[GlobalizationHomepage#LocalizationCommentsProp](../../../../samples/snippets/csharp/VS_Snippets_Wpf/GlobalizationHomepage/CS/Homepage.xaml#localizationcommentsprop)]  
  
 **本地化特性**  
  
 通常，开发人员或本地化经理需要控制本地化人员能够阅读和修改的内容。  例如，可能不希望本地化人员翻译贵公司的名称或法律用语。  [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 提供了一些特性，使用这些特性可以设置元素的内容或属性（本地化工具可以使用这些内容或属性锁定、隐藏元素或对元素进行排序）的可读性、可修改性和类别。  有关更多信息，请参见 <xref:System.Windows.Localization.Attributes%2A>。  为了演示此示例，LocBaml 工具仅输出这些特性的值。  [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 控件对这些特性都使用默认值，但可以重写这些默认值。  例如，下面的示例重写 `TextBlock_1` 的默认本地化特性，将其内容设置为可供本地化人员阅读，但不能被其修改。  
  
 [!code-xml[LocalizationComAtt#LocalizationAttributes](../../../../samples/snippets/csharp/VS_Snippets_Wpf/LocalizationComAtt/CSharp/Attributes.xaml#localizationattributes)]  
  
 除了可读性和可修改性特性之外，[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 还提供了常见 UI 类别 \(<xref:System.Windows.LocalizationCategory>\) 的枚举，使用该枚举可以为本地化人员提供更多的上下文。  平台控件的 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 默认类别也可以在 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] 中重写：  
  
 [!code-xml[LocalizationComAtt#LocalizationAttributesOverridden](../../../../samples/snippets/csharp/VS_Snippets_Wpf/LocalizationComAtt/CSharp/Attributes.xaml#localizationattributesoverridden)]  
  
 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 所提供的默认本地化特性还可以通过代码进行重写，因此您可以正确地为自定义控件设置合适的默认值。  例如：  
  
 `[Localizability(Readability = Readability.Readable, Modifiability=Modifiability.Unmodifiable, LocalizationCategory.None)]`  
  
 `public class CorporateLogo: TextBlock`  
  
 `{`  
  
 `…`  
  
 `..`  
  
 `.`  
  
 `}`  
  
 在 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] 中设置的实例特定特性优先于在自定义控件的代码中设置的值。  有关特性和注释的更多信息，请参见[本地化特性和注释](../../../../docs/framework/wpf/advanced/localization-attributes-and-comments.md)。  
  
 **字体回退和复合字体**  
  
 如果您指定一种不支持给定码位范围的字体，则 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 将使用位于“Windows\\Fonts”目录中的 Global User Interface.compositefont 自动回退到支持该范围的字体。  复合字体与任何其他字体的用法一样，通过设置元素的 FontFamily（例如  FontFamily\= "Global User Interface"）可以显式使用复合字体。  通过创建您自己的复合字体并指定针对特定码位范围和语言所使用的字体，可以指定您自己的字体回退首选项。  
  
 有关复合字体的更多信息，请参见 <xref:System.Windows.Media.FontFamily>。  
  
 **本地化 Microsoft 主页**  
  
 可以按照“运行”对话框示例中的相同步骤对此应用程序进行本地化。  在 [Globalization Homepage Sample](http://go.microsoft.com/fwlink/?LinkID=159990)（全球化主页示例）中可以找到本地化的阿拉伯语 .csv 文件。