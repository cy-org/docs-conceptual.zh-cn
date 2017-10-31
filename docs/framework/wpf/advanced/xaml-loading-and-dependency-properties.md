---
title: "XAML 加载和依赖项属性 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-wpf"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "自定义依赖项属性"
  - "依赖项属性, XAML 加载"
  - "加载 XML 数据"
ms.assetid: 6eea9f4e-45ce-413b-a266-f08238737bf2
caps.latest.revision: 8
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 7
---
# XAML 加载和依赖项属性
[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 当前对其 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] 处理器的实现在本质上能够识别依赖项属性。  在加载二进制 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] 并处理作为依赖项属性的特性时，[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] 处理器针对依赖项属性使用属性系统方法。  这会有效地跳过属性包装。  在实现自定义依赖项属性时，必须考虑此行为，而且应当避免将任何其他代码放在除属性系统方法 <xref:System.Windows.DependencyObject.GetValue%2A> 和 <xref:System.Windows.DependencyObject.SetValue%2A> 以外的属性包装中。  
  
   
  
<a name="prerequisites"></a>   
## 必备组件  
 本主题假设您同时从使用者和作者的角度理解了依赖项属性，而且已经阅读了[依赖项属性概述](../../../../docs/framework/wpf/advanced/dependency-properties-overview.md)和[自定义依赖项属性](../../../../docs/framework/wpf/advanced/custom-dependency-properties.md)。  您还应当已经阅读了 [XAML 概述 \(WPF\)](../../../../docs/framework/wpf/advanced/xaml-overview-wpf.md)和 [XAML 语法详述](../../../../docs/framework/wpf/advanced/xaml-syntax-in-detail.md)。  
  
<a name="implementation"></a>   
## WPF XAML 加载器的实现和性能  
 出于实现方面的原因，以下操作的计算成本较低：将某个属性标识为依赖项属性并访问属性系统的 <xref:System.Windows.DependencyObject.SetValue%2A> 方法来设置该属性（而不是使用属性包装及其 setter）。  这是由于只有当您知道由标记结构和各个字符串所指示的类型和成员关系时，[!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] 处理器才能推断支持代码的整个对象模型。  
  
 可通过 xmlns 和程序集特性的组合来查找类型，但是在标识成员、确定支持将哪个成员设置为特性，以及解析属性值支持哪些类型时，则会要求使用 <xref:System.Reflection.PropertyInfo> 进行广泛的反射。  由于给定类型的依赖项属性可作为存储表通过属性系统来进行访问，因此，[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 对其 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] 处理器的实现将使用该表，并推断可以通过以下方法来更高效地设置任何给定的属性 *ABC*：针对包含 <xref:System.Windows.DependencyObject> 派生类型调用 <xref:System.Windows.DependencyObject.SetValue%2A>，并使用依赖项属性标识符 *ABCProperty*。  
  
<a name="implications"></a>   
## 自定义依赖项属性的含义  
 由于当前 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 为属性设置实现的 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] 处理器行为会完全跳过包装，因此您不应当将任何其他逻辑放在自定义依赖项属性的包装集定义中。  如果您将此类逻辑放在包装集定义中，则当在 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)]（而不是代码）中设置属性时，将不会执行此类逻辑。  
  
 同样，在 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] 处理器中，从 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] 处理中获取属性值的其他方面也使用 <xref:System.Windows.DependencyObject.GetValue%2A>，而不是使用包装。  因此，您还应当避免在 `get` 定义中使用除 <xref:System.Windows.DependencyObject.GetValue%2A> 调用以外的任何其他实现。  
  
 下面的示例是所建议的具有包装的依赖项属性定义，其中的属性标识符存储为一个 `public` `static` `readonly` 字段，`get` 和 `set` 定义中仅包含定义依赖项属性支持所必需的属性系统方法，而不包含任何其他代码。  
  
 [!code-csharp[WPFAquariumSln#AGWithWrapper](../../../../samples/snippets/csharp/VS_Snippets_Wpf/WPFAquariumSln/CSharp/WPFAquariumObjects/Class1.cs#agwithwrapper)]
 [!code-vb[WPFAquariumSln#AGWithWrapper](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/WPFAquariumSln/visualbasic/wpfaquariumobjects/class1.vb#agwithwrapper)]  
  
## 请参阅  
 [依赖项属性概述](../../../../docs/framework/wpf/advanced/dependency-properties-overview.md)   
 [XAML 概述 \(WPF\)](../../../../docs/framework/wpf/advanced/xaml-overview-wpf.md)   
 [依赖项属性元数据](../../../../docs/framework/wpf/advanced/dependency-property-metadata.md)   
 [集合类型依赖项属性](../../../../docs/framework/wpf/advanced/collection-type-dependency-properties.md)   
 [依赖项属性的安全性](../../../../docs/framework/wpf/advanced/dependency-property-security.md)   
 [DependencyObject 的安全构造函数模式](../../../../docs/framework/wpf/advanced/safe-constructor-patterns-for-dependencyobjects.md)