---
title: "On Error 语句 (Visual Basic) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
f1_keywords: 
  - "vb.OnError"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "分支, on error"
  - "条件语句, On Error"
  - "控制流, 分支"
  - "错误处理, On Error 语句"
  - "Error 关键字"
  - "Error 语句, 和 On Error 语句"
  - "错误 [Visual Basic], 捕获"
  - "执行, conditional"
  - "GoTo 语句, 和 On Error 语句"
  - "Next 语句, On Error"
  - "On Error 语句"
  - "On Error 语句, 语法"
  - "On 关键字"
  - "Resume Next 语句"
  - "Resume 语句, 和 On Error 语句"
  - "运行时错误, 处理"
  - "Visual Basic 代码, 控制流"
ms.assetid: ff947930-fb84-40cf-bd66-1ea219561d5c
caps.latest.revision: 22
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 22
---
# On Error 语句 (Visual Basic)
[!INCLUDE[vs2017banner](../../../visual-basic/includes/vs2017banner.md)]

该语句启用错误处理例程，并指定该例程在过程中的位置；也可以用来禁用错误处理例程。  
  
 如果不使用 `On Error` 语句，所发生的任何运行时错误都会是致命的：显示错误信息，并且停止执行。  
  
 只要有可能，建议您使用结构化异常处理在代码中，使用非结构化异常处理和 `On Error` 语句，而不是。  有关更多信息，请参见 [Try...Catch...Finally 语句](../../../visual-basic/language-reference/statements/try-catch-finally-statement.md)。  
  
> [!NOTE]
>  `Error` 关键字也在 [Error 语句](../../../visual-basic/language-reference/statements/error-statement.md)中使用，以便能够向后兼容。  
  
## 语法  
  
```  
On Error { GoTo [ line | 0 | -1 ] | Resume Next }  
```  
  
## 部件  
  
|||  
|-|-|  
|术语|定义|  
|`GoTo` `line`|该语句启用从必选参数 `line` 指定的行开始的错误处理例程。  参数 `line` 可以是任意的行标签或行号。  如果发生了运行时错误，控制将跳转至指定行，以激活错误处理程序。  指定的行必须和 `On Error` 语句处在同一个过程中，否则会产生编译时错误。|  
|`GoTo` 0|该语句禁用当前过程中已启用的错误处理程序，并将其重置为 `Nothing`。|  
|`GoTo` \-1|该语句禁用当前过程中已启用的异常，并将其重置为 `Nothing`。|  
|`Resume Next`|该语句指定当发生运行时错误时，控制由错误语句跳转到紧随发生错误语句之后的语句，并从该位置继续执行。  在访问对象时，使用此形式而不是 `On Error GoTo`。|  
  
## 备注  
  
> [!NOTE]
>  建议使用非结构化异常处理和 `On Error` 语句，您可以在代码使用结构化异常处理只要有可能，而不是。  有关更多信息，请参见 [Try...Catch...Finally 语句](../../../visual-basic/language-reference/statements/try-catch-finally-statement.md)。  
  
 “enabled”错误处理程序是由 `On Error` 语句打开的一个错误处理程序。  “active”错误处理程序是处理错误过程中的已启用处理程序。  
  
 如果在错误处理程序处于活动状态期间发生错误（介于错误发生位置和 `Resume`、`Exit Sub`、`Exit Function` 或 `Exit Property` 语句之间），则当前过程的错误处理程序将无法处理该错误。  控制返回到调用过程。  
  
 如果调用过程有一个已启用的错误处理程序，该程序将被激活以处理错误。  如果调用过程的错误处理程序也处于活动状态，控制将继续返回到前一个调用过程，直到发现一个已启用的并且非活动的错误处理程序。  如果没有发现任何这样的错误处理程序，该错误就成为在其实际发生的位置处的致命错误。  
  
 每次错误处理程序将控制返回给调用过程时，那个过程就成为当前过程。  一旦错误由某一过程的错误处理程序进行了处理，程序的执行将在当前过程中由 `Resume` 语句指定的位置继续。  
  
> [!NOTE]
>  错误处理例程不是 `Sub` 过程或 `Function` 过程，  而是指由行标签或行号标识的一段代码。  
  
## Number 属性  
 错误处理例程根据 `Err` 对象的 `Number` 属性值来确定引起错误的原因。  在任何其他错误可能发生或者调用可能引发错误的过程之前，该例程应该测试或者保存 `Err` 对象的相关属性值。  `Err` 对象的属性值只反映最近的错误。  与 `Err.Number` 相关联的错误信息包含在 `Err.Description` 中。  
  
## Throw 语句  
 用 `Err.Raise` 方法引发的错误将 `Exception` 属性设置为 <xref:System.Exception> 类的新建实例。  为支持引发派生的异常类型的异常，本语言支持 `Throw` 语句。  该语句只带单个参数，代表将被引发的异常实例。  下面的示例显示了如何在现有的异常处理支持中使用这些特性：  
  
 [!code-vb[VbVbalrErrorHandling#17](../../../visual-basic/language-reference/statements/codesnippet/VisualBasic/on-error-statement_1.vb)]  
  
 请注意，`On Error GoTo` 语句捕获所有错误，与异常类无关。  
  
## On Error Resume Next  
 `On Error Resume Next` 会使程序从紧随产生错误的语句之后的语句继续执行，或是由紧随最近一次过程调用（该过程含有 `On Error Resume Next` 语句）之后的语句继续运行。  该语句允许即使发生了运行时错误时，仍继续执行。  可以在可能发生错误的位置放置错误处理例程，而不必将控制移交给过程中的另一位置。  在调用另一个过程时，`On Error Resume Next` 语句变为非活动状态。因此，如果希望在每一个调用的例程中进行内联错误处理，则应在例程中执行 `On Error Resume Next` 语句。  
  
> [!NOTE]
>  在处理访问其他对象期间生成的错误时，`On Error Resume Next` 构造可能比 `On Error GoTo` 更合适。  在每次与对象进行交互之后检查 `Err` 可以清楚地了解代码所访问的对象的情况。  由此，可以确定哪个对象在 `Err.Number` 中设置了错误代码，哪个对象导致了该错误（`Err.Source` 中指定的对象）。  
  
## On Error GoTo 0  
 `On Error GoTo 0` 禁止在当前过程中进行错误处理。  它不将行 0 指定为错误处理程序代码的开始，即使过程包含编号为 0 的行。  如果没有 `On Error GoTo 0` 语句，则在退出过程时会自动禁用错误处理程序。  
  
## On Error GoTo \-1  
 `On Error GoTo -1` 禁用当前过程中的异常。  它不将行 \-1 指定为错误处理程序代码的开始，即使过程包含编号为 \-1 的行。  如果没有 `On Error GoTo -1` 语句，则在退出过程时自动禁用异常。  
  
 若要防止错误处理代码在没有错误的情况下运行，请将 `Exit Sub`、`Exit Function` 或 `Exit Property` 语句放在紧靠错误处理例程之前，如以下片段所示：  
  
 [!code-vb[VbVbalrErrorHandling#18](../../../visual-basic/language-reference/statements/codesnippet/VisualBasic/on-error-statement_2.vb)]  
  
 此处，错误处理代码紧跟在 `Exit Sub` 语句之后，位于 `End Sub` 语句之前，这样就使其与过程流分离开。  当然，错误处理代码可以放在过程的任何位置。  
  
## 无法捕获的错误  
 当对象以可执行文件的方式运行时，对象中无法捕获的错误将返回给控制程序。  在开发环境中，只有进行了正确的选项设置，无法捕获的错误才被返回给控制程序。  请参见您的宿主应用程序文档，了解在调试过程中应该设置哪些选项，如何设置，以及宿主应用程序是否可以创建类。  
  
 如果创建了访问其他对象的对象，则应对任何它们可能传回的未处理错误进行处理。  如果无法处理，请将 `Err.Number` 中的错误代码映射到您自己的某个错误，并将其传回给对象的调用方。  应通过将错误代码添加到 `VbObjectError` 常数中来指定您的错误。  例如，如果您的错误代码是 1052，按照以下方式进行赋值：  
  
 [!code-vb[VbVbalrErrorHandling#19](../../../visual-basic/language-reference/statements/codesnippet/VisualBasic/on-error-statement_3.vb)]  
  
> [!CAUTION]
>  调用 Windows 动态链接库 \(DLL\) 时产生的系统错误并不引发异常，因而无法使用 Visual Basic 错误捕获机制进行捕获。  在调用 DLL 函数时，应该检查返回值以判断是否调用成功（根据 API 规范）；如果发生错误，则检查 `Err` 对象的 `LastDLLError` 属性值。  
  
## 示例  
 此示例首先使用 `On Error GoTo` 语句指定错误处理例程在过程中的位置。  在该示例中，被 0 除的尝试将生成错误号 6。  该错误将在错误处理例程中得到处理，然后控制权将返回到导致错误的语句。  `On Error GoTo 0` 语句关闭错误捕获。  然后 `On Error Resume Next` 语句将被用于推迟错误捕获，以确保能够肯定知道下一条语句所生成的错误所处的环境。  请注意，错误被处理后，将使用 `Err.Clear` 清除 `Err` 对象的属性。  
  
 [!code-vb[VbVbalrErrorHandling#20](../../../visual-basic/language-reference/statements/codesnippet/VisualBasic/on-error-statement_4.vb)]  
  
## 要求  
 **命名空间：** [Microsoft.VisualBasic](../../../visual-basic/language-reference/runtime-library-members.md)  
  
 **程序集：**Visual Basic 运行库（位于 Microsoft.VisualBasic.dll 中）  
  
## 请参阅  
 <xref:Microsoft.VisualBasic.Information.Err%2A>   
 <xref:Microsoft.VisualBasic.ErrObject.Number%2A>   
 <xref:Microsoft.VisualBasic.ErrObject.Description%2A>   
 <xref:Microsoft.VisualBasic.ErrObject.LastDllError%2A>   
 [End 语句](../../../visual-basic/language-reference/statements/end-statement.md)   
 [Exit 语句](../../../visual-basic/language-reference/statements/exit-statement.md)   
 [Resume 语句](../../../visual-basic/language-reference/statements/resume-statement.md)   
 [错误消息](../../../visual-basic/language-reference/error-messages/index.md)   
 [Try...Catch...Finally 语句](../../../visual-basic/language-reference/statements/try-catch-finally-statement.md)