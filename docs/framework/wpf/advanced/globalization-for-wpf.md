---
title: "WPF 的全球化 | Microsoft Docs"
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
  - "Globalization — 全球化"
  - "国际化用户界面, XAML"
  - "XAML, Globalization — 全球化"
  - "XAML, 国际化用户界面"
ms.assetid: 4571ccfe-8a60-4f06-9b37-7ac0b1c2d10f
caps.latest.revision: 35
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 31
---
# WPF 的全球化
本主题介绍了您在编写面向全球市场的 [!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)] 应用程序时应注意的问题。  [!INCLUDE[TLA#tla_net](../../../../includes/tlasharptla-net-md.md)] 的 `System.Globalization` 中定义了全球化编程元素。  
  
   
  
<a name="xaml_globalization"></a>   
## XAML 全球化  
 [!INCLUDE[TLA#tla_xaml#initcap](../../../../includes/tlasharptla-xamlsharpinitcap-md.md)] 基于 [!INCLUDE[TLA#tla_xml](../../../../includes/tlasharptla-xml-md.md)]，并采用在 [!INCLUDE[TLA2#tla_xml](../../../../includes/tla2sharptla-xml-md.md)] 规范中定义的全球化支持。  以下各节介绍了一些您应了解的 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] 功能。  
  
<a name="char_reference"></a>   
### 字符引用  
 字符引用使用十进制或十六进制的形式指定它表示的特定 [!INCLUDE[TLA#tla_unicode](../../../../includes/tlasharptla-unicode-md.md)] 字符的数字。  下面的示例演示十进制字符引用。  
  
```  
Ϩ  
```  
  
 此示例演示十六进制字符引用。  请注意，十六进制数的前面带有一个 **x**。  
  
```  
Ϩ  
```  
  
<a name="encoding"></a>   
### 编码  
 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] 支持的编码有 [!INCLUDE[TLA#tla_ascii](../../../../includes/tlasharptla-ascii-md.md)]、[!INCLUDE[TLA2#tla_unicode](../../../../includes/tla2sharptla-unicode-md.md)] UTF\-16 和 UTF\-8。  编码语句位于 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] 文档的开头。  如果不存在编码特性，并且没有任何字节顺序，则分析器默认为 UTF\-8。  UTF\-8 和 UTF\-16 都是首选编码。  不支持 UTF\-7。  下面的示例演示如何在 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] 文件中指定 UTF\-8 编码。  
  
```  
?xml encoding="UTF-8"?  
```  
  
<a name="lang_attrib"></a>   
### 语言特性  
 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] 使用 [xml:lang](../../../../docs/framework/xaml-services/xml-lang-handling-in-xaml.md) 来表示元素的语言特性。  若要使用 <xref:System.Globalization.CultureInfo> 类，语言特性值应为 <xref:System.Globalization.CultureInfo> 预定义的区域性名称之一。  [xml:lang](../../../../docs/framework/xaml-services/xml-lang-handling-in-xaml.md) 在元素树中可按 XML 规则继承（但并不一定这样继承，因为存在依赖项属性继承）；在未明确赋值的情况下，其默认值为空字符串。  
  
 语言特性对指定方言非常有用。  例如，法语在法国、魁北克、比利时和瑞士的拼写、词汇和发音各不相同。  此外，中文、日语和朝鲜语虽然具有相同的 [!INCLUDE[TLA2#tla_unicode](../../../../includes/tla2sharptla-unicode-md.md)] 码位，但表意图形各不一样，并使用完全不同的字体。  
  
 以下[!INCLUDE[TLA#tla_xaml](../../../../includes/tlasharptla-xaml-md.md)] 示例使用 `fr-CA` 语言特性指定加拿大法语。  
  
```  
<TextBlock xml:lang="fr-CA">Découvrir la France</TextBlock>  
```  
  
<a name="unicode"></a>   
### Unicode  
 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] 支持所有 [!INCLUDE[TLA2#tla_unicode](../../../../includes/tla2sharptla-unicode-md.md)] 功能（包括代理项）。  只要能将字符集映射到 [!INCLUDE[TLA2#tla_unicode](../../../../includes/tla2sharptla-unicode-md.md)]，则支持该字符集。  例如，GB18030 中引入了某些可映射到中日韩 \(CJK\) 扩展 A 和 B 以及代理项对的字符，因此完全受支持。  [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 应用程序可使用 <xref:System.Globalization.StringInfo> 操作字符串，而无需知道它们是否具有代理项对或组合字符。  
  
<a name="design_intl_ui_with_xaml"></a>   
## 使用 XAML 设计国际用户界面  
 本节说明编写应用程序时应考虑的[!INCLUDE[TLA#tla_ui](../../../../includes/tlasharptla-ui-md.md)] 功能。  
  
<a name="intl_text"></a>   
### 国际化文本  
 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 包含对所有 [!INCLUDE[TLA#tla_winfx](../../../../includes/tlasharptla-winfx-md.md)]支持的书写系统的内置处理。  
  
 下面是当前支持的脚本：  
  
-   阿拉伯语  
  
-   孟加拉语  
  
-   梵文  
  
-   西里尔语  
  
-   希腊语  
  
-   古吉拉特语  
  
-   古尔木其文  
  
-   希伯来语  
  
-   表意文字脚本  
  
-   卡纳达语  
  
-   老挝语  
  
-   拉丁语  
  
-   马拉雅拉姆语  
  
-   蒙古语  
  
-   奥里亚语  
  
-   叙利亚语  
  
-   泰米尔语  
  
-   泰卢固语  
  
-   塔纳文  
  
-   泰语\*  
  
-   藏语  
  
 \*此版本中支持显示和编辑泰语，但不支持断词。  
  
 当前不支持的脚本包括：  
  
-   高棉文  
  
-   古朝鲜语  
  
-   缅甸语  
  
-   僧伽罗文  
  
 所有书写系统引擎都支持 [!INCLUDE[TLA#tla_opentype](../../../../includes/tlasharptla-opentype-md.md)] 字体。  [!INCLUDE[TLA2#tla_opentype](../../../../includes/tla2sharptla-opentype-md.md)] 字体可以包含 [!INCLUDE[TLA2#tla_opentype](../../../../includes/tla2sharptla-opentype-md.md)] 布局表格，该布局表格可使字体创建者更好地设计国际化的高端版式字体。  [!INCLUDE[TLA2#tla_opentype](../../../../includes/tla2sharptla-opentype-md.md)] 字体布局表格包含有关标志符号替换、标志符号定位、论证、基线定位和启用文本处理应用程序以改进文本布局的信息。  
  
 通过 [!INCLUDE[TLA2#tla_opentype](../../../../includes/tla2sharptla-opentype-md.md)] 字体，可以使用 [!INCLUDE[TLA2#tla_unicode](../../../../includes/tla2sharptla-unicode-md.md)] 编码来处理大型标志符号集。  这种编码享有广泛的国际支持，并支持版式变体标志符号。  
  
 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 文本呈现使用 [!INCLUDE[TLA#tla_ct](../../../../includes/tlasharptla-ct-md.md)] 子像素技术，该技术支持分辨率独立性。  这极大地提高了可读性，并为所有脚本提供了支持高质量杂志样式文档的功能。  
  
<a name="intl_layout"></a>   
### 国际化布局  
 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 提供了一种支持水平、双向和垂直布局的简便方式。  在演示框架中，<xref:System.Windows.FrameworkElement.FlowDirection%2A> 属性可以用来定义布局。  流方向模式包括：  
  
-   *LeftToRight* \- 适用于拉丁语和东亚语言等语言的水平布局。  
  
-   *RightToLeft* \- 适用于阿拉伯语和希伯来语等语言的双向布局。  
  
<a name="developing_localizable_apps"></a>   
## 开发可本地化的应用程序  
 在编写全球使用的应用程序时，应牢记应用程序必须可本地化。  以下主题指出了若干注意事项。  
  
<a name="mui"></a>   
### 多语言用户界面  
 多语言用户界面 \(MUI\) 是由 [!INCLUDE[TLA#tla_ms](../../../../includes/tlasharptla-ms-md.md)] 提供的对在不同语言之间切换 [!INCLUDE[TLA2#tla_ui#plural](../../../../includes/tla2sharptla-uisharpplural-md.md)] 的支持。  [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 应用程序使用程序集模型来支持 MUI。  一个应用程序包含非特定语言程序集和与语言相关的附属资源程序集。  入口点是主程序集中的托管 .EXE。  [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 资源加载程序采用 [!INCLUDE[TLA2#tla_netframewk](../../../../includes/tla2sharptla-netframewk-md.md)] 的资源管理器来支持资源查找和回退。  多个语言附属程序集可同时与同一主程序集一起工作。  加载的资源程序集取决于当前线程的 <xref:System.Globalization.CultureInfo.CurrentUICulture%2A>。  
  
<a name="localizable_ui"></a>   
### 可本地化的用户界面  
 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 应用程序使用 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] 定义其 [!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)]。  [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] 使开发人员可以使用一组属性和逻辑指定对象的层次结构。  [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] 主要用于开发 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 应用程序，但也可用于指定任何[!INCLUDE[TLA#tla_clr](../../../../includes/tlasharptla-clr-md.md)] 对象的层次结构。  大多数开发人员使用 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] 指定其应用程序 [!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)]，并使用诸如的 [!INCLUDE[TLA#tla_cshrp](../../../../includes/tlasharptla-cshrp-md.md)] 的编程语言响应用户交互。  
  
 从资源方面来看，为描述与语言相关的 [!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)] 而专门设计的 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] 文件属于资源元素范畴，因此，其最终分发格式必须可本地化，以支持国际语言。  由于 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] 无法处理事件，因此，许多 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] 应用程序都包含用于执行此操作的代码块。  有关更多信息，请参见 [XAML 概述 \(WPF\)](../../../../docs/framework/wpf/advanced/xaml-overview-wpf.md)。  将 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] 文件标记为 XAML 的 BAML 形式时，会剥除代码并将其编译为不同的二进制文件。XAML 的 BAML 形式文件、图像以及其他类型的托管资源对象将被嵌入到附属资源程序集中（该程序集可以本地化为其他语言），如果不需要进行本地化，以上各项将被嵌入到主程序集中。  
  
> [!NOTE]
>  [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 应用程序支持所有 [!INCLUDE[TLA2#tla_netframewk](../../../../includes/tla2sharptla-netframewk-md.md)] [!INCLUDE[TLA2#tla_clr](../../../../includes/tla2sharptla-clr-md.md)] 资源（包括字符串表、图像等）。  
  
<a name="building_localizable_apps"></a>   
### 生成可本地化的应用程序  
 本地化意味着根据不同的区域性对 [!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)] 进行改编。  若要使 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 应用程序可本地化，开发人员需要将所有可本地化的资源生成为一个资源程序集。  该资源程序集本地化为不同语言，代码隐藏功能使用资源管理 [!INCLUDE[TLA#tla_api](../../../../includes/tlasharptla-api-md.md)] 来进行加载。  [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 应用程序所需的文件之一是项目文件 \(.proj\)。  您在应用程序中使用的所有资源都应包括在项目文件中。  下面的 .csproj 文件示例演示如何执行此操作。  
  
```  
<Resource Include="data\picture1.jpg"/>  
<EmbeddedResource Include="data\stringtable.en-US.restext"/>  
```  
  
 若要使用应用程序中的资源，请实例化一个 <xref:System.Resources.ResourceManager> 并加载要使用的资源。  下面的示例演示如何执行此操作。  
  
 [!code-csharp[LocalizationResources#2](../../../../samples/snippets/csharp/VS_Snippets_Wpf/LocalizationResources/CSharp/page1.xaml.cs#2)]  
  
<a name="using_clickonce"></a>   
## 在已本地化的应用程序中使用 ClickOnce  
 ClickOnce 是 [!INCLUDE[TLA#tla_visualstu2005](../../../../includes/tlasharptla-visualstu2005-md.md)] 附带的新 Windows 窗体部署技术。  通过该技术可以进行应用程序安装和 Web 应用程序升级。  对使用 ClickOnce 部署的应用程序进行本地化之后，只能在本地化的区域性中查看该应用程序。  例如，如果将已部署的应用程序本地化为日语，则只能在日语版的 [!INCLUDE[TLA#tla_win](../../../../includes/tlasharptla-win-md.md)] 上查看该应用程序，而不能在英语版的 [!INCLUDE[TLA2#tla_win](../../../../includes/tla2sharptla-win-md.md)] 上查看。  由于日语用户经常运行英语版本的 [!INCLUDE[TLA2#tla_win](../../../../includes/tla2sharptla-win-md.md)]，因此这常常会出现问题。  
  
 该问题的解决方案是设置非特定语言回退特性。  应用程序开发人员可以选择从主程序集中移除资源，并指定可在特定区域性对应的附属程序集中找到该资源。  若要控制此过程，请使用 <xref:System.Resources.NeutralResourcesLanguageAttribute>。  <xref:System.Resources.NeutralResourcesLanguageAttribute> 类的构造函数包含两个签名，其中一个签名使用 <xref:System.Resources.UltimateResourceFallbackLocation> 参数指定 <xref:System.Resources.ResourceManager> 应在主程序集还是附属程序集中提取回退资源。  下面的示例演示如何使用此特性。  对于最终回退位置，该代码将导致 <xref:System.Resources.ResourceManager> 在当前执行程序集的目录的“de”子目录中查找资源。  
  
```  
[assembly: NeutralResourcesLanguageAttribute(  
    "de" , UltimateResourceFallbackLocation.Satellite)]  
  
```  
  
## 请参阅  
 [WPF 全球化和本地化概述](../../../../docs/framework/wpf/advanced/wpf-globalization-and-localization-overview.md)