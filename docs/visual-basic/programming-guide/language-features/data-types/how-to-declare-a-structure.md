---
title: "如何：声明结构 (Visual Basic) | Microsoft Docs"
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
  - "声明, 结构"
  - "语句 [Visual Basic], 结构"
  - "结构语句"
  - "结构, 声明"
ms.assetid: d5e98381-eb81-47d4-af83-48cc534a2572
caps.latest.revision: 15
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 15
---
# 如何：声明结构 (Visual Basic)
[!INCLUDE[vs2017banner](../../../../visual-basic/includes/vs2017banner.md)]

使用语句作为结构声明的开始， [Structure 语句](../../../../visual-basic/language-reference/statements/structure-statement.md)因此，您关闭它与 `End` `Structure` 语句。  在这两个语句之间必须至少声明一个 *元素*。  元素可以是任何数据类型，但是，至少一个必须是非共享变量或非共享，非自定义事件。  
  
 无法初始化任何一个在结构声明的结构元素。  当您将变量声明为结构类型，则可以将值分配给组件通过访问它们将变量。  
  
 关于结构和类之间的区别的讨论，请参见 [结构和类](../../../../visual-basic/programming-guide/language-features/data-types/structures-and-classes.md)。  
  
 出于演示的目的，请考虑要跟踪雇员的姓名、电话分机和薪水的情况。  结构允许您执行此在单个变量。  
  
### 声明结构  
  
1.  创建结构的开始和结束语句。  
  
     使用， [Protected](../../../../visual-basic/language-reference/modifiers/protected.md)， [Friend](../../../../visual-basic/language-reference/modifiers/friend.md)或者 [Private](../../../../visual-basic/language-reference/modifiers/private.md) 关键字，可以指定结构的 [Public](../../../../visual-basic/language-reference/modifiers/public.md)访问级别 [Protected](../../../../visual-basic/language-reference/modifiers/protected.md) ，或者使用默认值为 `Public`。  
  
    ```  
    Private Structure employee  
    End Structure  
    ```  
  
2.  将元素添加到框架中的主体。  
  
     结构必须至少有一个元素。  必须声明每个元素并指定其访问级别。  如果使用 [Dim 语句](../../../../visual-basic/language-reference/statements/dim-statement.md) 不含任何关键字，则可访问性默认为 `Public`。  
  
    ```  
    Private Structure employee  
        Public givenName As String  
        Public familyName As String  
        Public phoneExtension As Long  
        Private salary As Decimal  
        Public Sub giveRaise(raise As Double)  
            salary *= raise  
        End Sub  
        Public Event salaryReviewTime()  
    End Structure  
    ```  
  
     前面示例中的 `salary` 字段是 `Private`，这意味着不能从结构之外不可访问，即使是从包含类。  但是， `giveRaise` 程序是 `Public`，因此，它可以从结构之外调用。  同样，可以从结构之外引发 `salaryReviewTime` 事件。  
  
     除了变量之外， `Sub` 程序和事件，还可以定义常数、 `Function` 程序和属性在结构。  ，只要该属性具有至少一个参数，可将最多一个属性作为 *默认属性*。  可以处理与`Sub` 程序的 [Shared](../../../../visual-basic/language-reference/modifiers/shared.md)事件。  有关更多信息，请参见 [如何：在 Visual Basic 中声明和调用默认属性](../../../../visual-basic/programming-guide/language-features/procedures/how-to-declare-and-call-a-default-property.md)。  
  
## 请参阅  
 [数据类型](../../../../visual-basic/programming-guide/language-features/data-types/index.md)   
 [基本数据类型](../../../../visual-basic/programming-guide/language-features/data-types/elementary-data-types.md)   
 [复合数据类型](../../../../visual-basic/programming-guide/language-features/data-types/composite-data-types.md)   
 [值类型和引用类型](../../../../visual-basic/programming-guide/language-features/data-types/value-types-and-reference-types.md)   
 [结构](../../../../visual-basic/programming-guide/language-features/data-types/structures.md)   
 [数据类型疑难解答](../../../../visual-basic/programming-guide/language-features/data-types/troubleshooting-data-types.md)   
 [结构变量](../../../../visual-basic/programming-guide/language-features/data-types/structure-variables.md)   
 [结构和其他编程元素](../../../../visual-basic/programming-guide/language-features/data-types/structures-and-other-programming-elements.md)   
 [结构和类](../../../../visual-basic/programming-guide/language-features/data-types/structures-and-classes.md)   
 [用户定义的数据类型](../../../../visual-basic/language-reference/data-types/user-defined-data-type.md)