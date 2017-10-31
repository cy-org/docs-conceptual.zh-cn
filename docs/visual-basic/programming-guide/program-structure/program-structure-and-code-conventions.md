---
title: "程序结构和代码约定 (Visual Basic 中) |Microsoft 文档"
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
- coding conventions
- Visual Basic code, coding conventions
- coding conventions, Visual Basic
- programs, structure
- program structure
- naming conventions, Visual Basic
- best practices, coding conventions
- conventions, Visual Basic coding
- Visual Basic code
- programming, Visual Basic coding conventions
ms.assetid: dd9be76f-6944-4e78-ad72-0b6084a3fc13
caps.latest.revision: 21
author: dotnet-bot
ms.author: dotnetcontent
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
translationtype: Machine Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: cd25d99d74bf1e4d416c9da63758f6ad04027258
ms.lasthandoff: 03/13/2017

---
# <a name="program-structure-and-code-conventions-visual-basic"></a>程序结构和代码约定 (Visual Basic)
本部分介绍的典型[!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)]程序结构中，提供了一个简单[!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)]程序，"Hello，World"，并讨论了[!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)]代码约定。 代码约定是针对不是程序的逻辑，而是其物理结构和外观的建议值。 按照它们使您的代码易于阅读、 理解和维护。 其他项中，代码约定，可以包括︰  
  
-   添加标记和注释的代码的标准化的格式。  
  
-   间距、 格式和缩进代码的指南。  
  
-   对象、 变量和过程的命名约定。  
  
 下列主题显示了一组编程指导方针[!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)]计划，以及一些很好的用法示例。  
  
## <a name="in-this-section"></a>本节内容  
 [Visual Basic 程序的结构](../../../visual-basic/programming-guide/program-structure/structure-of-a-visual-basic-program.md)  
 提供构成元素的概述[!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)]程序。  
  
 [在 Visual Basic 中的 main 过程](../../../visual-basic/programming-guide/program-structure/main-procedure.md)  
 讨论的过程作为起始点，以及对您的应用程序总体控制。  
  
 [引用和 Imports 语句](../../../visual-basic/programming-guide/program-structure/references-and-the-imports-statement.md)  
 讨论如何引用其他程序集中的对象。  
  
 [在 Visual Basic 中的命名空间](../../../visual-basic/programming-guide/program-structure/namespaces.md)  
 描述如何命名空间组织内的程序集的对象。  
  
 [Visual Basic 命名约定](../../../visual-basic/programming-guide/program-structure/naming-conventions.md)  
 包括命名过程、 常量、 变量、 参数和对象的一般准则。  
  
 [Visual Basic 编码约定](../../../visual-basic/programming-guide/program-structure/coding-conventions.md)  
 查看在开发本文档中的示例使用的准则。  
  
 [条件编译](../../../visual-basic/programming-guide/program-structure/conditional-compilation.md)  
 描述如何同时控制编译器忽略其他有选择性地编译的代码的特定块。  
  
 [如何：在代码中拆分和合并语句](../../../visual-basic/programming-guide/program-structure/how-to-break-and-combine-statements-in-code.md)  
 演示如何将划分为多行的长语句和合并内容位于一行的短语句。  
  
 [如何：折叠和隐藏代码节](../../../visual-basic/programming-guide/program-structure/how-to-collapse-and-hide-sections-of-code.md)  
 演示如何以折叠和隐藏代码节[!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)]代码编辑器中。  
  
 [如何：标记语句](../../../visual-basic/programming-guide/program-structure/how-to-label-statements.md)  
 演示如何将标记的一行代码以将其标识用于使用语句如`On Error Goto`。  
  
 [代码中的特殊字符](../../../visual-basic/programming-guide/program-structure/special-characters-in-code.md)  
 演示如何以及在何处使用非数字和非字母字符。  
  
 [代码中的注释](../../../visual-basic/programming-guide/program-structure/comments-in-code.md)  
 讨论如何向代码中添加说明性注释。  
  
 [代码中用作元素名称的关键字](../../../visual-basic/programming-guide/program-structure/keywords-as-element-names-in-code.md)  
 介绍如何使用方括号 (`[]`) 来分隔还有的变量名[!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)]关键字。  
  
 [Me、My、MyBase 和 MyClass](../../../visual-basic/programming-guide/program-structure/me-my-mybase-and-myclass.md)  
 介绍各种方式引用的元素[!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)]程序。  
  
 [Visual Basic 限制](../../../visual-basic/programming-guide/program-structure/limitations.md)  
 讨论中已知的编码限制删除[!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)]。  
  
## <a name="related-sections"></a>相关章节  
 [版式和代码约定](../../../visual-basic/language-reference/typographic-and-code-conventions.md)  
 提供了有关标准编码约定[!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)]。  
  
 [编写代码](https://docs.microsoft.com/visualstudio/ide/writing-code-in-the-code-and-text-editor)  
 介绍使您更轻松地编写和管理您的代码的功能。
