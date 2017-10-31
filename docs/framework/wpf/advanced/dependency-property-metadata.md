---
title: "依赖项属性元数据 | Microsoft Docs"
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
  - "API, 元数据"
  - "依赖项属性, 元数据"
  - "元数据, 用于依赖项属性"
  - "重写元数据"
ms.assetid: d01ed009-b722-41bf-b82f-fe1a8cdc50dd
caps.latest.revision: 24
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 23
---
# 依赖项属性元数据
[!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)] 属性系统包括一个元数据报告系统，该系统不局限于可以通过反射或常规[!INCLUDE[TLA#tla_clr](../../../../includes/tlasharptla-clr-md.md)] 特征报告的关于某个属性的内容。  [依赖项属性](GTMT)的元数据还可以由定义[依赖项属性](GTMT)的类来唯一地指定，可以在[依赖项属性](GTMT)添加到另一个类时进行更改，可以由所有从定义基类继承[依赖项属性](GTMT)的派生类来明确地重写。  
  
   
  
<a name="prerequisites"></a>   
## 必备组件  
 本主题假设您从 [!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)] 类的现有依赖项属性的使用者角度了解依赖项属性，并且已阅读[依赖项属性概述](../../../../docs/framework/wpf/advanced/dependency-properties-overview.md)。  若要采用本主题中的示例，还应当了解 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] 并知道如何编写 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 应用程序。  
  
<a name="dp_metadata_contents"></a>   
## 依赖项属性元数据的使用方式  
 依赖项属性的元数据作为一个对象存在，可以通过查询该对象来检查依赖项属性的特征。  当属性系统处理任何给定的依赖项属性时，也会经常访问这些元数据。  依赖项属性的元数据对象可以包含以下类型的信息：  
  
-   依赖项属性的默认值（如果通过本地值、样式和继承等信息不能确定依赖项属性的其他任何值）。  有关在为依赖项属性赋值时，默认值如何参与属性系统所使用的优先级的完整讨论，请参见[依赖项属性值优先级](../../../../docs/framework/wpf/advanced/dependency-property-value-precedence.md)。  
  
-   对影响每个所有者类型的强制行为或更改通知行为的回调实现的引用。  请注意，这些回调通常是用非公共访问级别定义的，因此，除非实际引用位于您允许的访问范围内，否则通常无法从元数据获得这些引用。  有关依赖项属性回调的更多信息，请参见[依赖项属性回调和验证](../../../../docs/framework/wpf/advanced/dependency-property-callbacks-and-validation.md)。  
  
-   如果所讨论的依赖项属性被视为一个 [WPF 框架级别](GTMT)的属性，则元数据中可能包含 [WPF 框架级别](GTMT)的依赖项属性特征，这些特征报告各种服务（如 [WPF 框架级别](GTMT)的布局引擎和属性继承逻辑）的信息和状态。  有关依赖项属性元数据的这一方面的更多信息，请参见[框架属性元数据](../../../../docs/framework/wpf/advanced/framework-property-metadata.md)。  
  
<a name="APIs"></a>   
## 元数据 API  
 可报告属性系统所使用的大部分元数据信息的类型是 <xref:System.Windows.PropertyMetadata> 类。  在向属性系统注册依赖项属性时，可以选择指定元数据实例，并且可以为以下附加类型再次指定这些实例：将自身作为所有者添加，或者重写它们从基类依赖项属性定义继承的元数据  （如果在注册属性时未指定元数据，则将使用该类的默认值来创建默认 <xref:System.Windows.PropertyMetadata>）。当您针对 <xref:System.Windows.DependencyObject> 实例调用各种从依赖项属性获取元数据的 <xref:System.Windows.DependencyProperty.GetMetadata%2A> 重载时，所注册的元数据将作为 <xref:System.Windows.PropertyMetadata> 返回。  
  
 随后将从 <xref:System.Windows.PropertyMetadata> 类派生，以便为结构区域（如 [WPF 框架级别](GTMT)的类）提供更具体的元数据。  <xref:System.Windows.UIPropertyMetadata> 添加动画报告功能，<xref:System.Windows.FrameworkPropertyMetadata> 提供上一节中提到的 [WPF 框架级别](GTMT)的属性。  在注册了依赖项属性之后，可以将它们注册到这些 <xref:System.Windows.PropertyMetadata> 派生类中。  在检查了元数据之后，可以将 <xref:System.Windows.PropertyMetadata> 基类型强制转换为派生类，这样您就可以检查更具体的属性。  
  
> [!NOTE]
>  在本文档中，有时将可以在 <xref:System.Windows.FrameworkPropertyMetadata> 中指定的属性特征称为“标志”。  在新建要用于注册依赖项属性或重写元数据的元数据实例时，将使用按标志枚举 <xref:System.Windows.FrameworkPropertyMetadataOptions> 来指定这些值，然后向 <xref:System.Windows.FrameworkPropertyMetadata> 构造函数提供枚举的可能连接值。  但是，一经构造，这些选项特征就会在 <xref:System.Windows.FrameworkPropertyMetadata> 中作为一系列布尔属性公开，而不是构造枚举值。  使用布尔属性，您可以检查每个条件，而不必为了获得感兴趣的信息而向按标志枚举值应用掩码。  构造函数使用连接的 <xref:System.Windows.FrameworkPropertyMetadataOptions> 使构造函数签名保持合理的长度，而实际构造的元数据公开不同的属性，使元数据的查询变得更加直观。  
  
<a name="override_or_subclass"></a>   
## 何时重写元数据以及何时派生类  
 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 属性系统已经建立了如下功能：在不必完全重新实现依赖项属性的情况下，更改依赖项属性的某些特征。  这是通过为特定类型上所存在的依赖项属性构造不同的属性元数据实例来完成的。  请注意，现有的大多数依赖项属性都不是虚拟属性，因此，严格地说，只能通过隐藏现有成员来针对继承类“重新实现”依赖项属性。  
  
 如果您尝试对某个类型的依赖项属性启用的方案不能通过修改现有依赖项属性的特征来完成，则可能有必要创建一个派生类，然后为该派生类声明一个自定义依赖项属性。  自定义依赖项属性与 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] [!INCLUDE[TLA#tla_api#plural](../../../../includes/tlasharptla-apisharpplural-md.md)] 定义的依赖项属性具有相同的行为。  有关自定义依赖项属性的更多详细信息，请参见[自定义依赖项属性](../../../../docs/framework/wpf/advanced/custom-dependency-properties.md)。  
  
 您不能重写的依赖项属性的一个显著特征就是它的值类型。  如果您要继承的依赖项属性的行为与所需的行为大体相同，但是您要求它具有另一种类型，则必须实现一个自定义依赖项属性，可能还需要通过类型转换或其他实现机制在自定义类上链接这些属性。  而且，您不能替换现有的 <xref:System.Windows.ValidateValueCallback>，因为这个回调存在于注册字段本身，而不是存在于它的元数据中。  
  
<a name="scenarios"></a>   
## 更改现有元数据的方案  
 如果要处理现有依赖项属性的元数据，则更改依赖项属性元数据的一种常见方案是更改默认值。  更改或添加属性系统回调是一种更高级的方案。  如果您所实现的派生类的依赖项属性之间具有不同的相互关系，则您可能希望这样做。  让编程模型既支持代码又支持声明性用法的条件之一就是，属性必须能够按任何顺序设置。  因此，需要在没有上下文的情况下实时设置任何依赖项属性，而且可以不必知道设置顺序（例如，可能在构造函数中找到的顺序）。  有关属性系统的这一方面的更多信息，请参见[依赖项属性回调和验证](../../../../docs/framework/wpf/advanced/dependency-property-callbacks-and-validation.md)。  请注意，验证回调不是元数据的一部分，而是依赖项属性标识符的一部分。  因此，不能通过重写元数据来更改验证回调。  
  
 在某些情况下，您可能还希望在现有的依赖项属性上改变 [WPF 框架级别](GTMT)的属性元数据选项。  这些选项将有关 [WPF 框架级别](GTMT)属性的某些已知条件传递到其他 [WPF 框架级别](GTMT)的进程，如布局系统。  通常，只有在注册新的依赖项属性时，才设置这些选项，但是也可以在调用 <xref:System.Windows.DependencyProperty.OverrideMetadata%2A> 或 <xref:System.Windows.DependencyProperty.AddOwner%2A> 的过程中更改 [WPF 框架级别](GTMT)属性的元数据。  有关要使用的特定值以及更多信息，请参见[框架属性元数据](../../../../docs/framework/wpf/advanced/framework-property-metadata.md)。  有关应当如何为新注册的依赖项属性设置这些选项的更多信息，请参见[自定义依赖项属性](../../../../docs/framework/wpf/advanced/custom-dependency-properties.md)。  
  
<a name="dp_override_metadata"></a>   
### 重写元数据  
 重写元数据的主要目的在于，使您有机会更改各种派生自元数据的行为，这些行为应用于您的类型上所存在的依赖项属性。  [元数据](#dp_metadata_contents)一节中更详细地介绍了重写元数据的原因。  有关更多信息（包括一些代码示例），请参见[重写依赖项属性的元数据](../../../../docs/framework/wpf/advanced/how-to-override-metadata-for-a-dependency-property.md)。  
  
 在注册调用 \(<xref:System.Windows.DependencyProperty.Register%2A>\) 过程中可以为依赖项属性提供属性元数据。  但是，在许多情况下，当您的类继承该依赖项属性时，您可能希望为该类提供特定于类型的元数据。  这可以通过调用 <xref:System.Windows.DependencyProperty.OverrideMetadata%2A> 方法来完成。  对于 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] [!INCLUDE[TLA2#tla_api#plural](../../../../includes/tla2sharptla-apisharpplural-md.md)] 中的示例，<xref:System.Windows.FrameworkElement> 类是第一个注册 <xref:System.Windows.UIElement.Focusable%2A> 依赖项属性的类型。  但是，<xref:System.Windows.Controls.Control> 类会重写该依赖项属性的元数据以提供自己的初始默认值，将它从 `false` 改为 `true`，并以其他方式重用最初的 <xref:System.Windows.UIElement.Focusable%2A> 实现。  
  
 当您重写元数据时，系统会合并或更换不同的元数据特征。  
  
-   将合并 <xref:System.Windows.PropertyMetadata.PropertyChangedCallback%2A>。  如果您添加一个新的 <xref:System.Windows.PropertyMetadata.PropertyChangedCallback%2A>，则该回调将存储在元数据中。  如果您没有在重写中指定 <xref:System.Windows.PropertyMetadata.PropertyChangedCallback%2A>，则 <xref:System.Windows.PropertyMetadata.PropertyChangedCallback%2A> 的值会从在元数据中指定它的最近上级提升为一个引用。  
  
-   <xref:System.Windows.PropertyMetadata.PropertyChangedCallback%2A> 的实际属性系统行为是：层次结构中所有元数据所有者的实现都保留并添加到表中，属性系统的执行顺序是首先调用最深派生类的回调。  
  
-   将替换 <xref:System.Windows.PropertyMetadata.DefaultValue%2A>。  如果您没有在重写中指定 <xref:System.Windows.PropertyMetadata.DefaultValue%2A>，则 <xref:System.Windows.PropertyMetadata.DefaultValue%2A> 的值从在元数据中指定它的最近上级获取。  
  
-   将替换 <xref:System.Windows.PropertyMetadata.CoerceValueCallback%2A> 实现。  如果您添加一个新的 <xref:System.Windows.PropertyMetadata.CoerceValueCallback%2A>，则该回调将存储在元数据中。  如果您没有在重写中指定 <xref:System.Windows.PropertyMetadata.CoerceValueCallback%2A>，则 <xref:System.Windows.PropertyMetadata.CoerceValueCallback%2A> 的值会从在元数据中指定它的最近上级提升为一个引用。  
  
-   属性系统的行为是仅调用直接元数据中的 <xref:System.Windows.PropertyMetadata.CoerceValueCallback%2A>，  而不保留对层次结构中所实现的其他 <xref:System.Windows.PropertyMetadata.CoerceValueCallback%2A> 的引用。  
  
 此行为由 <xref:System.Windows.PropertyMetadata.Merge%2A> 实现，并且可以由派生的元数据类重写。  
  
#### 重写附加属性元数据  
 在 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 中，[附加属性](GTMT)作为依赖项属性来实现。  这意味着它们还具有能够由个别类重写的属性元数据。  关于 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 中的附加属性的范围，通常需要注意：可以针对任何 <xref:System.Windows.DependencyObject> 设置附加属性。  因此，任何 <xref:System.Windows.DependencyObject> 派生类都可以重写任何附加属性的元数据，就好像它们是在类的实例上设置的一样。  您可以重写默认值、回调或 [WPF 框架级别](GTMT)的特征报告属性。  如果针对类的实例设置了附加属性，则这些重写属性元数据特征将适用。  例如，您可以重写默认值，这样，只要未以其他方式设置附加属性，您的重写值就将报告为类实例的附加属性的值。  
  
> [!NOTE]
>  <xref:System.Windows.FrameworkPropertyMetadata.Inherits%2A> 属性与附加属性无关。  
  
<a name="dp_add_owner"></a>   
### 将类作为现有依赖项属性的所有者来添加  
 通过使用 <xref:System.Windows.DependencyProperty.AddOwner%2A> 方法，类可以将自身作为已注册的依赖项属性的所有者来添加。  这使得该类可以使用最初针对另一个类型注册的依赖项属性。  添加类通常不是首先将该依赖项属性注册为所有者的类型的派生类。  实际上，这使您的类及其派生类可以“继承”[依赖项属性](GTMT)实现，而不需要最初的所有者类，而且添加类也不必位于同一个实际的类层次结构中。  另外，添加类（以及所有派生类）随后可以为最初的依赖项属性提供特定于类型的元数据。  
  
 添加类除了通过属性系统的实用工具方法将自身添加为所有者以外，还应当在自身声明其他公共成员，以使[依赖项属性](GTMT)向代码和标记公开，从而完全参与属性系统。  就为依赖项属性公开对象模型而言，添加现有依赖项属性的类与定义新的自定义依赖项属性的类具有相同的职责。  要公开的第一个此类成员是依赖项属性标识符字段。  此字段应当是类型为 <xref:System.Windows.DependencyProperty> 的 `public static readonly` 字段，此类型将赋予 <xref:System.Windows.DependencyProperty.AddOwner%2A> 调用的返回值。  要定义的第二个成员是[!INCLUDE[TLA#tla_clr](../../../../includes/tlasharptla-clr-md.md)]“包装”属性。  使用包装，可以更方便地在代码中操作依赖项属性（您应当避免每次都调用 <xref:System.Windows.DependencyObject.SetValue%2A>，而且在包装本身只能发出该调用一次）。  包装的实现方式与您在注册自定义[依赖项属性](GTMT)时的实现方式完全相同。  有关实现[依赖项属性](GTMT)的更多信息，请参见[自定义依赖项属性](../../../../docs/framework/wpf/advanced/custom-dependency-properties.md)和[为依赖项属性添加所有者类型](../../../../docs/framework/wpf/advanced/how-to-add-an-owner-type-for-a-dependency-property.md)。  
  
#### AddOwner 和附加属性  
 对于由所有者类定义为附加属性的依赖项属性，可以调用 <xref:System.Windows.DependencyProperty.AddOwner%2A>。  这样做的目的通常是为了将以前附加的属性作为非附加依赖项属性来公开。  随后您将 <xref:System.Windows.DependencyProperty.AddOwner%2A> 返回值作为一个要用作依赖项属性标识符的 `public static readonly` 字段来公开，并将定义相应的“包装”属性，以便该属性出现在成员表中并支持在您的类中使用非附加属性。  
  
## 请参阅  
 <xref:System.Windows.PropertyMetadata>   
 <xref:System.Windows.DependencyObject>   
 <xref:System.Windows.DependencyProperty>   
 <xref:System.Windows.DependencyProperty.GetMetadata%2A>   
 [依赖项属性概述](../../../../docs/framework/wpf/advanced/dependency-properties-overview.md)   
 [框架属性元数据](../../../../docs/framework/wpf/advanced/framework-property-metadata.md)