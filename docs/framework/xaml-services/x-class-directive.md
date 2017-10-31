---
title: "x:Class Directive | Microsoft Docs"
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
  - "x:Class"
  - "xClass"
  - "Class"
helpviewer_keywords: 
  - "Class attribute in XAML [XAML Services]"
  - "XAML [XAML Services], x:Class attribute"
  - "x:Class attribute [XAML Services]"
ms.assetid: bc4a3d8e-76e2-423e-a5d1-159a023e82ec
caps.latest.revision: 27
author: "wadepickett"
ms.author: "wpickett"
manager: "wpickett"
caps.handback.revision: 26
---
# x:Class Directive
配置 XAML 标记编译以便在标记与代码隐藏之间联接分部类。  代码分部类用 [!INCLUDE[TLA#tla_cls](../../../includes/tlasharptla-cls-md.md)] 语言在单独的代码文件中定义，而标记分部类由代码生成通常在 XAML 编译期间创建。  
  
## XAML 属性用法  
  
```  
<object x:Class="namespace.classname"...>  
  ...  
</object>  
```  
  
## XAML 值  
  
|||  
|-|-|  
|`namespace`|可选。  指定一个包含由 `classname` 标识的分部类的 [!INCLUDE[TLA2#tla_clr](../../../includes/tla2sharptla-clr-md.md)] 命名空间。  如果指定了 `namespace`，则用一个点 \(.\) 来分隔 `namespace` 和 `classname`。  请参见"备注"。|  
|`classname`|必选。  指定将加载的 XAML 与该 XAML 的代码隐藏相连接的分部类的 [!INCLUDE[TLA2#tla_clr](../../../includes/tla2sharptla-clr-md.md)] 名称。|  
  
## 依赖项  
 `x:Class` 只能在 XAML 生产的根元素上指定。  如果对象在 XAML 生产上有父级，`x:Class` 在任何这样的对象上都无效。  有关更多信息，请参见 [\[MS\-XAML\] Section 4.3.1.6](http://go.microsoft.com/fwlink/?LinkId=114525)（\[MS\-XAML\] 第 4.3.1.6 节）。  
  
## 备注  
 `namespace` 本身可能包含其他点以将相关命名空间组织到名称层次结构中，这是一种在 .NET 编程中常见的技术。  仅将 `x:Class` 值的字符串中的最后一个点解释为隔开 `namespace` 和 `classname.` 。用作 `x:Class` 的类不能是嵌套类。  如果允许嵌套类，则会因确定 `x:Class` 字符串的点的含义是不明确的而不允许嵌套类。  
  
 在现有的使用 `x:Class` 的编程模型中，如果没有代码隐藏的 XAML 页面是完全无效的，则 `x:Class` 是可选的。  这种功能将与生成操作交互，如使用 XAML 的框架所实现。  `x:Class` 功能也受应用程序模型中、以及相应的生成操作中的 XAML 指定内容的各种类型拥有的角色的影响。  如果 XAML 声明了事件处理特性值，或者实例化了其定义类位于代码隐藏类中的自定义元素，则必须为代码隐藏提供对适当类的 `x:Class` 指令引用（或 [x:Subclass](../../../docs/framework/xaml-services/x-subclass-directive.md)）。  
  
 `x:Class` 指令的值必须是一个指定某个类的完全限定名称的字符串，但不含任何程序集信息（等效于 <xref:System.Type.FullName%2A?displayProperty=fullName>）。  对于简单的应用程序，如果命名空间信息与代码隐藏的构建方式相同（代码定义从类级别开始），就可以省略 CLR 命名空间信息。  
  
 页面或应用程序定义的代码隐藏文件必须在代码文件内，而该代码文件应作为产生已编译应用程序和涉及标记编译的项目的一部分包括在该项目中。  必须遵循 CLR 类的命名规则。  有关更多信息，请参见 [Framework 设计准则](../../../ml/index.xml)。  默认情况下，代码隐藏类必须是 `public`；但可以通过使用 [x:ClassModifier Directive](../../../docs/framework/xaml-services/x-classmodifier-directive.md)在其他访问级别定义它。  
  
 `x:Class` 特性的此确切解释仅适用于基于 CLR 的 XAML 实现，特别是 .NET Framework XAML 服务。  不基于 CLR 和不使用 .NET Framework XAML 服务的其他 XAML 实现可能为连接 XAML 标记和备份运行时代码使用不同的解析公式。  有关 `x:Class` 的更多常规解释的更多信息，请参见 [\[MS\-XAML\]](http://go.microsoft.com/fwlink/?LinkId=114525)\(\[MS\-XAML\]\)。  
  
 在某种级别的结构中，`x:Class` 的性含义未在 .NET Framework XAML 服务中定义。  这是因为 .NET Framework XAML 服务不指定通过其连接 XAML 标记和备份代码的编程模型。  `x:Class` 指令的其他用法可以由使用编程模型或应用程序模型来定义如何连接 XAML 标记和基于 CLR 代码隐藏的特定框架实现。  每个框架可以都具有其自己的生成操作，该生成操作启用一些必须包含在生产环境中的行为或特定组件。  在框架中，生成操作也可由于用于代码隐藏的特定 CLR 语言的不同而不同。  
  
## x: Class 位于 WPF 编程模型中  
 在 WPF 应用程序和 WPF 应用程序模型中，`x:Class` 可以声明为充当 XAML 文件的根并且正在编译（XAML 通过 `Page` 生成操作包括在 WPF 应用程序项目中）的任何元素的特性，也可以声明为已编译 WPF 应用程序的应用程序定义中的 <xref:System.Windows.Application> 根的特性。  在页面根元素或应用程序根元素之外的任何元素上，以及在未编译的 WPF XAML 文件的任何环境下声明  `x:Class` 都会在 [!INCLUDE[net_v30_short](../../../includes/net-v30-short-md.md)] 和 [!INCLUDE[net_v35_short](../../../includes/net-v35-short-md.md)]下的 WPF XAML 编译器引起编译时错误。  关于在 WPF 中处理的 `x:Class` 的其他方面的信息，请参见 [WPF 中的代码隐藏和 XAML](../../../ocs/framework/wpf/advanced/code-behind-and-xaml-in-wpf.md)。  
  
## Windows Workflow Foundation 的 x:Class  
 对于窗口基础工作流，`x:Class` 命名了完全在 XAML 中组成的自定义活动的类或通过代码隐藏为活动设计器命名 XAML 页面的部分类。  
  
## Silverlight Usage 备注。  
 单独说明了 `x:Class` for Silverlight。  更多信息，请参见 [XAML Namespace \(x:\) Language Features \(Silverlight\)](http://go.microsoft.com/fwlink/?LinkId=199081) 。  
  
## 请参阅  
 [x:Subclass Directive](../../../docs/framework/xaml-services/x-subclass-directive.md)   
 [XAML 及 WPF 的自定义类](../../../ocs/framework/wpf/advanced/xaml-and-custom-classes-for-wpf.md)   
 [x:ClassModifier Directive](../../../docs/framework/xaml-services/x-classmodifier-directive.md)   
 [Types Migrated from WPF to System.Xaml](../../../docs/framework/xaml-services/types-migrated-from-wpf-to-system-xaml.md)