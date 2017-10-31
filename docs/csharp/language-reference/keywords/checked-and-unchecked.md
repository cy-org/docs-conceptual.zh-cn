---
title: "Checked 和 Unchecked（C# 参考）"
ms.date: 2015-07-20
ms.prod: .net
ms.technology:
- devlang-csharp
ms.topic: article
dev_langs:
- CSharp
helpviewer_keywords:
- operators [C#], checked and unchecked
- exceptions [C#], overflow checking
- checked statement [C#]
- overflow checking [C#]
- unchecked statement [C#]
- statements [C#], checked and unchecked
ms.assetid: a84bc877-2c7f-4396-8735-1ce97c42f35e
caps.latest.revision: 17
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
ms.openlocfilehash: 744f59dbf7ee8370010ff76d4e9dde20490de403
ms.contentlocale: zh-cn
ms.lasthandoff: 07/28/2017

---
# <a name="checked-and-unchecked-c-reference"></a>Checked 和 Unchecked（C# 参考）
C# 语句既可以在已检查的上下文中执行，也可以在未检查的上下文中执行。 在已检查的上下文中，算法溢出引发异常。 在未检查的上下文中，算法溢出被忽略并且结果被截断。  
  
-   [checked](../../../csharp/language-reference/keywords/checked.md) 指定已检查的上下文。  
  
-   [unchecked](../../../csharp/language-reference/keywords/unchecked.md) 指定未检查的上下文。  
  
 如果既未指定 `unchecked``checked` 也未指定 ，则默认上下文取决于外部因素（如编译器选项）。  
  
 下列操作受溢出检查的影响：  
  
-   表达式在整型上使用下列预定义运算符：  
  
     `++` `--` - (unary)   `+` -   `*` `/`  
  
-   整型间的显式数字转换。  
  
 使用 [/checked](../../../csharp/language-reference/compiler-options/checked-compiler-option.md) 编译器选项，可以为非明确位于 `checked` 或 `unchecked` 关键字范围内的所有整型算术语句指定已检查或未检查的上下文。  
  
## <a name="see-also"></a>另请参阅  
 [C# 参考](../../../csharp/language-reference/index.md)   
 [C# 编程指南](../../../csharp/programming-guide/index.md)   
 [C# 关键字](../../../csharp/language-reference/keywords/index.md)   
 [语句关键字](../../../csharp/language-reference/keywords/statement-keywords.md)

