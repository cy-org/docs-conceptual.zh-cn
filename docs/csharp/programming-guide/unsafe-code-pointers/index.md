---
title: "不安全代码和指针（C# 编程指南）"
ms.date: 2015-07-20
ms.prod: .net
ms.technology:
- devlang-csharp
ms.topic: article
dev_langs:
- CSharp
helpviewer_keywords:
- security [C#], type safety
- C# language, unsafe code
- type safety [C#]
- unsafe keyword [C#]
- unsafe code [C#]
- C# language, pointers
- pointers [C#], about pointers
ms.assetid: b0fcca10-a92d-4f2a-835b-b0ccae6739ee
caps.latest.revision: 24
author: BillWagner
ms.author: wiwagn
translation.priority.ht:
- de-de
- es-es
- fr-fr
- it-it
- ja-jp
- ko-kr
- ru-ru
- zh-cn
- zh-tw
translation.priority.mt:
- cs-cz
- pl-pl
- pt-br
- tr-tr
ms.translationtype: HT
ms.sourcegitcommit: 306c608dc7f97594ef6f72ae0f5aaba596c936e1
ms.openlocfilehash: 75e11b34f0749270650e0e5b5a2a191a1b9e9f9a
ms.contentlocale: zh-cn
ms.lasthandoff: 07/28/2017

---
# <a name="unsafe-code-and-pointers-c-programming-guide"></a>不安全代码和指针（C# 编程指南）
为了保持类型安全性，默认情况下，C# 不支持指针算法。 但是，通过使用 [unsafe](../../../csharp/language-reference/keywords/unsafe.md) 关键字，可以定义可在其中使用指针的不安全上下文。 有关指针的详细信息，请参阅主题[指针类型](../../../csharp/programming-guide/unsafe-code-pointers/pointer-types.md)。  
  
> [!NOTE]
>  在公共语言运行时 (CLR) 中，不安全代码是指无法验证的代码。 C# 中的不安全代码不一定是危险的；只是 CLR 无法验证该代码的安全性。 因此，CLR 将仅执行完全信任的程序集中的不安全代码。 如果你使用不安全代码，你应该负责确保代码不会引发安全风险或指针错误。  
  
## <a name="unsafe-code-overview"></a>不安全代码概述  
 不安全代码具有以下属性：  
  
-   可将方法、类型和代码块定义为不安全。  
  
-   在某些情况下，通过移除数组绑定检查，不安全代码可提高应用程序的性能。  
  
-   调用需要指针的本机函数时，需使用不安全代码。  
  
-   使用不安全代码将引发安全风险和稳定性风险。  
  
-   为使 C# 能够编译不安全代码，必须用 [/unsafe](../../../csharp/language-reference/compiler-options/unsafe-compiler-option.md) 编译应用程序。  
  
## <a name="related-sections"></a>相关章节  
 有关详细信息，请参见:  
  
-   [指针类型](../../../csharp/programming-guide/unsafe-code-pointers/pointer-types.md)  
  
-   [固定大小的缓冲区](../../../csharp/programming-guide/unsafe-code-pointers/fixed-size-buffers.md)  
  
-   [如何：使用指针复制字节数组](../../../csharp/programming-guide/unsafe-code-pointers/how-to-use-pointers-to-copy-an-array-of-bytes.md)  
  
-   [unsafe](../../../csharp/language-reference/keywords/unsafe.md)  
  
## <a name="c-language-specification"></a>C# 语言规范  
 [!INCLUDE[CSharplangspec](~/includes/csharplangspec-md.md)]  
  
## <a name="see-also"></a>另请参阅  
 [C# 编程指南](../../../csharp/programming-guide/index.md)

