---
title: "集合类型依赖项属性 | Microsoft Docs"
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
  - "集合类型属性"
  - "依赖项属性"
  - "属性, 集合类型"
  - "属性, 依赖项"
ms.assetid: 99f96a42-3ab7-4f64-a16b-2e10d654e97c
caps.latest.revision: 10
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 7
---
# 集合类型依赖项属性
本主题为属性类型是集合类型的情况下如何实现[依赖项属性](GTMT)提供了指导和建议的模式。  
  
   
  
<a name="implementing"></a>   
## 实现集合类型依赖项属性  
 通常情况下对于依赖项属性，遵循的实现是定义一个 [!INCLUDE[TLA2#tla_clr](../../../../includes/tla2sharptla-clr-md.md)] 属性包装，其中该属性由一个 <xref:System.Windows.DependencyProperty> 标识符（而不是字段或其他构造）支持。  若要实现一个集合类型属性，请遵循同样的模式。  但是，每当集合中包含的类型本身为 <xref:System.Windows.DependencyObject> 或 <xref:System.Windows.Freezable> 派生类时，集合类型属性会使模式更加复杂。  
  
<a name="initializing"></a>   
## 不使用默认值初始化集合  
 在您创建依赖项属性时，没有将属性默认值指定为初始字段值，  而是通过依赖项属性元数据指定默认值。  如果属性是一种引用类型，则在依赖项属性元数据中指定的默认值不是各个实例的默认值，而是应用到该类型的所有实例的默认值。  因此，您必须注意不要将集合属性元数据所定义的单个静态集合用作新创建的类型实例的适用默认值。  并且，在类构造函数逻辑中，必须确保特意将集合值设置为唯一的（实例）集合。  否则，会创建一个意外的单独的类。  
  
 请看下面的示例。  下面的示例部分演示 `Aquarium` 类的定义。  该类定义集合类型依赖项属性 `AquariumObjects`，它将泛型 <xref:System.Collections.Generic.List%601> 类型与 <xref:System.Windows.FrameworkElement> 类型约束一起使用。  在对依赖项属性的 <xref:System.Windows.DependencyProperty.Register%28System.String%2CSystem.Type%2CSystem.Type%2CSystem.Windows.PropertyMetadata%29> 调用中，元数据将默认值建立为一个新的泛型 <xref:System.Collections.Generic.List%601>。  
  
 <!-- TODO: review snippet reference [!code-csharp[PropertiesOvwSupport#CollectionProblemDefinition](../../../../samples/snippets/csharp/VS_Snippets_Wpf/PropertiesOvwSupport/CSharp/page4.xaml.cs#collectionproblemdefinition)]  -->
 [!code-vb[PropertiesOvwSupport#CollectionProblemDefinition](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/PropertiesOvwSupport/visualbasic/page4.xaml.vb#collectionproblemdefinition)]  
[!code-csharp[PropertiesOvwSupport#CollectionProblemEndB](../../../../samples/snippets/csharp/VS_Snippets_Wpf/PropertiesOvwSupport/CSharp/page4.xaml.cs#collectionproblemendb)]
[!code-vb[PropertiesOvwSupport#CollectionProblemEndB](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/PropertiesOvwSupport/visualbasic/page4.xaml.vb#collectionproblemendb)]  
  
 但是，如果您只是使用下面的代码，则该单个列表默认值会在 `Aquarium` 的所有实例中共享。  如果运行下面的测试代码（该测试代码旨在演示如何实例化两个独立的 `Aquarium` 实例并向这两个实例中分别添加一个不同的 `Fish`），您会看到令人惊讶的结果：  
  
 [!code-csharp[PropertiesOvwSupport#CollectionProblemTestCode](../../../../samples/snippets/csharp/VS_Snippets_Wpf/PropertiesOvwSupport/CSharp/page4.xaml.cs#collectionproblemtestcode)]
 [!code-vb[PropertiesOvwSupport#CollectionProblemTestCode](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/PropertiesOvwSupport/visualbasic/page4.xaml.vb#collectionproblemtestcode)]  
  
 每个集合的计数不是 1，而是 2\!  这是因为元数据中的单个构造函数调用导致每个 `Aquarium` 都将其 `Fish` 添加到默认值集合，从而会在所有实例中共享。  这种情况应该不是您想要的。  
  
 为了纠正此问题，在类构造函数调用中，必须将集合依赖项属性值重设为唯一的实例。  因为该属性是只读的依赖项属性，所以应使用 <xref:System.Windows.DependencyObject.SetValue%28System.Windows.DependencyPropertyKey%2CSystem.Object%29> 方法通过只能在该类中访问的 <xref:System.Windows.DependencyPropertyKey> 对该属性进行设置。  
  
 [!code-csharp[PropertiesOvwSupport#CollectionProblemCtor](../../../../samples/snippets/csharp/VS_Snippets_Wpf/PropertiesOvwSupport/CSharp/page4.xaml.cs#collectionproblemctor)]
 [!code-vb[PropertiesOvwSupport#CollectionProblemCtor](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/PropertiesOvwSupport/visualbasic/page4.xaml.vb#collectionproblemctor)]  
  
 现在，如果您再次运行上述测试代码，应能看到更接近预期的结果，其中每个 `Aquarium` 都支持它自己的唯一集合。  
  
 如果您选择使集合属性成为读写属性，则此模式会稍有变化。  此时，您将从构造函数调用公共 set 访问器来执行初始化，即仍使用公共的 <xref:System.Windows.DependencyProperty> 标识符来调用 set 包装中 <xref:System.Windows.DependencyObject.SetValue%28System.Windows.DependencyProperty%2CSystem.Object%29> 的非键签名。  
  
## 从集合属性报告绑定值更改  
 本身为依赖项属性的集合属性不会自动报告对其子属性的更改。  如果正在创建与集合的绑定，这可以防止绑定报告更改而使某些数据绑定方案无效。  但是，如果您使用集合类型 <xref:System.Windows.FreezableCollection%601> 作为您的集合类型，则会以合适的方式报告对集合所包含元素的子属性更改，并且绑定会按预期工作。  
  
 若要在依赖项对象集合中启用子属性绑定，请将集合属性创建为类型 <xref:System.Windows.FreezableCollection%601>，该集合的类型约束到任何 <xref:System.Windows.DependencyObject> 派生类。  
  
## 请参阅  
 <xref:System.Windows.FreezableCollection%601>   
 [XAML 及 WPF 的自定义类](../../../../docs/framework/wpf/advanced/xaml-and-custom-classes-for-wpf.md)   
 [数据绑定概述](../../../../docs/framework/wpf/data/data-binding-overview.md)   
 [依赖项属性概述](../../../../docs/framework/wpf/advanced/dependency-properties-overview.md)   
 [自定义依赖项属性](../../../../docs/framework/wpf/advanced/custom-dependency-properties.md)   
 [依赖项属性元数据](../../../../docs/framework/wpf/advanced/dependency-property-metadata.md)