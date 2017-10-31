---
title: "如何：使用 try-catch 处理异常（C# 编程指南）"
ms.date: 2015-07-20
ms.prod: .net
ms.technology:
- devlang-csharp
ms.topic: article
dev_langs:
- CSharp
helpviewer_keywords:
- exception handling [C#], try/catch blocks
- exceptions [C#], try/catch blocks
- try/catch blocks [C#]
ms.assetid: ca8e3773-980e-4767-8633-7408540e9818
caps.latest.revision: 14
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
ms.openlocfilehash: f6f714cd1b652845e77405ff74fbfc860e71dc21
ms.contentlocale: zh-cn
ms.lasthandoff: 07/28/2017

---
# <a name="how-to-handle-an-exception-using-trycatch-c-programming-guide"></a>如何：使用 try/catch 处理异常（C# 编程指南）
[try-catch](../../../csharp/language-reference/keywords/try-catch.md) 块的用途是捕获并处理工作代码产生的异常。 某些异常可以在 `catch` 块中进行处理，问题得以解决并不再出现异常；但是，大多数情况下你唯一可做的是确保引发的异常是合理异常。  
  
## <a name="example"></a>示例  
 在此示例中，<xref:System.IndexOutOfRangeException> 不是最合理的异常：<xref:System.ArgumentOutOfRangeException> 对于此方法来说更有意义，因为此错误是由调用方传递的 `index` 参数引起的。  
  
 [!code-cs[csProgGuideExceptions#5](../../../csharp/programming-guide/exceptions/codesnippet/CSharp/how-to-handle-an-exception-using-try-catch_1.cs)]  
  
## <a name="comments"></a>注释  
 引发异常的代码包含在 `try` 块中。 在此块后面紧挨着添加 `catch` 语句以处理 `IndexOutOfRangeException` 异常（如果发生此异常）。 `catch` 块处理 `IndexOutOfRangeException` 异常并改为引发更合理的 `ArgumentOutOfRangeException` 异常。 为了向调用方提供尽可能多的信息，请考虑将原始异常指定为新异常的 <xref:System.Exception.InnerException%2A>。 因为 <xref:System.Exception.InnerException%2A> 属性为 [readonly](../../../csharp/language-reference/keywords/readonly.md)，所以必须在新异常的构造函数中指定此属性。  
  
## <a name="see-also"></a>另请参阅  
 [C# 编程指南](../../../csharp/programming-guide/index.md)   
 [异常和异常处理](../../../csharp/programming-guide/exceptions/index.md)   
 [异常处理](../../../csharp/programming-guide/exceptions/exception-handling.md)

