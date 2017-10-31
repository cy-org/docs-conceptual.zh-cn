---
title: "属性值继承 | Microsoft Docs"
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
  - "继承, 属性值"
  - "属性, 值继承"
  - "值继承"
ms.assetid: d7c338f9-f2bf-48ed-832c-7be58ac390e4
caps.latest.revision: 16
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 15
---
# 属性值继承
属性值继承是 [!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)] 属性系统的一项功能。  属性值继承使元素树中的子元素可以从父元素那里获取特定属性的值，并继承该值，就好像它是在最近的父元素中的任意位置设置的一样。  父元素还可以通过属性值继承来获得其值，因此系统有可能一直递归到页面根元素。  属性值继承不是属性系统的默认行为；属性必须用特定的元数据设置来建立，以便使该属性能够对子元素启动属性值继承。  
  
   
  
<a name="Property_Value_Inheritance_is_Containment_Inheritance"></a>   
## 属性值继承是包容继承  
 此处的“继承”术语与讲到类型以及常规的面向对象的编程时的继承并非完全相同的概念，在后一种继承概念中，派生类从其基类继承成员定义。  这一继承含义在 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 中也有效：当在各个基类中定义的属性在代码中用作元素且公开为成员时，将公开为 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] 派生类的特性。  属性值继承则是关于属性值如何基于元素树中的父子关系从一个元素继承到另一个元素。  如果在 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] 标记中定义应用程序，那么，在将一些元素嵌套在其他元素中时，元素树是最为直观的。  还可以通过向一些对象的指定集合中添加其他对象来以编程方式创建对象树，在运行时，属性值继承按照与完成树中相同的方式工作。  
  
<a name="Practical_Applications_of_Property_Value_Inheritance"></a>   
## 属性值继承的实际应用  
 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] [!INCLUDE[TLA#tla_api#plural](../../../../includes/tlasharptla-apisharpplural-md.md)] 包括几个支持属性继承的属性。  通常，使用这些属性的方案是涉及到一个属性，每页最好仅对该属性设置一次，但是该属性还是某个基元素类的成员，因此还存在于大多数子元素中。  例如，<xref:System.Windows.FrameworkElement.FlowDirection%2A> 属性控制流式内容应当沿哪个方向在页面上呈现和排列。  通常，您希望在所有的子元素中以一致的方式处理文本流概念。  如果用户或环境操作因某种原因而在元素树的某一层重置了流方向，则流方向通常会在整个树中重置。  在将 <xref:System.Windows.FrameworkElement.FlowDirection%2A> 属性设置为继承后，只需在元素树中满足应用程序中每一页的呈现需求的那一层设置或重置该值一次。  即使最初的默认值也将按照这种方式继承。  在极个别情况下会有意混用不同的流方向，此时属性值继承模型仍允许个别元素重置其值。  
  
<a name="Making_a_Custom_Property_Inheritable"></a>   
## 使自定义属性可继承  
 通过更改自定义属性的元数据，还可以使您自己的自定义属性可继承。  但是，请注意，将属性指定为可继承需要考虑性能方面的一些因素。  如果该属性没有已建立的本地值或者通过样式、模板或数据绑定获取的值，则可继承的属性会将赋给它的属性值提供给逻辑树中的所有子元素。  
  
 为了让属性参与值继承，请按照[注册附加属性](../../../../docs/framework/wpf/advanced/how-to-register-an-attached-property.md)中的说明创建一个自定义附加属性。  向元数据 \(<xref:System.Windows.FrameworkPropertyMetadata>\) 注册属性，并在这些元数据内的选项设置中指定“Inherits”选项。  还要确保该属性已建立了默认值，因为该值现在将继承。  尽管您已经将该属性注册为附加属性，您可能还希望像对“非附加的”[依赖项属性](GTMT)一样，在所有者类型上为 get\/set 访问创建一个属性“包装”。  之后，可以通过在所有者类型或派生类型上使用直接属性包装，或者通过在任何 <xref:System.Windows.DependencyObject> 上使用附加属性语法来设置可继承的属性。  
  
 附加属性在概念上与全局属性类似；您可以在任何 <xref:System.Windows.DependencyObject> 上检查值并获得有效的结果。  附加属性的典型方案是针对子元素设置属性值，如果所讨论的属性是附加属性，而且在树中的每个元素 \(<xref:System.Windows.DependencyObject>\) 上总是隐式地表示为附加属性，则该方案更为有效。  
  
> [!NOTE]
>  尽管属性值继承看起来对非附加依赖项属性有效，但通过运行时树中某些元素边界的非附加属性继承行为并未定义。  如果要在元数据中指定 <xref:System.Windows.DependencyProperty.RegisterAttached%2A>，请始终使用 <xref:System.Windows.FrameworkPropertyMetadata.Inherits%2A> 来注册属性。  
  
<a name="InheritanceContext"></a>   
## 跨树边界继承属性值  
 属性继承通过遍历元素树来工作。  此树通常与逻辑树平行。  但是，每当您在定义元素树的标记中包括 [WPF 核心级别](GTMT)对象（如 <xref:System.Windows.Media.Brush>）时，即创建了一个不连续的逻辑树。  真正的逻辑树在概念上不能通过 <xref:System.Windows.Media.Brush> 来扩展，因为逻辑树是 [WPF 框架级别](GTMT)的概念。  在使用 <xref:System.Windows.LogicalTreeHelper> 的方法时，会看到这种情况反映在结果中。  但是，只要可继承的属性注册为附加属性，而且没有遇到有意设置的继承阻止边界（如 <xref:System.Windows.Controls.Frame>），属性值继承就可以弥合逻辑树中的这种间隙，而且仍可以传递所继承的值。  
  
## 请参阅  
 [依赖项属性元数据](../../../../docs/framework/wpf/advanced/dependency-property-metadata.md)   
 [附加属性概述](../../../../docs/framework/wpf/advanced/attached-properties-overview.md)   
 [依赖项属性值优先级](../../../../docs/framework/wpf/advanced/dependency-property-value-precedence.md)