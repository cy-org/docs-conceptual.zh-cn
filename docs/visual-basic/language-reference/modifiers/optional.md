---
title: "Optional (Visual Basic) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
f1_keywords: 
  - "vb.Optional"
  - "vb.optional"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "Optional 关键字"
  - "Optional 关键字, 上下文"
ms.assetid: 4571ce88-a539-4115-b230-54eb277c6aa7
caps.latest.revision: 14
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 14
---
# Optional (Visual Basic)
[!INCLUDE[vs2017banner](../../../visual-basic/includes/vs2017banner.md)]

指定在调用过程时可以省略过程参数。  
  
## 备注  
 对于每个可选参数，必须指定常数表达式作为该参数的默认值。  如果表达式的计算结果为 [nothing](../../../visual-basic/language-reference/nothing.md)，值数据类型的默认值用作该参数的默认值。  
  
 如果参数包含一个可选参数，其后的每个参数也都必须是可选的。  
  
 `Optional` 修饰符可用于下面的上下文中：  
  
-   [Declare 语句](../../../visual-basic/language-reference/statements/declare-statement.md)  
  
-   [Function 语句](../../../visual-basic/language-reference/statements/function-statement.md)  
  
-   [Property 语句](../../../visual-basic/language-reference/statements/property-statement.md)  
  
-   [Sub 语句](../../../visual-basic/language-reference/statements/sub-statement.md)  
  
> [!NOTE]
>  在调用程序 \(带或不带可选参数时，可以通过位置的名称参数或。  有关更多信息，请参见 [按位置和按名称传递参数](../../../visual-basic/programming-guide/language-features/procedures/passing-arguments-by-position-and-by-name.md)。  
  
> [!NOTE]
>  通过使用重载，还可以定义带可选参数的过程。  如果有一个可选参数，可以定义接受此参数不的两个重载版本的程序，一个和一个。  有关更多信息，请参见 [过程重载](../../../visual-basic/programming-guide/language-features/procedures/procedure-overloading.md)。  
  
## 示例  
 下面的示例定义了一个可选参数的过程。  
  
```  
Public Function FindMatches(ByRef values As List(Of String),  
                            ByVal searchString As String,  
                            Optional ByVal matchCase As Boolean = False) As List(Of String)  
  
    Dim results As IEnumerable(Of String)  
  
    If matchCase Then  
        results = From v In values  
                  Where v.Contains(searchString)  
    Else  
        results = From v In values  
                  Where UCase(v).Contains(UCase(searchString))  
    End If  
  
    Return results.ToList()  
End Function  
```  
  
## 示例  
 下面的示例演示如何调用一个过程具有位置传递的参数并按名称传递参数。  该程序有两个可选参数。  
  
 [!code-vb[VbVbalrKeywords#21](../../../visual-basic/language-reference/codesnippet/VisualBasic/optional_1.vb)]  
  
## 请参阅  
 [参数列表](../../../visual-basic/language-reference/statements/parameter-list.md)   
 [可选参数](../../../visual-basic/programming-guide/language-features/procedures/optional-parameters.md)   
 [关键字](../../../visual-basic/language-reference/keywords/index.md)