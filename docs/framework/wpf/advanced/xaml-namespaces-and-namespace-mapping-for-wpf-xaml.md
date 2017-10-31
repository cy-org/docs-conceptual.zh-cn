---
title: "WPF XAML 的 XAML 命名空间和命名空间映射 | Microsoft Docs"
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
  - "程序集, 映射命名空间到"
  - "类, 映射命名空间到"
  - "自定义类, 映射命名空间到"
  - "映射命名空间"
  - "命名空间映射"
  - "命名空间"
  - "XAML, 命名空间映射"
  - "XAML, 命名空间"
ms.assetid: 5c0854e3-7470-435d-9fe2-93eec9d3634e
caps.latest.revision: 23
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 22
---
# WPF XAML 的 XAML 命名空间和命名空间映射
本主题进一步介绍 WPF XAML 文件的根标记中通常存在的两个 XAML 命名空间映射及其用途。  同时还介绍如何生成类似的映射，以便使用在您自己的代码中和\/或单独的程序集中定义的元素。  
  
   
  
## 什么是 XAML 命名空间？  
 XAML 命名空间实际上是 XML 命名空间概念的扩展。  指定 XAML 命名空间的技术依赖于 XML 命名空间语法、使用 URI 作为命名空间标识符的约定、使用前缀提供从同一标记源中引用多个命名空间的方法，诸如此类。  XML 命名空间的 XAML 定义中增加的主要概念是：XAML 命名空间既暗指标记用法的唯一性范围，也影响特定 CLR 命名空间和引用的程序集对标记实体的潜在支持方式。  后一种考虑因素也受到 XAML 架构上下文的概念的影响。  但对于 WPF 使用 XAML 命名空间的方式而言，您通常可以将 XAML 命名空间认为是默认 XAML 命名空间、XAML 语言命名空间，以及 XAML 标记直接映射到特定支持 CLR 命名空间和引用程序集的任何进一步的 XAML 命名空间。  
  
<a name="The_WPF_and_XAML_Namespace_Declarations"></a>   
## WPF 和 XAML 命名空间声明  
 在许多 XAML 文件的根标记中的命名空间声明内，您都会发现通常有两个 XML 命名空间声明。  第一个声明将整个 WPF 客户端\/框架 XAML 命名空间映射为默认命名空间：  
  
 `xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"`  
  
 第二个声明映射一个单独的 XAML 命名空间，通常将其映射到 `x:` 前缀。  
  
 `xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"`  
  
 这些声明之间的关系是：`x:` 前缀映射支持作为 XAML 语言定义一部分的内部，而 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 是一个实现，它使用 XAML 作为语言，并为 XAML 定义其对象的词汇。  由于 WPF 词汇的使用将远比 XAML 内部的使用常见得多，因此将 WPF 词汇映射为默认。  
  
 用于映射 XAML 语言内部支持的 `x:` 前缀约定后跟有项目模板、代码示例以及此 [!INCLUDE[TLA2#tla_sdk](../../../../includes/tla2sharptla-sdk-md.md)] 内的语言功能文档之后。  XAML 命名空间定义了许多常用功能，这些功能即使对于基本的 WPF 应用程序也是必需的。  例如，若要通过分部类将任何代码隐藏加入到 XAML 文件中，必须将该类命名为相关 XAML 文件的根元素中的 `x:Class` 特性。  或者，对于在 XAML 页中定义的希望作为键控资源访问的任何元素都应在相关元素上设置 `x:Key` 特性。  有关 XAML 的这些方面和其他方面的更多信息，请参见 [XAML 概述 \(WPF\)](../../../../docs/framework/wpf/advanced/xaml-overview-wpf.md)或 [XAML 语法详述](../../../../docs/framework/wpf/advanced/xaml-syntax-in-detail.md)。  
  
<a name="Mapping_To_Custom_Classes_and_Assemblies"></a>   
## 映射到自定义类和程序集  
 可以使用 `xmlns` 前缀声明中的一系列令牌将 XML 命名空间映射到程序集，这与将标准 WPF 和 XAML 内部 XAML 命名空间映射到前缀类似。  
  
 语法使用下列可能的命名标记和值：  
  
 `clr-namespace:` 在包含要作为元素公开的公共类型的程序集中声明的 CLR 命名空间。  
  
 `assembly=` 是指包含部分或全部引用的 [!INCLUDE[TLA2#tla_clr](../../../../includes/tla2sharptla-clr-md.md)] 命名空间的程序集。  此值通常只是程序集的名称，而不是路径，并且不包含扩展名（如 .exe 或 .dll）。  必须在包含要映射的 XAML 的项目文件中以项目引用形式建立该程序集的路径。  为了加入版本控制和强名称签名，`assembly` 值可以是由 <xref:System.Reflection.AssemblyName> 定义的字符串，而非简单字符串名称。  
  
 请注意，分隔 `clr-namespace` 标记和其值的字符是冒号 \(:\)，而分隔 `assembly` 标记和其值的字符是等号 \(\=\)。  这两个标记之间使用的字符是分号。  另外，不要在声明中的任何位置包含任何空白。  
  
### 基本自定义映射示例  
 以下代码定义了一个自定义类的示例：  
  
```csharp  
namespace SDKSample {  
    public class ExampleClass : ContentControl {  
        public ExampleClass() {  
        ...  
        }  
    }  
}  
```  
  
```vb  
Namespace SDKSample  
    Public Class ExampleClass  
        Inherits ContentControl  
         ...  
        Public Sub New()  
        End Sub  
    End Class  
End Namespace  
```  
  
 随后此自定义类将编译为一个库，根据项目设置（未显示）该库命名为 `SDKSampleLibrary`。  
  
 为了引用此自定义类，还需要包括此类作为当前项目的一个引用，此操作通常在 Visual Studio 中使用解决方案资源管理器 UI 完成。  
  
 现在已经有了包含类的库以及对项目设置中该库的引用，可以添加以下前缀映射作为 XAML 中根元素的一部分：  
  
 `xmlns:custom="clr-namespace:SDKSample;assembly=SDKSampleLibrary"`  
  
 综上所述，下面的 XAML 在根标记中包括自定义映射以及典型的默认映射和 x: 映射，然后使用带有前缀的引用将该 UI 中的 `ExampleClass` 实例化：  
  
```xaml  
<Page x:Class="WPFApplication1.MainPage"  
    xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"   
    xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"  
    xmlns:custom="clr-namespace:SDKSample;assembly=SDKSampleLibrary">  
  ...  
  <custom:ExampleClass/>  
...  
</Page>  
```  
  
### 映射到当前程序集  
 如果引用的 `clr-namespace` 是在引用自定义类的应用程序代码所在的程序集中定义的，则可以省略 `assembly`。  这种情况的等效语法是指定 `assembly=`，等号后不需要任何字符串标记。  
  
 如果自定义类是在同一程序集中定义的，则不能将其用作页的根元素。  不需要映射分部类；如果要在 XAML 中以元素形式引用自定义类，则只需要映射应用程序中页面的非分部类。  
  
<a name="Mapping_CLR_Namespaces_to_XML_Namespaces_in_an"></a>   
## 在程序集中将 CLR 命名空间映射为 XML 命名空间  
 WPF 定义一个 CLR 特性，XAML 处理器使用该特性将多个 CLR 命名空间映射到一个 XAML 命名空间。  <xref:System.Windows.Markup.XmlnsDefinitionAttribute> 特性放置在生成程序集的源代码中的程序集级别。  WPF 程序集源代码使用此特性将多种常见的命名空间（如 <xref:System.Windows> 和 <xref:System.Windows.Controls>）映射到 [!INCLUDE[TLA#tla_wpfxmlnsv1](../../../../includes/tlasharptla-wpfxmlnsv1-md.md)] 命名空间。  
  
 <xref:System.Windows.Markup.XmlnsDefinitionAttribute> 采用两个参数：XML\/XAML 命名空间名称和 CLR 命名空间名称。  可以存在多个 <xref:System.Windows.Markup.XmlnsDefinitionAttribute>，以便将多个 CLR 命名空间映射到同一个 XML 命名空间。  映射后，如果需要，还可以通过在分部类代码隐藏页中提供相应的 `using` 语句来引用这些命名空间的成员，而无需完全限定。  有关更多详细信息，请参见 <xref:System.Windows.Markup.XmlnsDefinitionAttribute>。  
  
## XAML 模板中的设计器命名空间和其他前缀  
 如果正在使用 WPF XAML 的开发环境和\/或设计工具，您可能会注意到 XAML 标记内有其他定义的 XAML 命名空间\/前缀。  
  
 [!INCLUDE[wpfdesigner_current_long](../../../../includes/wpfdesigner-current-long-md.md)] 使用通常映射到前缀 `d:` 的设计器命名空间。  WPF 的最新项目模板可能会预先映射此 XAML 命名空间，以支持 [!INCLUDE[wpfdesigner_current_long](../../../../includes/wpfdesigner-current-long-md.md)] 和其他设计环境之间的 XAML 交换。  此设计 XAML 命名空间用于在遍历设计器中基于 XAML 的 UI 的同时保留设计状态。  它还用于诸如 `d:IsDataSource` 等功能，这些功能在设计器中启用运行时数据源。  
  
 可能会显示为已映射的另一个前缀是 `mc:`。  `mc:` 用于保持标记兼容性，并利用不一定特定于 XAML 的标记兼容性模式。  在某种程度上，可以使用标记兼容性功能在框架之间或跨支持实现的其他边界交换 XAML、在 XAML 架构上下文之间工作、为设计器中的受限模式提供兼容性，诸如此类。  有关标记兼容性概念以及这些概念如何与 WPF 相关的更多信息，请参见[标记兼容性 \(mc:\) 语言功能](../../../../docs/framework/wpf/advanced/markup-compatibility-mc-language-features.md)。  
  
## WPF 和程序集加载  
 WPF 的 XAML 架构内容与 WPF 应用程序模型集成，而后者使用又使用 CLR 定义的 <xref:System.AppDomain> 概念。  下面的序列描述 XAML 架构上下文如何基于 <xref:System.AppDomain> 的 WPF 使用和其他因素，在运行时或设计时加载程序集或查找类型。  
  
1.  循环访问 <xref:System.AppDomain>，并从最新加载的程序集开始，查找与该名称的所有方面匹配的已加载程序集。  
  
2.  如果该名称是限定名称，则对该限定名称调用 <xref:System.Reflection.Assembly.Load%28System.String%29?displayProperty=fullName>。  
  
3.  如果限定名称的短名称 \+ 公钥令牌与从其加载标记的程序集匹配，则返回该程序集。  
  
4.  使用短名称 \+ 公钥令牌调用 <xref:System.Reflection.Assembly.Load%28System.String%29?displayProperty=fullName>。  
  
5.  如果该名称是非限定名称，则调用 <xref:System.Reflection.Assembly.LoadWithPartialName%2A?displayProperty=fullName>。  
  
 宽松 XAML 不使用步骤 3；没有从其加载的程序集。  
  
 针对 WPF 的已编译 XAML（通过 XamlBuildTask 生成）不使用来自 <xref:System.AppDomain>（步骤 1）的已加载程序集。  此外，名称在 XamlBuildTask 输出中绝不应是非限定的，因此步骤 5 不适用。  
  
 已编译 BAML（通过 PresentationBuildTask 生成）使用所有步骤，尽管 BAML 也不应包含非限定程序集名称。  
  
## 请参阅  
 [Understanding XML Namespaces](http://go.microsoft.com/fwlink/?LinkId=98069)   
 [XAML 概述 \(WPF\)](../../../../docs/framework/wpf/advanced/xaml-overview-wpf.md)