---
title: "x:Arguments Directive | Microsoft Docs"
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
  - "x:Arguments directive [XAML Services]"
  - "Arguments directive in XAML [XAML Services]"
  - "XAML [XAML Services], x:Arguments directive"
ms.assetid: 87cc10b0-b610-4025-b6b0-ab27ca27c92e
caps.latest.revision: 12
author: "wadepickett"
ms.author: "wpickett"
manager: "wpickett"
caps.handback.revision: 12
---
# x:Arguments Directive
在 XAML 中为非默认构造函数的对象元素声明或工厂方法对象声明打包构造参数。  
  
## XAML 元素用法（非默认构造函数）  
  
```  
<object ...>  
  <x:Arguments>  
    oneOrMoreObjectElements  
  </x:Arguments>  
</object>  
```  
  
## XAML 元素用法（工厂方法）  
  
```  
<object x:FactoryMethod="methodName"...>  
  <x:Arguments>  
    oneOrMoreObjectElements  
  </x:Arguments>  
</object>  
```  
  
## XAML 值  
  
|||  
|-|-|  
|`oneOrMoreObjectElements`|一个以上对象元素，指定参数要传递到的后备非默认构造函数或工厂方法。<br /><br /> 典型用途是用于初始化对象元素中的文本，以指定实际的参数值。  请参见示例部分。<br /><br /> 元素的顺序有意义。  顺序中的 XAML 类型必须与后备构造函数或工厂方法重载的类型和类型顺序相匹配。|  
|`methodName`|应能处理任何 `x:Arguments` 自变量的工厂方法的名称。|  
  
## 依赖项  
 `x:FactoryMethod` 可以修改范围和行为，其中 `x:Arguments` 适用。  
  
 如果没有指定 `x:FactoryMethod`，则 `x:Arguments` 适用于后备构造函数的备用（非默认）签名。  
  
 如果指定 `x:FactoryMethod`，则 `x:Arguments` 将适用于命名方法的重载。  
  
## 备注  
 XAML 2006 可支持通过初化文本进行非默认初始化。  但是，初始化文本构造种技术的实际应用是有限的。  初始化文本被视为一个单独的文本字符串；因此，它只会添加初始化单个参数的功能，除非对类型转换器定义了可分析自定义信息项并可自定义字符串中的分隔符的构造行为。  此外，文本字符串到对象逻辑可能是给定的 XAML 分析器的本机默认基元类型转换器，而不是真字符串。  
  
 `x:Arguments` XAML 元素用法不是属性元素用法，因为指令标记未引用包含的对象元素类型。  它更类似于诸如 `x:Code` 这样的其他指令。在这些指令中元素区分出一个范围，在这个范围中标记并非子内容的默认值。  在这种情况下，每个对象元素的 XAML 类型与有关参数类型的信息进行通信，XAML 分析器会使用此信息确定 `x:Arguments` 使用率试图引用的特定构造函数工厂方法签名。  
  
 要构造的对象元素的 `x:Arguments` 必须在其他所有属性元素之前，并且必须在对象元素的内容、内部文本、初始化字符串之前。  `x:Arguments` 内的对象元素，如同 XAML 类型及其后备构造函数或工厂方法允许的那样，可以包括特性和初始化字符串。  对于对象或参数，您可以指定自定义 XAML 类型或通过引用既定前缀映射在默认 XAML 命名空间外的 XAML 类型。  
  
 XAML 处理器使用以下准则来确定 `x:Arguments` 中指定的参数应如何用于构造对象。  如果指定了 `x:FactoryMethod`，则会将信息比作指定的 `x:FactoryMethod`（请注意，`x:FactoryMethod` 值为方法名称，命名的方法可以包含重载。  如果未指定 `x:FactoryMethod`，则将信息比作对象的所有公共构造函数重载集。  然后，XAML 处理逻辑将比较参数的数目，并根据匹配的参数数量选择过载。  如果存在多个匹配项，则 XAML 处理器应基于提供的对象元素的 XAML 类型，比较参数的类型。  如果仍存在多个匹配项，则 XAML 处理器行为未定义。  如果指定 `x:FactoryMethod` 但未能解析方法，则 XAML 处理器应引发异常。  
  
 从技术上来说，XAML 特性用法 `<x:Arguments>string</x:Arguments>` 是可行的。  但是，这不提供功能之外的功能，否则初始化文本和类型装换器，本语法使用等功能都不是 XAML 2009 工厂方法功能的设计目标。  
  
## 示例  
 以下示例显示了一个非默认的构造函数的签名，然后显示了访问该签名的 `x:Arguments` 的 XAML 用法。  
  
```csharp  
public class Food {  
    private string _name;  
    private Int32 _calories;  
    public Food(string name, Int32 calories) {  
        _name=name;  
        _calories=calories;  
    }  
}  
```  
  
```  
<my:Food>  
    <x:Arguments>  
        <x:String>Apple</x:String>  
        <x:Int32>150</x:Int32>  
    </x:Arguments>  
</my:Food>  
```  
  
 以下示例显示了一个目标工厂方法的签名，然后显示了访问该签名的 `x:Arguments` 的 XAML 用法。  
  
```csharp  
public Food TryLookupFood(string name)  
{  
  switch (name) {  
    case "Apple": return new Food("Apple",150);  
    case "Chocolate": return new Food("Chocolate",200);  
    case "Cheese": return new Food("Cheese", 450);  
    default: {return new Food(name,0);  
  }  
}  
```  
  
```  
<my:Food x:FactoryMethod="TryLookupFood">  
    <x:Arguments>  
        <x:String>Apple</x:String>  
    </x:Arguments>  
</my:Food>  
```  
  
## 请参阅  
 [Defining Custom Types for Use with .NET Framework XAML Services](../../../docs/framework/xaml-services/defining-custom-types-for-use-with-net-framework-xaml-services.md)   
 [XAML 概述 \(WPF\)](../../../ocs/framework/wpf/advanced/xaml-overview-wpf.md)