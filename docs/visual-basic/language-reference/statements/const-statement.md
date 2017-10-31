---
title: "Const 语句 (Visual Basic) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
f1_keywords: 
  - "vb.Const"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "Const 语句 [Visual Basic]"
ms.assetid: 495b318d-b7c5-4198-94f8-0790a541b07a
caps.latest.revision: 28
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 28
---
# Const 语句 (Visual Basic)
[!INCLUDE[vs2017banner](../../../visual-basic/includes/vs2017banner.md)]

声明和定义一个或多个常数。  
  
## 语法  
  
```  
[ <attributelist> ] [ accessmodifier ] [ Shadows ]   
Const constantlist  
```  
  
## 部件  
 `attributelist`  
 可选。  特性列表，适用于此语句中声明的所有常数。  请参见尖括号（“`<`”和“`>`”）中的[特性列表](../../../visual-basic/language-reference/statements/attribute-list.md)。  
  
 `accessmodifier`  
 可选。  使用此项来指定哪个代码可以访问这些常数。  可以是 [Public](../../../visual-basic/language-reference/modifiers/public.md)、[Protected](../../../visual-basic/language-reference/modifiers/protected.md)、[Friend](../../../visual-basic/language-reference/modifiers/friend.md)、`Protected Friend` 或 [Private](../../../visual-basic/language-reference/modifiers/private.md)。  
  
 `Shadows`  
 可选。  使用此项来重新声明和隐藏基类中的编程元素。  请参见 [Shadows](../../../visual-basic/language-reference/modifiers/shadows.md)。  
  
 `constantlist`  
 必选。  在此语句中声明的常数的列表。  
  
 `constant` `[ ,` `constant` `... ]`  
  
 每个 `constant` 均有下列语法和部分：  
  
 `constantname` `[ As` `datatype` `] =` `initializer`  
  
|组成部分|说明|  
|----------|--------|  
|`constantname`|必选。  常数名称。  请参见 [已声明的元素名称](../../../visual-basic/programming-guide/language-features/declared-elements/declared-element-names.md)。|  
|`datatype`|如果 `Option Strict` 为 `On`，则为必选项。  常数的数据类型。|  
|`initializer`|必选。  先在编译时计算然后分配给此常数的表达式。|  
  
## 备注  
 如果有一个值在应用程序中始终不变，则可以定义一个命名常数，并用该常数取代文本值。  名称比值更容易记忆。  可以只定义该常数一次，然后在代码中的多处使用它。  如果需要在以后的版本中重新定义值，则只需更改 `Const` 语句即可。  
  
 只能在模块或过程级别使用 `Const`。  这意味着变量的声明上下文必须是类、结构、模块、过程或块，而不能是源文件、命名空间或接口。  有关更多信息，请参见[声明上下文和默认访问级别](../../../visual-basic/language-reference/statements/declaration-contexts-and-default-access-levels.md)。  
  
 局部常数（在某个过程的内部）默认为公共访问，并且不能对这些常数使用任何访问修饰符。  类和模块成员常数（在任何过程的外部）默认为私有访问，而结构成员常数则默认为公共访问。  可以使用访问修饰符来调整它们的访问级别。  
  
## 规则  
  
-   **声明上下文。**在任何过程之外的模块级别声明的常量是“成员常量”；该常量是声明它的类、结构或模块的成员。  
  
     在过程级别声明的常数是局部常数，该常数局限于声明它的过程或块。  
  
-   **特性。**只能将特性应用于成员常数，而不能应用于局部常数。  特性为程序集的元数据提供信息，该信息对于临时存储（如局部常数）没有意义。  
  
-   **修饰符。**默认情况下，所有常量均为 `Shared`、`Static` 和 `ReadOnly`。  在声明常数时，不能使用这些关键字中的任何一个。  
  
     在过程级别，不能使用 `Shadows` 或任何访问修饰符来声明局部常数。  
  
-   **多个常数。**可以在同一声明语句中声明多个常量，并为每个常量指定 `constantname` 部分。  以逗号分隔多个常数。  
  
## 数据类型规则  
  
-   **数据类型。** `Const` 语句可以声明变量的数据类型。  可以指定任何数据类型或枚举的名称。  
  
-   **默认类型。**如果不指定 `datatype`，常量将采用 `initializer` 的数据类型。  如果指定 `datatype` 和 `initializer`，则 `initializer` 的数据类型必须能够转换为 `datatype`。  如果既不存在 `datatype` 也不存在 `initializer`，则数据类型默认为 `Object`。  
  
-   **不同的类型。**可以为不同的常量指定不同的数据类型，方法是为声明的每个变量使用单独的 `As` 子句。  但是，不能通过使用公用 `As` 子句将多个常数声明为同一类型。  
  
-   **初始化。**必须初始化 `constantlist` 中每个常量的值。  可以使用 `initializer` 来提供要分配给常数的表达式。  表达式可以是文本、其他已定义的常数以及已定义的枚举成员的任意组合。  可以使用算术运算符和逻辑运算符来组合这些元素。  
  
     不能在 `initializer` 中使用变量或函数。  但是，可以使用转换关键字，例如 `CByte` 和 `CShort`。  也可以使用 `AscW`（如果使用常数 `String` 或 `Char` 参数调用它），因为这可以在编译时进行计算。  
  
## 行为  
  
-   **范围。**局部常数只能从它们的过程或块中访问；  而成员常数则可以从它们的类、结构或模块内的任意位置访问。  
  
-   **限定。**类、结构或模块之外的代码必须使用该类、结构或模块的名称来限定成员常数的名称。  过程或块之外的代码不能引用该过程或块内的任何局部常数。  
  
## 示例  
 下面的示例使用 `Const` 语句来声明用于代替文本值的常数。  
  
 [!code-vb[VbVbalrStatements#13](../../../visual-basic/language-reference/error-messages/codesnippet/VisualBasic/const-statement_1.vb)]  
  
## 示例  
 如果使用数据类型 `Object` 定义常数，Visual Basic 编译器将为其赋予 `initializer` 的类型，而不是 `Object`。  在下面的示例中，常数 `naturalLogBase` 具有运行时类型 `Decimal`。  
  
 [!code-vb[VbVbalrStatements#87](../../../visual-basic/language-reference/error-messages/codesnippet/VisualBasic/const-statement_2.vb)]  
  
 前面的示例在 [GetType 运算符](../../../visual-basic/language-reference/operators/gettype-operator.md) 返回的 <xref:System.Type> 对象上使用 <xref:System.Type.ToString%2A> 方法，原因是无法使用 `CStr` 将 <xref:System.Type> 转换为 `String`。  
  
## 请参阅  
 <xref:Microsoft.VisualBasic.Strings.Asc%2A>   
 <xref:Microsoft.VisualBasic.Strings.AscW%2A>   
 [Enum 语句](../../../visual-basic/language-reference/statements/enum-statement.md)   
 [\#Const 指令](../../../visual-basic/language-reference/directives/const-directive.md)   
 [Dim 语句](../../../visual-basic/language-reference/statements/dim-statement.md)   
 [ReDim 语句](../../../visual-basic/language-reference/statements/redim-statement.md)   
 [隐式转换和显式转换](../../../visual-basic/programming-guide/language-features/data-types/implicit-and-explicit-conversions.md)   
 [常量和枚举](../../../visual-basic/programming-guide/language-features/constants-enums/index.md)   
 [常量和枚举](../../../visual-basic/language-reference/constants-and-enumerations.md)   
 [类型转换函数](../../../visual-basic/language-reference/functions/type-conversion-functions.md)