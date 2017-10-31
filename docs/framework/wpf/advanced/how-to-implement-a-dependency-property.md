---
title: "如何：实现依赖项属性 | Microsoft Docs"
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
  - "依赖项属性, 后备属性"
  - "属性, 使用依赖项属性进行后备"
ms.assetid: 855fd6d7-19ac-493c-bf5e-2f40b57cdc92
caps.latest.revision: 19
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 18
---
# 如何：实现依赖项属性
本示例演示如何使用 <xref:System.Windows.DependencyProperty> 字段来支持[!INCLUDE[TLA#tla_clr](../../../../includes/tlasharptla-clr-md.md)] 属性，从而定义一个[依赖项属性](GTMT)。  当您定义自己的属性并需要它们支持 [!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)] 功能的诸多方面（包括样式、数据绑定、继承、动画和默认值）时，应将其实现为[依赖项属性](GTMT)。  
  
## 示例  
 以下示例首先通过调用 <xref:System.Windows.DependencyProperty.Register%2A> 方法来注册一个[依赖项属性](GTMT)。  用于存储[依赖项属性](GTMT)的名称和特征的标识符字段的名称必须是作为 <xref:System.Windows.DependencyProperty.Register%2A> 调用的一部分为依赖项属性选择的 <xref:System.Windows.DependencyProperty.Name%2A>，并追加字符串 `Property`。  例如，如果使用 `Location` 的 <xref:System.Windows.DependencyProperty.Name%2A> 注册一个依赖项属性，则为依赖项属性定义的标识符字段必须名为 `LocationProperty`。  
  
 在此示例中，[依赖项属性](GTMT)的名称及其 [!INCLUDE[TLA2#tla_clr](../../../../includes/tla2sharptla-clr-md.md)] 访问器均为 `State`；标识符字段为 `StateProperty`；属性的类型为 <xref:System.Boolean>；注册[依赖项属性](GTMT)的类型为 `MyStateControl`。  
  
 如果不遵循此命名模式，则设计器可能无法正确地报告您的属性，而且属性系统样式应用程序的某些方面可能不会以预期的方式工作。  
  
 还可以为[依赖项属性](GTMT)属性指定默认元数据。  此示例将 `State` [依赖项属性](GTMT)的默认值注册为 `false`。  
  
 [!code-csharp[PropertySystemEsoterics#MyStateControl](../../../../samples/snippets/csharp/VS_Snippets_Wpf/PropertySystemEsoterics/CSharp/SDKSampleLibrary/class1.cs#mystatecontrol)]
 [!code-vb[PropertySystemEsoterics#MyStateControl](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/PropertySystemEsoterics/visualbasic/sdksamplelibrary/class1.vb#mystatecontrol)]  
  
 有关如何以及为何实现一个[依赖项属性](GTMT)，而非仅使用私有字段支持 [!INCLUDE[TLA2#tla_clr](../../../../includes/tla2sharptla-clr-md.md)] 属性的更多信息，请参见[依赖项属性概述](../../../../docs/framework/wpf/advanced/dependency-properties-overview.md)。  
  
## 请参阅  
 [依赖项属性概述](../../../../docs/framework/wpf/advanced/dependency-properties-overview.md)   
 [帮助主题](../../../../docs/framework/wpf/advanced/properties-how-to-topics.md)