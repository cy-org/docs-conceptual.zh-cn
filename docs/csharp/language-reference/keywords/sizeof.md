---
title: "sizeof（C# 参考）"
ms.date: 2015-07-20
ms.prod: .net
ms.technology:
- devlang-csharp
ms.topic: article
f1_keywords:
- sizeof_CSharpKeyword
- sizeof
dev_langs:
- CSharp
helpviewer_keywords:
- sizeof keyword [C#]
ms.assetid: c548592c-677c-4f40-a4ce-e613f7529141
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
ms.sourcegitcommit: 81117b1419c2a9c3babd6a7429052e2b23e08a70
ms.openlocfilehash: 6b3e0b5d0b91da3cc63c7caeed8d4ba4ea0b2ad1
ms.contentlocale: zh-cn
ms.lasthandoff: 09/25/2017

---
# <a name="sizeof-c-reference"></a>sizeof（C# 参考）
用于获取非托管类型的大小（以字节为单位）。 非托管类型包括下表列出的内置类型以及以下类型：  
  
-   枚举类型  
  
-   指针类型  
  
-   用户定义的结构，不包含任何属于引用类型的字段或属性  
  
 下面的示例演示如何检索 `int` 的大小：  
  
```csharp  
// Constant value 4:  
int intSize = sizeof(int);   
```  
  
## <a name="remarks"></a>备注  
 从 C# 2.0 版开始，将 `sizeof` 应用于内置类型不再要求使用 [unsafe](../../../csharp/language-reference/keywords/unsafe.md) 模式。  
  
 不能重载 `sizeof` 运算符。 `sizeof` 运算符的返回值是 `int` 类型。 下表列出了一些常量值，这些值对应于以某些内置类型为操作数的 `sizeof` 表达式。  
  
|Expression|常量值|  
|----------------|--------------------|  
|`sizeof(sbyte)`|1|  
|`sizeof(byte)`|1|  
|`sizeof(short)`|2|  
|`sizeof(ushort)`|2|  
|`sizeof(int)`|4|  
|`sizeof(uint)`|4|  
|`sizeof(long)`|8|  
|`sizeof(ulong)`|8|  
|`sizeof(char)`|2 (Unicode)|  
|`sizeof(float)`|4|  
|`sizeof(double)`|8|  
|`sizeof(decimal)`|16|  
|`sizeof(bool)`|1|  
  
 对于所有其他类型（包括结构），`sizeof` 运算符只能在不安全代码块中使用。 虽然可以使用 <xref:System.Runtime.InteropServices.Marshal.SizeOf%2A?displayProperty=nameWithType> 方法，但此方法返回的值并不总是与 `sizeof` 返回的值相同。 <xref:System.Runtime.InteropServices.Marshal.SizeOf%2A?displayProperty=nameWithType> 在封送类型后返回大小，而 `sizeof` 返回公共语言运行时分配的大小（包括所有填充）。  
  
## <a name="example"></a>示例  
 [!code-cs[csrefKeywordsOperator#11](../../../csharp/language-reference/keywords/codesnippet/CSharp/sizeof_1.cs)]  
  
## <a name="c-language-specification"></a>C# 语言规范  
 [!INCLUDE[CSharplangspec](~/includes/csharplangspec-md.md)]  
  
## <a name="see-also"></a>请参阅  
 [C# 参考](../../../csharp/language-reference/index.md)   
 [C# 编程指南](../../../csharp/programming-guide/index.md)   
 [C# 关键字](../../../csharp/language-reference/keywords/index.md)   
 [运算符关键字](../../../csharp/language-reference/keywords/operator-keywords.md)   
 [enum](../../../csharp/language-reference/keywords/enum.md)   
 [不安全代码和指针](../../../csharp/programming-guide/unsafe-code-pointers/index.md)   
 [结构](../../../csharp/programming-guide/classes-and-structs/structs.md)   
 [常量](../../../csharp/programming-guide/classes-and-structs/constants.md)

