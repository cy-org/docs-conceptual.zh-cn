---
title: "固定大小的缓冲区（C# 编程指南）"
ms.date: 2015-07-20
ms.prod: .net
ms.technology:
- devlang-csharp
ms.topic: article
dev_langs:
- CSharp
helpviewer_keywords:
- fixed size buffers [C#]
- unsafe buffers [C#]
- unsafe code [C#], fixed size buffers
ms.assetid: 6220d454-947c-4977-ac9d-9308c6ed5051
caps.latest.revision: 31
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
ms.openlocfilehash: e1a3dcf953cb56fc3436fdd5e7ecb60478a12922
ms.contentlocale: zh-cn
ms.lasthandoff: 07/28/2017

---
# <a name="fixed-size-buffers-c-programming-guide"></a>固定大小的缓冲区（C# 编程指南）
在 C# 中，可以使用 [fixed](../../../csharp/language-reference/keywords/fixed-statement.md) 语句来创建在数据结构中具有固定大小的数组的缓冲区。 当使用现有代码（例如使用其他语言编写的代码、预先存在的 DLL 或 COM 项目）时，这非常有用。 固定的数组可以采用允许用于常规结构成员的任何属性或修饰符。 唯一的限制是数组类型必须为 `bool`、`byte`、`char`、`short`、`int`, `long`、`sbyte`、`ushort`、`uint`、`ulong`、`float` 或 `double`。  
  
```  
private fixed char name[30];  
```  
  
## <a name="remarks"></a>备注  
 在早期版本的 C# 中，声明 C++ 样式固定大小的结构是很困难的，因为包含数组的 C# 结构不包含数组元素。 而该结构包含对元素的引用。  
  
 C# 2.0 增加了在[结构](../../../csharp/language-reference/keywords/struct.md)中嵌入固定大小的数组的功能（当在[不安全的](../../../csharp/language-reference/keywords/unsafe.md)代码块中使用该数组时）。  
  
 例如，在 C# 2.0 之前，以下 `struct` 的大小为 8 个字节。 `pathName` 数组是对堆分配数组的引用：  
  
 [!code-cs[csProgGuidePointers#19](../../../csharp/programming-guide/unsafe-code-pointers/codesnippet/CSharp/fixed-size-buffers_1.cs)]  
  
 从 C# 2.0 开始，`struct` 可以包含嵌入的数组。 在下面的示例中，`fixedBuffer` 数组具有固定的大小。 若要访问数组的元素，请使用 `fixed` 语句，以建立指向第一个元素的指针。 `fixed` 语句将 `fixedBuffer` 的实例锁定到内存中的特定位置。  
  
 [!code-cs[csProgGuidePointers#20](../../../csharp/programming-guide/unsafe-code-pointers/codesnippet/CSharp/fixed-size-buffers_2.cs)]  
  
 包含 128 个元素的 `char` 数组的大小为 256 个字节。 固定大小的 [char](../../../csharp/language-reference/keywords/char.md) 缓冲区每个字符始终占用两个字节，而不考虑编码。 甚至在将 char 缓冲区封送到 API 方法或具有 `CharSet = CharSet.Auto` 或 `CharSet = CharSet.Ansi` 的结构时，这也为 true。 有关更多信息，请参见<xref:System.Runtime.InteropServices.CharSet>。  
  
 另一常见的固定大小的数组是 [bool](../../../csharp/language-reference/keywords/bool.md) 数组。 `bool` 数组中的元素大小始终为一个字节。 `bool` 数组不适用于创建位数组或缓冲区。  
  
> [!NOTE]
>  除了通过使用 [stackalloc](../../../csharp/language-reference/keywords/stackalloc.md) 创建的内存外，C# 编译器和公共语言运行时 (CLR) 不执行任何安全缓冲区溢出检查。 与所有不安全代码一样，请谨慎使用。  
  
 不安全的缓冲区与常规数组的区别体现在以下方面：  
  
-   只能在不安全的上下文中使用不安全的缓冲区。  
  
-   不安全的缓冲区始终是矢量或一维数组。  
  
-   数组的声明应包括计数，如 `char id[8]`。 不能改用 `char id[]`。  
  
-   在不安全的上下文中，不安全的缓冲区只能是结构的实例字段。  
  
## <a name="see-also"></a>另请参阅  
 [C# 编程指南](../../../csharp/programming-guide/index.md)   
 [不安全代码和指针](../../../csharp/programming-guide/unsafe-code-pointers/index.md)   
 [fixed 语句](../../../csharp/language-reference/keywords/fixed-statement.md)   
 [互操作性](../../../csharp/programming-guide/interop/index.md)

