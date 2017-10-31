---
title: "只读依赖项属性 | Microsoft Docs"
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
  - "依赖项属性, 只读"
  - "只读依赖项属性"
ms.assetid: f23d6ec9-3780-4c09-a2ff-b2f0a2deddf1
caps.latest.revision: 8
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 7
---
# 只读依赖项属性
本主题介绍只读依赖项属性，包括现有的只读依赖项属性和创建自定义只读依赖项属性的方案和方法。  
  
   
  
<a name="prerequisites"></a>   
## 必备组件  
 本主题假定您了解实现依赖项属性的基本方案以及如何将元数据应用到自定义依赖项属性。  有关上下文，请参见[自定义依赖项属性](../../../../docs/framework/wpf/advanced/custom-dependency-properties.md)和[依赖项属性元数据](../../../../docs/framework/wpf/advanced/dependency-property-metadata.md)。  
  
<a name="existing"></a>   
## 现有的只读依赖项属性  
 在 [!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)] 框架中定义的某些依赖项属性为只读。  通常指定只读依赖项属性的原因是：这些属性应该用于状态确定，但是有多种因素影响该状态，从用户界面设计的角度看，仅将属性设置为该状态并不能达到预期的效果。  例如，通过鼠标输入确认，属性 <xref:System.Windows.UIElement.IsMouseOver%2A> 实际上仅为表层状态。  任何通过避开真正的鼠标输入以编程方式设置此值的尝试都将是不可预期的并将导致产生不一致的情况。  
  
 由于不可设置性，只读依赖项属性不适于很多依赖项属性通常为其提供一个解决方案（即：数据绑定，可直接对值、验证、动画和继承样式化）的情形。  尽管具有不可设置性，只读依赖项属性仍有一些其他由属性系统中的依赖项属性支持的功能。  只读依赖项属性仍可以用作样式中的属性触发器，这是其他功能中最为重要的一个。  您无法使用常规的[!INCLUDE[TLA#tla_clr](../../../../includes/tlasharptla-clr-md.md)] 属性启用触发器，因为该属性必须是依赖项属性。  前面提到的 <xref:System.Windows.UIElement.IsMouseOver%2A> 属性是以下情形的一个极好的示例：对于定义一个控件的样式非常有用；当用户将鼠标放置在某些控件的定义的区域上方时，一些诸如背景、前景或控件内复合元素的类似属性等可视属性将会发生更改。  属性系统固有的失效过程还可以检测并报告只读依赖项属性发生的更改，这实际上是在内部支持属性触发器功能。  
  
<a name="new"></a>   
## 创建自定义只读依赖项属性  
 请确保已阅读上一节中有关只读依赖项属性对很多典型的依赖项属性情形不起作用的原因。  如果您有适当的方案，则可能希望创建自己的只读依赖项属性。  
  
 创建只读依赖项属性的大部分过程与[自定义依赖项属性](../../../../docs/framework/wpf/advanced/custom-dependency-properties.md)和[实现依赖项属性](../../../../docs/framework/wpf/advanced/how-to-implement-a-dependency-property.md)主题中介绍的内容相同。  其中有三个重要的差异：  
  
-   注册属性时，调用 <xref:System.Windows.DependencyProperty.RegisterReadOnly%2A> 方法而不是常规的 <xref:System.Windows.DependencyProperty.Register%2A> 方法进行属性注册。  
  
-   当实现 [!INCLUDE[TLA2#tla_clr](../../../../includes/tla2sharptla-clr-md.md)]“包装”属性时，请确保该包装也没有设置的实现，以使公开的公共包装的只读状态中不存在不一致现象。  
  
-   只读注册返回的对象是 <xref:System.Windows.DependencyPropertyKey>，而不是 <xref:System.Windows.DependencyProperty>。  您仍应将此字段作为成员存储，但是通常不将其设置为此类型的公共成员。  
  
 当然，无论是用私有字段还是值支持只读依赖项属性，使用任何您决定的逻辑都可以是完全可写的。  但是，无论是在初始状态下，还是在作为运行时逻辑的一部分时，设置该属性最简单的方法是使用属性系统的 [!INCLUDE[TLA2#tla_api#plural](../../../../includes/tla2sharptla-apisharpplural-md.md)]，而不是避开该属性系统和直接设置私有支持字段。  尤其是当存在接受类型 <xref:System.Windows.DependencyPropertyKey> 的参数的 <xref:System.Windows.DependencyObject.SetValue%2A> 的签名的情况时更是如此。  在应用程序逻辑中以编程方式设置此值的方式和位置都将影响可能希望如何设置首次注册依赖项属性时创建的 <xref:System.Windows.DependencyPropertyKey> 上的访问。  如果在可以使此逻辑变为私有的类中处理它，或者需要在程序集（可以在内部设置该逻辑）的其他部分设置该逻辑，  则一种方法是调用关联事件的类事件处理程序内的 <xref:System.Windows.DependencyObject.SetValue%2A>，该关联事件通知类实例：存储的属性值需要进行更改。  另一种方法是通过在注册期间将成对的 <xref:System.Windows.PropertyChangedCallback> 和 <xref:System.Windows.CoerceValueCallback> 回调用作这些属性元数据的一部分来将依赖项属性关联在一起。  
  
 由于 <xref:System.Windows.DependencyPropertyKey> 是私有的，属性系统不会将其传播到代码外，因此只读依赖项属性相对于读写依赖项属性的确具有更好的设置安全。  对于读写依赖项属性，由于标识字段为显式或隐式公开，所以这种属性可广泛设置。  有关详细内容，请参见[依赖项属性的安全性](../../../../docs/framework/wpf/advanced/dependency-property-security.md)。  
  
## 请参阅  
 [依赖项属性概述](../../../../docs/framework/wpf/advanced/dependency-properties-overview.md)   
 [自定义依赖项属性](../../../../docs/framework/wpf/advanced/custom-dependency-properties.md)   
 [样式设置和模板化](../../../../docs/framework/wpf/controls/styling-and-templating.md)