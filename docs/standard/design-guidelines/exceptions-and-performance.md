---
title: "异常和性能 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-standard"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "VB"
  - "CSharp"
  - "C++"
  - "jsharp"
helpviewer_keywords: 
  - "tester-doer 模式"
  - "Tryparse"
  - "引发的异常"
  - "例外情况之外性能"
  - "引发异常，性能"
ms.assetid: 3ad6aad9-08e6-4232-b336-0e301f2493e6
caps.latest.revision: 12
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 12
---
# 异常和性能
与异常相关的一个常见的问题都是这样如果经常性执行失败的代码使用了异常，该实现的性能不可接受。 这是值得关注的问题。 当成员引发了异常时，其性能，可以是数量级的速度较慢。 但是，就可以实现很好的性能，同时严格符合不允许使用错误代码的异常指导原则。 本部分中所述的两个模式建议执行此操作的方法。  
  
 **X 不** 由于异常可能会对性能产生负面影响的问题而使用错误代码。  
  
 为了提高性能，则可以使用 Tester\-doer 模式或尝试分析模式中，接下来的两部分中所述。  
  
## Tester\-doer 模式  
 有时可通过成员分为两部分提高性能的引发异常的成员。 让我们看一下 <xref:System.Collections.Generic.ICollection%601.Add%2A> 方法 <xref:System.Collections.Generic.ICollection%601> 接口。  
  
```  
ICollection<int> numbers = ...   
numbers.Add(1);  
```  
  
 该方法 `Add` 集合为只读时引发。 这可能会在方法调用的地方经常失败的情况下的性能问题。 若要缓解这一问题的方法之一是测试集合是否是可写然后再尝试添加一个值。  
  
```  
ICollection<int> numbers = ...   
...  
if(!numbers.IsReadOnly){  
    numbers.Add(1);  
}  
```  
  
 用于测试条件，它在我们的示例中为该属性的成员 `IsReadOnly`, ，称为测试人员。 用于执行可能引发的操作，该成员 `Add` 方法在示例中，被称为 doer。  
  
 **✓ 请考虑** 可能引发异常的成员 Tester\-doer 模式在常见方案以避免性能问题与异常相关。  
  
## 尝试分析模式  
 对于极性能敏感的 Api，应使用更快的运行模式比上一节中所述的 Tester\-doer 模式。 该模式需要调整要进行明确定义测试案例的成员语义的一部分的成员名称。 例如， <xref:System.DateTime> 定义 <xref:System.DateTime.Parse%2A> 字符串的分析失败时引发异常的方法。 它还定义了相应 <xref:System.DateTime.TryParse%2A> ，尝试进行分析，但如果方法返回 false 分析失败并返回成功分析使用结果 `out` 参数。  
  
```  
public struct DateTime {  
    public static DateTime Parse(string dateTime){   
        ...   
    }  
    public static bool TryParse(string dateTime, out DateTime result){  
        ...  
    }  
}  
```  
  
 使用此模式时，务必在严格的术语定义的重试功能。 如果该成员定义完善的重试以外的任何原因失败，该成员仍必须引发相应异常。  
  
 **✓ 请考虑** 可能引发异常的成员尝试分析模式在常见方案以避免性能问题与异常相关。  
  
 **✓ 执行** 方法实现此模式对使用该前缀"Try"和一个布尔值返回的类型。  
  
 **✓ 执行** 提供了用于使用 Try 分析模式每个成员引发异常的成员。  
  
 *部分 © 2005年、 2009 Microsoft Corporation。 保留所有权利。*  
  
 *转载已获得的权限从 Pearson Education，Inc. [Framework 设计准则︰ 约定、 惯例和可重用的.NET 库，第二版模式](http://www.informit.com/store/framework-design-guidelines-conventions-idioms-and-9780321545619) 通过 Krzysztof Cwalina 和 Brad Abrams，作为 Microsoft Windows 开发系列的一部分发布 2008 年 10 月 22 日由 Addison\-wesley Professional。*  
  
## 请参阅  
 [Framework 设计准则](../../../docs/standard/design-guidelines/index.md)   
 [异常设计准则](../../../docs/standard/design-guidelines/exceptions.md)