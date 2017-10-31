---
title: "Property 语句 |Microsoft 文档"
ms.date: 2015-07-20
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology:
- devlang-visual-basic
ms.topic: article
f1_keywords:
- vb.PropertySet
- vb.Property
- vb.PropertyGet
dev_langs:
- VB
helpviewer_keywords:
- Property statement
- default modifier
- property procedures, Property statements
- Property keyword
ms.assetid: 3155edaf-8ebd-45c6-9cef-11d5d2dc8d38
caps.latest.revision: 41
author: dotnet-bot
ms.author: dotnetcontent
translation.priority.ht:
- cs-cz
- de-de
- es-es
- fr-fr
- it-it
- ja-jp
- ko-kr
- pl-pl
- pt-br
- ru-ru
- tr-tr
- zh-cn
- zh-tw
ms.translationtype: Machine Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: 87cb32c12ab3238508a6a4bb114306909e409dda
ms.contentlocale: zh-cn
ms.lasthandoff: 03/13/2017

---
# <a name="property-statement"></a>Property Statement
声明用于存储和检索属性值的属性名称和属性过程。  
  
## <a name="syntax"></a>语法  
  
```  
[ <attributelist> ] [ Default ] [ accessmodifier ]   
[ propertymodifiers ] [ Shared ] [ Shadows ] [ ReadOnly | WriteOnly ] [ Iterator ]  
Property name ( [ parameterlist ] ) [ As returntype ] [ Implements implementslist ]  
    [ <attributelist> ] [ accessmodifier ] Get  
        [ statements ]  
    End Get  
    [ <attributelist> ] [ accessmodifier ] Set ( ByVal value As returntype [, parameterlist ] )  
        [ statements ]  
    End Set  
End Property  
- or -  
[ <attributelist> ] [ Default ] [ accessmodifier ]   
[ propertymodifiers ] [ Shared ] [ Shadows ] [ ReadOnly | WriteOnly ]   
Property name ( [ parameterlist ] ) [ As returntype ] [ Implements implementslist ]  
```  
  
## <a name="parts"></a>部件  
  
-   `attributelist`  
  
     可选。 将应用于此属性的属性的列表或`Get`或`Set`过程。 请参阅[属性列表](../../../visual-basic/language-reference/statements/attribute-list.md)。  
  
-   `Default`  
  
     可选。 指定此属性是类或结构在其定义的默认属性。 默认属性必须接受参数并可以设置并检索，而不必指定属性名称。 如果您声明的属性作为`Default`，不能使用`Private`在属性上或它的属性过程中的任何一个。  
  
-   `accessmodifier`  
  
     上是可选的`Property`语句和上最多一种`Get`和`Set`语句。 可以是以下各项之一：  
  
    -   [Public](../../../visual-basic/language-reference/modifiers/public.md)  
  
    -   [Protected](../../../visual-basic/language-reference/modifiers/protected.md)  
  
    -   [Friend](../../../visual-basic/language-reference/modifiers/friend.md)  
  
    -   [Private](../../../visual-basic/language-reference/modifiers/private.md)  
  
    -   `Protected Friend`  
  
     请参阅[访问 Visual Basic 中的级别](../../../visual-basic/programming-guide/language-features/declared-elements/access-levels.md)。  
  
-   `propertymodifiers`  
  
     可选。 可以是以下各项之一：  
  
    -   [重载](../../../visual-basic/language-reference/modifiers/overloads.md)  
  
    -   [Overrides](../../../visual-basic/language-reference/modifiers/overrides.md)  
  
    -   [Overridable](../../../visual-basic/language-reference/modifiers/overridable.md)  
  
    -   [NotOverridable](../../../visual-basic/language-reference/modifiers/notoverridable.md)  
  
    -   [MustOverride](../../../visual-basic/language-reference/modifiers/mustoverride.md)  
  
    -   `MustOverride Overrides`  
  
    -   `NotOverridable Overrides`  
  
-   `Shared`  
  
     可选。 请参阅[共享](../../../visual-basic/language-reference/modifiers/shared.md)。  
  
-   `Shadows`  
  
     可选。 请参阅[阴影](../../../visual-basic/language-reference/modifiers/shadows.md)。  
  
-   `ReadOnly`  
  
     可选。 请参阅[ReadOnly](../../../visual-basic/language-reference/modifiers/readonly.md)。  
  
-   `WriteOnly`  
  
     可选。 请参阅[WriteOnly](../../../visual-basic/language-reference/modifiers/writeonly.md)。  
  
-   `Iterator`  
  
     可选。 请参阅[迭代器](../../../visual-basic/language-reference/modifiers/iterator.md)。  
  
-   `name`  
  
     必需。 属性的名称。 请参阅[声明的元素名称](../../../visual-basic/programming-guide/language-features/declared-elements/declared-element-names.md)。  
  
-   `parameterlist`  
  
     可选。 表示此属性的参数及可能具有的其他参数的本地变量名的列表`Set`过程。 请参阅[参数列表](../../../visual-basic/language-reference/statements/parameter-list.md)。  
  
-   `returntype`  
  
     如果使用`Option``Strict`是`On`。 此属性返回的值的数据类型。  
  
-   `Implements`  
  
     可选。 指示此属性实现一个或多个属性，此属性包含类或结构实现的接口中定义每个组。 请参阅[实现语句](../../../visual-basic/language-reference/statements/implements-statement.md)。  
  
-   `implementslist`  
  
     如果提供 `Implements`，则是必需的。 将实现的属性的列表。  
  
     `implementedproperty [ , implementedproperty ... ]`  
  
     每个 `implementedproperty` 都具有以下语法和部件：  
  
     `interface.definedname`  
  
    |部件|描述|  
    |---|---|  
    |`interface`|必需。 此属性实现的接口的名称的包含类或结构。|  
    |`definedname`|必需。 依据属性定义的名称`interface`。|  
  
-   `Get`  
  
     可选。 如果标记了该属性所需`WriteOnly`。 启动`Get`用于返回属性的值的属性过程。  
  
-   `statements`  
  
     可选。 要在中运行的语句块`Get`或`Set`过程。  
  
-   `End Get`  
  
     终止`Get`属性过程。  
  
-   `Set`  
  
     可选。 如果标记了该属性所需`ReadOnly`。 启动`Set`属性用来存储属性的值的过程。  
  
-   `End Set`  
  
     终止`Set`属性过程。  
  
-   `End Property`  
  
     终止此属性的定义。  
  
## <a name="remarks"></a>备注  
 `Property`语句引入属性声明。 属性可以具有`Get`过程 （只读），`Set`过程 （只写） 或二者 （读写）。 可以省略`Get`和`Set`过程时使用自动实现的属性。 有关详细信息，请参阅[类属性](../../../visual-basic/programming-guide/language-features/procedures/auto-implemented-properties.md)。  
  
 您可以使用`Property`只能在类级别。 这意味着*声明上下文*属性必须是类、 结构、 模块或接口，并且不能为源文件、 命名空间、 过程或块。 有关详细信息，请参阅[声明上下文和默认访问级别](../../../visual-basic/language-reference/statements/declaration-contexts-and-default-access-levels.md)。  
  
 默认情况下，属性使用公共访问权限。 您可以调整使用访问修饰符的属性的访问级别上`Property`语句中，还可以选择性地调整它的属性过程限制性更强的访问级别之一。  
  
 Visual Basic 将传递到参数`Set`期间属性赋值的过程。 如果不提供的参数`Set`，集成的开发环境 (IDE) 使用一个名为的隐式参数`value`。 此参数包含要分配给属性的值。 通常将此值存储在专用的本地变量并将其返回每当`Get`调用过程。  
  
## <a name="rules"></a>规则  
  
-   **混合的访问级别。** 如果要定义一个读 / 写属性，您可以选择指定不同的访问级别适用于`Get`或`Set`的过程中，但不要同时使用两者。 如果执行此操作时，过程访问级别必须是限制性强于属性的访问级别。 例如，如果声明该属性为`Friend`，您可以声明`Set`过程`Private`，但不是`Public`。  
  
     如果您正在定义`ReadOnly`或`WriteOnly`属性中，单个 property 过程 (`Get`或`Set`分别) 表示所有属性。 不能声明此类过程中，不同的访问级别，因为这会设置该属性的两个访问级别。  
  
-   **返回类型。** `Property`语句可以声明它返回的值的数据类型。 您可以指定任何数据类型或枚举、 结构、 类或接口的名称。  
  
     如果未指定`returntype`，该属性返回`Object`。  
  
-   **实现。** 如果此属性使用`Implements`关键字、 包含的类或结构必须具有`Implements`紧随其`Class`或`Structure`语句。 `Implements`语句必须包含以指定每个接口`implementslist`。 但是，通过该接口定义的名称`Property`(在`definedname`) 没有为此属性的名称相同 (在`name`)。  
  
## <a name="behavior"></a>行为  
  
-   **从属性过程中返回。** 当`Get`或`Set`过程返回到调用代码时，继续执行的语句之后调用它的语句。  
  
     `Exit Property`和`Return`语句属性过程就会立即退出。 任意数量的`Exit Property`和`Return`语句可以在过程中，任何位置出现，并可混合`Exit Property`和`Return`语句。  
  
-   **返回值。** 返回一个介于`Get`的过程中，您可以将该值赋给属性名称或将其包含在`Return`语句。 下面的示例将返回值分配给属性名称`quoteForTheDay`，然后使用`Exit Property`语句返回。  
  
     [!code-vb[VbVbalrStatements #&27;](../../../visual-basic/language-reference/error-messages/codesnippet/VisualBasic/property-statement_1.vb)]  
  
     [!code-vb[VbVbalrStatements #&28;](../../../visual-basic/language-reference/error-messages/codesnippet/VisualBasic/property-statement_2.vb)]  
  
     如果您使用`Exit Property`而无需将值分配给`name`、`Get`过程将返回属性的数据类型的默认值。  
  
     `Return`语句同时分配`Get`过程返回值并退出该过程。 下面的示例演示了此过程。  
  
     [!code-vb[VbVbalrStatements #&27;](../../../visual-basic/language-reference/error-messages/codesnippet/VisualBasic/property-statement_1.vb)]  
  
     [!code-vb[VbVbalrStatements #&29;](../../../visual-basic/language-reference/error-messages/codesnippet/VisualBasic/property-statement_3.vb)]  
  
## <a name="example"></a>示例  
 下面的示例声明一个类中的属性。  
  
 [!code-vb[VbVbalrStatements #&51;](../../../visual-basic/language-reference/error-messages/codesnippet/VisualBasic/property-statement_4.vb)]  
  
## <a name="see-also"></a>另请参阅  
 [自动实现的属性](../../../visual-basic/programming-guide/language-features/procedures/auto-implemented-properties.md)   
 [对象和类](../../../visual-basic/programming-guide/language-features/objects-and-classes/index.md)   
 [Get 语句](../../../visual-basic/language-reference/statements/get-statement.md)   
 [Set 语句](../../../visual-basic/language-reference/statements/set-statement.md)   
 [参数列表](../../../visual-basic/language-reference/statements/parameter-list.md)   
 [默认](../../../visual-basic/language-reference/modifiers/default.md)

