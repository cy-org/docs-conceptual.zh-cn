---
title: "Visual Basic 限制 |Microsoft 文档"
ms.custom: 
ms.date: 2015-07-20
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology:
- devlang-visual-basic
ms.topic: article
dev_langs:
- VB
helpviewer_keywords:
- limits
- limitations, Visual Basic
- limitations
- limits, Visual Basic code
- Visual Basic code, limitations
ms.assetid: cf1646b7-5d24-48c6-9616-bda8a4849d91
caps.latest.revision: 14
author: dotnet-bot
ms.author: dotnetcontent
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
translationtype: Machine Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: d556b045b4ebae6ba24c0571a6cb7e5337c6a8f2
ms.lasthandoff: 03/13/2017

---
# <a name="visual-basic-limitations"></a>Visual Basic 限制
早期版本的[!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)]强制在代码中，如变量名的长度的边界中的模块和模块的大小允许的变量的数目。 在[!INCLUDE[vbprvblong](../../../visual-basic/developing-apps/customizing-extending-my/includes/vbprvblong_md.md)]，已放宽这些限制，使您可以编写和安排您的代码以更大的自由度。  
  
 所依赖的编译时的注意事项的更多地运行时内存比物理限制。 如果你使用比较明智的做法的编程方法，并将大型应用程序划分为多个类和模块，则没有遇到内部的可能性很小[!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)]限制。  
  
 以下是在极端情况下可能会遇到一些限制︰  
  
-   **名称长度。** 没有最大为每个已声明的编程元素的名称的字符数。 如果元素名称进行限定，此最大值适用于整个限定字符串。 请参阅[声明的元素名称](../../../visual-basic/programming-guide/language-features/declared-elements/declared-element-names.md)。  
  
-   **行长度。** 则最多 65535 中的字符代码的源代码在物理行。 可以使用行继续符的情况下更长的逻辑的源代码行。 请参阅[如何︰ 拆分和合并代码中的语句](../../../visual-basic/programming-guide/program-structure/how-to-break-and-combine-statements-in-code.md)。  
  
-   **数组维度。** 有可以声明为数组的维数的最大数目。 这就限制了多少个索引可用于指定数组元素。 请参阅[数组在 Visual Basic 中的维度](../../../visual-basic/programming-guide/language-features/arrays/array-dimensions.md)。  
  
-   **字符串长度。** 有可以存储在单个字符串中的 Unicode 字符的最大数目。 请参阅[字符串数据类型](../../../visual-basic/language-reference/data-types/string-data-type.md)。  
  
-   **环境字符串的长度。** 没有为 32768 个字符作为命令行参数使用任何环境字符串的最大值。 这是在所有平台上的限制。  
  
## <a name="see-also"></a>另请参阅  
 [程序结构和代码约定](../../../visual-basic/programming-guide/program-structure/program-structure-and-code-conventions.md)   
 [Visual Basic 命名约定](../../../visual-basic/programming-guide/program-structure/naming-conventions.md)
