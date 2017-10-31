---
title: "成员（C# 编程指南）"
ms.date: 2015-07-20
ms.prod: .net
ms.technology:
- devlang-csharp
ms.topic: article
dev_langs:
- CSharp
helpviewer_keywords:
- types [C#], nested types
- C# language, type members
ms.assetid: 4a30a4ab-d690-4936-9124-92ce9448665a
caps.latest.revision: 20
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
ms.openlocfilehash: 98446a2eb0415c92aa44cbddf8539477a00a2666
ms.contentlocale: zh-cn
ms.lasthandoff: 07/28/2017

---
# <a name="members-c-programming-guide"></a>成员（C# 编程指南）
类和结构具有表示其数据和行为的成员。 类的成员包括在类中声明的所有成员，以及在该类的继承层次结构中的所有类中声明的所有成员（构造函数和析构函数除外）。 基类中的私有成员被继承，但不能从派生类访问。  
  
 下表列出类或结构中可包含的成员类型：  
  
|成员|描述|  
|------------|-----------------|  
|[字段](../../../csharp/programming-guide/classes-and-structs/fields.md)|字段是在类范围声明的变量。 字段可以是内置数值类型或其他类的实例。 例如，日历类可能具有一个包含当前日期的字段。|  
|[常量](../../../csharp/programming-guide/classes-and-structs/constants.md)|常量是在编译时设置其值并且不能更改其值的字段或属性。|  
|[属性](../../../csharp/programming-guide/classes-and-structs/properties.md)|属性是类中可以像类中的字段一样访问的方法。 属性可以为类字段提供保护，以避免字段在对象不知道的情况下被更改。|  
|[方法](../../../csharp/programming-guide/classes-and-structs/methods.md)|方法定义类可以执行的操作。 方法可接受提供输入数据的参数，并可通过参数返回输出数据。 方法还可以不使用参数而直接返回值。|  
|[事件](../../../csharp/programming-guide/events/index.md)|事件向其他对象提供有关发生的事情（如单击按钮或成功完成某个方法）的通知。 事件是使用委托定义和触发的。|  
|[运算符](../../../csharp/programming-guide/statements-expressions-operators/operators.md)|重载运算符被视为类成员。 在重载运算符时，在类中将该运算符定义为公共静态方法。 预定义的运算符（`+`、`*`、`<` 等）不被视为成员。 有关详细信息，请参阅[可重载运算符](../../../csharp/programming-guide/statements-expressions-operators/overloadable-operators.md)。|  
|[索引器](../../../csharp/programming-guide/indexers/index.md)|使用索引器可以用类似于数组的方式为对象建立索引。|  
|[构造函数](../../../csharp/programming-guide/classes-and-structs/constructors.md)|构造函数是首次创建对象时调用的方法。 它们通常用于初始化对象的数据。|  
|[终结器](../../../csharp/programming-guide/classes-and-structs/destructors.md)|C# 中很少使用终结器。 终结器是当对象即将从内存中移除时由运行时执行引擎调用的方法。 它们通常用来确保任何必须释放的资源都得到适当的处理。|  
|[嵌套类型](../../../csharp/programming-guide/classes-and-structs/nested-types.md)|嵌套类型是在其他类型中声明的类型。 嵌套类型通常用于描述仅由包含它们的类型使用的对象。|  
  
## <a name="see-also"></a>另请参阅  
 [C# 编程指南](../../../csharp/programming-guide/index.md)   
 [类](../../../csharp/programming-guide/classes-and-structs/classes.md)   
 [方法](../../../csharp/programming-guide/classes-and-structs/methods.md)   
 [构造函数](../../../csharp/programming-guide/classes-and-structs/constructors.md)   
 [终结器](../../../csharp/programming-guide/classes-and-structs/destructors.md)   
 [属性](../../../csharp/programming-guide/classes-and-structs/properties.md)   
 [字段](../../../csharp/programming-guide/classes-and-structs/fields.md)   
 [索引器](../../../csharp/programming-guide/indexers/index.md)   
 [事件](../../../csharp/programming-guide/events/index.md)   
 [嵌套类型](../../../csharp/programming-guide/classes-and-structs/nested-types.md)   
 [运算符](../../../csharp/programming-guide/statements-expressions-operators/operators.md)   
 [可重载运算符](../../../csharp/programming-guide/statements-expressions-operators/overloadable-operators.md)

