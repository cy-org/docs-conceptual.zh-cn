---
title: "绑定声明概述 | Microsoft Docs"
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
  - "绑定数据, 声明"
  - "绑定声明"
  - "Data Binding — 数据绑定, 声明"
  - "标记扩展"
  - "对象元素语法"
  - "语法, 对象元素"
ms.assetid: b97fd626-4c0d-4761-872a-2bca5820da2c
caps.latest.revision: 34
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 33
---
# 绑定声明概述
本主题讨论声明绑定的不同方法。  
  
   
  
<a name="Prereq"></a>   
## 必备组件  
 在阅读本主题之前，应当先熟悉标记扩展的概念和使用，这一点非常重要。  有关标记扩展的更多信息，请参见[标记扩展和 WPF XAML](../../../../docs/framework/wpf/advanced/markup-extensions-and-wpf-xaml.md)。  
  
 本主题不介绍数据绑定的概念。  有关数据绑定概念的讨论，请参见[数据绑定概述](../../../../docs/framework/wpf/data/data-binding-overview.md)。  
  
<a name="BindinginXAML"></a>   
## 在 XAML 中声明绑定  
 本节讨论如何在 XAML 中声明绑定。  
  
<a name="MarkupExtensionSyntax"></a>   
### 标记扩展使用  
 <xref:System.Windows.Data.Binding> 是标记扩展。  当您使用绑定扩展来声明绑定时，声明包含一系列子句，这些子句跟在 `Binding` 关键字后面，并由逗号 \(,\) 分隔。  绑定声明中的子句可以按任意顺序排列，因此有许多可能的组合。  子句是*名称*\=*值* 对，其中*名称* 是 <xref:System.Windows.Data.Binding> 属性，*值* 是您要为该属性设置的值。  
  
 当在标记中创建绑定声明字符串时，必须将它们附加到目标对象的特定[依赖项属性](GTMT)。  下面的示例演示如何通过使用绑定扩展并指定 <xref:System.Windows.Data.Binding.Source%2A> 和 <xref:System.Windows.Data.Binding.Path%2A> 属性来绑定 <xref:System.Windows.Controls.TextBox.Text%2A?displayProperty=fullName> 属性。  
  
 [!code-xml[SimpleBinding#BDO1](../../../../samples/snippets/csharp/VS_Snippets_Wpf/SimpleBinding/CSharp/Page1.xaml#bdo1)]  
  
 您可以通过这种方法来指定 <xref:System.Windows.Data.Binding> 类的大部分属性。  有关绑定扩展的更多信息，以及不能使用绑定扩展设置的 <xref:System.Windows.Data.Binding> 属性的列表，请参见 [绑定标记扩展](../../../../docs/framework/wpf/advanced/binding-markup-extension.md)概述。  
  
<a name="ObjectElementSyntax"></a>   
### 对象元素语法  
 对象元素语法是创建绑定声明的另一种方法。  在大多数情况下，使用标记扩展或对象元素语法没有特定的优势。  但是，在标记扩展不支持您的方案的情况下，例如，当您的属性值是不存在类型转换的非字符串类型时，您将需要使用对象元素语法。  
  
 下面是对象元素语法和标记扩展使用的一个示例：  
  
 [!code-xml[BindConversionMarkup#1](../../../../samples/snippets/csharp/VS_Snippets_Wpf/BindConversionMarkup/CSharp/Page1.xaml#1)]  
  
 此示例通过使用扩展语法声明绑定来绑定 <xref:System.Windows.Controls.TextBlock.Foreground%2A> 属性。  <xref:System.Windows.Controls.TextBlock.Text%2A> 属性的绑定声明使用对象元素语法。  
  
 有关不同术语的更多信息，请参见 [XAML 语法详述](../../../../docs/framework/wpf/advanced/xaml-syntax-in-detail.md)。  
  
<a name="MBandPB"></a>   
### MultiBinding 和 PriorityBinding  
 <xref:System.Windows.Data.MultiBinding> 和 <xref:System.Windows.Data.PriorityBinding> 不支持 XAML 扩展语法。  因此，如果要在 XAML 中声明 <xref:System.Windows.Data.MultiBinding> 或 <xref:System.Windows.Data.PriorityBinding>，则必须使用对象元素语法。  
  
<a name="BindinginCode"></a>   
## 在代码中创建绑定  
 指定绑定的另一种方法是在代码中直接为 <xref:System.Windows.Data.Binding> 对象设置属性。  下面的示例演示如何在代码中创建 <xref:System.Windows.Data.Binding> 对象并指定属性。  在此示例中，`TheConverter` 是实现 <xref:System.Windows.Data.IValueConverter> 接口的对象。  
  
 [!code-csharp[BindConversion#1](../../../../samples/snippets/csharp/VS_Snippets_Wpf/BindConversion/CSharp/Window1.xaml.cs#1)]
 [!code-vb[BindConversion#1](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/BindConversion/visualbasic/window1.xaml.vb#1)]  
[!code-csharp[BindConversion#end1](../../../../samples/snippets/csharp/VS_Snippets_Wpf/BindConversion/CSharp/Window1.xaml.cs#end1)]
[!code-vb[BindConversion#end1](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/BindConversion/visualbasic/window1.xaml.vb#end1)]  
  
 如果您要绑定的对象是 <xref:System.Windows.FrameworkElement> 或 <xref:System.Windows.FrameworkContentElement>，则您可以直接对该对象调用 `SetBinding` 方法，而不是使用 <xref:System.Windows.Data.BindingOperations.SetBinding%2A?displayProperty=fullName>。  有关示例，请参见[在代码中创建绑定](../../../../docs/framework/wpf/data/how-to-create-a-binding-in-code.md)。  
  
<a name="Path_Syntax"></a>   
## 绑定路径语法  
 使用 <xref:System.Windows.Data.Binding.Path%2A> 属性可以指定您要绑定到的源值：  
  
-   在最简单的情况下，<xref:System.Windows.Data.Binding.Path%2A> 属性值是要用于绑定的源对象的属性名，如 `Path=PropertyName`。  
  
-   在 [!INCLUDE[TLA#tla_cshrp](../../../../includes/tlasharptla-cshrp-md.md)] 中可以通过类似语法指定属性的子属性。  例如，子句 `Path=ShoppingCart.Order` 设置与对象或属性 `ShoppingCart` 的 `Order` 子属性的绑定。  
  
-   若要绑定到[附加属性](GTMT)，应在[附加属性](GTMT)周围放置圆括号。  例如，若要绑定到[附加属性](GTMT) <xref:System.Windows.Controls.DockPanel.Dock%2A?displayProperty=fullName>，则语法是 `Path=(DockPanel.Dock)`。  
  
-   可以在要应用索引器的属性名后面的方括号内指定属性的索引器。  例如，子句 `Path=ShoppingCart[0]` 将绑定设置为与属性的内部索引处理文本字符串“0”的方式对应的索引。  还支持嵌套的索引器。  
  
-   可以在 `Path` 子句中混合索引器和子属性；例如，`Path=ShoppingCart.ShippingInfo[MailingAddress,Street].`  
  
-   在索引器内部，您可以有多个由逗号 \(,\) 分隔的索引器参数。  可以使用圆括号指定每个参数的类型。  例如，您可以有 `Path="[(sys:Int32)42,(sys:Int32)24]"`，其中 `sys` 映射到 `System` 命名空间。  
  
-   如果源为集合视图，则可以用斜杠 \(\/\) 指定当前项。  例如，子句 `Path=/` 用于设置到视图中当前项的绑定。  如果源为集合，则此语法指定默认集合视图的当前项。  
  
-   可以结合使用属性名和斜杠来遍历作为集合的属性。  例如，`Path=/Offices/ManagerName` 指定源集合的当前项，该源集合包含也作为集合的 `Offices` 属性。  其当前项是一个包含 `ManagerName` 属性的对象。  
  
-   也可以使用句点 \(.\) 路径绑定到当前源。  例如，`Text="{Binding}"` 等效于 `Text="{Binding Path=.}"`。  
  
### 转义机制  
  
-   在索引器 \(\[ \]\) 内部，插入符号 \(^\) 用于对下一个字符进行转义。  
  
-   如果在 XAML 中设置 <xref:System.Windows.Data.Binding.Path%2A>，则还需要使用 XML 实体对 XML 语言定义专用的某些字符进行转义：  
  
    -   使用 `&` 对字符“&”进行转义。  
  
    -   使用 `>` 对结束标记“\>”进行转义。  
  
-   此外，如果您使用标记扩展语法描述特性中的整个绑定，则需要使用反斜杠 \\ 对 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 标记扩展分析程序专用的字符进行转义：  
  
    -   反斜杠 \\ 本身是转义字符。  
  
    -   等号 \(\=\) 将属性名与属性值隔开。  
  
    -   逗号 \(,\) 用于分隔属性。  
  
    -   右大括号 \(}\) 是标记扩展的结尾。  
  
<a name="Default"></a>   
## 默认行为  
 如果未在声明中指定默认行为，则默认行为如下。  
  
-   创建一个尝试在[绑定源](GTMT)值与[绑定目标](GTMT)值之间执行类型转换的默认转换器。  如果无法进行转换，则默认转换器会返回 `null`。  
  
-   如果您不设置 <xref:System.Windows.Data.Binding.ConverterCulture%2A>，则绑定引擎会使用[绑定目标](GTMT)对象的 `Language` 属性。  在 XAML 中，此属性默认为“en\-US”，如果已显式设置了一个值，则从页面的根元素（或任何元素）继承该值。  
  
-   只要绑定已有数据上下文（例如，来自父元素的继承数据上下文），并且该上下文所返回的项或集合适合于绑定，而不需要进一步的路径修改，则绑定声明可以不必有任何子句：`{Binding}`。在绑定作用于集合的情况下，这通常是为数据样式指定绑定的方式。  有关更多信息，请参见[绑定源概述](../../../../docs/framework/wpf/data/binding-sources-overview.md)中的“整个对象用作绑定源”一节。  
  
-   默认 <xref:System.Windows.Data.Binding.Mode%2A> 可能是单向，也可能是双向，具体取决于所绑定的[依赖项属性](GTMT)。  您始终可以显式声明绑定模式，以确保绑定具有所需的行为。  通常，用户可编辑的控件属性（如 <xref:System.Windows.Controls.TextBox.Text%2A?displayProperty=fullName> 和 <xref:System.Windows.Controls.Primitives.RangeBase.Value%2A?displayProperty=fullName>）默认为双向绑定，而其他大多数属性默认为单向绑定。  
  
-   默认 <xref:System.Windows.Data.Binding.UpdateSourceTrigger%2A> 值可能是 <xref:System.Windows.Data.UpdateSourceTrigger>，也可能是 <xref:System.Windows.Data.UpdateSourceTrigger>，具体也取决于所绑定的[依赖项属性](GTMT)。  多数[依赖项属性](GTMT)的默认值为 <xref:System.Windows.Data.UpdateSourceTrigger>，而 <xref:System.Windows.Controls.TextBox.Text%2A?displayProperty=fullName> 属性的默认值为 <xref:System.Windows.Data.UpdateSourceTrigger>。  
  
## 请参阅  
 [数据绑定概述](../../../../docs/framework/wpf/data/data-binding-overview.md)   
 [帮助主题](../../../../docs/framework/wpf/data/data-binding-how-to-topics.md)   
 [数据绑定](../../../../docs/framework/wpf/advanced/optimizing-performance-data-binding.md)   
 [PropertyPath XAML 语法](../../../../docs/framework/wpf/advanced/propertypath-xaml-syntax.md)