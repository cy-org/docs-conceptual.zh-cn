---
title: "x:TypeArguments Directive | Microsoft Docs"
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
  - "x:TypeArguments"
  - "xTypeArguments"
  - "TypeArguments"
helpviewer_keywords: 
  - "x:TypeArguments attribute [XAML Services]"
  - "TypeArguments attribute in XAML [XAML Services]"
  - "XAML [XAML Services], x:TypeArguments attribute"
ms.assetid: 86561058-d393-4a44-b5c3-993a4513ea74
caps.latest.revision: 18
author: "wadepickett"
ms.author: "wpickett"
manager: "wpickett"
caps.handback.revision: 18
---
# x:TypeArguments Directive
将泛型的约束类型参数传递给泛型类型的构造函数。  
  
## XAML 属性用法  
  
```  
<object x:TypeArguments="typeString" .../>  
```  
  
## XAML 值  
  
|||  
|-|-|  
|`object`|由 CLR 泛型类型支持的 XAML 类型的对象元素声明。  如果 `object` 不是来自默认 XAML 命名空间的 XAML 类型，则  `object` 需要一个指示 XAML 命名空间的前缀，且该命名空间需有  `object`存在。|  
|`typeString`|将一个或多个 XAML 类型名称声明为字符串的字符串，为 CLR 泛型类型提供类型参数。  有关其他语法说明，请参见备注。|  
  
## 备注  
 在大多数情况下，以用作 `typeString` 字符串中的信息项的 XAML 类型为前缀。  CLR 泛型约束的典型类型（例如 <xref:System.Int32> 和 <xref:System.String>）来自 CLR 基类库。  这些库未映射到典型的特定于框架的默认 XAML 命名空间，因此需要为 XAML 用法进行前缀映射。  
  
 可通过使用命令分隔符指定多个 XAML 类型名称。  
  
 泛型约束自身使用泛型类型，则嵌套的约束类型参数可以用括号 \(\) 括起来。  
  
 请注意，`x:TypeArguments` 的定义特定于 .NET Framework XAML 服务并使用 CLR 支持。  有关语言级别定义，请参见 [\[MS\-XAML\] Section 5.3.11](http://go.microsoft.com/fwlink/?LinkId=114525)（\[MS\-XAML\] 第 5.3.11 节）。  
  
## 用法示例  
 对于这些示例，假定声明了以下 XAML 命名空间定义：  
  
```  
xmlns:sys="clr-namespace:System;assembly=mscorlib"  
xmlns:scg="clr-namespace:System.Collections.Generic;assembly=mscorlib"  
```  
  
### List\<字符串\>  
 `<scg:List x:TypeArguments="sys:String" ...>` 实例化新的带有两个 <xref:System.String> 类型参数的 <xref:System.Collections.Generic.List%601>。  
  
### Dictionary\<字符串,字符串\>  
 `<scg:Dictionary x:TypeArguments="sys:String,sys:String" ...>` 实例化新的带有两个 <xref:System.String> 类型参数的 <xref:System.Collections.Generic.Dictionary%602>。  
  
### Queue\<KeyValuePair\<字符串,字符串\>\>  
 `<scg:Queue x:TypeArguments="scg:KeyValuePair(sys:String,sys:String)" ...>` 实例化新的具有 <xref:System.Collections.Generic.KeyValuePair%602> 约束，带有内部约束类型参数 <xref:System.String> 和 <xref:System.String> 的 <xref:System.Collections.Generic.Queue%601>。  
  
## XAML 2006 和 WPF 泛型 XAML 用法  
 对于 XAML 2006 用法和用于 WPF 应用程序的 XAML，针对 `x:TypeArguments` 和 XAML 的一般泛型类型用法存在以下限制：  
  
-   仅有 XAML 文件的根元素可以支持引用泛型类型的泛型 XAML 用法。  
  
-   根元素必须映射到至少具有一个类型参数的泛型类型。  一个示例是 <xref:System.Windows.Navigation.PageFunction%601>。  这些页面函数是用于 WPF 中的 XAML 泛型用法支持的主要方案。  
  
-   用于泛型的根元素 XAML 对象元素必须也使用 `x:Class`声明一个分部类。  即使定义了 WPF 生成操作，这也为 true。  
  
-   `x:TypeArguments` 不能引用嵌套的泛型约束。  
  
## 无 WPF 3.0 或 WPF 3.5 依赖项的 XAML 2009 或 XAML 2006  
 在 XAML 2006 或 XAML 2009 的 .NET Framework XAML 服务中，放宽了泛型 XAML 用法中的相关 WPF 限制。  您可以实例化泛型对象元素，可以支持后备类型系统和对象模型的 XAML 标记中的任何位置处。  
  
 如果使用 XAML 2009，而不是映射 CLR 基类来获取常用语言基元的 XAML 类型，则可以使用 [常用 XAML 语言基元的内置类型](../../../docs/framework/xaml-services/built-in-types-for-common-xaml-language-primitives.md)作为 `typeString` 中的信息项。  例如，可以声明以下内容（不显示前缀映射，但 x 是用于 XAML 2009 的 XAML 语言 XAML 命名空间）：  
  
```  
<my:BusinessObject x:TypeArguments="x:String,x:Int32"/>  
```  
  
 在 WPF 中面向 [!INCLUDE[net_v40_long](../../../includes/net-v40-long-md.md)]时，您可将 XAML 2009 功能与 `x:TypeArguments` 结合在一起使用，但仅用于宽松 XAML（未进行标记编译的 XAML）。  WPF 的已编译标记的 XAML 以及 XAML 的 BAML 形式当前不支持 XAML 2009 关键字和功能。  如果需要标记编译 XAML，则您必须在“XAML 2006 和 WPF 通用 XAML 用法”一节中说明的限制下进行操作。  
  
## 请参阅  
 [x:Class Directive](../../../docs/framework/xaml-services/x-class-directive.md)   
 [x:Type Markup Extension](../../../docs/framework/xaml-services/x-type-markup-extension.md)   
 [常见 XAML 语言基元的内置类型](../../../docs/framework/xaml-services/built-in-types-for-common-xaml-language-primitives.md)   
 [Generics in XAML](../../../docs/framework/xaml-services/generics-in-xaml.md)