---
title: "const（C# 参考）"
ms.date: 2015-07-20
ms.prod: .net
ms.technology:
- devlang-csharp
ms.topic: article
f1_keywords:
- const_CSharpKeyword
- const
dev_langs:
- CSharp
helpviewer_keywords:
- const keyword [C#]
ms.assetid: 79eb447c-117b-4418-933f-97c50aa472db
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
ms.openlocfilehash: b8f6d567deed513ff5693fe39bd21c8607677402
ms.contentlocale: zh-cn
ms.lasthandoff: 09/25/2017

---
# <a name="const-c-reference"></a>const（C# 参考）
使用 `const` 关键字来声明某个常量字段或常量局部变量。 常量字段和常量局部变量不是变量并且不能修改。 常量可以为数字、布尔值、字符串或 null 引用。 不要创建常量来表示你需要随时更改的信息。 例如，不要使用常量字段来存储服务的价格、产品版本号或公司的品牌名称。 这些值会随着时间发生变化；因为编译器会传播常量，所以必须重新编译通过库编译的其他代码以查看更改。 另请参阅 [readonly](../../../csharp/language-reference/keywords/readonly.md) 关键字。 例如：  
  
```csharp
const int x = 0;  
public const double gravitationalConstant = 6.673e-11;  
private const string productName = "Visual C#";  
```  
  
## <a name="remarks"></a>备注  
 常数声明的类型指定声明引入的成员类型。 常量局部变量或常量字段的初始值设定项必须是一个可以隐式转换为目标类型的常量表达式。  
  
 常数表达式是在编译时可被完全计算的表达式。 因此，对于引用类型的常数，可能的值只能是 `string` 和 null 引用。  
  
 常数声明可以声明多个常数，例如：  
  
```csharp
public const double x = 1.0, y = 2.0, z = 3.0;  
```  
  
 不允许在常数声明中使用 `static` 修饰符。  
  
 常数可以参与常数表达式，如下所示：  
  
```csharp
public const int c1 = 5;  
public const int c2 = c1 + 100;  
```  
  
> [!NOTE]
>  [readonly](../../../csharp/language-reference/keywords/readonly.md) 关键字与 `const` 关键字不同。 
          
          
          `const` 字段只能在该字段的声明中初始化。 
          
          
          `readonly` 字段可以在声明或构造函数中初始化。 因此，根据所使用的构造函数，`readonly` 字段可能具有不同的值。 另外，虽然 `const` 字段是编译时常量，但 `readonly` 字段可用于运行时常量，如此行所示：`public static readonly uint l1 = (uint)DateTime.Now.Ticks;`  
  
## <a name="example"></a>示例  
 [!code-cs[csrefKeywordsModifiers#5](../../../csharp/language-reference/keywords/codesnippet/CSharp/const_1.cs)]  
  
## <a name="example"></a>示例  
 此示例说明如何将常数用作局部变量。  
  
 [!code-cs[csrefKeywordsModifiers#6](../../../csharp/language-reference/keywords/codesnippet/CSharp/const_2.cs)]  
  
## <a name="c-language-specification"></a>C# 语言规范  
 [!INCLUDE[CSharplangspec](~/includes/csharplangspec-md.md)]  
  
## <a name="see-also"></a>请参阅  
 [C# 参考](../../../csharp/language-reference/index.md)   
 [C# 编程指南](../../../csharp/programming-guide/index.md)   
 [C# 关键字](../../../csharp/language-reference/keywords/index.md)   
 [修饰符](../../../csharp/language-reference/keywords/modifiers.md)   
 [只读](../../../csharp/language-reference/keywords/readonly.md)

