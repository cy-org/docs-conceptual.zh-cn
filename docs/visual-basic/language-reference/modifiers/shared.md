---
title: "Shared (Visual Basic) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
f1_keywords: 
  - "vb.Shared"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "元素, 共享"
  - "成员, 共享"
  - "非共享"
  - "共享元素"
  - "Shared 关键字"
  - "共享成员"
ms.assetid: 2bf7cf2c-b0dd-485e-8749-b5d674dab4cd
caps.latest.revision: 16
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 16
---
# Shared (Visual Basic)
[!INCLUDE[vs2017banner](../../../visual-basic/includes/vs2017banner.md)]

指定一个或多个声明的编程元素与一个类或结构在整体上相关联，而不是与类或结构的特定实例关联。  
  
## 备注  
  
## 何时使用 Shared  
 共享类或结构的成员使每个实例都可以使用该成员，而不是采用非共享模式，在非共享模式下，每个实例都需要有自己的副本。  例如，如果一个变量的值应用于整个应用程序，这点很有用。  如果声明该变量为 `Shared`，那么所有实例会访问相同的存储位置，而如果一个实例更改了变量值，所有实例都会访问更新后的值。  
  
 共享不改变成员的访问级别。  例如，类成员可以为共享的和私有的（只能从类的内部进行访问），也可以为非共享的和公共的。  有关更多信息，请参见 [Visual Basic 中的访问级别](../../../visual-basic/programming-guide/language-features/declared-elements/access-levels.md)。  
  
## 规则  
  
-   **声明上下文。**仅可以在模块级别使用 `Shared`。  这意味着 `Shared` 元素的声明上下文必须是类或结构，不能是源文件、命名空间或过程。  
  
-   **组合修饰符。**不能在同一声明中将 `Shared` 与 [Overrides](../../../visual-basic/language-reference/modifiers/overrides.md)、[Overridable](../../../visual-basic/language-reference/modifiers/overridable.md)、[NotOverridable](../../../visual-basic/language-reference/modifiers/notoverridable.md)、[MustOverride](../../../visual-basic/language-reference/modifiers/mustoverride.md) 或 [Static](../../../visual-basic/language-reference/modifiers/static.md) 同时指定。  
  
-   **访问。**通过用类或结构名称而不是类或结构的特定实例的变量名称限定一个共享元素来访问它。  您甚至不必创建类或结构的实例就可以访问它的共享成员。  
  
     下面的示例调用由 <xref:System.Double> 结构所公开的共享过程 <xref:System.Double.IsNaN%2A>。  
  
     `If Double.IsNaN(result) Then MsgBox("Result is mathematically undefined.")`  
  
-   **隐式共享。**您无法在 [Const 语句](../../../visual-basic/language-reference/statements/const-statement.md) 中使用 `Shared` 修饰符，但常数会被隐式共享。  同样，您无法将模块或接口的成员声明为 `Shared`，但它们会被隐式共享。  
  
## 行为  
  
-   **存储。**共享变量或事件只能在内存中存储一次，而无论您创建多少个它的类或结构的实例。  同样，共享过程或属性仅存储一组局部变量。  
  
-   **通过实例变量进行访问。**可以通过用包含类或结构的特定实例的变量名称限定一个共享元素来访问它。  虽然这通常会按预期设想起作用，但编译器会生成一条警告消息，并使访问通过类或结构名称而不是变量来进行。  
  
-   **通过实例表达式进行访问。**通过返回类或结构实例的表达式访问共享元素时，编译器会使访问通过类或结构名称而不是计算表达式来进行。  如果您要表达式执行其他操作以及返回实例，将产生意外结果。  下面的示例阐释了这一点。  
  
    ```  
    Sub main()  
        shareTotal.total = 10  
        ' The preceding line is the preferred way to access total.  
        Dim instanceVar As New shareTotal  
        instanceVar.total += 100  
        ' The preceding line generates a compiler warning message and  
        ' accesses total through class shareTotal instead of through  
        ' the variable instanceVar. This works as expected and adds  
        ' 100 to total.  
        returnClass().total += 1000  
        ' The preceding line generates a compiler warning message and  
        ' accesses total through class shareTotal instead of calling  
        ' returnClass(). This adds 1000 to total but does not work as  
        ' expected, because the MsgBox in returnClass() does not run.  
        MsgBox("Value of total is " & CStr(shareTotal.total))  
    End Sub  
    Public Function returnClass() As shareTotal  
        MsgBox("Function returnClass() called")  
        Return New shareTotal  
    End Function  
    Public Class shareTotal  
        Public Shared total As Integer  
    End Class  
    ```  
  
     在前面的示例中，编译器在代码通过实例访问共享变量 `total` 时两次都生成警告消息。  每次它都使访问直接通过类 `shareTotal` 来进行，而不利用任何实例。  在特意调用过程 `returnClass` 的情况下，意味着它甚至不会生成对 `returnClass` 的调用，因此不会执行显示“Function returnClass\(\) called”的额外操作。  
  
 `Shared` 修饰符可用于下面的上下文中：  
  
 [Dim 语句](../../../visual-basic/language-reference/statements/dim-statement.md)  
  
 [Event 语句](../../../visual-basic/language-reference/statements/event-statement.md)  
  
 [Function 语句](../../../visual-basic/language-reference/statements/function-statement.md)  
  
 [Operator 语句](../../../visual-basic/language-reference/statements/operator-statement.md)  
  
 [Property 语句](../../../visual-basic/language-reference/statements/property-statement.md)  
  
 [Sub 语句](../../../visual-basic/language-reference/statements/sub-statement.md)  
  
## 请参阅  
 [Shadows](../../../visual-basic/language-reference/modifiers/shadows.md)   
 [Static](../../../visual-basic/language-reference/modifiers/static.md)   
 [Visual Basic 中的生存期](../../../visual-basic/programming-guide/language-features/declared-elements/lifetime.md)   
 [过程](../../../visual-basic/programming-guide/language-features/procedures/index.md)   
 [结构](../../../visual-basic/programming-guide/language-features/data-types/structures.md)   
 [对象和类](../../../visual-basic/programming-guide/language-features/objects-and-classes/index.md)