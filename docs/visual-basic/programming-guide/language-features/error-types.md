---
title: "错误类型 (Visual Basic 中) |Microsoft 文档"
ms.custom: 
ms.date: 2015-07-20
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology:
- devlang-visual-basic
ms.topic: article
helpviewer_keywords:
- exceptions, types
- errors [Visual Basic], types
- errors [Visual Basic], logic
- errors [Visual Basic], syntax
- logic errors, Visual Basic
- run-time errors, types of errors
- syntax errors, Visual Basic
ms.assetid: 3048aabf-8c97-4e13-9150-853769cb5f6f
caps.latest.revision: 13
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
ms.openlocfilehash: d48756b74baf757f043e68124d8b65c2f613e595
ms.lasthandoff: 03/13/2017

---
# <a name="error-types-visual-basic"></a>错误类型 (Visual Basic)
在[!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)]，错误 (也称为*异常*) 分为三个类别之一︰ 语法错误、 运行时错误和逻辑错误。  
  
## <a name="syntax-errors"></a>语法错误  
 *语法错误*是指那些编写代码时出现。 [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)]检查您的代码，并在您键入**代码编辑器**窗口，并提醒您，如果犯错，如拼错单词或不正确地使用一个语言元素。 语法错误则是最常见的错误类型。 您可以解决它们轻松地在编码的环境中就立即发生。  
  
> [!NOTE]
>  `Option Explicit`语句是一种避免语法错误。 它会强制您能够提前声明应用程序中使用的所有变量。 因此，当在代码中使用这些变量时，版式的任何错误都将被立即捕获，并且可以修复。  
  
## <a name="run-time-errors"></a>运行时错误  
 *运行时错误*是指那些仅在编译并运行您的代码后，才出现。 这些技术包括可能看上去没有问题，因为它有没有语法错误，但不是会执行的代码。 例如，您可能正确编写一行代码打开文件。 如果该文件已损坏，无法执行该应用程序，但`Open`函数，并且它将停止运行。 通过重写了错误代码，然后重新编译并重新运行它，可以修复大多数运行时错误。  
  
## <a name="logic-errors"></a>逻辑错误  
 *逻辑错误*是指那些正在使用应用程序后显示。 它们是以响应用户操作的大多数通常不需要的或意外结果。 例如，错误键入的键或其他外部影响可能会导致您的应用程序停止工作中预期的参数，或完全。 逻辑错误通常是最难的类型，若要修复，因为它不是始终清除它们发生的位置。  
  
## <a name="see-also"></a>另请参阅  
 [Try...Catch...Finally 语句](../../../visual-basic/language-reference/statements/try-catch-finally-statement.md)   
 [调试器基础知识](https://docs.microsoft.com/visualstudio/debugger/debugger-basics)
