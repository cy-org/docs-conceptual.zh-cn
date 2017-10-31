---
title: "Interface 语句 (Visual Basic) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
f1_keywords: 
  - "vb.Interface"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "Interface 语句 [Visual Basic]"
  - "接口, 接口定义"
ms.assetid: 8997af73-bda3-4f79-bd41-ca396b610260
caps.latest.revision: 26
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 26
---
# Interface 语句 (Visual Basic)
[!INCLUDE[vs2017banner](../../../visual-basic/includes/vs2017banner.md)]

声明接口的名称，并引入接口包含的成员的定义。  
  
## 语法  
  
```  
[ <attributelist> ] [ accessmodifier ] [ Shadows ] _  
Interface name [ ( Of typelist ) ]  
    [ Inherits interfacenames ]  
    [ [ modifiers ] Property membername ]  
    [ [ modifiers ] Function membername ]  
    [ [ modifiers ] Sub membername ]  
    [ [ modifiers ] Event membername ]  
    [ [ modifiers ] Interface membername ]  
    [ [ modifiers ] Class membername ]  
    [ [ modifiers ] Structure membername ]  
End Interface  
```  
  
## 部件  
  
|||  
|-|-|  
|术语|定义|  
|`attributelist`|可选。  请参见[特性列表](../../../visual-basic/language-reference/statements/attribute-list.md)。|  
|`accessmodifier`|可选。  可以是如下内容之一：<br /><br /> -   [Public](../../../visual-basic/language-reference/modifiers/public.md)<br />-   [Protected](../../../visual-basic/language-reference/modifiers/protected.md)<br />-   [Friend](../../../visual-basic/language-reference/modifiers/friend.md)<br />-   [Private](../../../visual-basic/language-reference/modifiers/private.md)<br />-   `Protected Friend`<br /><br /> 请参见 [Visual Basic 中的访问级别](../../../visual-basic/programming-guide/language-features/declared-elements/access-levels.md)。|  
|`Shadows`|可选。  请参见 [Shadows](../../../visual-basic/language-reference/modifiers/shadows.md)。|  
|`name`|必选。  此接口的名称。  请参见 [已声明的元素名称](../../../visual-basic/programming-guide/language-features/declared-elements/declared-element-names.md)。|  
|`Of`|可选。  指定这是一个泛型接口。|  
|`typelist`|如果使用 [Of](../../../visual-basic/language-reference/statements/of-clause.md) 关键字，则为必选项。  此接口的类型参数列表。  （可选）可以使用 `In` 和 `Out` 泛型修饰符将每个类型参数声明为 Variant。  请参见[类型列表](../../../visual-basic/language-reference/statements/type-list.md)。|  
|`Inherits`|可选。  指示此接口继承另一个接口或另外多个接口的特性与成员。  请参见 [Inherits 语句](../../../visual-basic/language-reference/statements/inherits-statement.md)。|  
|`interfacenames`|如果使用 `Inherits` 语句，则为必选项。  此接口派生自的接口的名称。|  
|`modifiers`|可选。  适用于所定义的接口成员的修饰符。|  
|`Property`|可选。  定义一个作为此接口成员的属性。|  
|`Function`|可选。  定义一个作为此接口成员的 `Function` 过程。|  
|`Sub`|可选。  定义一个作为此接口成员的 `Sub` 过程。|  
|`Event`|可选。  定义一个作为此接口成员的事件。|  
|`Interface`|可选。  定义一个嵌套在此接口中的接口。  嵌套的接口的定义必须以 `End Interface` 语句终止。|  
|`Class`|可选。  定义一个作为此接口成员的类。  成员类的定义必须以 `End Class` 语句终止。|  
|`Structure`|可选。  定义一个作为此接口成员的结构。  成员结构的定义必须以 `End Structure` 语句终止。|  
|`membername`|对于这些项目为必选项：定义为接口成员的每个属性、过程、事件、接口、类或结构。  成员的名称。|  
|`End Interface`|终止 `Interface` 定义。|  
  
## 备注  
 “接口”定义类和结构可以实现的一系列成员，如属性和过程。  接口只定义成员的签名，而不定义其内部的具体运作。  
  
 类或结构通过为接口定义的每个成员提供代码来实现接口。  最后，当应用程序通过该类或结构创建实例时，对象将会存在并在内存中运行。  有关更多信息，请参见[对象和类](../../../visual-basic/programming-guide/language-features/objects-and-classes/index.md)和 [接口](../../../visual-basic/programming-guide/language-features/interfaces/index.md)。  
  
 您只能在命名空间或模块级别使用 `Interface`。  这意味着接口的声明上下文必须是源文件、命名空间、类、结构、模块或接口，不能是过程或块。  有关更多信息，请参见[声明上下文和默认访问级别](../../../visual-basic/language-reference/statements/declaration-contexts-and-default-access-levels.md)。  
  
 接口默认为 [Friend](../../../visual-basic/language-reference/modifiers/friend.md) 访问级别。  可以使用访问修饰符来调整它们的访问级别。  有关更多信息，请参见 [Visual Basic 中的访问级别](../../../visual-basic/programming-guide/language-features/declared-elements/access-levels.md)。  
  
## 规则  
  
-   **嵌套接口。**可以在一个接口中定义另一个接口。  外部接口称为“包含接口”，而内部接口称为“嵌套接口”。  
  
-   **成员声明。**在将属性或过程声明为接口的成员时，您只是定义该属性或过程的签名。  这包括元素类型（属性或过程）、它的参数和参数类型以及它的返回类型。  有鉴于此，成员定义只使用一行代码，而且终止语句（如 `End Function` 或 `End Property`）在接口中无效。  
  
     相反，在定义枚举、结构或嵌套的类或接口时，必须包括它们的数据成员。  
  
-   **成员修饰符。**在定义模块成员时无法使用任何访问修饰符，也无法指定 [Shared](../../../visual-basic/language-reference/modifiers/shared.md) 或任何过程修饰符（[Overloads](../../../visual-basic/language-reference/modifiers/overloads.md) 除外）。  您可以使用 [Shadows](../../../visual-basic/language-reference/modifiers/shadows.md) 声明任何成员，并且可以在定义属性时使用 [Default](../../../visual-basic/language-reference/modifiers/default.md) 以及 [ReadOnly](../../../visual-basic/language-reference/modifiers/readonly.md) 或 [WriteOnly](../../../visual-basic/language-reference/modifiers/writeonly.md)。  
  
-   **继承。**如果接口使用 [Inherits 语句](../../../visual-basic/language-reference/statements/inherits-statement.md)，则可以指定一个或多个基接口。  可以从两个接口继承，即使它们各自定义了名称相同的成员也是如此。  如果这样做，则实现代码必须使用名称限定来指定它实现的是哪个成员。  
  
     接口无法从另一个具有限制性更高的访问级别的接口继承。  例如，`Public` 接口不能从 `Friend` 接口继承。  
  
     接口不能从其内部嵌套的接口继承。  
  
-   **实现。**当类使用 [Implements](../../../visual-basic/language-reference/statements/implements-clause.md) 语句来实现此接口时，它必须实现在此接口中定义的每个成员。  此外，实现代码中的每个签名均必须与此接口中定义的对应签名完全匹配。  但是，实现代码中的成员名称不必与接口中定义的成员名称匹配。  
  
     当类实现过程时，它无法将过程指定为 `Shared`。  
  
-   **默认属性。**一个接口至多可以将一个属性指定为其默认属性，您无需使用其属性名称即可引用此属性。  指定此类属性的方法是：利用 [Default](../../../visual-basic/language-reference/modifiers/default.md) 修饰符来声明它。  
  
     请注意，这表示接口只能在它未进行任何继承时定义默认属性。  
  
## 行为  
  
-   **访问级别。**所有接口成员都隐式地具有 [Public](../../../visual-basic/language-reference/modifiers/public.md) 访问级别。  在定义成员时，无法使用任何访问修饰符。  但是，实现接口的类可以为所实现的每个成员声明一个访问级别。  
  
     如果将类实例赋予某个变量，则此实例的成员的访问级别可能取决于该变量的数据类型是基础接口还是实现类。  下面的示例阐释了这一点。  
  
     [!code-vb[VbVbalrStatements#39](../../../visual-basic/language-reference/error-messages/codesnippet/VisualBasic/interface-statement_1.vb)]  
  
     如果通过 `varAsInterface` 访问类成员，则它们全都具有公共访问级别。  但是，如果通过 `varAsClass` 访问成员，则 `Sub` 过程 `doSomething` 具有私有访问级别。  
  
-   **范围。**接口的范围贯穿它的命名空间、类、结构或模块。  
  
     每个接口成员的范围是整个接口。  
  
-   **生存期。**接口本身和它的成员都没有生存期。  在类实现接口而且创建一个作为该类实例的对象时，此对象在它于其中运行的应用程序内具有生存期。  有关更多信息，请参见[Class 语句](../../../visual-basic/language-reference/statements/class-statement.md) 中的“生存期”。  
  
## 示例  
 下面的示例使用 `Interface` 语句来定义一个名为 `thisInterface` 的接口，后者必须利用 `Property` 语句和 `Function` 语句来实现。  
  
 [!code-vb[VbVbalrStatements#40](../../../visual-basic/language-reference/error-messages/codesnippet/VisualBasic/interface-statement_2.vb)]  
  
 请注意，`Property` 和 `Function` 语句并不在接口内引入以 `End Property` 和 `End Function` 结束的块。  接口只定义其成员的签名。  完整的 `Property` 和 `Function` 块出现在实现 `thisInterface` 的类中。  
  
## 请参阅  
 [接口](../../../visual-basic/programming-guide/language-features/interfaces/index.md)   
 [Class 语句](../../../visual-basic/language-reference/statements/class-statement.md)   
 [Module 语句](../../../visual-basic/language-reference/statements/module-statement.md)   
 [Structure 语句](../../../visual-basic/language-reference/statements/structure-statement.md)   
 [Property 语句](../../../visual-basic/language-reference/statements/property-statement.md)   
 [Function 语句](../../../visual-basic/language-reference/statements/function-statement.md)   
 [Sub 语句](../../../visual-basic/language-reference/statements/sub-statement.md)   
 [Visual Basic 中的泛型类型](../../../visual-basic/programming-guide/language-features/data-types/generic-types.md)   
 [泛型接口中的变体](../Topic/Variance%20in%20Generic%20Interfaces%20\(C%23%20and%20Visual%20Basic\).md)   
 [In](../../../visual-basic/language-reference/modifiers/in-generic-modifier.md)   
 [Out](../../../visual-basic/language-reference/modifiers/out-generic-modifier.md)