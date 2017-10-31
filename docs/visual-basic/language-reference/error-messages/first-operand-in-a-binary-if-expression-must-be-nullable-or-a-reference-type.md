---
title: "二元“If”表达式中的第一个操作数必须是可以为 null 的类型或引用类型 | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
f1_keywords: 
  - "bc33107"
  - "vbc33107"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "BC33107"
ms.assetid: 493c8899-3f6b-4471-8eb6-9284e8492768
caps.latest.revision: 5
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 5
---
# 二元“If”表达式中的第一个操作数必须是可以为 null 的类型或引用类型
[!INCLUDE[vs2017banner](../../../visual-basic/includes/vs2017banner.md)]

`If` 表达式可以采用两个或三个参数。  当仅发送两个参数时，第一个参数必须为引用类型或可以为 null 的类型。  如果第一个参数的计算结果不为 `Nothing`，则返回第一个参数的值。  如果第一个参数的计算结果为 `Nothing`，则计算并返回第二个参数的值。  
  
 例如，下面的代码包含两个 `If` 表达式，其中一个表达式具有三个参数，另一个具有两个参数。  这两个表达式的计算结果相同并返回相同的值。  
  
```vb#  
' firstChoice is a nullable value type.  
Dim firstChoice? As Integer = Nothing  
Dim secondChoice As Integer = 1128  
' If expression with three arguments.  
Console.WriteLine(If(firstChoice IsNot Nothing, firstChoice, secondChoice))  
' If expression with two arguments.  
Console.WriteLine(If(firstChoice, secondChoice))  
```  
  
 下面的表达式将导致该错误：  
  
```vb#  
Dim choice1 = 4  
Dim choice2 = 5  
Dim booleanVar = True  
  
' Not valid.  
'Console.WriteLine(If(choice1 < choice2, 1))  
' Not valid.  
'Console.WriteLine(If(booleanVar, "Test returns True."))  
```  
  
 **错误 ID：**BC33107  
  
### 更正此错误  
  
-   如果无法更改代码以使第一个参数是可以为 null 的类型或引用类型，请考虑将其转换为包含三个参数的 `If` 表达式，或者转换为 `If...Then...Else` 语句。  
  
    ```vb#  
    Console.WriteLine(If(choice1 < choice2, 1, 2))  
    Console.WriteLine(If(booleanVar, "Test returns True.", "Test returns False."))  
    ```  
  
## 请参阅  
 [If 运算符](../../../visual-basic/language-reference/operators/if-operator.md)   
 [If...Then...Else 语句](../../../visual-basic/language-reference/statements/if-then-else-statement.md)   
 [可以为 Null 的值类型](../../../visual-basic/programming-guide/language-features/data-types/nullable-value-types.md)