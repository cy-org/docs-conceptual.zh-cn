---
title: "volatile（C# 参考）"
ms.date: 2015-07-20
ms.prod: .net
ms.technology:
- devlang-csharp
ms.topic: article
f1_keywords:
- volatile_CSharpKeyword
- volatile
dev_langs:
- CSharp
helpviewer_keywords:
- volatile keyword [C#]
ms.assetid: 78089bc7-7b38-4cfd-9e49-87ac036af009
caps.latest.revision: 29
author: BillWagner
ms.author: wiwagn
translation.priority.ht:
- cs-cz
- de-de
- es-es
- fr-fr
- it-it
- ja-jp
- ko-kr
- pl-pl
- pt-br
- ru-ru
- tr-tr
- zh-cn
- zh-tw
ms.translationtype: HT
ms.sourcegitcommit: 306c608dc7f97594ef6f72ae0f5aaba596c936e1
ms.openlocfilehash: c8f9fba15991197be885a973435089098a57db87
ms.contentlocale: zh-cn
ms.lasthandoff: 09/25/2017

---
# <a name="volatile-c-reference"></a>volatile（C# 参考）
`volatile` 关键字指示一个字段可以由多个同时执行的线程修改。 声明为 `volatile` 的字段不受编译器优化（假定由单个线程访问）的限制。 这样可以确保该字段在任何时间呈现的都是最新的值。  
  
 `volatile` 修饰符通常用于由多个线程访问、但不使用 [lock](../../../csharp/language-reference/keywords/lock-statement.md) 语句对访问进行序列化的字段。  
  
 `volatile` 关键字可应用于以下类型的字段：  
  
-   引用类型。  
  
-   指针类型（在不安全的上下文中）。 请注意，虽然指针本身可以是可变的，但是它指向的对象不能是可变的。 换句话说，不能声明“指向可变对象的指针”。  
  
-   类型，如 sbyte、byte、short、ushort、int、uint、char、float 和 bool。  
  
-   具有以下基类型之一的枚举类型：byte、sbyte、short、ushort、int 或 uint。  
  
-   已知为引用类型的泛型类型参数。  
  
-   <xref:System.IntPtr> 和 <xref:System.UIntPtr>。  
  
 可变关键字仅可应用于类或结构的字段。 不能将局部变量声明为 `volatile`。  
  
## <a name="example"></a>示例  
 下面的示例说明如何将公共字段变量声明为 `volatile`。  
  
 [!code-cs[csrefKeywordsModifiers#24](../../../csharp/language-reference/keywords/codesnippet/CSharp/volatile_1.cs)]  
  
## <a name="example"></a>示例  
 下面的示例演示如何创建辅助线程，并用它与主线程并行执行处理。 有关多线程处理的背景信息，请参 [线程](../../../standard/threading/index.md)和[线程](http://msdn.microsoft.com/library/552f6c68-dbdb-4327-ae36-32cf9063d88c)。  
  
 [!code-cs[csProgGuideThreading#1](../../../csharp/language-reference/keywords/codesnippet/CSharp/volatile_2.cs)]  
  
## <a name="c-language-specification"></a>C# 语言规范  
 [!INCLUDE[CSharplangspec](~/includes/csharplangspec-md.md)]  
  
## <a name="see-also"></a>请参阅  
 [C# 参考](../../../csharp/language-reference/index.md)   
 [C# 编程指南](../../../csharp/programming-guide/index.md)   
 [C# 关键字](../../../csharp/language-reference/keywords/index.md)   
 [修饰符](../../../csharp/language-reference/keywords/modifiers.md)

