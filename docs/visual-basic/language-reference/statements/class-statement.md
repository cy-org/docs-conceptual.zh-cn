---
title: "Class 语句 (Visual Basic) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
f1_keywords: 
  - "vb.Class"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "类模块"
  - "Class 语句"
  - "类类型, class 语句"
  - "类 [Visual Basic], 创建"
  - "类 [Visual Basic], 数据成员"
  - "类 [Visual Basic], 字段"
  - "数据成员, 类"
  - "字段, 类"
ms.assetid: f2664f38-eb5a-4d4b-a374-1d041521fb6c
caps.latest.revision: 29
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 29
---
# Class 语句 (Visual Basic)
[!INCLUDE[vs2017banner](../../../visual-basic/includes/vs2017banner.md)]

声明类的名称，并引入构成该类的变量、属性、事件和过程的定义。  
  
## 语法  
  
```  
[ <attributelist> ] [ accessmodifier ] [ Shadows ] [ MustInherit | NotInheritable ] [ Partial ] _  
Class name [ ( Of typelist ) ]  
    [ Inherits classname ]  
    [ Implements interfacenames ]  
    [ statements ]  
End Class  
```  
  
## 部件  
  
|||  
|-|-|  
|术语|定义|  
|`attributelist`|可选。  请参见[特性列表](../../../visual-basic/language-reference/statements/attribute-list.md)。|  
|`accessmodifier`|可选。  可以是如下内容之一：<br /><br /> -   [Public](../../../visual-basic/language-reference/modifiers/public.md)<br />-   [Protected](../../../visual-basic/language-reference/modifiers/protected.md)<br />-   [Friend](../../../visual-basic/language-reference/modifiers/friend.md)<br />-   [Private](../../../visual-basic/language-reference/modifiers/private.md)<br />-   `Protected Friend`<br /><br /> 请参见 [Visual Basic 中的访问级别](../../../visual-basic/programming-guide/language-features/declared-elements/access-levels.md)。|  
|`Shadows`|可选。  请参见 [Shadows](../../../visual-basic/language-reference/modifiers/shadows.md)。|  
|`MustInherit`|可选。  请参见 [MustInherit](../../../visual-basic/language-reference/modifiers/mustinherit.md)。|  
|`NotInheritable`|可选。  请参见 [NotInheritable](../../../visual-basic/language-reference/modifiers/notinheritable.md)。|  
|`Partial`|可选。  指示该类的分部定义。  请参见 [分部](../../../visual-basic/language-reference/modifiers/partial.md)。|  
|`name`|必选。  此类的名称。  请参见 [已声明的元素名称](../../../visual-basic/programming-guide/language-features/declared-elements/declared-element-names.md)。|  
|`Of`|可选。  指定这是一个泛型类。|  
|`typelist`|如果使用 [Of](../../../visual-basic/language-reference/statements/of-clause.md) 关键字，则为必选项。  此类的类型参数列表。  请参见[类型列表](../../../visual-basic/language-reference/statements/type-list.md)。|  
|`Inherits`|可选。  指示该类继承了另一个类的成员。  请参见 [Inherits 语句](../../../visual-basic/language-reference/statements/inherits-statement.md)。|  
|`classname`|如果使用 `Inherits` 语句，则为必选项。  派生此类的类的名称。|  
|`Implements`|可选。  指示此类实现一个或多个接口的成员。  请参见 [Implements 语句](../../../visual-basic/language-reference/statements/implements-statement.md)。|  
|`interfacenames`|如果使用 `Implements` 语句，则为必选项。  此类实现的接口的名称。|  
|`statements`|可选。  定义此类的成员的语句。|  
|`End Class`|必选。  终止 `Class` 定义。|  
  
## 备注  
 一条 `Class` 语句定义一个新数据类型。  “类”是面向对象编程 \(OOP\) 的基本构造块。  有关更多信息，请参见 [对象和类](../../../visual-basic/programming-guide/language-features/objects-and-classes/index.md)。  
  
 您只能在命名空间或模块级别使用 `Class`。  这意味着类的声明上下文必须是源文件、命名空间、类、结构、模块或接口，而且不能是过程或块。  有关更多信息，请参见[声明上下文和默认访问级别](../../../visual-basic/language-reference/statements/declaration-contexts-and-default-access-levels.md)。  
  
 类的每个实例都拥有一个独立于所有其他实例的生存期。  此生存期开始于 [New 运算符](../../../visual-basic/language-reference/operators/new-operator.md) 子句或函数（如 <xref:Microsoft.VisualBasic.Interaction.CreateObject%2A>）创建实例时，  结束于指向实例的所有变量都已设置为 [Nothing](../../../visual-basic/language-reference/nothing.md) 或其他类的实例时。  
  
 类默认为 [Friend](../../../visual-basic/language-reference/modifiers/friend.md) 访问。  可以使用访问修饰符来调整它们的访问级别。  有关更多信息，请参见 [Visual Basic 中的访问级别](../../../visual-basic/programming-guide/language-features/declared-elements/access-levels.md)。  
  
## 规则  
  
-   **嵌套。**可以在一个类中定义另一个类。  外部类称为“包含类”，而内部类称为“嵌套类”。  
  
-   **继承。**如果类使用 [Inherits 语句](../../../visual-basic/language-reference/statements/inherits-statement.md)，则只能指定一个基类或接口。  一个类不能从多个元素中继承。  
  
     一个类不能从访问级别的限制性较强的另一个类中继承。  例如，`Public` 类不能从 `Friend` 类继承。  
  
     类不能从嵌套在该类中的类继承。  
  
-   **实现。**如果类使用 [Implements 语句](../../../visual-basic/language-reference/statements/implements-statement.md)，则必须实现由 `interfacenames` 中指定的每个接口定义的每个成员。  此情况的例外是基类成员的重新实现。  有关更多信息，请参见 [Implements](../../../visual-basic/language-reference/statements/implements-clause.md) 中的“重新实现”。  
  
-   **默认属性。**一个类最多只能指定一个属性作为其默认属性。  有关更多信息，请参见[Default](../../../visual-basic/language-reference/modifiers/default.md)。  
  
## 行为  
  
-   **访问级别。**在类中，可以使用其自身的访问级别声明每个成员。  类成员默认为 [Public](../../../visual-basic/language-reference/modifiers/public.md) 访问，但变量和常数除外，它们默认为 [Private](../../../visual-basic/language-reference/modifiers/private.md) 访问。  当某个类比其成员之一具有限制性更强的访问时，类访问级别将优先。  
  
-   **范围。**类的范围遍及包含它的命名空间、类、结构或模块。  
  
     每个类成员的范围是整个类。  
  
     **生存期。**Visual Basic 不支持静态类。  模块提供了与静态类等效的功能。  有关更多信息，请参见 [Module 语句](../../../visual-basic/language-reference/statements/module-statement.md)。  
  
     类成员根据其声明的方式和位置而具有不同的生存期。  有关更多信息，请参见 [Visual Basic 中的生存期](../../../visual-basic/programming-guide/language-features/declared-elements/lifetime.md)。  
  
-   **限定。**类外部的代码必须使用该类的名称限定成员的名称。  
  
     如果嵌套类内部的代码建立了对编程元素的非限定性引用，Visual Basic 将首先在该嵌套类中搜索该元素，然后在其包含类中搜索，一直向外直到最外层的包含元素。  
  
## 类和模块  
 这些元素具有许多相似性，但是也存在一些重要的差异。  
  
-   **术语。**以前的 Visual Basic 版本识别两种类型的模块：类模块（.cls 文件）和标准模块（.bas 文件）。  当前版本会分别调用这些类和模块。  
  
-   **共享成员。**可以控制类的成员是共享成员还是实例成员。  
  
-   **面向对象。**类是面向对象的，但模块不是。  您可以创建类的一个或多个实例。  有关更多信息，请参见 [对象和类](../../../visual-basic/programming-guide/language-features/objects-and-classes/index.md)。  
  
## 示例  
 下面的示例使用 `Class` 语句定义一个类和几个成员。  
  
 [!code-vb[VbVbalrStatements#62](../../../visual-basic/language-reference/error-messages/codesnippet/VisualBasic/class-statement_1.vb)]  
  
## 请参阅  
 [对象和类](../../../visual-basic/programming-guide/language-features/objects-and-classes/index.md)   
 [结构和类](../../../visual-basic/programming-guide/language-features/data-types/structures-and-classes.md)   
 [Interface 语句](../../../visual-basic/language-reference/statements/interface-statement.md)   
 [Module 语句](../../../visual-basic/language-reference/statements/module-statement.md)   
 [Property 语句](../../../visual-basic/language-reference/statements/property-statement.md)   
 [对象生存期：如何创建和销毁对象](../../../visual-basic/programming-guide/language-features/objects-and-classes/object-lifetime-how-objects-are-created-and-destroyed.md)   
 [Visual Basic 中的泛型类型](../../../visual-basic/programming-guide/language-features/data-types/generic-types.md)   
 [如何：使用泛型类](../../../visual-basic/programming-guide/language-features/data-types/how-to-use-a-generic-class.md)