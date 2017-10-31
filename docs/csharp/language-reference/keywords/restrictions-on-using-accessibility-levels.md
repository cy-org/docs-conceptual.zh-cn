---
title: "可访问性级别的使用限制（C# 参考）"
ms.date: 2015-07-20
ms.prod: .net
ms.technology:
- devlang-csharp
ms.topic: article
dev_langs:
- CSharp
helpviewer_keywords:
- access modifiers [C#], accessibility level restrictions
ms.assetid: 987e2f22-46bf-4fea-80ee-270b9cd01045
caps.latest.revision: 21
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
ms.openlocfilehash: 8e49afd38fd776593b87f065a079da0d546df4a6
ms.contentlocale: zh-cn
ms.lasthandoff: 09/25/2017

---
# <a name="restrictions-on-using-accessibility-levels-c-reference"></a>可访问性级别的使用限制（C# 参考）
在声明中指定类型时，检查类型的可访问性级别是否依赖于成员或其他类型的可访问性级别。 例如，直接基类必须至少具有与派生类相同的可访问性。 以下声明会导致编译器错误，因为基类 `BaseClass` 的可访问性低于 `MyClass`：  
  
```  
class BaseClass {...}  
public class MyClass: BaseClass {...} // Error  
```  
  
 下表汇总了对已声明可访问性级别的限制。  
  
|上下文|备注|  
|-------------|-------------|  
|[类](../../../csharp/programming-guide/classes-and-structs/classes.md)|类类型的直接基类必须至少具有与类类型本身相同的可访问性。|  
|[接口](../../../csharp/programming-guide/interfaces/index.md)|接口类型的显式基接口必须至少具有与接口类型本身相同的可访问性。|  
|[委托](../../../csharp/programming-guide/delegates/index.md)|委托类型的返回类型和参数类型必须至少具有与委托类型本身相同的可访问性。|  
|[常量](../../../csharp/programming-guide/classes-and-structs/constants.md)|常量的类型必须至少具有与常量本身相同的可访问性。|  
|[字段](../../../csharp/programming-guide/classes-and-structs/fields.md)|字段的类型必须至少具有与字段本身相同的可访问性。|  
|[方法](../../../csharp/programming-guide/classes-and-structs/methods.md)|方法的返回类型和参数类型必须至少具有与方法本身相同的可访问性。|  
|[属性](../../../csharp/programming-guide/classes-and-structs/properties.md)|属性的类型必须至少具有与属性本身相同的可访问性。|  
|[事件](../../../csharp/programming-guide/events/index.md)|事件的类型必须至少具有与事件本身相同的可访问性。|  
|[索引器](../../../csharp/programming-guide/indexers/index.md)|索引器的类型和参数类型必须至少具有与索引器本身相同的可访问性。|  
|[运算符](../../../csharp/programming-guide/statements-expressions-operators/operators.md)|运算符的类型和参数类型必须至少具有与运算符本身相同的可访问性。|  
|[构造函数](../../../csharp/programming-guide/classes-and-structs/constructors.md)|构造函数的参数类型必须至少具有与构造函数本身相同的可访问性。|  
  
## <a name="example"></a>示例  
 下面的示例包含不同类型的错误声明。 每个声明后的注释指示预期编译器错误。  
  
```  
// Restrictions on Using Accessibility Levels  
// CS0052 expected as well as CS0053, CS0056, and CS0057  
// To make the program work, change access level of both class B  
// and MyPrivateMethod() to public.  
  
using System;  
  
// A delegate:  
delegate int MyDelegate();  
  
class B  
{  
    // A private method:  
    static int MyPrivateMethod()  
    {  
        return 0;  
    }  
}  
  
public class A  
{  
    // Error: The type B is less accessible than the field A.myField.  
    public B myField = new B();  
  
    // Error: The type B is less accessible  
    // than the constant A.myConst.  
    public readonly B myConst = new B();  
  
    public B MyMethod()  
    {  
        // Error: The type B is less accessible   
        // than the method A.MyMethod.  
        return new B();  
    }  
  
    // Error: The type B is less accessible than the property A.MyProp  
    public B MyProp  
    {  
        set  
        {  
        }  
    }  
  
    MyDelegate d = new MyDelegate(B.MyPrivateMethod);  
    // Even when B is declared public, you still get the error:   
    // "The parameter B.MyPrivateMethod is not accessible due to   
    // protection level."  
  
    public static B operator +(A m1, B m2)  
    {  
        // Error: The type B is less accessible  
        // than the operator A.operator +(A,B)  
        return new B();  
    }  
  
    static void Main()  
    {  
        Console.Write("Compiled successfully");  
    }  
}  
```  
  
## <a name="c-language-specification"></a>C# 语言规范  
 [!INCLUDE[CSharplangspec](~/includes/csharplangspec-md.md)]  
  
## <a name="see-also"></a>请参阅  
 [C# 参考](../../../csharp/language-reference/index.md)   
 [C# 编程指南](../../../csharp/programming-guide/index.md)   
 [C# 关键字](../../../csharp/language-reference/keywords/index.md)   
 [访问修饰符](../../../csharp/language-reference/keywords/access-modifiers.md)   
 [可访问域](../../../csharp/language-reference/keywords/accessibility-domain.md)   
 [可访问性级别](../../../csharp/language-reference/keywords/accessibility-levels.md)   
 [访问修饰符](../../../csharp/programming-guide/classes-and-structs/access-modifiers.md)   
 [public](../../../csharp/language-reference/keywords/public.md)   
 [private](../../../csharp/language-reference/keywords/private.md)   
 [protected](../../../csharp/language-reference/keywords/protected.md)   
 [内部](../../../csharp/language-reference/keywords/internal.md)

