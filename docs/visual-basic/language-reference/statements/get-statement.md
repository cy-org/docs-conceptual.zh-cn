---
title: "Get 语句 | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
f1_keywords: 
  - "vb.Get"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "Get 关键字"
  - "Get 语句"
  - "Get 语句, 语法"
  - "属性 [Visual Basic], 只读"
  - "属性过程, Get 语句"
  - "只读属性"
ms.assetid: 56b05cdc-bd64-4dfd-bb12-824eacec6f94
caps.latest.revision: 19
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 19
---
# Get 语句
[!INCLUDE[vs2017banner](../../../visual-basic/includes/vs2017banner.md)]

声明用于检索属性值的 `Get` 属性过程。  
  
## 语法  
  
```  
[ <attributelist> ] [ accessmodifier ] Get()  
    [ statements ]  
End Get  
```  
  
## 部件  
  
|||  
|-|-|  
|术语|定义|  
|`attributelist`|可选。  请参见[特性列表](../../../visual-basic/language-reference/statements/attribute-list.md)。|  
|`accessmodifier`|在此属性中的至多一个 `Get` 和 `Set` 语句上为可选项。  可以是如下内容之一：<br /><br /> -   [Protected](../../../visual-basic/language-reference/modifiers/protected.md)<br />-   [Friend](../../../visual-basic/language-reference/modifiers/friend.md)<br />-   [Private](../../../visual-basic/language-reference/modifiers/private.md)<br />-   `Protected Friend`<br /><br /> 请参见 [Visual Basic 中的访问级别](../../../visual-basic/programming-guide/language-features/declared-elements/access-levels.md)。|  
|`statements`|可选。  在调用 `Get` 属性过程时运行的一个或多个语句。|  
|`End Get`|必选。  终止 `Get` 属性过程的定义。|  
  
## 备注  
 除非属性被标记为 `WriteOnly`，否则每个属性都必须有一个 `Get` 属性过程。  `Get` 过程用于返回属性的当前值。  
  
 当表达式请求属性的值时，Visual Basic 会自动调用属性的 `Get` 过程。  
  
 属性声明体只能在 [Property 语句](../../../visual-basic/language-reference/statements/property-statement.md) 和 `End Property` 语句之间包含属性的 `Get` 和 `Set` 过程。  它不能存储除这些过程外的任何内容。  特别地，它不能存储属性的当前值。  必须在属性外存储此值，原因是，如果在以上任一属性过程中存储此值，则另一个属性过程将无法访问它。  常用的方法是将此值存储在 [Private](../../../visual-basic/language-reference/modifiers/private.md) 变量（在与属性相同的级别上声明）中。  必须在要应用 `Get` 过程的属性内部定义该过程。  
  
 `Get` 过程默认为其包含属性的访问级别，除非您在 `Get` 语句中使用 `accessmodifier`。  
  
## 规则  
  
-   **混合访问级别。**如果定义一个读写属性，则可以根据需要为 `Get` 或 `Set` 过程指定不同的访问级别，但不能同时为两者这样做。  否则，过程访问级别在限制性上必须比属性的访问级别更高。  例如，如果将属性声明为 `Friend`，则可以将 `Get` 过程声明为 `Private`，但不能声明为 `Public`。  
  
     如果要定义 `ReadOnly` 属性，则 `Get` 过程代表整个属性。  不能为 `Get` 声明另一个访问级别，因为这会为属性设置两个访问级别。  
  
-   **返回类型。** [Property 语句](../../../visual-basic/language-reference/statements/property-statement.md)可以声明其返回值的数据类型。  `Get` 过程会自动返回该数据类型。  可以指定任何数据类型或枚举、结构、类或接口的名称。  
  
     如果 `Property` 语句未指定 `returntype`，则过程将返回 `Object`。  
  
## 行为  
  
-   **从过程中返回。**当 `Get` 过程返回到调用代码时，执行过程将在请求属性值的语句内继续进行。  
  
     `Get` 属性过程可以使用 [Return 语句](../../../visual-basic/language-reference/statements/return-statement.md) 来返回值，也可以通过将返回值赋给属性名称来返回值。  有关更多信息，请参见 [Function 语句](../../../visual-basic/language-reference/statements/function-statement.md) 中的“返回值”。  
  
     使用 `Exit Property` 和 `Return` 语句可以立即从属性过程中退出。  过程中的任何地方可以出现任意数量的 `Exit Property` 和 `Return` 语句，而且可以混用 `Exit Property` 和 `Return` 语句。  
  
-   **返回值。**若要从 `Get` 过程返回某个值，您可以将该值赋给属性名称，或者将其包含在 [Return 语句](../../../visual-basic/language-reference/statements/return-statement.md) 语句中。  `Return` 语句将同时分配 `Get` 过程返回值并退出过程。  
  
     如果使用 `Exit Property` 而未将值赋给属性名称，`Get` 过程将返回属性数据类型的默认值。  有关更多信息，请参见 [Function 语句](../../../visual-basic/language-reference/statements/function-statement.md) 中的“返回值”。  
  
     下面的示例阐释了只读属性 `quoteForTheDay` 返回保存在私有变量 `quoteValue` 中的值的两种方式。  
  
     [!code-vb[VbVbalrStatements#27](../../../visual-basic/language-reference/error-messages/codesnippet/VisualBasic/get-statement_1.vb)]  
  
     [!code-vb[VbVbalrStatements#28](../../../visual-basic/language-reference/error-messages/codesnippet/VisualBasic/get-statement_2.vb)]  
  
     [!code-vb[VbVbalrStatements#29](../../../visual-basic/language-reference/error-messages/codesnippet/VisualBasic/get-statement_3.vb)]  
  
## 示例  
 下面的示例使用 `Get` 语句返回属性的值。  
  
 [!code-vb[VbVbalrStatements#30](../../../visual-basic/language-reference/error-messages/codesnippet/VisualBasic/get-statement_4.vb)]  
  
## 请参阅  
 [Set 语句](../../../visual-basic/language-reference/statements/set-statement.md)   
 [Property 语句](../../../visual-basic/language-reference/statements/property-statement.md)   
 [Exit 语句](../../../visual-basic/language-reference/statements/exit-statement.md)   
 [对象和类](../../../visual-basic/programming-guide/language-features/objects-and-classes/index.md)   
 [演练：定义类](../../../visual-basic/programming-guide/language-features/objects-and-classes/walkthrough-defining-classes.md)