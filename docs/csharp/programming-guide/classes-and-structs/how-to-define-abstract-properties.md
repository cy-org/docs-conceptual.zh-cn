---
title: "如何：定义抽象属性（C# 编程指南）"
ms.date: 2015-07-20
ms.prod: .net
ms.technology:
- devlang-csharp
ms.topic: article
dev_langs:
- CSharp
helpviewer_keywords:
- properties [C#], abstract
- abstract properties [C#]
ms.assetid: 672a90eb-47b9-4ae0-9914-af53852fddcb
caps.latest.revision: 13
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
ms.openlocfilehash: c6decaae138a21c24e94e2ed74111c860777f64b
ms.contentlocale: zh-cn
ms.lasthandoff: 07/28/2017

---
# <a name="how-to-define-abstract-properties-c-programming-guide"></a>如何：定义抽象属性（C# 编程指南）
以下示例演示如何定义[抽象](../../../csharp/language-reference/keywords/abstract.md)属性。 抽象属性声明不提供属性访问器的实现，它声明该类支持属性，而将访问器实现留给派生类。 以下示例演示如何实现从基类继承抽象属性。  
  
 此示例由三个文件组成，其中每个文件都单独编译，产生的程序集由下一次编译引用：  
  
-   abstractshape.cs：包含抽象 `Area` 属性的 `Shape` 类。  
  
-   shapes.cs： `Shape` 类的子类。  
  
-   shapetest.cs：测试程序，用于显示某些 `Shape` 派生对象的区域。  
  
 若要编译该示例，请使用以下命令：  
  
 `csc abstractshape.cs shapes.cs shapetest.cs`  
  
 这将创建可执行文件 shapetest.exe。  
  
## <a name="example"></a>示例  
 此文件声明 `Shape` 类，该类包含 `double` 类型的 `Area` 属性。  
  
 [!code-cs[csProgGuideInheritance#1](../../../csharp/programming-guide/classes-and-structs/codesnippet/CSharp/how-to-define-abstract-properties_1.cs)]  
  
-   属性的修饰符放置在属性声明中。 例如：  
  
    ```  
    public abstract double Area  
    ```  
  
-   声明抽象属性时（如本示例中的 `Area`），只需指明哪些属性访问器可用即可，不要实现它们。 在此示例中，仅 [get](../../../csharp/language-reference/keywords/get.md) 访问器可用，因此该属性是只读属性。  
  
## <a name="example"></a>示例  
 下面的代码演示 `Shape` 的三个子类，并演示它们如何替代 `Area` 属性来提供自己的实现。  
  
 [!code-cs[csProgGuideInheritance#2](../../../csharp/programming-guide/classes-and-structs/codesnippet/CSharp/how-to-define-abstract-properties_2.cs)]  
  
## <a name="example"></a>示例  
 下面的代码演示一个创建若干 `Shape` 派生对象并输出其区域的测试程序。  
  
 [!code-cs[csProgGuideInheritance#3](../../../csharp/programming-guide/classes-and-structs/codesnippet/CSharp/how-to-define-abstract-properties_3.cs)]  
  
## <a name="see-also"></a>另请参阅  
 [C# 编程指南](../../../csharp/programming-guide/index.md)   
 [类和结构](../../../csharp/programming-guide/classes-and-structs/index.md)   
 [抽象类、密封类及类成员](../../../csharp/programming-guide/classes-and-structs/abstract-and-sealed-classes-and-class-members.md)   
 [属性](../../../csharp/programming-guide/classes-and-structs/properties.md)   
 [如何：使用命令行创建和使用程序集](http://msdn.microsoft.com/library/70f65026-3687-4e9c-ab79-c18b97dd8be4)

