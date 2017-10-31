---
title: "PropertyPath XAML 语法 | Microsoft Docs"
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
  - "PropertyPath 对象"
  - "XAML, PropertyPath 对象"
ms.assetid: 0e3cdf07-abe6-460a-a9af-3764b4fd707f
caps.latest.revision: 24
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 22
---
# PropertyPath XAML 语法
<xref:System.Windows.PropertyPath> 对象支持复杂内联 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] 语法以设置将 <xref:System.Windows.PropertyPath> 类型作为其值的各种属性。  本主题讨论应用于绑定的 <xref:System.Windows.PropertyPath> 语法和动画语法。  
  
   
  
<a name="where"></a>   
## PropertyPath 的使用场合  
 <xref:System.Windows.PropertyPath> 是在一些 [!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)] 功能中使用的通用对象。  尽管使用此通用 <xref:System.Windows.PropertyPath> 可以传输属性路径信息，但是将 <xref:System.Windows.PropertyPath> 用作类型的每个功能区域的用法却各不相同。  因此，基于每个功能来讨论语法更实际一些。  
  
 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 主要使用 <xref:System.Windows.PropertyPath> 来描述用于传递对象数据源属性的对象模型路径，以及目标动画的目标路径。  
  
 某些样式和模板属性，例如 <xref:System.Windows.Setter.Property%2A?displayProperty=fullName> 采用貌似 <xref:System.Windows.PropertyPath> 的限定属性名。  但是，这不是真实的 <xref:System.Windows.PropertyPath>，而是由 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] 处理器与 <xref:System.Windows.DependencyProperty> 的类型转换器联合启用的限定 *owner.property* 字符串格式用法。  
  
<a name="databinding_s"></a>   
## 数据绑定中对象的 PropertyPath  
 数据绑定是 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 功能，借此您可以绑定到任意[依赖项属性](GTMT)的目标值。  但是，这样的数据绑定源不需要是[依赖项属性](GTMT)，它可以是适用数据提供程序能识别的任意属性类型。  属性路径专用于 <xref:System.Windows.Data.ObjectDataProvider>，它用于从[!INCLUDE[TLA#tla_clr](../../../../includes/tlasharptla-clr-md.md)] 对象及其属性获取绑定源。  
  
 请注意，数据绑定到 [!INCLUDE[TLA#tla_xml](../../../../includes/tlasharptla-xml-md.md)] 不会使用 <xref:System.Windows.PropertyPath>，因为它不使用 <xref:System.Windows.Data.Binding> 中的 <xref:System.Windows.Data.Binding.Path%2A>。  而是，使用 <xref:System.Windows.Data.Binding.XPath%2A> 并将有效的 XPath 语法指定到数据的 [!INCLUDE[TLA#tla_xmldom](../../../../includes/tlasharptla-xmldom-md.md)] 中。  <xref:System.Windows.Data.Binding.XPath%2A> 也被指定为字符串，但是不会在此讨论；请参见 [使用 XMLDataProvider 和 XPath 查询绑定到 XML 数据](../../../../docs/framework/wpf/data/how-to-bind-to-xml-data-using-an-xmldataprovider-and-xpath-queries.md)。  
  
 理解数据绑定中的属性路径的关键是您可以将绑定目标定为单个属性值，或者您可以绑定到采用列表或集合的目标属性。  如果要绑定集合，例如绑定将根据集合中的数据项数而展开的 <xref:System.Windows.Controls.ListBox>，则您的属性路径应引用集合对象，而不是单个集合项。  数据绑定引擎会自动将用作数据源的集合与绑定目标的类型匹配，从而导致诸如使用项数组填充 <xref:System.Windows.Controls.ListBox> 之类的行为。  
  
<a name="singlecurrent"></a>   
### 直接对象上作为数据上下文的单个属性  
  
```  
<Binding Path="propertyName" .../>  
```  
  
 *属性名称* 必须解析为 <xref:System.Windows.Data.Binding.Path%2A> 用法的当前 <xref:System.Windows.FrameworkElement.DataContext%2A> 中属性的名称。  如果绑定更新源，则属性必须为读写属性，并且源对象必须可变。  
  
<a name="singleindex"></a>   
### 直接对象上作为数据上下文的单个索引器  
  
```  
<Binding Path="[key]" .../>  
```  
  
 `key` 必须为字典或哈希表的键入索引，或者为数组的整数索引。  同时，键值必须为可直接绑定到所应用属性的类型。  例如，包含字符串键和字符串值的哈希表可以使用这种方式绑定到 <xref:System.Windows.Controls.TextBox> 的文本。  或者，如果键指向集合或子索引，则您可以使用此语法绑定到目标集合属性。  否则，您需要通过类似于 `<Binding Path="[``key``].``propertyName``" .../>` 的语法来引用特定属性。  
  
 如果需要，可以指定索引的类型。  有关索引属性路径方面的详细信息，请参见 <xref:System.Windows.Data.Binding.Path%2A?displayProperty=fullName>。  
  
<a name="multipleindirect"></a>   
### 多个属性（间接确定属性目标）  
  
```  
<Binding Path="propertyName.propertyName2" .../>  
```  
  
 `propertyName` 必须解析为作为当前 <xref:System.Windows.FrameworkElement.DataContext%2A> 的属性的名称。  路径属性 `propertyName` 和 `propertyName2` 可以是关系中的任意属性，其中 `propertyName2` 是存在于作为 `propertyName` 值的类型中的属性。  
  
<a name="singleattached"></a>   
### 附加的或其他类型限定的单个属性  
  
```  
<object property="(ownerType.propertyName)" .../>  
```  
  
 括号表示 <xref:System.Windows.PropertyPath> 中的此属性应该使用部分限定来构建。  它可以使用 XML 命名空间来查找具有适当的映射的类型。  `ownerType` 通过每个程序集中的 <xref:System.Windows.Markup.XmlnsDefinitionAttribute> 声明来搜索 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] 处理器有权访问的类型。  大部分应用程序都具有映射到 [!INCLUDE[TLA#tla_wpfxmlnsv1](../../../../includes/tlasharptla-wpfxmlnsv1-md.md)] 命名空间的默认 XML 命名空间，因此通常只有自定义类型或该命名空间之外的类型才需要前缀。   `propertyName` 必须解析为 `ownerType` 中存在的属性的名称。  此语法一般用于下列情况之一：  
  
-   路径是在 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] 中的样式或模板（该样式或模板没有指定的目标类型）中指定的。  除此之外，限定用法一般无效，因为在非样式、非模式情况下，属性存在于实例中，而不是类型中。  
  
-   属性为附加属性。  
  
-   您要绑定到静态属性。  
  
 当用作演示图板目标时，指定为 `propertyName` 的属性必须为 <xref:System.Windows.DependencyProperty>。  
  
<a name="sourcetraversal"></a>   
### 源遍历（绑定到集合的层次结构）  
  
```  
<object Path="propertyName/propertyNameX" .../>  
```  
  
 此语法中的 \/ 用于在分层数据源对象中导航，并且支持使用连续的 \/ 字符分多个步骤导航层次结构。  源遍历说明了当前记录指针位置，该位置是通过将数据与其视图的 UI 同步而确定的。  有关与分层数据源对象的绑定的详细信息，以及数据绑定中当前记录指针的概念，请参见[对分层数据使用主\-从模式](../../../../docs/framework/wpf/data/how-to-use-the-master-detail-pattern-with-hierarchical-data.md)或[数据绑定概述](../../../../docs/framework/wpf/data/data-binding-overview.md)。  
  
> [!NOTE]
>  此语法貌似 [!INCLUDE[TLA2#tla_xpath](../../../../includes/tla2sharptla-xpath-md.md)]。  绑定到 [!INCLUDE[TLA2#tla_xml](../../../../includes/tla2sharptla-xml-md.md)] 数据源的真实 [!INCLUDE[TLA2#tla_xpath](../../../../includes/tla2sharptla-xpath-md.md)] 表达式不用作 <xref:System.Windows.Data.Binding.Path%2A> 值，而应当用于相互独占的 <xref:System.Windows.Data.Binding.XPath%2A> 属性。  
  
### 集合视图  
 若要引用一个已命名的集合视图，请用哈希字符 \(`#`\) 给集合视图名称加前缀。  
  
### 当前记录指针  
 若要引用集合视图的当前记录指针或引用主从数据绑定方案，请启动带正斜杠 \(`/`\) 的路径字符串。  从当前记录指针开始遍历任何超出正斜杠的路径。  
  
### 多个索引器  
  
```  
<object Path="[index1,index2...]" .../>  
or  
<object Path="propertyName[index,index2...]" .../>  
```  
  
 如果给定的对象支持多个索引器，则可以按顺序指定这些索引器，类似于数组引用语法。  所讨论的对象可以是当前上下文，也可以是包含多索引对象的属性值。  
  
 默认情况下，通过使用基础对象的特性来键入索引器值。  如果需要，可以指定索引的类型。  有关键入索引器的详细信息，请参见 <xref:System.Windows.Data.Binding.Path%2A?displayProperty=fullName>。  
  
<a name="mixing"></a>   
### 混合语法  
 以上显示的每条语法都可以独立使用。  例如，下面的示例创建了一个属性路径，该路径指向 `ColorGrid` 属性（该属性包含 <xref:System.Windows.Media.SolidColorBrush> 对象的像素网格数组）的特定 x，y 值处的颜色：  
  
```  
<Rectangle Fill="{Binding ColorGrid[20,30].SolidColorBrushResult}" .../>  
```  
  
### 属性路径字符串的转义  
 对于某些业务对象中，您可能会遇到属性路径字符串需要转义序列以进行正确分析的情况。  因为大多数此类字符在常用于定义业务对象的语言方面具有类似的命名交互问题，因此转义需要非常少见。  
  
-   在索引器 \(\[ \]\) 内部，插入符号 \(^\) 用于对下一个字符进行转义。  
  
-   必须使用 XML 实体对 XML 语言定义专用的某些字符进行转义。  使用 `&` 对字符“&”进行转义。  使用 `>` 对结束标记“\>”进行转义。  
  
-   必须对特定于 WPF XAML 分析器行为的字符（使用反斜杠 `\`）进行转义，以处理标记扩展。  
  
    -   反斜杠 \(`\`\) 本身是转义字符。  
  
    -   等号 \(\=\) \(`=`\) 将属性名与属性值隔开。  
  
    -   逗号 \(`,`\) 用于分隔属性。  
  
    -   右大括号 \(`}`\) 是标记扩展的结尾。  
  
> [!NOTE]
>  从技术上讲，这些转义符还适用于演示图板属性路径，但您通常会遍历适用于现有 WPF 对象的对象模型，并且转义应该是不必要的。  
  
<a name="databinding_sa"></a>   
## 动画目标的 PropertyPath  
 动画目标属性必须是[依赖项属性](GTMT)，它采用 <xref:System.Windows.Freezable> 或基元类型。  不过，类型中的目标属性和最终动画属性可以存在于不同的对象中。  对于动画，属性路径用于通过遍历属性值中的对象\-属性关系，来定义命名动画目标对象的属性和预期目标动画属性之间的连接。  
  
<a name="general"></a>   
### 动画的一般对象属性注意事项  
 有关一般动画概念的更多信息，请参见[演示图板概述](../../../../docs/framework/wpf/graphics-multimedia/storyboards-overview.md)和[动画概述](../../../../docs/framework/wpf/graphics-multimedia/animation-overview.md)。  
  
 要进行动画处理的值类型或属性必须是 <xref:System.Windows.Freezable> 类型或基元。  启动路径的属性必须解析为存在于指定的 <xref:System.Windows.Media.Animation.Storyboard.TargetName%2A> 类型中的[依赖项属性](GTMT)的名称。  
  
 为了支持克隆对已冻结的 <xref:System.Windows.Freezable> 的动画处理，<xref:System.Windows.Media.Animation.Storyboard.TargetName%2A> 指定的对象必须为 <xref:System.Windows.FrameworkElement> 或 <xref:System.Windows.FrameworkContentElement> 派生类。  
  
<a name="singlestepanim"></a>   
### 目标对象上的单个属性  
  
```  
<animation Storyboard.TargetProperty="propertyName" .../>  
```  
  
 `propertyName` 必须解析为存在于指定的 <xref:System.Windows.Media.Animation.Storyboard.TargetName%2A> 类型中的[依赖项属性](GTMT)的名称。  
  
<a name="indirectanim"></a>   
### 间接确定属性目标  
  
```  
<animation Storyboard.TargetProperty="propertyName.propertyName2" .../>  
```  
  
 `propertyName` 必须为属于 <xref:System.Windows.Freezable> 值类型或基元的属性，该属性存在于指定的 <xref:System.Windows.Media.Animation.Storyboard.TargetName%2A> 类型中。  
  
 `propertyName2` 必须为[依赖项属性](GTMT)的名称，该属性存在于作为 `propertyName` 值的对象中。  换言之，`propertyName2` 必须作为依赖项属性存在于类型中，该类型为 `propertyName` <xref:System.Windows.DependencyProperty.PropertyType%2A>。  
  
 因为应用了样式和模板，所以间接确定动画的目标是必要的。  为了确定动画的目标，您需要目标对象上的 <xref:System.Windows.Media.Animation.Storyboard.TargetName%2A>，该名称是由 [x:Name](../../../../docs/framework/xaml-services/x-name-directive.md) 或 <xref:System.Windows.FrameworkElement.Name%2A> 建立的。  虽然模板和样式元素也可以有名称，但是这些名称仅在样式和模板的命名范围内有效。  （如果模板和样式与应用程序标记共享命名范围，则名称不可能是唯一的。  按字面而言，样式和模板是在实例之间共享的，并会永久保留重复名称。）因此，如果您希望进行动画处理的元素的各个属性来自某个样式或模板，则您需要从不是来自样式模板的命名元素实例开始，以样式或模板可视树作为目标，来找到您希望进行动画处理的属性。  
  
 例如，<xref:System.Windows.Controls.Panel> 的 <xref:System.Windows.Controls.Panel.Background%2A> 属性是来自主题模板的完整 <xref:System.Windows.Media.Brush>（实际上为 <xref:System.Windows.Media.SolidColorBrush>）。  若要对 <xref:System.Windows.Media.Brush> 进行完全动画处理，将需要 BrushAnimation（可能每个 <xref:System.Windows.Media.Brush> 类型都需要一个），然而没有这样的类型。  若要对 Brush 进行动画处理，请改为对特定 <xref:System.Windows.Media.Brush> 类型的属性进行动画处理。  您需要从 <xref:System.Windows.Media.SolidColorBrush> 到其 <xref:System.Windows.Media.SolidColorBrush.Color%2A>，在那里才能应用 <xref:System.Windows.Media.Animation.ColorAnimation>。  本示例的属性路径应该为 `Background.Color`。  
  
<a name="attachedanim"></a>   
### 附加属性  
  
```  
<animation Storyboard.TargetProperty="(ownerType.propertyName)" .../>  
```  
  
 括号表示 <xref:System.Windows.PropertyPath> 中的此属性应该使用部分限定来构建。  它可以使用 XML 命名空间来查找类型。  `ownerType` 通过每个程序集中的 <xref:System.Windows.Markup.XmlnsDefinitionAttribute> 声明来搜索 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] 处理器有权访问的类型。  大部分应用程序都具有映射到 [!INCLUDE[TLA#tla_wpfxmlnsv1](../../../../includes/tlasharptla-wpfxmlnsv1-md.md)] 命名空间的默认 XML 命名空间，因此通常只有自定义类型或该命名空间之外的类型才需要前缀。   `propertyName` 必须解析为 `ownerType` 中存在的属性的名称。  指定为 `propertyName` 的属性必须是 <xref:System.Windows.DependencyProperty>。  （所有 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 附加属性都实现为依赖项属性，因此该问题仅存在于自定义附加属性中。）  
  
<a name="indexanim"></a>   
### 索引器  
  
```  
<animation Storyboard.TargetProperty="propertyName.propertyName2[index].propertyName3" .../>  
```  
  
 大部分依赖项属性或 <xref:System.Windows.Freezable> 类型不支持索引器。  因此，动画路径中唯一使用索引器的地方是在用于启动命名目标上的链的属性与最终动画属性之间的中间位置。  在提供的语法中，它是 `propertyName2`。  例如，如果中间属性是属性路径（例如，`RenderTransform.Children[1].Angle`）中的集合（例如，<xref:System.Windows.Media.TransformGroup>），则可能需要使用索引器。  
  
<a name="ppincode"></a>   
## 代码中的 PropertyPath  
 <xref:System.Windows.PropertyPath> 的代码用法（包括如何构建 <xref:System.Windows.PropertyPath>）在 <xref:System.Windows.PropertyPath> 的参考主题中会进行说明。  
  
 一般而言，<xref:System.Windows.PropertyPath> 旨在使用两个不同的构造函数，一个用于绑定用法和最简单的动画用法，另一个用于复杂动画用法。  对绑定用法使用 <xref:System.Windows.PropertyPath.%23ctor%28System.Object%29> 签名，其中对象是字符串。  对一步动画路径使用 <xref:System.Windows.PropertyPath.%23ctor%28System.Object%29> 签名，其中对象是 <xref:System.Windows.DependencyProperty>。  对复杂动画使用 [PropertyPath\(String, Object\<xref:System.Windows.PropertyPath.%23ctor%28System.String%2CSystem.Object%5B%5D%29>。  后一个构造函数使用第一个参数的标记字符串，但在该标记字符串的位置填充了一个对象数组来定义属性路径关系。  
  
## 请参阅  
 <xref:System.Windows.PropertyPath>   
 [数据绑定概述](../../../../docs/framework/wpf/data/data-binding-overview.md)   
 [演示图板概述](../../../../docs/framework/wpf/graphics-multimedia/storyboards-overview.md)