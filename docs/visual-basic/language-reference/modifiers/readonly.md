---
title: "ReadOnly (Visual Basic) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
f1_keywords: 
  - "vb.ReadOnly"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "属性 [Visual Basic], 只读"
  - "ReadOnly 关键字"
  - "ReadOnly 属性"
  - "只读变量"
  - "变量 [Visual Basic], 只读"
ms.assetid: e868185d-6142-4359-a2fd-a7965cadfce8
caps.latest.revision: 15
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 15
---
# ReadOnly (Visual Basic)
[!INCLUDE[vs2017banner](../../../visual-basic/includes/vs2017banner.md)]

指定可对变量或属性进行读操作但不能进行写操作。  
  
## 备注  
  
## 规则  
  
-   **声明上下文。**仅可以在模块级别使用 `ReadOnly`。  这意味着 `ReadOnly` 元素的声明上下文必须是一个类、结构或模块，而不能是源文件、命名空间或过程。  
  
-   **组合修饰符。**不能在同一声明中将 `ReadOnly` 与 `Static` 同时指定。  
  
-   **赋值。**使用 `ReadOnly` 属性的代码不可以设置值。  但是具有基础存储访问权限的代码可以随时赋值或更改值。  
  
     您只可以在声明或者在定义类或结构的构造函数中，将一个值赋给 `ReadOnly` 变量。  
  
## 何时使用 ReadOnly 变量  
 有时不能使用 [Const 语句](../../../visual-basic/language-reference/statements/const-statement.md) 声明常数值和给常数赋值。  例如，`Const` 语句可能不接受要赋给它的数据类型，或者在编译时可能无法使用常数表达式计算值。  在编译时甚至不知道值。  在这种情况下，可以使用 `ReadOnly` 变量保存常数值。  
  
> [!IMPORTANT]
>  如果变量的数据类型为引用类型，例如数组或类实例，则即使变量本身为 `ReadOnly`，也可以更改其成员。  下面的示例阐释了这一点。  
  
 `ReadOnly characterArray() As Char = {"x"c, "y"c, "z"c}`  
  
 `Sub changeArrayElement()`  
  
 `characterArray(1) = "M"c`  
  
 `End Sub`  
  
 在初始化时，由 `characterArray()` 指向的数组保存“x”、“y”和“z”。  因为变量 `characterArray` 为 `ReadOnly`，所以在初始化它之后不可以更改它的值；即，不能将一个新数组赋给它。  但是，您可以更改一个或多个数组成员的值。  调用过程 `changeArrayElement` 之后，由 `characterArray()` 指向的数组保存“x”、“M”和“z”。  
  
 请注意，这与将过程参数声明为 [ByVal](../../../visual-basic/language-reference/modifiers/byval.md) 类似，因而可防止过程更改调用参数本身，但允许过程更改其成员。  
  
## 示例  
 下面的示例为雇佣某位职员的日期定义一个 `ReadOnly` 属性。  类将该属性值在内部存储为 `Private` 变量，因而只有该类中的代码可以更改该值。  但是，该属性为 `Public`，因此可以访问该类的任何代码都可以读取该属性。  
  
 [!code-vb[VbVbalrKeywords#4](../../../visual-basic/language-reference/codesnippet/VisualBasic/readonly_1.vb)]  
  
 `ReadOnly` 修饰符可用于下面的上下文中：  
  
 [Dim 语句](../../../visual-basic/language-reference/statements/dim-statement.md)  
  
 [Property 语句](../../../visual-basic/language-reference/statements/property-statement.md)  
  
## 请参阅  
 [WriteOnly](../../../visual-basic/language-reference/modifiers/writeonly.md)   
 [关键字](../../../visual-basic/language-reference/keywords/index.md)