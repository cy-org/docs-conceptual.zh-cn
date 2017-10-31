---
title: "abstract（C# 参考）"
ms.date: 2015-07-20
ms.prod: .net
ms.technology:
- devlang-csharp
ms.topic: article
f1_keywords:
- abstract
- abstract_CSharpKeyword
dev_langs:
- CSharp
helpviewer_keywords:
- abstract keyword [C#]
ms.assetid: b0797770-c1f3-4b4d-9441-b9122602a6bb
caps.latest.revision: 24
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
ms.openlocfilehash: a109a8e37f84a2e91229bfce789a69cdc26adba9
ms.contentlocale: zh-cn
ms.lasthandoff: 09/25/2017

---
# <a name="abstract-c-reference"></a>abstract（C# 参考）
`abstract` 修饰符指示被修改内容的实现已丢失或不完整。 abstract 修饰符可用于类、方法、属性、索引和事件。 在类声明中使用 `abstract` 修饰符以指示某个类仅旨在作为其他类的基类。 标记为 abstract 的成员，或包含在抽象类中的成员，都必须由派生自抽象类的类来实现。  
  
## <a name="example"></a>示例  
 在此示例中，类 `Square` 必须提供 `Area` 的实现，因为它派生自 `ShapesClass`：  
  
 [!code-cs[csrefKeywordsModifiers#1](../../../csharp/language-reference/keywords/codesnippet/CSharp/abstract_1.cs)]  
  
 抽象类具有以下功能：  
  
-   抽象类不能实例化。  
  
-   抽象类可能包含抽象方法和访问器。  
  
-   无法使用 [sealed](../../../csharp/language-reference/keywords/sealed.md) 修饰符来修改抽象类，因为两个修饰符具有相反的含义。 `sealed` 修饰符阻止类被继承，而 `abstract` 修饰符要求类被继承。  
  
-   派生自抽象类的非抽象类，必须包含全部已继承的抽象方法和访问器的实际实现。  
  
 在方法或属性声明中使用 `abstract` 修饰符，以指示该方法或属性不包含实现。  
  
 抽象方法具有以下功能：  
  
-   抽象方法是隐式的虚拟方法。  
  
-   只有抽象类中才允许抽象方法声明。  
  
-   由于抽象方法声明不提供实际的实现，因此没有方法主体；方法声明仅以分号结尾，且签名后没有大括号 ({ })。 例如:   
  
    ```  
    public abstract void MyMethod();  
    ```  
  
     实现由替代方法 [override](../../../csharp/language-reference/keywords/override.md) 提供，它是非抽象类的成员。  
  
-   在抽象方法声明中使用 [static](../../../csharp/language-reference/keywords/static.md) 或 [virtual](../../../csharp/language-reference/keywords/virtual.md) 修饰符是错误的。  
  
 除了声明和调用语法方面不同外，抽象属性的行为与抽象方法相似。  
  
-   在静态属性上使用 `abstract` 修饰符是错误的。  
  
-   通过包含使用 [override](../../../csharp/language-reference/keywords/override.md) 修饰符的属性声明，可在派生类中重写抽象继承属性。  
  
 有关抽象类的详细信息，请参阅[抽象类、密封类及类成员](../../../csharp/programming-guide/classes-and-structs/abstract-and-sealed-classes-and-class-members.md)。  
  
 抽象类必须为所有接口成员提供实现。  
  
 实现接口的抽象类有可能将接口方法映射到抽象方法上。 例如:   
  
 [!code-cs[csrefKeywordsModifiers#2](../../../csharp/language-reference/keywords/codesnippet/CSharp/abstract_2.cs)]  
  
## <a name="example"></a>示例  
 在此示例中，类 `DerivedClass` 派生自抽象类 `BaseClass`。 抽象类包含抽象方法 `AbstractMethod`，以及两个抽象属性 `X` 和 `Y`。  
  
 [!code-cs[csrefKeywordsModifiers#3](../../../csharp/language-reference/keywords/codesnippet/CSharp/abstract_3.cs)]  
  
 在前面的示例中，如果你尝试通过使用如下语句来实例化抽象类：  
  
```  
BaseClass bc = new BaseClass();   // Error  
```  
  
 将遇到一个错误，告知编译器无法创建抽象类“BaseClass”的实例。  
  
## <a name="c-language-specification"></a>C# 语言规范  
 [!INCLUDE[CSharplangspec](~/includes/csharplangspec-md.md)]  
  
## <a name="see-also"></a>请参阅  
 [C# 参考](../../../csharp/language-reference/index.md)   
 [C# 编程指南](../../../csharp/programming-guide/index.md)   
 [修饰符](../../../csharp/language-reference/keywords/modifiers.md)   
 [virtual](../../../csharp/language-reference/keywords/virtual.md)   
 [override](../../../csharp/language-reference/keywords/override.md)   
 [C# 关键字](../../../csharp/language-reference/keywords/index.md)

