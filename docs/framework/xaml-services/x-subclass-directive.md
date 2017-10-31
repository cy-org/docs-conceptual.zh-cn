---
title: "x:Subclass Directive | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-wpf"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "Subclass"
  - "xSubclass"
  - "x:Subclass"
helpviewer_keywords: 
  - "x:Subclass attribute [XAML Services]"
  - "XAML [XAML Services], x:Subclass attribute"
  - "Subclass attribute in XAML [XAML Services]"
ms.assetid: 99f66072-8107-4362-ab99-8171dc83b469
caps.latest.revision: 20
author: "wadepickett"
ms.author: "wpickett"
manager: "wpickett"
caps.handback.revision: 20
---
# x:Subclass Directive
在同时提供了 `x:Class` 的情况下，修改 XAML 标记编译行为。  不必根据 `x:Class` 类创建分部类，而是将提供的 `x:Class` 创建为中间类，然后提供的派生类应基于 `x:Class`。  
  
## XAML 属性用法  
  
```  
<object x:Class="namespace.classname" x:Subclass="subclassNamespace.subclassName">  
   ...  
</object>  
```  
  
## XAML 值  
  
|||  
|-|-|  
|`namespace`|可选。  指定一个包含 `classname` 的 CLR 命名空间。  如果指定了 `namespace`，则用一个点 \(.\) 来分隔 `namespace` 和 `classname`。|  
|`classname`|必选。  指定连接加载的 XAML 和该 XAML 的代码隐藏的分部类的 CLR 名称。  请参见"备注"。|  
|`subclassNamespace`|可选。  如果每个命名空间可以解析另一个命名空间，该值可以不同于 `namespace`。  指定一个包含 `subclassName` 的 CLR 命名空间。  如果指定了 `subclassName`，则用一个点 \(.\) 来分隔 `subclassNamespace` 和 `subclassName`。|  
|`subclassName`|必选。  指定子类的 CLR 名称。|  
  
## 依赖项  
 还必须对同一对象提供 [x:Class Directive](../../../docs/framework/xaml-services/x-class-directive.md)，且该对象必须是 XAML 生产的根元素。  
  
## 备注  
 `x:Subclass` 用法主要针对不支持分部类声明的语言。  
  
 用作 `x:Subclass` 的类不能为嵌套类，且 `x:Subclass` 必须引用根对象，如上文“依赖项”一节所解释的那样。  
  
 否则，`x:Subclass` 的概念性含义不由 .NET Framework XAML 服务实现定义。  这是因为 .NET Framework XAML 服务行为不指定通过其连接 XAML 标记和备份代码的整个编程模型。  与 `x:Class` 和 `x:Subclass` 有关的更多概念的实现是由使用编程模型或应用程序模型来定义如何连接 XAML 标记、已编译标记和基于 CLR 代码隐藏的特定框架执行的。  每个框架可能都具有其自己的生成操作，该生成操作启用一些必须包含在生产环境中的行为或特定组件。  在框架中，生成操作也可由于用于代码隐藏的特定 CLR 语言的不同而不同。  
  
## WPF 用法说明  
 `x:Subclass` 可以位于页面根元素上，或位于应用程序定义中的 <xref:System.Windows.Application> 根元素上，且此根元素已经具有 `x:Class`。  无论对页或应用程序根之外的任何元素声明 `x:Subclass` ，还是在不存在 `x:Class` 的情况下指定它，都会导致编译时错误。  
  
 创建完全适用于 `x:Subclass` 方案的派生类非常复杂。  您可能需要检查中间文件（标记编译时项目的 obj 文件夹中产生的 .g 文件，其名称合并了 .xaml 文件名）。  这些中间文件有助于在编译的应用程序的联接分部类中确定某些编程构造的源。  
  
 派生类中的事件处理程序必须是 `internal override`（在 [!INCLUDE[TLA#tla_visualb](../../../includes/tlasharptla-visualb-md.md)] 中必须是 `Friend Overrides`），才能重写编译期间在中间类中创建的处理程序的存根。  否则，派生类实现将隐藏中间类实现，并且中间类处理程序无法被调用。  
  
 如果您既定义了 `x:Class`，又定义了 `x:Subclass`，则不必为 `x:Class` 引用的类提供任何实现。  您只需通过 `x:Class` 特性为它指定一个名称，以便编译器为在中间文件中创建的类提供一些指导（此时编译器不会选择默认名称）。  可对 `x:Class` 类给出实现；但是，这不是使用 `x:Class` 和 `x:Subclass` 的典型方案。  
  
## 请参阅  
 [x:Class Directive](../../../docs/framework/xaml-services/x-class-directive.md)   
 [XAML 及 WPF 的自定义类](../../../ocs/framework/wpf/advanced/xaml-and-custom-classes-for-wpf.md)