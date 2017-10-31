---
title: "无法将匿名类型转换为表达式树，因为它包含用于初始化另一个字段的字段 | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
f1_keywords: 
  - "bc36548"
  - "vbc36548"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "BC36548"
ms.assetid: 27de068f-080e-4160-86bf-1ec23fd1925a
caps.latest.revision: 9
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 9
---
# 无法将匿名类型转换为表达式树，因为它包含用于初始化另一个字段的字段
[!INCLUDE[vs2017banner](../../../visual-basic/includes/vs2017banner.md)]

如果匿名类型的一个属性用于初始化匿名类型的另一个属性，则编译器无法接受将该匿名类型转换为表达式树。  例如，在下面的代码中，先在初始化列表中声明 `Prop1`，然后将其用作 `Prop2` 的初始值。  
  
```vb#  
Module M2  
  
    Sub ExpressionExample(Of T)(ByVal x As Expressions.Expression(Of Func(Of T)))  
    End Sub  
  
    Sub Main()  
        ' The following line causes the error.  
        ' ExpressionExample(Function() New With {.Prop1 = 2, .Prop2 = .Prop1})  
  
    End Sub  
End Module  
```  
  
 **错误 ID：**BC36548  
  
### 更正此错误  
  
-   将 `Prop1` 的初始值赋予局部变量。  将该变量分配给 `Prop1` 和 `Prop2`，如下面的代码所示。  
  
    ```  
    Sub Main()  
  
        Dim temp = 2  
        ExpressionExample(Function() New With {.Prop1 = temp, .Prop2 = temp})  
  
    End Sub  
    ```  
  
## 请参阅  
 [匿名类型](../../../visual-basic/programming-guide/language-features/objects-and-classes/anonymous-types.md)   
 [表达式树](../Topic/Expression%20Trees%20\(C%23%20and%20Visual%20Basic\).md)   
 [如何：使用表达式树来生成动态查询](../Topic/How%20to:%20Use%20Expression%20Trees%20to%20Build%20Dynamic%20Queries%20\(C%23%20and%20Visual%20Basic\).md)