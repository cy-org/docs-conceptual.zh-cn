---
title: "依赖项属性的安全性 | Microsoft Docs"
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
  - "依赖项属性, access"
  - "依赖项属性, 安全性"
  - "安全性, 依赖项属性"
  - "安全性, 包装"
  - "验证, 依赖项属性"
  - "包装, access"
  - "包装, 安全性"
ms.assetid: d10150ec-90c5-4571-8d35-84bafa2429a4
caps.latest.revision: 8
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 7
---
# 依赖项属性的安全性
依赖项属性通常应当被视为公共属性。  [!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)] 属性系统在本质上无法对依赖项属性值提供安全保证。  
  
   
  
<a name="AccessSecurity"></a>   
## 包装和依赖项属性的访问和安全性  
 通常，依赖项属性是随“包装”[!INCLUDE[TLA#tla_clr](../../../../includes/tlasharptla-clr-md.md)] 属性一起实现的，这些包装属性可以简化从实例获取或设置属性的过程。  但是，包装实际上只是一种便捷的方法，用以实现在与依赖项属性交互时所使用的基础 <xref:System.Windows.DependencyObject.GetValue%2A> 和 <xref:System.Windows.DependencyObject.SetValue%2A> 静态调用。  从另外一个角度考虑，这些属性作为恰好由依赖项属性（而非私有字段）支持的[!INCLUDE[TLA#tla_clr](../../../../includes/tlasharptla-clr-md.md)] 属性公开。  应用于包装的安全机制与属性系统行为以及基础依赖项属性的访问并不可比。  为包装设置安全要求只是防止使用便捷方法，而不会防止调用 <xref:System.Windows.DependencyObject.GetValue%2A> 或 <xref:System.Windows.DependencyObject.SetValue%2A>。  同样，为包装设置受保护或私有访问级别也不会提供任何有效的安全性。  
  
 如果您要编写自己的依赖项属性，应当将包装和 <xref:System.Windows.DependencyProperty> 标识符字段声明为公共成员，以便调用方不会（由于它的存储是作为依赖项属性而实现的）获得有关该属性的实际访问级别的误导信息。  
  
 对于自定义依赖项属性，可以将您的属性注册为只读依赖项属性，而且这确实提供了一种有效的方法来防止属性被任何不拥有对该属性的 <xref:System.Windows.DependencyPropertyKey> 的引用的人设置。  有关更多信息，请参见[只读依赖项属性](../../../../docs/framework/wpf/advanced/read-only-dependency-properties.md)。  
  
> [!NOTE]
>  不禁止将 <xref:System.Windows.DependencyProperty> 标识符字段声明为私有字段，而且可以放心地使用这种方法来帮助减小自定义类的直接公开命名空间，但是这种属性的“私有”性质不应当被视为与[!INCLUDE[TLA#tla_clr](../../../../includes/tlasharptla-clr-md.md)] 语言定义所定义的私有访问级别一样，具体原因将在下一节介绍。  
  
<a name="PropertySystemExposure"></a>   
## 依赖项属性的属性系统公开  
 将 <xref:System.Windows.DependencyProperty> 声明为公共级别以外的任何访问级别通常毫无用处而且可能会产生误导作用。  该访问级别设置只是防止某人从声明类获得对实例的引用。  但是，属性系统有几个方面将返回 <xref:System.Windows.DependencyProperty> 作为一种标识在类实例或派生类实例上存在的特定属性的方式，而且该标识符在 <xref:System.Windows.DependencyObject.SetValue%2A> 调用中仍可用，即使最初的静态标识符声明为非公共也是如此。  而且，<xref:System.Windows.DependencyObject.OnPropertyChanged%2A> 虚方法接收任何现有依赖项属性的值发生改变的信息。  另外，<xref:System.Windows.DependencyObject.GetLocalValueEnumerator%2A> 方法为具有本地设置值的实例上的任何属性返回标识符。  
  
### 验证和安全  
 下面的安全机制不足以保证安全：向 <xref:System.Windows.DependencyProperty.ValidateValueCallback%2A> 应用一个要求，并期望在该要求未满足时验证失败以防止设置属性。  如果恶意调用方在应用程序域中操作，则这些调用方还可能会禁止通过 <xref:System.Windows.DependencyProperty.ValidateValueCallback%2A> 强制执行的“set\-value”失效。  
  
## 请参阅  
 [自定义依赖项属性](../../../../docs/framework/wpf/advanced/custom-dependency-properties.md)