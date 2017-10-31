---
title: "如何：标记语句 (Visual Basic) | Microsoft Docs"
ms.custom: ""
ms.date: "2015-07-20"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - ": 分隔符"
  - "冒号 (:)"
  - "语句 [Visual Basic], 标签"
  - "Visual Basic 代码, 标记语句"
ms.assetid: 38f1ff43-2054-42cb-963b-1998e60c6ed4
caps.latest.revision: 18
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 18
---
# 如何：标记语句 (Visual Basic)
[!INCLUDE[vs2017banner](../../../visual-basic/includes/vs2017banner.md)]

语句块由冒号分隔的代码行组成。  标识字符串或整数后的代码行称为“已标记”。  语句标签用来标记要标识的代码行，便于与 `On Error Goto` 之类的语句一起使用。  
  
 标签可能是标识符这样任何有效的 Visual Basic，如标识编程元素或整数标识符的类型。  标签必须出现在源代码行的行首，之后必须有冒号，无论在同一行内它后面有无语句。  
  
 编译器通过检查行首是否与任何已定义的标识符匹配来标识标签。  如果不匹配，编译器假定它是一个标签。  
  
 标签具有自己的声明空间，并不影响其他标识符。  标签的范围是方法的主体。  标签声明在任何模糊环境中都有优先权。  
  
> [!NOTE]
>  标签只能用于方法内的可执行语句中。  
  
### 标记代码行  
  
-   将标识符放在源代码行的行首，后面加上冒号。  
  
     例如，下列代码行分别标记为 `Jump` 和 `120`：  
  
     [!code-vb[VbVbalrStatements#708](../../../visual-basic/language-reference/error-messages/codesnippet/VisualBasic/how-to-label-statements_1.vb)]  
  
## 请参阅  
 [语句](../../../visual-basic/programming-guide/language-features/statements.md)   
 [已声明的元素名称](../../../visual-basic/programming-guide/language-features/declared-elements/declared-element-names.md)   
 [程序结构和代码约定](../../../visual-basic/programming-guide/program-structure/program-structure-and-code-conventions.md)