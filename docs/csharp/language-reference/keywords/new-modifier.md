---
title: "new 修饰符（C# 参考）"
ms.date: 2015-07-20
ms.prod: .net
ms.technology:
- devlang-csharp
ms.topic: article
dev_langs:
- CSharp
helpviewer_keywords:
- new modifier keyword [C#]
ms.assetid: a2e20856-33b9-4620-b535-a60dbce8349b
caps.latest.revision: 28
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
ms.openlocfilehash: f763b9a1d2f146b8ebb475a01bd12f1a4238050a
ms.contentlocale: zh-cn
ms.lasthandoff: 09/25/2017

---
# <a name="new-modifier-c-reference"></a>new 修饰符（C# 参考）
在用作声明修饰符时，`new` 关键字可以显式隐藏从基类继承的成员。 隐藏继承的成员时，该成员的派生版本将替换基类版本。 虽然可以不使用 `new` 修饰符来隐藏成员，但将收到编译器警告。 如果使用 `new` 来显式隐藏成员，将禁止此警告。  
  
 若要隐藏继承的成员，请使用相同名称在派生类中声明该成员，并使用 `new` 修饰符对其进行修饰。 例如:   
  
 [!code-cs[csrefKeywordsOperator#8](../../../csharp/language-reference/keywords/codesnippet/CSharp/new-modifier_1.cs)]  
  
 在此示例中，使用 `BaseC.Invoke` 隐藏了 `DerivedC.Invoke`。 字段 `x` 不受影响，因为未使用类似名称将其隐藏。  
  
 通过继承隐藏名称采用下列形式之一：  
  
-   通常，在类或结构中引入的常数、字段、属性或类型会隐藏与其共享名称的所有基类成员。  有三种特殊情况。  例如，如果将名称为 `N` 的新字段声明为不可调用的类型，并且基类型将 `N` 声明为一种方法，则新字段在调用语法中不会隐藏基声明。  请参阅 [C# 语言规范](http://go.microsoft.com/fwlink/?LinkId=199552)了解详细信息（参阅“表达式”一节中的“成员查找”部分）。  
  
-   类或结构中引入的方法会隐藏基类中共享该名称的属性、字段和类型。 它还会隐藏具有相同签名的所有基类方法。  
  
-   类或结构中引入的索引器会隐藏具有相同签名的所有基类索引器。  
  
 对同一成员同时使用 `new` 和 [override](../../../csharp/language-reference/keywords/override.md) 是错误的做法，因为这两个修饰符的含义互斥。 `new` 修饰符会用同样的名称创建一个新成员并使原始成员变为隐藏。 `override` 修饰符会扩展继承成员的实现。  
  
 在不隐藏继承成员的声明中使用 `new` 修饰符将会生成警告。  
  
## <a name="example"></a>示例  
 在此示例中，基类 `BaseC` 和派生类 `DerivedC` 使用相同的字段名 `x`，从而隐藏了继承字段的值。 此示例演示 `new` 修饰符的用法。 另外还演示了如何使用完全限定名访问基类的隐藏成员。  
  
 [!code-cs[csrefKeywordsOperator#9](../../../csharp/language-reference/keywords/codesnippet/CSharp/new-modifier_2.cs)]  
  
## <a name="example"></a>示例  
 在此示例中，嵌套类隐藏了基类中同名的类。 此示例演示如何使用 `new` 修饰符来消除警告消息，以及如何使用完全限定名来访问隐藏的类成员。  
  
 [!code-cs[csrefKeywordsOperator#10](../../../csharp/language-reference/keywords/codesnippet/CSharp/new-modifier_3.cs)]  
  
 如果移除 `new` 修饰符，程序仍将编译和运行，但你会收到以下警告：  
  
```  
The keyword new is required on 'MyDerivedC.x' because it hides inherited member 'MyBaseC.x'.  
```  
  
## <a name="c-language-specification"></a>C# 语言规范  
 [!INCLUDE[CSharplangspec](~/includes/csharplangspec-md.md)]  
  
## <a name="see-also"></a>请参阅  
 [C# 参考](../../../csharp/language-reference/index.md)   
 [C# 编程指南](../../../csharp/programming-guide/index.md)   
 [C# 关键字](../../../csharp/language-reference/keywords/index.md)   
 [运算符关键字](../../../csharp/language-reference/keywords/operator-keywords.md)   
 [修饰符](../../../csharp/language-reference/keywords/modifiers.md)   
 [使用 Override 和 New 关键字进行版本控制](../../../csharp/programming-guide/classes-and-structs/versioning-with-the-override-and-new-keywords.md)   
 [了解何时使用 Override 和 New 关键字](../../../csharp/programming-guide/classes-and-structs/knowing-when-to-use-override-and-new-keywords.md)

