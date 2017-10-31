---
title: "x:Key Directive | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-wpf"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "xKey"
  - "Key"
  - "x:Key"
helpviewer_keywords: 
  - "x:Key attribute [XAML Services]"
  - "Key attribute in XAML [XAML Services]"
  - "XAML [XAML Services], x:Key attribute"
ms.assetid: 1985cd45-f197-42d5-b75e-886add64b248
caps.latest.revision: 25
author: "wadepickett"
ms.author: "wpickett"
manager: "wpickett"
caps.handback.revision: 25
---
# x:Key Directive
唯一地标识在 XAML 定义的字典中创建和引用的元素。  将 `x:Key` 值添加到 XAML 对象元素是标识资源字典（如 WPF <xref:System.Windows.ResourceDictionary>）中资源的最常用的方法。  
  
## XAML 属性用法  
  
```  
<object x:Key="stringKeyValue".../>  
-or-  
<object x:Key="{markupExtensionUsage}".../>  
```  
  
## XAML 特性用法（特定于 WPF）  
  
```  
<object.Resources>  
  <object x:Key="stringKeyValue".../>  
</object.Resources>  
-or-  
<object.Resources>  
  <object x:Key="{markupExtensionUsage}".../>  
</object.Resources>  
```  
  
## XAML 值  
  
|||  
|-|-|  
|`stringKeyValue`|要用作键的文本字符串。  文本字符串必须符合 [XamlName 语法](../../../docs/framework/xaml-services/xamlname-grammar.md)。|  
|`markupExtensionUsage`|在标记扩展分隔符 {} 中，标记扩展用法提供对象以用作键。  请参见“备注”。|  
  
## 备注  
 `x:Key` 支持 XAML 资源字典概念。  作为语言的 XAML 不定义资源字典实现，而是由具体的 UI 框架定义。  若要了解有关 XAML 资源字典如何在 WPF 中实现的更多信息，请参见 [XAML 资源](../../../ocs/framework/wpf/advanced/xaml-resources.md)。  
  
 在 XAML 2006 和 WPF 中，必须以特性形式提供 `x:Key`。  您仍可以使用非字符串键，但这需要标记扩展用法来提供特性窗体中的非字符串值。  如果使用 XAML 2009，则 `x:Key` 可以被指定为显式支持以对象类型而不是字符串为键的词典而不需要标记扩展中间语言。  请参见本主题中的“XAML 2009”一节。  备注部分的剩余部分专门应用于 XAML 2006 实现。  
  
 `x:Key` 的特性值可以是在 [XamlName 语法](../../../docs/framework/xaml-services/xamlname-grammar.md)中定义的任何字符串，也可以是通过标记扩展计算的对象。  有关来自 WPF 的示例，请参见“WPF 用法说明”。  
  
 作为 <xref:System.Collections.IDictionary> 实现的父元素的子元素通常必须包括一个 `x:Key` 特性，用来指定该字典中的唯一键值。  Frameworks 可以实现具有别名的键属性，以替换特定类型中的 `x:Key`；定义此类属性的类型应使用 <xref:System.Windows.Markup.DictionaryKeyPropertyAttribute> 进行特性化。  
  
 与指定 `x:Key` 等效的代码是用于基础 <xref:System.Collections.IDictionary> 的键。  例如，当您向代码中的 WPF <xref:System.Windows.ResourceDictionary> 添加资源时，应用于 WPF 中的资源的标记中的 `x:Key` 等效于 <xref:System.Windows.ResourceDictionary.Add%2A?displayProperty=fullName> 的 `key` 参数值。  
  
## WPF 用法说明  
 作为 <xref:System.Collections.IDictionary> 实现（如 WPF <xref:System.Windows.ResourceDictionary>）的父对象的子对象通常必须包括一个 `x:Key` 特性，并且该字典中的键值必须唯一。  有两种值得注意的例外情况：  
  
-   某些 WPF 类型声明一个隐式的字典使用键。  例如，具有 <xref:System.Windows.Style.TargetType%2A> 的 <xref:System.Windows.Style> 或具有 <xref:System.Windows.DataTemplate.DataType%2A> 的 <xref:System.Windows.DataTemplate> 可以放置在 <xref:System.Windows.ResourceDictionary> 中，并使用隐式键。  
  
-   WPF 支持一个合并的资源字典概念。  键可在合并的字典之间共享，并且共享的键行为可以使用 <xref:System.Windows.FrameworkContentElement.FindResource%2A> 进行访问。  有关详细信息，请参阅 [合并资源字典](../../../ocs/framework/wpf/advanced/merged-resource-dictionaries.md)。  
  
 在整个 WPF XAML 实现和应用程序模型中，XAML 标记编译器不会检测密钥的唯一性。  相反，丢失或非唯一的 `x:Key` 值导致加载时 XAML 分析程序错误。  但是，WPF 的 [!INCLUDE[vs_current_short](../../../includes/vs-current-short-md.md)] 词典处理常常可以在设计阶段记下那些错误。  
  
 请注意，在所显示的语法中，<xref:System.Windows.ResourceDictionary> 对象在 WPF XAML 处理器生成一个集合来填充 <xref:System.Windows.FrameworkElement.Resources%2A> 集合的方式上是隐式的。  <xref:System.Windows.ResourceDictionary> 在标记中通常不以显式方式作为元素提供，尽管在某些情况下为了清楚起见希望这样做（此时它将充当 <xref:System.Windows.FrameworkElement.Resources%2A> 属性元素和其中填充字典的项之间的集合对象元素）。  关于集合对象在标记中几乎始终为隐式元素的原因的信息，请参见 [XAML 语法详述](../../../ocs/framework/wpf/advanced/xaml-syntax-in-detail.md)。  
  
 在 WPF XAML 实现中，资源字典键的处理由 <xref:System.Windows.ResourceKey> 抽象类定义。  但是，WPF XAML 处理器会基于键的用法为键生成不同的基础扩展类型。  例如，<xref:System.Windows.DataTemplate> 或任何派生类的键是单独处理的，并生成一个不同的 <xref:System.Windows.DataTemplateKey> 对象。  
  
 键和名称在基本 XAML 定义中使用不同的指令和语言元素（`x:Key` 与 `x:Name`）。  键和名称还可通过 WPF 定义和应用这些概念在不同的情况中使用。  有关详细信息，请参见[WPF XAML 名称范围](../../../ocs/framework/wpf/advanced/wpf-xaml-namescopes.md)。  
  
 如前所述，键值可以是通过标记扩展提供的值，也可以是字符串值以外的值。  WPF 方案的一个示例为 `x:Key` 的值可以是 [ComponentResourceKey](../../../ocs/framework/wpf/advanced/componentresourcekey-markup-extension.md)。  某些控件公开该类型的自定义样式资源的样式键，这些资源会影响该控件的外观和行为，而不是替换整个控件的样式。  <xref:System.Windows.Controls.ToolBar.ButtonStyleKey%2A> 就是这样的一个键。  
  
 WPF 合并的词典功能引入了关于键唯一性和键查找行为的其他注意事项。  有关详细信息，请参阅 [合并资源字典](../../../ocs/framework/wpf/advanced/merged-resource-dictionaries.md)。  
  
## XAML 2009  
 XAML 2009 解除 `x:Key` 始终以特性形式提供的限制。  
  
 在 WPF 中，可以使用 XAML 2009 功能，但仅针对未进行标记编译的 XAML。  WPF 的已编译标记的 XAML 以及 XAML 的 BAML 形式当前不支持 XAML 2009 关键字和功能。  
  
 在 XAML 2009 下，您可以通过下面的用法指定 `x:Key` 元素：  
  
### XAML 元素使用情况（仅限于 XAML 2009）  
  
```  
<object>  
  <x:Key>  
     keyObject  
  </x:Key>  
...  
</object>  
```  
  
### XAML 值  
  
|||  
|-|-|  
|`keyObject`|在专用字典中用作给定 `object` 的键的对象的对象元素。|  
  
-   这种类型的用法的容器\/父级不会在此处显示。  `object` 应为某种表示专用的词典实现的对象元素的子级。  `keyObject` 应为对象实例（或值类型的值），适合用作该特定专用的词典实现的关键字。  
  
-   WPF 不实现要求此用法的词典。  对象键是 XAML 语言的常规功能。对于某些要在 XAML 中创建词典的自定义词典方案而言，该功能很有用。  隐式样式等 WPF 功能会将非字符串键用于资源，将其他技术用于建立或指定键存在性，所以没必要使用对象键。  
  
-   在对象元素窗体中，*keyObject* 还可以是标记扩展用法，而不是直接对象实例。  
  
## Silverlight Usage 备注。  
 单独说明了 `x:Key` for Silverlight。  有关详情，请参阅 [XAML 命名空间 \(x:\) 语言功能 \(Silverlight\)](http://go.microsoft.com/fwlink/?LinkId=199081)。  
  
## 请参阅  
 [XAML 资源](../../../ocs/framework/wpf/advanced/xaml-resources.md)   
 [资源和代码](../../../ocs/framework/wpf/advanced/resources-and-code.md)   
 [StaticResource 标记扩展](../../../ocs/framework/wpf/advanced/staticresource-markup-extension.md)