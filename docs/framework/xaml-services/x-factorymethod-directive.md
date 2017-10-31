---
title: "x:FactoryMethod Directive | Microsoft Docs"
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
  - "XAML. x:FactoryMethod directive [XAML Services]"
  - "FactoryMethod directive in XAML [XAML Services]"
  - "x:FactoryMethod directive [XAML Services]"
ms.assetid: 829bcbdf-5318-4afb-9a03-c310e0d2f23d
caps.latest.revision: 8
author: "wadepickett"
ms.author: "wpickett"
manager: "wpickett"
caps.handback.revision: 8
---
# x:FactoryMethod Directive
指定一个构造函数之外的方法，XAML 处理器应使用该方法在解析其后备类型后初始化对象。  
  
## XAML 特性用法，非x:Arguments  
  
```  
<object x:FactoryMethod="methodname"...>  
  ...  
</object>  
```  
  
## XAML 特性用法，x:Arguments 作为元素  
  
```  
<object x:FactoryMethod="methodname"...>  
  <x:Arguments>  
    oneOrMoreObjectElements  
  </x:Arguments>  
</object>  
```  
  
## XAML 值  
  
|||  
|-|-|  
|`methodname`|该 XAML 处理器调用的字符串方法名称，以初始化该指定为 `object` 的实例。  请参见"备注"。|  
|`oneOrMoreObjectElements`|指定工厂方法参数的对象的一个或多个对象元素。  顺序非常重要；它表示应将参数传递到工厂方法签名中的顺序。|  
  
## 备注  
 如果 `methodname` 为实例方法，则无法限定。  
  
 支持将静态方法作为工厂方法。  如果 `methodname` 是静态方法，则 `methodname` 会作为 *typeName* 和 *methodName* 的组合提供，*typeName* 在其中命名了定义静态工厂方法的类。  *typeName* 可以是前缀限定的，前提是涉及映射的 xmlns 中的一种类型。  *typeName* 可以是与 `typeof(``object``)` 不同的类型。  
  
 工厂方法必须为已声明的类型的公共方法，该方法支持相关的对象元素。  
  
 工厂方法必须返回可以指定给相关对象的实例。  工厂方法决不应返回 null。  
  
 `x:Arguments` 以最佳匹配原则对工厂方法的签名进行计算。  匹配将首先计算参数计数。  如果一个参数计数有多个可能的匹配项，则会计算参数类型的值和确定最佳匹配项。  如果在求值的此阶段后仍存在多义性，则 XAML 处理器行为未定义。  
  
 通常，`x:FactoryMethod` 元素用法不是属性元素用法，因为指令标记未引用包含的对象元素类型。  元素用法不如特性用法通用。  `x:Arguments`（特性或元素用法）可连同 `x:FactoryMethod` 元素用法使用，但这并没有专门显示在用法部分。  
  
 `x:FactoryMethod` 作为元素必须在其他所有属性元素之前，并且必须在也作为元素提供的 `x:Arguments` 之前，并必须在任何内容\/内部文本\/初始化文本之前。  
  
## 请参阅  
 [x:Arguments Directive](../../../docs/framework/xaml-services/x-arguments-directive.md)