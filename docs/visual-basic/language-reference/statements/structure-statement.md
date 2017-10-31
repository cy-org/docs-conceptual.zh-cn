---
title: "Structure 语句 | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
f1_keywords: 
  - "vb.Structure"
  - "Structure"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "复合数据类型"
  - "Structure 关键字"
  - "Structure 语句"
  - "类型 [Visual Basic], 用户定义的"
  - "UDT（用户定义的类型）"
  - "用户定义的类型, Structure 语句"
ms.assetid: 9bd1deea-2a89-4cdc-812c-6dcbb947c391
caps.latest.revision: 28
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 28
---
# Structure 语句
[!INCLUDE[vs2017banner](../../../visual-basic/includes/vs2017banner.md)]

声明结构的名称，并引入结构包含的变量、属性、事件和过程的定义。  
  
## 语法  
  
```  
[ <attributelist> ] [ accessmodifier ] [ Shadows ] [ Partial ] _  
Structure name [ ( Of typelist ) ]  
    [ Implements interfacenames ]  
    [ datamemberdeclarations ]  
    [ methodmemberdeclarations ]  
End Structure  
```  
  
## 部件  
  
|||  
|-|-|  
|术语|定义|  
|`attributelist`|可选。  请参见[特性列表](../../../visual-basic/language-reference/statements/attribute-list.md)。|  
|`accessmodifier`|可选。  可以是如下内容之一：<br /><br /> -   [Public](../../../visual-basic/language-reference/modifiers/public.md)<br />-   [Protected](../../../visual-basic/language-reference/modifiers/protected.md)<br />-   [Friend](../../../visual-basic/language-reference/modifiers/friend.md)<br />-   [Private](../../../visual-basic/language-reference/modifiers/private.md)<br />-   `Protected Friend`<br /><br /> 请参见 [Visual Basic 中的访问级别](../../../visual-basic/programming-guide/language-features/declared-elements/access-levels.md)。|  
|`Shadows`|可选。  请参见 [Shadows](../../../visual-basic/language-reference/modifiers/shadows.md)。|  
|`Partial`|可选。  指示结构的分部定义。  请参见 [分部](../../../visual-basic/language-reference/modifiers/partial.md)。|  
|`name`|必需。  此结构的名称。  请参见 [已声明的元素名称](../../../visual-basic/programming-guide/language-features/declared-elements/declared-element-names.md)。|  
|`Of`|可选。  指定这是一个泛型结构。|  
|`typelist`|如果使用 [Of](../../../visual-basic/language-reference/statements/of-clause.md) 关键字，则为必选项。  此结构的类型参数列表。  请参见[类型列表](../../../visual-basic/language-reference/statements/type-list.md)。|  
|`Implements`|可选。  指示此结构实现一个或多个接口成员。  请参见 [Implements 语句](../../../visual-basic/language-reference/statements/implements-statement.md)。|  
|`interfacenames`|如果使用 `Implements` 语句，则为必选项。  此结构实现的接口的名称。|  
|`datamemberdeclarations`|必需。  一个或多个 `Const`、`Dim`、`Enum` 或 `Event` 语句声明结构的数据成员。|  
|`methodmemberdeclarations`|可选。  作为结构的方法成员的零个或多个 `Function`、`Operator`、`Property` 或 `Sub` 过程的声明。|  
|`End Structure`|必需。  终止 `Structure` 定义。|  
  
## 备注  
 `Structure` 语句定义一种您可以自定义的复合值类型。  “结构”是 Visual Basic 早期版本的用户定义类型 \(UDT\) 的泛化。  有关详细信息，请参阅[结构](../../../visual-basic/programming-guide/language-features/data-types/structures.md)。  
  
 结构支持的许多功能与类支持的一样。  例如，结构可以拥有属性和过程，可以实现接口，也可以拥有参数化的构造函数。  但是，在某些地方（例如继承、声明和用法）结构和类之间存在着重大的差异。  而且，类是引用类型，而结构是值类型。  有关详细信息，请参阅[结构和类](../../../visual-basic/programming-guide/language-features/data-types/structures-and-classes.md)。  
  
 您只能在命名空间或模块级别使用 `Structure`。  这意味着结构的声明上下文必须是源文件、命名空间、类、结构、模块或接口，不能是过程或块。  有关详细信息，请参阅[声明上下文和默认访问级别](../../../visual-basic/language-reference/statements/declaration-contexts-and-default-access-levels.md)。  
  
 结构默认为 [Friend](../../../visual-basic/language-reference/modifiers/friend.md) 访问级别。  可以使用访问修饰符来调整它们的访问级别。  有关详细信息，请参阅[Visual Basic 中的访问级别](../../../visual-basic/programming-guide/language-features/declared-elements/access-levels.md)。  
  
## 规则  
  
-   **嵌套。**可以在一个结构中定义另一个结构。  外部结构称为“包含结构”，而内部结构称为“嵌套结构”。  但是，无法通过包含结构来访问嵌套结构的成员，  而是必须声明一个嵌套结构的数据类型的变量。  
  
-   **成员声明。**必须声明结构的每个成员。  由于无法从结构中继承任何内容，因此结构成员不能是 [Protected](../../../visual-basic/language-reference/modifiers/protected.md) 或 `Protected Friend`。  但是，结构本身可以是 `Protected` 或 `Protected Friend`。  
  
     可以声明零个或多个非共享变量或非共享、非自定义的结构事件。  在结构中不能只包含常数、属性和过程，即使某些成员是非共享的。  
  
-   **初始化。**不能将结构的任何非共享数据成员的值初始化成其声明的一部分。  必须通过结构上参数化的构造函数初始化此类数据成员，或者在创建了该结构的实例后将值赋给该成员。  
  
-   **继承。**结构无法从除 <xref:System.ValueType>（所有结构均从它继承）外的任何类型继承。  特别地，一个结构无法从另一个结构继承。  
  
     无法在结构定义中使用 [Inherits 语句](../../../visual-basic/language-reference/statements/inherits-statement.md)，即使是指定 <xref:System.ValueType> 亦为如此。  
  
-   **实现。**如果结构使用 [Implements 语句](../../../visual-basic/language-reference/statements/implements-statement.md)，则必须实现您在 `interfacenames` 中指定的每个接口所定义的每个成员。  
  
-   **默认属性。**一个结构至多可以指定一个属性作为其默认属性（通过使用 [Default](../../../visual-basic/language-reference/modifiers/default.md) 修饰符）。  有关详细信息，请参阅[Default](../../../visual-basic/language-reference/modifiers/default.md)。  
  
## 行为  
  
-   **访问级别。**在结构中，可以利用成员自己的访问级别来声明每个成员。  所有结构成员均默认为 [Public](../../../visual-basic/language-reference/modifiers/public.md) 访问级别。  请注意，如果结构本身具有限制性更高的访问级别，这会自动限制对其成员的访问，即使您使用访问修饰符来调整其成员的访问级别也是如此。  
  
-   **范围。**结构的范围贯穿它的包含命名空间、类、结构或模块。  
  
     结构成员的范围是整个结构。  
  
-   **生存期。**结构本身没有生存期。  相反，结构的每个实例具有独立于所有其他实例的生存期。  
  
     实例的生存期在它由 [New 运算符](../../../visual-basic/language-reference/operators/new-operator.md) 子句创建时开始，  并在保存实例的变量的生存期结束时结束。  
  
     无法延长结构实例的生存期。  模块提供了近似的静态结构功能。  有关详细信息，请参阅[Module 语句](../../../visual-basic/language-reference/statements/module-statement.md)。  
  
     结构成员具有由如何以及在哪里声明它们决定的生存期。  有关更多信息，请参见[Class 语句](../../../visual-basic/language-reference/statements/class-statement.md) 中的“生存期”。  
  
-   **限定。**结构外的代码必须用结构的名称来限定成员的名称。  
  
     如果嵌套结构外的代码以非限定的方式引用某个编程元素，则 Visual Basic 会按此顺序搜索该元素：先在嵌套结构中搜索，然后在其包含结构中搜索，依此类推，一直到最外部的包含元素。  有关详细信息，请参阅[对已声明元素的引用](../../../visual-basic/programming-guide/language-features/declared-elements/references-to-declared-elements.md)。  
  
-   **内存消耗。**与所有的复合数据类型一样，您无法通过将结构成员的名义存储分配相加来得到确切的总内存消耗。  此外，不能完全假定成员在内存中的存储顺序与声明的顺序相同。  如果需要控制结构的存储布局，可以对 `Structure` 语句应用 <xref:System.Runtime.InteropServices.StructLayoutAttribute> 特性。  
  
## 示例  
 下面的示例使用 `Structure` 语句定义雇员的一系列相关数据。  它演示了 `Public`、`Friend` 和 `Private` 成员的用法，从而反映数据项的敏感性。  它还将显示过程、属性和事件成员。  
  
 [!code-vb[VbVbalrStatements#57](../../../visual-basic/language-reference/error-messages/codesnippet/VisualBasic/structure-statement_1.vb)]  
  
## 请参阅  
 [Class 语句](../../../visual-basic/language-reference/statements/class-statement.md)   
 [Interface 语句](../../../visual-basic/language-reference/statements/interface-statement.md)   
 [Module 语句](../../../visual-basic/language-reference/statements/module-statement.md)   
 [Dim 语句](../../../visual-basic/language-reference/statements/dim-statement.md)   
 [Const 语句](../../../visual-basic/language-reference/statements/const-statement.md)   
 [Enum 语句](../../../visual-basic/language-reference/statements/enum-statement.md)   
 [Event 语句](../../../visual-basic/language-reference/statements/event-statement.md)   
 [Operator 语句](../../../visual-basic/language-reference/statements/operator-statement.md)   
 [Property 语句](../../../visual-basic/language-reference/statements/property-statement.md)   
 [结构和类](../../../visual-basic/programming-guide/language-features/data-types/structures-and-classes.md)