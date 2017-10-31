---
title: "WPF 中的代码隐藏和 XAML | Microsoft Docs"
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
  - "代码隐藏文件, XAML"
  - "XAML, 代码隐藏"
ms.assetid: 9df6d3c9-aed3-471c-af36-6859b19d999f
caps.latest.revision: 14
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 14
---
# WPF 中的代码隐藏和 XAML
<a name="introduction"></a> 代码隐藏是一个术语，用于描述对 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] 页进行标记编译时与标记定义的对象联接的代码。  本主题描述代码隐藏的要求以及在 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] 中的代码的可选内联代码机制。  
  
 本主题包含以下各节：  
  
-   [必备组件](#Prerequisites)  
  
-   [代码隐藏和 XAML 语言](#codebehind_and_the_xaml_language)  
  
-   [WPF 中的代码隐藏、事件处理程序和分部类要求](#Code_behind__Event_Handler__and_Partial_Class)  
  
-   [x:Code](#x_Code)  
  
-   [内联代码限制](#Inline_Code_Limitations)  
  
<a name="Prerequisites"></a>   
## 必备组件  
 本主题假设您已阅读 [XAML 概述 \(WPF\)](../../../../docs/framework/wpf/advanced/xaml-overview-wpf.md)并已基本了解 [!INCLUDE[TLA2#tla_clr](../../../../includes/tla2sharptla-clr-md.md)] 和面向对象的编程。  
  
<a name="codebehind_and_the_xaml_language"></a>   
## 代码隐藏和 XAML 语言  
 XAML 语言包括语言级功能，这些功能可以从标记文件端将代码文件与标记文件关联。  具体而言，XAML 语言定义语言功能 [x:Class 指令](../../../../docs/framework/xaml-services/x-class-directive.md)、[x:Subclass 指令](../../../../docs/framework/xaml-services/x-subclass-directive.md) 和 [x:ClassModifier 指令](../../../../docs/framework/xaml-services/x-classmodifier-directive.md)。  应如何生成代码以及如何集成标记和代码恰好不属于 XAML 语言指定的内容。  如何集成代码、如何在应用程序和编程模型中使用 XAML 以及如何生成操作或所有这些操作所需的其他支持，都留给框架（例如 WPF）来确定。  
  
<a name="Code_behind__Event_Handler__and_Partial_Class"></a>   
## WPF 中的代码隐藏、事件处理程序和分部类要求  
  
-   分部类必须派生自支持根元素的类型。  
  
-   请注意，在标记编译生成操作的默认行为下，您可以在代码隐藏端的分部类定义中将派生保留为空。  编译的结果将假定页根的支持类型为分部类的基础，即使未指定也是如此。  但是，依赖于此行为并不是最佳做法。  
  
-   在代码隐藏中编写的事件处理程序必须是实例方法且不能是静态方法。  这些方法必须由 `x:Class` 标识的 CLR 命名空间中的分部类定义。  您不能限定事件处理程序的名称来指示 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] 处理器在不同的类范围中查找事件连结的事件处理程序。  
  
-   处理程序必须与支持类型系统中相应事件的委托匹配。  
  
-   专门针对 [!INCLUDE[TLA#tla_visualb](../../../../includes/tlasharptla-visualb-md.md)] 语言，您可以使用特定于语言的 `Handles` 关键字将处理程序与处理程序声明中的实例和事件关联，而不是在 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] 中将处理程序附加到特性。  但是，这一技术确实存在一些限制，因为 `Handles` 关键字不支持 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 事件系统的所有特定功能，例如某些路由事件方案或附加事件。  有关详细信息，请参见 [Visual Basic 和 WPF 事件处理](../../../../docs/framework/wpf/advanced/visual-basic-and-wpf-event-handling.md)。  
  
<a name="x_Code"></a>   
## x:Code  
 [x:Code](../../../../docs/framework/xaml-services/x-code-intrinsic-xaml-type.md) 是在 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] 中定义的指令元素。`x:Code` 指令元素可以包含内联编程代码。  内联定义的代码可以与同一页中的 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] 进行交互。  下面的示例阐释了内联 [!INCLUDE[TLA2#tla_cshrp](../../../../includes/tla2sharptla-cshrp-md.md)] 代码。  请注意，该代码位于 `x:Code` 元素内，并且必须包围在 `<CDATA[`...`]]>` 内，以便针对 [!INCLUDE[TLA2#tla_xml](../../../../includes/tla2sharptla-xml-md.md)] 对内容进行转义，这样 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] 处理器（解释 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] 架构或 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 架构时）不会尝试按原义将内容解释为 [!INCLUDE[TLA2#tla_xml](../../../../includes/tla2sharptla-xml-md.md)]。  
  
 [!code-xml[XAMLOvwSupport#ButtonWithInlineCode](../../../../samples/snippets/csharp/VS_Snippets_Wpf/XAMLOvwSupport/CSharp/page4.xaml#buttonwithinlinecode)]  
  
<a name="Inline_Code_Limitations"></a>   
## 内联代码限制  
 应注意避免或限制使用内联代码。  在体系结构和编码原理方面，保留标记和代码隐藏之间的独立性可以更显著地区分设计人员和开发人员这两个角色。  从更为技术性的角度看，为内联代码编写的代码更难编写，因为您总是要写入到 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] 生成的分部类中，并且只能使用默认的 XML 命名空间映射。  因为不能添加 `using` 语句，因此必须完全限定您所进行的大量 [!INCLUDE[TLA2#tla_api](../../../../includes/tla2sharptla-api-md.md)] 调用。  默认的 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 映射包括在 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 程序集中出现的大多数而非全部 [!INCLUDE[TLA2#tla_clr](../../../../includes/tla2sharptla-clr-md.md)] 命名空间；您必须完全限定对其他 CLR 命名空间中包含的类型和成员的调用。  此外，您还不能在内联代码中定义超出分部类的任何类，并且引用的所有用户代码实体均必须作为生成的分部类中的一个成员或变量存在。  其他特定于语言的编程功能（例如宏或对全局变量或生成变量的 `#ifdef`）也不可用。  有关更多信息，请参见 [x:Code 内部 XAML 类型](../../../../docs/framework/xaml-services/x-code-intrinsic-xaml-type.md)。  
  
## 请参阅  
 [XAML 概述 \(WPF\)](../../../../docs/framework/wpf/advanced/xaml-overview-wpf.md)   
 [x:Code 内部 XAML 类型](../../../../docs/framework/xaml-services/x-code-intrinsic-xaml-type.md)   
 [生成 WPF 应用程序](../../../../docs/framework/wpf/app-development/building-a-wpf-application-wpf.md)   
 [XAML 语法详述](../../../../docs/framework/wpf/advanced/xaml-syntax-in-detail.md)