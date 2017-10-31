---
title: "如何：重写依赖项属性的元数据 | Microsoft Docs"
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
  - "依赖项属性, 重写元数据"
  - "元数据, 为依赖项属性重写"
  - "重写依赖项属性的元数据"
ms.assetid: f90f026e-60d8-428a-933d-edf0dba4441f
caps.latest.revision: 15
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 14
---
# 如何：重写依赖项属性的元数据
此示例演示如何重写来自继承类的默认依赖项属性元数据，其方法是调用 <xref:System.Windows.DependencyProperty.OverrideMetadata%2A> 方法并提供特定于类型的元数据。  
  
## 示例  
 通过定义其 <xref:System.Windows.PropertyMetadata>，类可以定义[依赖项属性](GTMT)的行为，例如，其默认值和属性系统回调。  很多依赖项属性类都已经将默认元数据作为其注册过程的一部分而创建。  这包含作为 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] [!INCLUDE[TLA2#tla_api](../../../../includes/tla2sharptla-api-md.md)] 一部分的依赖项属性。  通过其类继承继承依赖项属性的类可以重写原始的元数据，以便可以通过元数据更改的属性的特征将与任何特定于子类的要求匹配。  
  
 在依赖项属性上重写元数据的操作必须在将该属性提供给属性系统使用之前进行，也就是说，在对注册属性的对象的特定实例进行实例化之前进行。  必须在将其自身提供为 <xref:System.Windows.DependencyProperty.OverrideMetadata%2A> 的 `forType` 参数的类型的静态构造内执行对 <xref:System.Windows.DependencyProperty.OverrideMetadata%2A> 的调用。  如果在所有者类型的实例存在之后尝试更改元数据，这将不会引发异常，但会在属性系统中导致不一致的行为。  此外，每种类型只可以重写一次元数据。  以后在同一类型上重写元数据的尝试将会引发异常。  
  
 在下面示例中，自定义类 `MyAdvancedStateControl` 重写由带有新属性元数据的 `MyAdvancedStateControl` 为 `StateProperty` 提供的元数据。  例如，当在新构造的 `MyAdvancedStateControl` 实例上查询 `StateProperty` 时，其默认值现在是 `true`。  
  
 [!code-csharp[PropertySystemEsoterics#MyStateControl](../../../../samples/snippets/csharp/VS_Snippets_Wpf/PropertySystemEsoterics/CSharp/SDKSampleLibrary/class1.cs#mystatecontrol)]
 [!code-vb[PropertySystemEsoterics#MyStateControl](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/PropertySystemEsoterics/visualbasic/sdksamplelibrary/class1.vb#mystatecontrol)]  
[!code-csharp[PropertySystemEsoterics#MyAdvancedStateControl](../../../../samples/snippets/csharp/VS_Snippets_Wpf/PropertySystemEsoterics/CSharp/SDKSampleLibrary/class1.cs#myadvancedstatecontrol)]
[!code-vb[PropertySystemEsoterics#MyAdvancedStateControl](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/PropertySystemEsoterics/visualbasic/sdksamplelibrary/class1.vb#myadvancedstatecontrol)]  
  
## 请参阅  
 <xref:System.Windows.DependencyProperty>   
 [依赖项属性概述](../../../../docs/framework/wpf/advanced/dependency-properties-overview.md)   
 [自定义依赖项属性](../../../../docs/framework/wpf/advanced/custom-dependency-properties.md)   
 [帮助主题](../../../../docs/framework/wpf/advanced/properties-how-to-topics.md)