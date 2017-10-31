---
title: "如何：定义和引用资源 | Microsoft Docs"
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
  - "定义资源"
  - "引用资源"
  - "资源, 定义"
  - "资源, 引用"
ms.assetid: b86b876b-0a10-489b-9a5d-581ea9b32406
caps.latest.revision: 10
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 10
---
# 如何：定义和引用资源
本示例演示如何使用[!INCLUDE[TLA#tla_xaml](../../../../includes/tlasharptla-xaml-md.md)] 中的一个特性来定义和引用资源。  
  
## 示例  
 下面的示例定义两种类型的资源：一个 <xref:System.Windows.Media.SolidColorBrush> 资源和多个 <xref:System.Windows.Style> 资源。  <xref:System.Windows.Media.SolidColorBrush> 资源 `MyBrush` 用于提供多个属性的值，其中每个属性都有一个 <xref:System.Windows.Media.Brush> 类型值。  <xref:System.Windows.Style> 资源 `PageBackground`、`TitleText` 和 `Label` 均针对一种特定的控件类型。  当该样式资源由资源键引用并用于设置 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] 中定义的多个特定控件元素的 <xref:System.Windows.FrameworkElement.Style%2A> 属性时，这些样式即设置目标控件的多个不同属性。  
  
 请注意，`Label` 样式的 setter 中的某个属性还引用前面定义的 `MyBrush` 资源。  这是一种很常见的技术，但是一定要记住资源是按照它们的给出顺序进行分析并输入到资源字典中的，这一点非常重要。  如果您使用 [StaticResource 标记扩展](../../../../docs/framework/wpf/advanced/staticresource-markup-extension.md)从其他资源引用这些资源，则也是按照它们在字典中的顺序来请求它们的。  确保在请求资源之前已在资源集合中对该资源进行了定义。  如有必要，您可以使用 [DynamicResource 标记扩展](../../../../docs/framework/wpf/advanced/dynamicresource-markup-extension.md)在运行时引用资源，这样可以绕过严格的资源引用创建顺序，但应注意这种 DynamicResource 技术会对性能产生一定的负面影响。  有关详细信息，请参见[XAML 资源](../../../../docs/framework/wpf/advanced/xaml-resources.md)。  
  
 [!code-xml[FEResource#XAML](../../../../samples/snippets/csharp/VS_Snippets_Wpf/FEResource/CS/default.xaml#xaml)]  
  
## 请参阅  
 [XAML 资源](../../../../docs/framework/wpf/advanced/xaml-resources.md)   
 [样式设置和模板化](../../../../docs/framework/wpf/controls/styling-and-templating.md)