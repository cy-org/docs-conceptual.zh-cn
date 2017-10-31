---
title: "x:Shared Attribute | Microsoft Docs"
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
  - "XAML [XAML Services], x:Shared attribute"
  - "x:Shared attribute [XAML Services]"
  - "Shared attribute in XAML [XAML Services]"
ms.assetid: c8cff434-2785-405f-9f95-16deb34c9e64
caps.latest.revision: 16
author: "wadepickett"
ms.author: "wpickett"
manager: "wpickett"
caps.handback.revision: 16
---
# x:Shared Attribute
当设置为 `false` 时，会修改 WPF 资源检索行为，以便特性化资源请求为每个请求创建一个新实例，而不是所有请求共享同一个实例。  
  
## XAML 属性用法  
  
```  
<ResourceDictionary>  
  <object x:Shared="false".../>  
</ResourceDictionary>  
```  
  
## 备注  
 `x:Shared` 映射到 XAML 语言 XAML 命名空间，并由 .NET Framework XAML 服务及其 XAML 读取器识别为有效的 XAML 语言元素。  但是，`x:Shared` 的规定功能仅与 WPF 应用程序和 WPF XAML 分析器有关。  在 WPF 中，`x:Shared` 仅当作为特性被应用到存在于 WPF <xref:System.Windows.ResourceDictionary> 中的对象时才有用。  其他用法不会引发分析异常或其他错误，但它们不起任何作用。  
  
 在 XAML 语言规范中未指定 `x:Shared` 的含义。  其他 XAML 实现，例如在 .NET Framework XAML 服务上生成的实现，不一定提供资源共享支持。  此类 XAML 实现可以在同样使用过 `x:Shared` 值的支持框架中提供类似行为。  
  
 在 WPF 中，资源的默认 `x:Shared` 条件是 `true`。  此条件意味着任何给定资源请求都始终返回同一个实例。  
  
 修改通过资源 API（如 <xref:System.Windows.FrameworkElement.FindResource%2A>）返回的对象或者直接在 <xref:System.Windows.ResourceDictionary> 内部修改对象会更改原始资源。  如果对该资源的引用是动态资源引用，则该资源的使用者将获得更改后的资源。  
  
 如果对资源的引用是静态资源引用，则在 [!INCLUDE[TLA2#tla_xaml](../../../includes/tla2sharptla-xaml-md.md)] 处理时间之后的资源更改是不相关的。  关于静态资源引用与动态资源引用对比的更多信息，请参见 [XAML 资源](../../../ocs/framework/wpf/advanced/xaml-resources.md)。  
  
 显式指定 `x:Shared="true"` 很少做，因为这已经是默认行为。  在 WPF 对象模型中，对于 `x:Shared`，没有直接的代码等效项；它只能在 XAML 用法中指定，且必须由默认 WPF 行为处理，或在加载路径上的中间 XAML 节点流中处理（如果使用 .NET Framework XAML 服务及其 XAML 读取器处理）。  
  
 `x:Shared="false"` 的一种情况是：您将 <xref:System.Windows.FrameworkElement> 或<xref:System.Windows.FrameworkContentElement> 派生类定义为资源，然后将此元素资源引入内容模型。  `x:Shared="false"` 使得元素资源可以多次引入到同一个集合（如 <xref:System.Windows.Controls.UIElementCollection>）中。  如果没有 `x:Shared="false"`，则这将是无效的，因为集合强制执行内容的唯一性。  但是 `x:Shared="false"` 行为创建资源的另一个完全相同的实例，而不是返回同一个实例。  
  
 指定 `x:Shared="false"` 的另一种情况是：您对动画值使用一个 <xref:System.Windows.Freezable> 资源，但希望在每个动画的基础上修改此资源。  
  
 `false` 字符串的处理不区分大小写。  
  
 在 WPF 中，`x:Shared` 只有在满足以下条件的情况下才是有效的：  
  
-   包含具有 `x:Shared` 的项的 <xref:System.Windows.ResourceDictionary> 必须已编译。  <xref:System.Windows.ResourceDictionary> 不能在宽松 XAML 内或用于主题。  
  
-   包含项的 <xref:System.Windows.ResourceDictionary> 不得嵌套在另一个 <xref:System.Windows.ResourceDictionary> 内。  例如，您不能对已经是 <xref:System.Windows.ResourceDictionary> 项的 <xref:System.Windows.Style> 内部的 <xref:System.Windows.ResourceDictionary> 中的项使用 `x:Shared`。  
  
## 请参阅  
 <xref:System.Windows.ResourceDictionary>   
 [XAML 资源](../../../ocs/framework/wpf/advanced/xaml-resources.md)   
 [基元素](../../../ocs/framework/wpf/advanced/base-elements.md)