---
title: "Set 语句 (Visual Basic) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
f1_keywords: 
  - "vb.Set"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "属性 [Visual Basic], write-only"
  - "属性过程, Set 语句"
  - "Set 语句"
  - "Set 语句, 语法"
  - "只写属性"
ms.assetid: 9ecc27b4-df84-420d-9075-db25455fb3cd
caps.latest.revision: 16
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 16
---
# Set 语句 (Visual Basic)
[!INCLUDE[vs2017banner](../../../visual-basic/includes/vs2017banner.md)]

声明用于给属性赋值的 `Set` 属性过程。  
  
## 语法  
  
```  
[ <attributelist> ] [ accessmodifier ] Set (ByVal value [ As datatype ])  
    [ statements ]  
End Set  
```  
  
## 部件  
 `attributelist`  
 可选。  请参见[特性列表](../../../visual-basic/language-reference/statements/attribute-list.md)。  
  
 `accessmodifier`  
 在此属性中的至多一个 `Get` 和 `Set` 语句上为可选项。  可以是如下内容之一：  
  
-   [Protected](../../../visual-basic/language-reference/modifiers/protected.md)  
  
-   [Friend](../../../visual-basic/language-reference/modifiers/friend.md)  
  
-   [Private](../../../visual-basic/language-reference/modifiers/private.md)  
  
-   `Protected Friend`  
  
 请参见 [Visual Basic 中的访问级别](../../../visual-basic/programming-guide/language-features/declared-elements/access-levels.md)。  
  
 `value`  
 必选。  包含此属性的新值的参数。  
  
 `datatype`  
 如果 `Option Strict` 为 `On`，则为必选项。  `value` 参数的数据类型。  指定的数据类型必须与声明此 `Set` 语句的属性的数据类型相同。  
  
 `statements`  
 可选。  在调用 `Set` 属性过程时运行的一个或多个语句。  
  
 `End Set`  
 必选。  终止 `Set` 属性过程的定义。  
  
## 备注  
 每个属性均必须具有一个 `Set` 属性过程（除非该属性标记为 `ReadOnly`）。  `Set` 过程用于设置属性的值。  
  
 当赋值语句提供一个将存储在属性中的值时，Visual Basic 会自动调用属性的 `Set` 过程。  
  
 在属性赋值期间，Visual Basic 会将参数传递给 `Set` 过程。  如果没有为 `Set` 提供参数，则集成开发环境 \(IDE\) 将使用一个名为 `value` 的隐式参数。  此参数保存将赋给属性的值。  通常在私有局部变量中存储此值，并在调用 `Get` 过程时返回它。  
  
 属性声明体只能在 [Property 语句](../../../visual-basic/language-reference/statements/property-statement.md) 和 `End Property` 语句之间包含属性的 `Get` 和 `Set` 过程。  它不能存储除这些过程外的任何内容。  特别地，它不能存储属性的当前值。  必须在属性外存储此值，原因是，如果在以上任一属性过程中存储此值，则另一个属性过程将无法访问它。  常用的方法是将此值存储在 [Private](../../../visual-basic/language-reference/modifiers/private.md) 变量（在与属性相同的级别上声明）中。  必须在此值应用于的属性的内部定义 `Set` 过程。  
  
 `Set` 过程默认为它的包含属性的访问级别（除非在 `Set` 语句中使用 `accessmodifier`）。  
  
## 规则  
  
-   **混合访问级别。**如果定义一个读写属性，则可以根据需要为 `Get` 或 `Set` 过程指定不同的访问级别，但不能同时为两者这样做。  否则，过程访问级别在限制性上必须比属性的访问级别更高。  例如，如果属性被声明为 `Friend`，则可以将 `Set` 过程声明为 `Private`，但不能声明为 `Public`。  
  
     如果定义 `WriteOnly` 属性，则 `Set` 过程将代表整个属性。  不能为 `Set` 声明不同的访问级别，原因是这会为属性设置两个访问级别。  
  
## 行为  
  
-   **从属性过程返回。**在 `Set` 过程返回到调用代码时，将会从提供了要存储的值的语句后面继续执行语句。  
  
     `Set` 属性过程可以使用 [Return 语句](../../../visual-basic/language-reference/statements/return-statement.md) 或 [Exit 语句](../../../visual-basic/language-reference/statements/exit-statement.md) 返回。  
  
     使用 `Exit Property` 和 `Return` 语句可以立即从属性过程中退出。  过程中的任何地方可以出现任意数量的 `Exit Property` 和 `Return` 语句，而且可以混用 `Exit Property` 和 `Return` 语句。  
  
## 示例  
 下面的示例使用 `Set` 语句设置属性值。  
  
 [!code-vb[VbVbalrStatements#55](../../../visual-basic/language-reference/error-messages/codesnippet/VisualBasic/set-statement_1.vb)]  
  
## 请参阅  
 [Get 语句](../../../visual-basic/language-reference/statements/get-statement.md)   
 [Property 语句](../../../visual-basic/language-reference/statements/property-statement.md)   
 [Sub 语句](../../../visual-basic/language-reference/statements/sub-statement.md)   
 [Property 过程](../../../visual-basic/programming-guide/language-features/procedures/property-procedures.md)