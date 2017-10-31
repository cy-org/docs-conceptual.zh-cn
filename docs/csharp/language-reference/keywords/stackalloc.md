---
title: "stackalloc（C# 参考）"
ms.date: 2015-07-20
ms.prod: .net
ms.technology:
- devlang-csharp
ms.topic: article
f1_keywords:
- stackalloc_CSharpKeyword
- stackalloc
dev_langs:
- CSharp
helpviewer_keywords:
- stackalloc keyword [C#]
ms.assetid: adc04c28-3ed2-4326-807a-7545df92b852
caps.latest.revision: 27
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
ms.openlocfilehash: 53d61cfdcf4d356a28881c57ad923017c2b479ae
ms.contentlocale: zh-cn
ms.lasthandoff: 09/25/2017

---
# <a name="stackalloc-c-reference"></a>stackalloc（C# 参考）
在不安全代码上下文中使用 `stackalloc` 关键字在堆栈上分配内存块。  
  
```  
int* block = stackalloc int[100];  
```  
  
## <a name="remarks"></a>备注  
 此关键字仅在局部变量初始值设定项中有效。 以下代码导致编译器错误。  
  
```  
int* block;  
// The following assignment statement causes compiler errors. You  
// can use stackalloc only when declaring and initializing a local   
// variable.  
block = stackalloc int[100];  
```  
  
 由于涉及指针类型，因此 `stackalloc` 需要 [unsafe](../../../csharp/language-reference/keywords/unsafe.md) 上下文。 有关详细信息，请参阅[不安全代码和指针](../../../csharp/programming-guide/unsafe-code-pointers/index.md)。  
  
 `stackalloc` 就像 C 运行时库中的 [_alloca](/cpp/c-runtime-library/reference/alloca)。  
  
 下面的示例计算并显示 Fibonacci 序列中的前 20 个数字。 每个数字是前两个数字的总和。 在此代码中，在堆栈上分配足够大的可包含 20 个 `int` 类型元素的内存块，而不是在堆上分配。 块的地址存储在指针 `fib` 中。 此内存不受垃圾回收的限制，因此不必对其进行单边锁定（使用 [fixed](../../../csharp/language-reference/keywords/fixed-statement.md)）。 内存块的生存期受到定义此内存块的方法的生存期的限制。 在方法返回之前，无法释放内存。  
  
## <a name="example"></a>示例  
 [!code-cs[csrefKeywordsOperator#15](../../../csharp/language-reference/keywords/codesnippet/CSharp/stackalloc_1.cs)]  
  
## <a name="security"></a>安全性  
 不安全代码的安全性低于安全替代项。 但是，使用 `stackalloc` 会自动启用公共语言运行时 (CLR) 中的缓冲区溢出检测功能。 如果检测到缓冲区溢出，则将尽快终止进程，以便将执行恶意代码的可能性降到最低。  
  
## <a name="c-language-specification"></a>C# 语言规范  
 [!INCLUDE[CSharplangspec](~/includes/csharplangspec-md.md)]  
  
## <a name="see-also"></a>请参阅  
 [C# 参考](../../../csharp/language-reference/index.md)   
 [C# 编程指南](../../../csharp/programming-guide/index.md)   
 [C# 关键字](../../../csharp/language-reference/keywords/index.md)   
 [运算符关键字](../../../csharp/language-reference/keywords/operator-keywords.md)   
 [不安全代码和指针](../../../csharp/programming-guide/unsafe-code-pointers/index.md)

