---
title: "错误消息 (Visual Basic)"
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
- errors [Visual Basic]
- error messages
- trappable errors
- errors [Visual Basic], trappable
ms.assetid: f2dda05b-baef-41f5-8bb1-598bd7cf239f
caps.latest.revision: 19
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
ms.translationtype: HT
ms.sourcegitcommit: 306c608dc7f97594ef6f72ae0f5aaba596c936e1
ms.openlocfilehash: cbeca9d1b6971f8b3de112eb6a199b8bacbc1670
ms.contentlocale: zh-cn
ms.lasthandoff: 07/28/2017

---
# <a name="error-messages-visual-basic"></a>错误消息 (Visual Basic)
编写、编译或运行 Visual Basic 应用程序时，可能会生成以下类型的错误：  
  
1.  在 Visual Studio 中编写应用程序时发生的设计时错误。  
  
2.  在 Visual Studio 或命令提示符中编译应用程序时发生的编译时错误。  
  
3.  在 Visual Studio 中运行应用程序或作为独立可执行文件运行时发生的运行时错误。  
  
 若要了解如何排查特定错误，请参阅[为 Visual Basic 程序员提供的附加资源](../../../visual-basic/getting-started/additional-resources.md)。  
  
## <a name="run-time-errors"></a>运行时错误  
 如果 Visual Basic 应用程序试图执行系统无法执行的操作，则会生成运行时错误，并且 [!INCLUDE[vbprvb](~/includes/vbprvb-md.md)] 会抛出 `Exception` 对象。 [!INCLUDE[vbprvb](~/includes/vbprvb-md.md)] 可以使用 `Throw` 语句生成任何数据类型的自定义错误，包括 `Exception` 对象。 应用程序可以通过显示捕获到的异常的错误号和消息来识别错误。 如果未捕获到错误，应用程序会结束。  
  
 代码可用于捕获和检查运行时错误。 如果将生成错误的代码封闭在 `Try` 代码块中，则可以在匹配的 `Catch` 代码块中捕获抛出的任何错误。 若要了解如何在运行时捕获错误并在代码中响应错误，请参阅 [Try...Catch...Finally 语句](../../../visual-basic/language-reference/statements/try-catch-finally-statement.md)。  
  
## <a name="compile-time-errors"></a>编译时错误  
 如果 Visual Basic 编译器遇到代码问题，则会发生编译时错误。 在代码编辑器中，可以轻松确定哪行代码导致错误发生，因为其下方会显示一条波形线。 指向波形下划线或打开“错误列表”，即可看到错误消息（还可以查看其他消息）。  
  
 如果标识符有波形下划线，且最右边的字符下面有短下划线，可以为类、构造函数、方法、属性、字段或枚举生成存根。 有关详细信息，请参阅[根据使用情况生成](/visualstudio/ide/visual-csharp-intellisense#generate-from-usage)。
  
 通过解决 Visual Basic 编译器警告提示的问题，可以编写运行速度更快、bug 更少的代码。 这些警告可以识别可能会在应用程序运行时生成错误的代码。 例如，如果尝试调用未赋值的对象变量的成员、让未设置返回值的函数返回值或执行有逻辑错误的 `Try` 代码块来捕获异常，编译器都会生成警告。 若要详细了解警告（包括如何启用和禁用警告），请参阅[在 Visual Basic 中配置警告](/visualstudio/ide/configuring-warnings-in-visual-basic)。

