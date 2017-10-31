---
title: "如何：为依赖项属性添加所有者类型 | Microsoft Docs"
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
  - "类, 添加为依赖项属性的所有者"
  - "依赖项属性, 添加类作为所有者"
ms.assetid: edcce050-0576-4edb-a31a-3f909637b452
caps.latest.revision: 11
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 11
---
# 如何：为依赖项属性添加所有者类型
此示例演示如何将类添加为针对不同类型注册的依赖性属性的所有者。  通过执行此操作，[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] 读取器和属性系统都可以将该类识别为属性的其他所有者。  添加所有者时，也可以选择添加类来提供类型特定的元数据。  
  
 在下面的示例中，`StateProperty` 是由 `MyStateControl` 类注册的属性。  类 `UnrelatedStateControl` 使用 <xref:System.Windows.DependencyProperty.AddOwner%2A> 方法将本身添加为 `StateProperty` 的所有者，当添加类型上存在依赖项属性时，则专门使用依赖项属性的新元数据允许的签名。  请注意，对于与[实现依赖项属性](../../../../docs/framework/wpf/advanced/how-to-implement-a-dependency-property.md)示例中所示的示例类似的属性，应提供[!INCLUDE[TLA#tla_clr](../../../../includes/tlasharptla-clr-md.md)] 访问器，并在要添加为所有者的类上重新公开依赖项属性标识符。  
  
 未使用包装时，从使用 <xref:System.Windows.DependencyObject.GetValue%2A> 或 <xref:System.Windows.DependencyObject.SetValue%2A> 的程序访问的角度来看，依赖项属性仍将有效。  但是，您通常需要将此属性系统的行为与 [!INCLUDE[TLA2#tla_clr](../../../../includes/tla2sharptla-clr-md.md)] 属性包装并行处理。  包装使以编程方式对依赖项属性进行设置的操作更加容易，并可以将属性设置为 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] 特性。  
  
 若要了解如何重写默认元数据，请参见[重写依赖项属性的元数据](../../../../docs/framework/wpf/advanced/how-to-override-metadata-for-a-dependency-property.md)。  
  
## 示例  
 [!code-csharp[PropertySystemEsoterics#MyStateControl](../../../../samples/snippets/csharp/VS_Snippets_Wpf/PropertySystemEsoterics/CSharp/SDKSampleLibrary/class1.cs#mystatecontrol)]
 [!code-vb[PropertySystemEsoterics#MyStateControl](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/PropertySystemEsoterics/visualbasic/sdksamplelibrary/class1.vb#mystatecontrol)]  
[!code-csharp[PropertySystemEsoterics#UnrelatedStateControl](../../../../samples/snippets/csharp/VS_Snippets_Wpf/PropertySystemEsoterics/CSharp/SDKSampleLibrary/class1.cs#unrelatedstatecontrol)]
[!code-vb[PropertySystemEsoterics#UnrelatedStateControl](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/PropertySystemEsoterics/visualbasic/sdksamplelibrary/class1.vb#unrelatedstatecontrol)]  
  
## 请参阅  
 [自定义依赖项属性](../../../../docs/framework/wpf/advanced/custom-dependency-properties.md)   
 [依赖项属性概述](../../../../docs/framework/wpf/advanced/dependency-properties-overview.md)