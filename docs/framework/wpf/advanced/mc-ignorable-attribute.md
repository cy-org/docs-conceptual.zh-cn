---
title: "mc:Ignorable 特性 | Microsoft Docs"
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
  - "mc XML 命名空间前缀"
  - "mc:Ignorable 特性"
  - "mc:ProcessContent 特性"
  - "XAML, mc:Ignorable 特性"
  - "XAML, mc:ProcessContent 特性"
  - "XML, mc 命名空间前缀"
ms.assetid: acd9a6ef-b7ca-4146-abb6-60f3b366e9ec
caps.latest.revision: 8
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 8
---
# mc:Ignorable 特性
指定标记文件中遇到的哪些 [!INCLUDE[TLA2#tla_xml](../../../../includes/tla2sharptla-xml-md.md)] 命名空间前缀可以被 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] 处理器忽略。  `mc:Ignorable` 特性为自定义命名空间映射和 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] 版本管理提供标记兼容性支持。  
  
## XAML 特性用法（一个前缀）  
  
```  
<object  
  xmlns:ignorablePrefix="ignorableUri"  
  xmlns:mc="http://schemas.openxmlformats.org/markup-compatibility/2006"  
  mc:Ignorable="ignorablePrefix"...>  
    <ignorablePrefix1:ThisElementCanBeIgnored/>  
</object>  
```  
  
## XAML 特性用法（两个前缀）  
  
```  
<object  
  xmlns:ignorablePrefix1="ignorableUri"  
  xmlns:ignorablePrefix2="ignorableUri2"  
  xmlns:mc="http://schemas.openxmlformats.org/markup-compatibility/2006"  
  mc:Ignorable="ignorablePrefix1 ignorablePrefix2"...>  
    <ignorablePrefix1:ThisElementCanBeIgnored/>  
</object>  
```  
  
## XAML 值  
  
|||  
|-|-|  
|*ignorablePrefix、ignorablePrefix1 等*|任何符合 XML 1.0 规范的有效的前缀字符串。|  
|*ignorableUri*|任何符合 XML 1.0 规范、用于指定命名空间的有效 URI。|  
|*ThisElementCanBeIgnored*|可以由[!INCLUDE[TLA#tla_xaml](../../../../includes/tlasharptla-xaml-md.md)] 处理器实现忽略的元素（如果无法解析基础类型）。|  
  
## 备注  
 映射 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] 兼容命名空间 [!INCLUDE[TLA#tla_mcxmlnsv1](../../../../includes/tlasharptla-mcxmlnsv1-md.md)] 时，建议使用 `mc` [!INCLUDE[TLA2#tla_xml](../../../../includes/tla2sharptla-xml-md.md)] 命名空间前缀作为前缀约定。  
  
 元素名称的前缀部分标识为 `mc:Ignorable` 的元素或特性在由 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] 处理时，将不会引发错误。  如果该特性未能解析为基础类型或编程构造，则忽略此元素。  但是，请注意被忽略的元素仍可能会因为其他元素要求而生成其他分析错误，这是未处理该元素的副作用。  例如，某个特定元素内容模型可能刚好只需要一个子元素，但如果该指定子元素已位于 `mc:Ignorable` 前缀中并且未能解析为一个类型，则 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] 处理器可能会引发错误。  
  
 `mc:Ignorable` 仅应用于命名空间与标识符字符串的映射。  `mc:Ignorable` 并不应用于命名空间与程序集的映射，该映射指定 [!INCLUDE[TLA2#tla_clr](../../../../includes/tla2sharptla-clr-md.md)] 命名空间和程序集（或默认为作为程序集的当前可执行文件）。  
  
 如果您实现的是 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] 处理器，在对由标识为 `mc:Ignorable` 的前缀限定的任何元素或特性进行类型解析时，您的处理器实现不能引发分析或处理错误，  但仍然可以引发作为无法加载或处理某元素的间接后果的异常（例如前面的一个子元素示例）。  
  
 默认情况下，[!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] 处理器将忽略被忽略元素中的内容。  但是，您可以指定一个附加特性 [mc:ProcessContent 特性](../../../../docs/framework/wpf/advanced/mc-processcontent-attribute.md)，以要求下一个可用的父元素继续处理被忽略元素中的内容。  
  
 可以使用一个或多个空格作为分隔符在特性中指定多个前缀，例如：`mc:Ignorable="ignore1 ignore2"`。  
  
 [!INCLUDE[TLA#tla_mcxmlnsv1](../../../../includes/tlasharptla-mcxmlnsv1-md.md)] 命名空间定义了本部分[!INCLUDE[TLA#tla_sdk](../../../../includes/tlasharptla-sdk-md.md)] 中未介绍的其他元素和特性。  有关更多信息，请参见 [XML Markup Compatibility Specification](http://go.microsoft.com/fwlink/?LinkId=73824)（XML 标记兼容性规范）。  
  
## 请参阅  
 <xref:System.Windows.Markup.XamlReader>   
 [PresentationOptions:Freeze 特性](../../../../docs/framework/wpf/advanced/presentationoptions-freeze-attribute.md)   
 [XAML 概述 \(WPF\)](../../../../docs/framework/wpf/advanced/xaml-overview-wpf.md)   
 [WPF 中的文档](../../../../docs/framework/wpf/advanced/documents-in-wpf.md)