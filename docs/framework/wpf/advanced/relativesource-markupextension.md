---
title: "RelativeSource MarkupExtension | Microsoft Docs"
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
  - "RelativeSource"
helpviewer_keywords: 
  - "RelativeSource 标记扩展"
  - "XAML, RelativeSource 标记扩展"
ms.assetid: 26be4721-49b5-4717-a92e-7d54ad0d3a81
caps.latest.revision: 18
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 18
---
# RelativeSource MarkupExtension
指定一个 <xref:System.Windows.Data.RelativeSource> 绑定源的属性，以便在 [绑定标记扩展](../../../../docs/framework/wpf/advanced/binding-markup-extension.md) 中使用，或在设置 XAML 中创建的 <xref:System.Windows.Data.Binding> 元素的 <xref:System.Windows.Data.Binding.RelativeSource%2A> 属性时使用。  
  
## XAML 属性用法  
  
```  
<Binding RelativeSource="{RelativeSource modeEnumValue}" .../>  
```  
  
## XAML 属性用法（嵌套在 Binding 扩展内）  
  
```  
<object property="{Binding RelativeSource={RelativeSource modeEnumValue} ...}" .../>  
```  
  
## XAML 对象元素用法  
  
```  
<Binding>  
  <Binding.RelativeSource>  
    <RelativeSource Mode="modeEnumValue"/>  
  </Binding.RelativeSource>  
</Binding>  
- or   
<Binding>  
  <Binding.RelativeSource>  
    <RelativeSource  
      Mode="FindAncestor"  
      AncestorType="{x:Type typeName}"  
      AncestorLevel="intLevel"  
    />  
  </Binding.RelativeSource>  
</Binding>  
```  
  
## XAML 值  
  
|||  
|-|-|  
|`modeEnumValue`|以下项之一：<br /><br /> -   字符串标记 `Self`；对应于通过将 <xref:System.Windows.Data.RelativeSource.Mode%2A> 属性设置为 <xref:System.Windows.Data.RelativeSourceMode> 而创建的 <xref:System.Windows.Data.RelativeSource>。<br />-   字符串标记 `TemplatedParent`；对应于通过将 <xref:System.Windows.Data.RelativeSource.Mode%2A> 属性设置为 <xref:System.Windows.Data.RelativeSourceMode> 而创建的 <xref:System.Windows.Data.RelativeSource>。<br />-   字符串标记 `PreviousData`；对应于通过将 <xref:System.Windows.Data.RelativeSource.Mode%2A> 属性设置为 <xref:System.Windows.Data.RelativeSourceMode> 而创建的 <xref:System.Windows.Data.RelativeSource>。<br />-   有关 `FindAncestor` 模式的信息，请参阅下文。|  
|`FindAncestor`|字符串标记 `FindAncestor`。  使用此标记可输入一个模式，以便 `RelativeSource` 指定上级类型和可选的上级级别。  它对应于通过将 <xref:System.Windows.Data.RelativeSource.Mode%2A> 属性设置为 <xref:System.Windows.Data.RelativeSourceMode> 而创建的 <xref:System.Windows.Data.RelativeSource>。|  
|`typeName`|对于 `FindAncestor` 模式是必需的。  类型的名称，用于填充 <xref:System.Windows.Data.RelativeSource.AncestorType%2A> 属性。|  
|`intLevel`|对于 `FindAncestor` 模式是可选的。  上级级别（在逻辑树中向父级方向计算）。|  
  
## 备注  
 `{RelativeSource TemplatedParent}` 绑定用法是解析分离控件的用户界面和控件的逻辑这一大概念的关键方法。  这可以实现从模板定义内绑定到模板化父级（在其中应用模板的运行时对象实例）。  这种情况下，[TemplateBinding 标记扩展](../../../../docs/framework/wpf/advanced/templatebinding-markup-extension.md) 其实是以下绑定表达式的简写：`{Binding RelativeSource={RelativeSource TemplatedParent}}`。  `TemplateBinding` 或 `{RelativeSource TemplatedParent}` 用法仅在用于定义模板的 XAML 内部适用。  有关详细信息，请参阅 [TemplateBinding 标记扩展](../../../../docs/framework/wpf/advanced/templatebinding-markup-extension.md)。  
  
 `{RelativeSource FindAncestor}` 主要用于控件模板或可预测的自包含 UI 组合，在此情况下，控件应该始终位于某个上级类型的可视化树中。  例如，项控件的项可能使用 `FindAncestor` 用法绑定到其项控件父级\/祖先级。  或者，属于模板中控件组合一部分的元素可使用 `FindAncestor` 绑定到同一组合结构中的父元素。  
  
 在 XAML 语法章节显示的 `FindAncestor` 模式的对象元素语法中，第二个对象元素语法专门用于 `FindAncestor` 模式。  `FindAncestor` 模式需要 <xref:System.Windows.Data.RelativeSource.AncestorType%2A> 值。  你必须使用要查找的上级类型的 [x:Type 标记扩展](../../../../docs/framework/xaml-services/x-type-markup-extension.md) 引用，将 <xref:System.Windows.Data.RelativeSource.AncestorType%2A> 设置为一个特性。  当在运行时处理绑定请求时，将会用到 <xref:System.Windows.Data.RelativeSource.AncestorType%2A> 值。  
  
 对于 `FindAncestor` 模式，当元素树中可能存在多个该类型的上级时，可以使用可选属性 <xref:System.Windows.Data.RelativeSource.AncestorLevel%2A> 帮助消除上级查找的歧义。  
  
 有关如何使用 `FindAncestor` 模式的详细信息，请参阅 <xref:System.Windows.Data.RelativeSource>。  
  
 `{RelativeSource Self}` 在以下情形下很有用：即一个实例的一个属性应依赖同一个实例的另一个属性的值，并且这两个属性之间不存在任何一般依赖属性关系（如强制）。  虽然很少有两个属性位于同一对象上的情况（这种情况下，它们的值可以说完全相同，并且以相同方式键入），但你也可以将一个 `Converter` 参数应用于具有 `{RelativeSource Self}` 的绑定，并使用此转换器在源类型和目标类型之间进行转换。  `{RelativeSource Self}` 的另一种情形是作为 <xref:System.Windows.MultiDataTrigger> 的一部分。  
  
 例如，以下 XAML 定义了一个 <xref:System.Windows.Shapes.Rectangle> 元素，以便无论为 <xref:System.Windows.FrameworkElement.Width%2A> 输入什么值，都确保 <xref:System.Windows.Shapes.Rectangle> 始终是一个方形：`<Rectangle Width="200" Height="{Binding RelativeSource={RelativeSource Self}, Path=Width}" .../>`  
  
 `{RelativeSource PreviousData}` 在数据模板中很有用，在绑定使用集合作为数据源的情况下也很有用。  你可使用 `{RelativeSource PreviousData}` 来突出集合中相邻数据项之间的关系。  相关技术是在数据源中的当前项和前一个项之间建立 <xref:System.Windows.Data.MultiBinding>，并使用此绑定上的转换器来确定这两个项及其属性的差异。  
  
 在下面的示例中，项目模板中的第一个 <xref:System.Windows.Controls.TextBlock> 可显示当前编号。  第二个 <xref:System.Windows.Controls.TextBlock> 绑定是 <xref:System.Windows.Data.MultiBinding>，名义上有两个 <xref:System.Windows.Data.Binding> 构成要素：当前记录，以及通过使用 `{RelativeSource PreviousData}` 刻意采用前一个数据记录的绑定。  然后，<xref:System.Windows.Data.MultiBinding> 上的转换器将计算差异，并将其返回到绑定。  
  
```  
<ListBox Name="fibolist">  
    <ListBox.ItemTemplate>  
        <DataTemplate>  
            <StackPanel Orientation="Horizontal">  
            <TextBlock Text="{Binding}"/>  
            <TextBlock>, difference = </TextBlock>  
                <TextBlock>  
                    <TextBlock.Text>  
                        <MultiBinding Converter="{StaticResource DiffConverter}">  
                            <Binding/>  
                            <Binding RelativeSource="{RelativeSource PreviousData}"/>  
                        </MultiBinding>  
                    </TextBlock.Text>  
                </TextBlock>  
            </StackPanel>  
            </DataTemplate>  
    </ListBox.ItemTemplate>  
```  
  
 本文未介绍数据绑定概念，请参阅 [数据绑定概述](../../../../docs/framework/wpf/data/data-binding-overview.md)。  
  
 在 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] XAML 处理器实现中，对此标记扩展的处理由 <xref:System.Windows.Data.RelativeSource> 类来定义。  
  
 `RelativeSource` 是标记扩展。  当要求转义特性值应为非文本值或非处理程序名称时，通常会实现标记扩展，相对于只在某些类型或属性上放置类型转换器而言，此要求更具有全局性。  XAML 中的所有标记扩展在其特性语法中均使用 `{` 和 `}` 字符，正是依据这一约定，XAML 处理器认定标记扩展必须处理特性。  有关详细信息，请参阅[标记扩展和 WPF XAML](../../../../docs/framework/wpf/advanced/markup-extensions-and-wpf-xaml.md)。  
  
## 请参阅  
 <xref:System.Windows.Data.Binding>   
 [样式设置和模板化](../../../../docs/framework/wpf/controls/styling-and-templating.md)   
 [XAML 概述 \(WPF\)](../../../../docs/framework/wpf/advanced/xaml-overview-wpf.md)   
 [标记扩展和 WPF XAML](../../../../docs/framework/wpf/advanced/markup-extensions-and-wpf-xaml.md)   
 [数据绑定概述](../../../../docs/framework/wpf/data/data-binding-overview.md)   
 [绑定声明概述](../../../../docs/framework/wpf/data/binding-declarations-overview.md)   
 [x:Type 标记扩展](../../../../docs/framework/xaml-services/x-type-markup-extension.md)