---
title: "类、 结构和接口的名称 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "VB"
  - "CSharp"
  - "C++"
  - "jsharp"
helpviewer_keywords: 
  - "指导原则的类型名称"
  - "名称的类 [.NET Framework]"
  - "名称的枚举 [.NET Framework]"
  - "接口的名称 [.NET Framework]"
  - "通用类型名称"
  - "名称 [.NET Framework]，类型名称"
  - "类的名称 [.NET Framework]"
  - "名称的接口 [.NET Framework]"
  - "泛型类型参数"
ms.assetid: 87a4b0da-ed64-43b1-ac43-968576c444ce
caps.latest.revision: 16
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 16
---
# 类、 结构和接口的名称
请按照命名准则适用于常规类型命名。  
  
 **✓ 执行** 命名类和结构用名词或名词短语，使用 PascalCasing。  
  
 这区分开来的类型名称以动词短语命名的方法。  
  
 **✓ 执行** 命名接口使用形容词短语以及有时与名词或名词短语。  
  
 应很少使用名词和名词短语，它们可能指示该类型应为一个抽象类，而不是接口。  
  
 **X 不** 为类名前缀 \(例如，"C"\)。  
  
 **✓ 请考虑** 结束的名称的派生类同名的类的基类。  
  
 这是非常易读，清楚地说明了该关系。 这在代码中的一些示例包括︰ `ArgumentOutOfRangeException`, ，这是一种类型的 `Exception`, ，和 `SerializableAttribute`, ，这是一种类型的 `Attribute`。 但是，很重要使用合理判断中应用这一准则;例如， `Button` 类是一种类型的 `Control` 事件，尽管 `Control` 没有出现在它的名称。  
  
 **✓ 执行** 前缀接口名称以字母 I，以指示该类型为接口。  
  
 例如， `IComponent` （描述性名词） `ICustomAttributeProvider` （名词短语） 和 `IPersistable` （形容词） 都是适当的接口名称。 与其他类型名称，避免缩写。  
  
 **✓ 执行** 确保名称与仅由"I"前缀上的接口名称在定义类 – 接口对其中类是接口的标准实现时不同。  
  
## 泛型类型参数的名称  
 中增加了.NET Framework 2.0 的泛型。 此功能引入了一种新的标识符称为 *类型参数*。  
  
 **✓ 执行** 具有描述性名称命名的泛型类型参数，除非单个字母的名称是完全很容易理解，并且一个描述性名称将不会增加价值。  
  
 **✓ 请考虑** 使用 `T` 作为具有单个字母类型参数的类型的类型参数名。  
  
```  
public int IComparer<T> { ... }  
public delegate bool Predicate<T>(T item);  
public struct Nullable<T> where T:struct { ... }  
```  
  
 **✓ 执行** 前缀描述性类型参数名的 `T`。  
  
```  
public interface ISessionChannel<TSession> where TSession : ISession{  
    TSession Session { get; }  
}  
```  
  
 **✓ 请考虑** ，该值指示约束放置在类型参数在参数名。  
  
 例如，参数约束为 `ISession` 可能调用 `TSession`。  
  
## 常见类型的名称  
 **✓ 执行** 按照命名类型派生自或实现某些.NET Framework 类型时下表中所述的准则。  
  
|基类型|派生的实现类型准则|  
|---------|---------------|  
|`System.Attribute`|**✓ 执行** 将"Attribute"后缀添加到自定义特性类的名称。 将"Attribute"后缀添加到自定义特性类的名称。|  
|`System.Delegate`|**✓ 执行** 添加到事件中使用的委托的名称后缀"事件处理程序"。<br /><br /> **✓ 执行** 添加后缀"Callback"的名称的委托之外，用作事件处理程序。<br /><br /> **X 不** 向委托中添加后缀"委托"。|  
|`System.EventArgs`|**✓ 执行** 添加后缀"EventArgs。"|  
|`System.Enum`|**X 不** 派生自此类; 使用改为支持您的语言关键字; 例如，在 C\# 中，使用 enum 关键字。<br /><br /> **X 不** 添加后缀"枚举"或"标志"。|  
|`System.Exception`|**✓ 执行** 添加后缀"异常"。|  
|`IDictionary` <br /> `IDictionary<TKey,TValue>`|**✓ 执行** 添加后缀"字典。 请注意， `IDictionary` 是特定类型的集合，但这一准则将优先于后面的更为通用集合准则。|  
|`IEnumerable` <br /> `ICollection` <br /> `IList` <br /> `IEnumerable<T>` <br /> `ICollection<T>` <br /> `IList<T>`|**✓ 执行** 添加后缀"集合"。|  
|`System.IO.Stream`|**✓ 执行** 添加后缀"流"。|  
|`CodeAccessPermission IPermission`|**✓ 执行** 添加后缀"权限"。|  
  
## 命名的枚举  
 一般情况 （也称为枚举） 的枚举类型的名称应遵循的标准类型命名规则 （PascalCasing 等）。 但是，有一些其他指南，尤其适用于枚举。  
  
 **✓ 执行** 使用枚举的单数形式的类型名称，除非它的值是位域。  
  
 **✓ 执行** 作为值，也称为标志枚举与位域使用枚举的复数形式的类型名称。  
  
 **X 不** 枚举类型名称中使用"枚举"后缀。  
  
 **X 不** 使用"标记"或"Flags"后缀枚举中的键入名称。  
  
 **X 不** 使用一个前缀在枚举值名称 \(例如，"ad"对 ADO 枚举。\)、"rtf"丰富文本枚举，等等。  
  
 *部分 © 2005年、 2009 Microsoft Corporation。 保留所有权利。*  
  
 *转载已获得的权限从 Pearson Education，Inc. [Framework 设计准则︰ 约定、 惯例和可重用的.NET 库，第二版模式](http://www.informit.com/store/framework-design-guidelines-conventions-idioms-and-9780321545619) 通过 Krzysztof Cwalina 和 Brad Abrams，作为 Microsoft Windows 开发系列的一部分发布 2008 年 10 月 22 日由 Addison\-wesley Professional。*  
  
## 请参阅  
 [Framework 设计准则](../../../docs/standard/design-guidelines/index.md)   
 [命名准则](../../../docs/standard/design-guidelines/naming-guidelines.md)