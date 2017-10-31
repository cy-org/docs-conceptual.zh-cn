---
title: "指针类型（C# 编程指南）"
ms.date: 2015-07-20
ms.prod: .net
ms.technology:
- devlang-csharp
ms.topic: article
dev_langs:
- CSharp
helpviewer_keywords:
- unsafe code [C#], pointers
- pointers [C#]
ms.assetid: 3319faf9-336d-4148-9af2-1da2579cdd1e
caps.latest.revision: 19
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
ms.openlocfilehash: 1a4ebc69762f18dc630100b544c18df0f43734ac
ms.contentlocale: zh-cn
ms.lasthandoff: 09/25/2017

---
# <a name="pointer-types-c-programming-guide"></a>指针类型（C# 编程指南）
在不安全的上下文中，类型可以是指针类型、值类型或引用类型。 指针类型声明采用下列形式之一：  
  
```  
type* identifier;  
void* identifier; //allowed but not recommended  
```  
  
 以下任一类型均可为指针类型：  
  
-   [sbyte](../../../csharp/language-reference/keywords/sbyte.md)、[byte](../../../csharp/language-reference/keywords/byte.md)、[short](../../../csharp/language-reference/keywords/short.md)、[ushort](../../../csharp/language-reference/keywords/ushort.md)、[int](../../../csharp/language-reference/keywords/int.md)、[uint](../../../csharp/language-reference/keywords/uint.md)、[long](../../../csharp/language-reference/keywords/long.md)、[ulong](../../../csharp/language-reference/keywords/ulong.md)、[char](../../../csharp/language-reference/keywords/char.md)、[float](../../../csharp/language-reference/keywords/float.md)、[double](../../../csharp/language-reference/keywords/double.md)、[decimal](../../../csharp/language-reference/keywords/decimal.md) 或 [bool](../../../csharp/language-reference/keywords/bool.md)。  
  
-   任何[枚举](../../../csharp/language-reference/keywords/enum.md)类型。  
  
-   任何指针类型。  
  
-   任何仅包含非托管类型字段的用户定义的结构类型。  
  
 指针类型不从[对象](../../../csharp/language-reference/keywords/object.md)继承，并且指针类型与 `object` 之间不存在转换。 此外，装箱和取消装箱不支持指针。 但是，你可在不同的指针类型之间以及指针类型和整型之间进行转换。  
  
 在同一个声明中声明多个指针时，星号 (*) 仅与基础类型一起写入；而不是用作每个指针名称的前缀。 例如:   
  
```  
int* p1, p2, p3;   // Ok  
int *p1, *p2, *p3;   // Invalid in C#  
```  
  
 指针不能指向引用或包含引用的[结构](../../../csharp/language-reference/keywords/struct.md)，因为无法对对象引用进行垃圾回收，即使有指针指向它也是如此。 垃圾回收器并不跟踪是否有任何类型的指针指向对象。  
  
 `myType*` 类型的指针变量的值为 `myType` 类型的变量的地址。 下面是指针类型声明的示例：  
  
|示例|描述|  
|-------------|-----------------|  
|`int* p`|`p` 是指向整数的指针。|  
|`int** p`|`p` 是指向整数的指针的指针。|  
|`int*[] p`|`p` 是指向整数的指针的一维数组。|  
|`char* p`|`p` 是指向字符的指针。|  
|`void* p`|`p` 是指向未知类型的指针。|  
  
 指针间接寻址运算符 * 可用于访问位于指针变量所指向的位置的内容。 例如，请考虑以下声明：  
  
```  
int* myVariable;  
```  
  
 表达式 `*myVariable` 表示在 `int` 中包含的地址处找到的 `myVariable` 变量。  
  
 [fixed 语句](../../../csharp/language-reference/keywords/fixed-statement.md)和[指针转换](../../../csharp/programming-guide/unsafe-code-pointers/pointer-conversions.md)主题中有几个指针示例。  下面的示例显示需要 `unsafe` 关键字和 `fixed` 语句以及如何递增内部指针。  你可将此代码粘贴到控制台应用程序的 Main 函数中来运行它。 （记住在“项目设计器”中启用不安全代码；选择菜单栏上的“项目”、“属性”，然后选择“生成”选项卡中的“允许不安全代码”。）  
  
```  
// Normal pointer to an object.  
int[] a = new int[5] {10, 20, 30, 40, 50};  
// Must be in unsafe code to use interior pointers.  
unsafe  
{  
    // Must pin object on heap so that it doesn't move while using interior pointers.  
    fixed (int* p = &a[0])  
    {  
        // p is pinned as well as object, so create another pointer to show incrementing it.  
        int* p2 = p;  
        Console.WriteLine(*p2);  
        // Incrementing p2 bumps the pointer by four bytes due to its type ...  
        p2 += 1;  
        Console.WriteLine(*p2);  
        p2 += 1;  
        Console.WriteLine(*p2);  
        Console.WriteLine("--------");  
        Console.WriteLine(*p);  
        // Deferencing p and incrementing changes the value of a[0] ...  
        *p += 1;  
        Console.WriteLine(*p);  
        *p += 1;  
        Console.WriteLine(*p);  
    }  
}  
  
Console.WriteLine("--------");  
Console.WriteLine(a[0]);  
Console.ReadLine();  
  
// Output:  
//10  
//20  
//30  
//--------  
//10  
//11  
//12  
//--------  
//12  
```  
  
 你无法对 `void*` 类型的指针应用间接寻址运算符。 但是，你可以使用强制转换将 void 指针转换为任何其他指针类型，反之亦然。  
  
 指针可以为 `null`。 将间接寻址运算符应用于 null 指针将导致由实现定义的行为。  
  
 请注意，在方法之间传递指针会导致未定义的行为。 示例通过 Out 或 Ref 参数或作为函数结果返回一个指向局部变量的指针。 如果已在固定块中设置指针，则它指向的变量不再是固定的。  
  
 下表列出了可在不安全的上下文中对指针执行的运算符和语句：  
  
|运算符/语句|使用|  
|-------------------------|---------|  
|*|执行指针间接寻址。|  
|->|通过指针访问结构的成员。|  
|[]|为指针建立索引。|  
|`&`|获取变量的地址。|  
|++ 和 --|递增和递减指针。|  
|+ 和 -|执行指针算法。|  
|==、!=、\<、>、\<= 和 >=|比较指针。|  
|`stackalloc`|在堆栈上分配内存。|  
|`fixed` 语句|临时固定变量以便找到其地址。|  
  
## <a name="c-language-specification"></a>C# 语言规范  
 [!INCLUDE[CSharplangspec](~/includes/csharplangspec-md.md)]  
  
## <a name="see-also"></a>请参阅  
 [C# 编程指南](../../../csharp/programming-guide/index.md)   
 [不安全代码和指针](../../../csharp/programming-guide/unsafe-code-pointers/index.md)   
 [指针转换](../../../csharp/programming-guide/unsafe-code-pointers/pointer-conversions.md)   
 [指针表达式](../../../csharp/programming-guide/unsafe-code-pointers/pointer-expressions.md)   
 [类型](../../../csharp/language-reference/keywords/types.md)   
 [unsafe](../../../csharp/language-reference/keywords/unsafe.md)   
 [fixed 语句](../../../csharp/language-reference/keywords/fixed-statement.md)   
 [stackalloc](../../../csharp/language-reference/keywords/stackalloc.md)   
 [装箱和取消装箱](../../../csharp/programming-guide/types/boxing-and-unboxing.md)

