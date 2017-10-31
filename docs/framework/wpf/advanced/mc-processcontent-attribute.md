---
title: "mc:ProcessContent 特性 | Microsoft Docs"
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
  - "mc:ProcessContent 特性"
  - "XAML, mc:ProcessContent 特性"
ms.assetid: 2689b2c8-b4dc-4b71-b9bd-f95e619122d7
caps.latest.revision: 6
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 6
---
# mc:ProcessContent 特性
指定即使在由于指定了 [mc:Ignorable 特性](../../../../docs/framework/wpf/advanced/mc-ignorable-attribute.md)而导致直接父元素可能被 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] 处理器忽略的情况下，哪些 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] 元素的内容仍然应由相关父元素来处理。  `mc:ProcessContent` 特性为自定义命名空间映射和 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] 版本登记提供标记兼容性支持。  
  
## XAML 属性用法  
  
```  
<object  
  xmlns:ignorablePrefix="ignorableUri"  
  xmlns:mc="http://schemas.openxmlformats.org/markup-compatibility/2006"  
  mc:Ignorable="ignorablePrefix"...  
  mc:ProcessContent="ignorablePrefix:ThisElementCanBeIgnored"  
>  
    <ignorablePrefix:ThisElementCanBeIgnored>  
        [content]  
    </ignorablePrefix:ThisElementCanBeIgnored>  
</object>  
```  
  
## XAML 值  
  
|||  
|-|-|  
|*ignorablePrefix*|任何符合 XML 1.0 规范的有效的前缀字符串。|  
|*ignorableUri*|任何符合 XML 1.0 规范、用于指定命名空间的有效 URI。|  
|*ThisElementCanBeIgnored*|可以由[!INCLUDE[TLA#tla_xaml](../../../../includes/tlasharptla-xaml-md.md)] 处理器实现忽略的元素（如果无法解析基础类型）。|  
|*\[content\]*|*ThisElementCanBeIgnored* 被标记为可以忽略。  如果处理器忽略该元素，*\[content\]* 将由 *object* 来处理。|  
  
## 备注  
 默认情况下，[!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] 处理器将忽略被忽略元素中的内容。  您可以按 `mc:ProcessContent` 指定特定的元素，而 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] 处理器将继续处理被忽略的元素中的内容。  如果内容嵌套在几个标记内，而至少有一个标记可以忽略，至少有一个标记不可以忽略，这种情况下通常会使用此方法。  
  
 可以在特性中指定多个前缀，而使用空格作为分隔符，例如：`mc:ProcessContent="ignore:Element1 ignore:Element2"`。  
  
 [!INCLUDE[TLA#tla_mcxmlnsv1](../../../../includes/tlasharptla-mcxmlnsv1-md.md)] 命名空间定义了本部分[!INCLUDE[TLA#tla_sdk](../../../../includes/tlasharptla-sdk-md.md)] 中未介绍的其他元素和特性。  有关更多信息，请参见 [XML Markup Compatibility Specification](http://go.microsoft.com/fwlink/?LinkId=73824)（XML 标记兼容性规范）。  
  
## 请参阅  
 [mc:Ignorable 特性](../../../../docs/framework/wpf/advanced/mc-ignorable-attribute.md)   
 [XAML 概述 \(WPF\)](../../../../docs/framework/wpf/advanced/xaml-overview-wpf.md)