---
title: "Delegate 语句 |Microsoft 文档"
ms.date: 2015-07-20
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology:
- devlang-visual-basic
ms.topic: article
f1_keywords:
- vb.Delegate
dev_langs:
- VB
helpviewer_keywords:
- delegate keyword
- Delegate statement
ms.assetid: f799c518-0817-40cc-ad0b-4da846fdba57
caps.latest.revision: 27
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
translationtype: Machine Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: 9ac9e28c82f8a6b5a9c1398961d831c956a649e0
ms.lasthandoff: 03/13/2017

---
# <a name="delegate-statement"></a>Delegate 语句
用于声明委托。 委托是一个引用类型，是指`Shared`方法的类型或对象的实例方法。 任何具有匹配的参数和返回类型的过程可以用于创建此委托类的实例。 然后可以通过委托实例就调用该过程。  
  
## <a name="syntax"></a>语法  
  
```  
[ <attrlist> ] [ accessmodifier ] _  
[ Shadows ] Delegate [ Sub | Function ] name [( Of typeparamlist )] [([ parameterlist ])] [ As type ]  
```  
  
## <a name="parts"></a>部件  
  
|术语|定义|  
|---|---|  
|`attrlist`|可选。 适用于此委托属性的列表。 用逗号分隔多个属性。 必须将括[属性列表](../../../visual-basic/language-reference/statements/attribute-list.md)在尖括号 ("`<`"和"`>`")。|  
|`accessmodifier`|可选。 指定哪些代码可以访问该委托。 可以是以下各项之一：<br /><br /> -   [公共](../../../visual-basic/language-reference/modifiers/public.md)。 可以访问的元素声明委托的任何代码都可以访问它。<br />-   [受保护的](../../../visual-basic/language-reference/modifiers/protected.md)。 只有在委托的类或派生的类中的代码可以访问它。<br />-   [友元](../../../visual-basic/language-reference/modifiers/friend.md)。 只有同一程序集中的代码可以访问该委托。<br />-   [专用](../../../visual-basic/language-reference/modifiers/private.md)。 仅在声明委托的元素内的代码可以访问它。<br /><br /> 您可以指定`Protected Friend`以便实现从委托的类，派生的类中或同一程序集中的代码中访问。|  
|`Shadows`|可选。 指示此委托重新声明隐藏同名的编程元素或在基类中重载元素集。 可以与任何其他类型一起隐藏任何类型的已声明元素。<br /><br /> 隐藏的元素不可在隐藏它的派生类中使用（除了从隐藏元素不可访问的位置）。 例如，如果`Private`元素将隐藏基类元素，不具有访问权限的代码`Private`元素访问的基类元素相反。|  
|`Sub`|可选，但任何一个`Sub`或`Function`必须出现。 将委托作为此过程声明`Sub`不返回值的过程。|  
|`Function`|可选，但任何一个`Sub`或`Function`必须出现。 将委托作为此过程声明`Function`返回一个值的过程。|  
|`name`|必需。 委托类型; 的名称遵循标准的变量命名规则。|  
|`typeparamlist`|可选。 此委托的类型参数列表。 由逗号分隔多个类型参数。 （可选） 每个类型参数可以声明变量使用`In`和`Out`泛型修饰符。 必须将括[类型列表](../../../visual-basic/language-reference/statements/type-list.md)在括号中，并引入其与`Of`关键字。|  
|`parameterlist`|可选。 被调用时传递给过程的参数的列表。 必须将括[参数列表](../../../visual-basic/language-reference/statements/parameter-list.md)在括号中。|  
|`type`|如果指定，则必需`Function`过程。 返回值的数据类型。|  
  
## <a name="remarks"></a>备注  
 `Delegate`语句定义委托类的参数和返回类型。 任何具有匹配的参数和返回类型的过程可以用于创建此委托类的实例。 然后就可以被调用过程通过委托实例，通过调用该委托的`Invoke`方法。  
  
 可以声明委托，在命名空间、 模块、 类或结构级别，但不是能在过程。  
  
 每个委托类均可定义将对象方法指定传递到的构造函数。 委托构造函数的参数必须是对方法或 lambda 表达式的引用。  
  
 若要指定对方法的引用，请使用以下语法︰  
  
 `AddressOf` [`expression`.]`methodname`  
  
 编译时类型`expression`必须是一个类或接口包含其签名与委托类的签名匹配的指定名称的方法的名称。 `methodname`可以是共享的方法或实例方法。 `methodname`不是可选的即使您创建的类的默认方法的委托。  
  
 若要指定 lambda 表达式，请使用以下语法︰  
  
 `Function`([`parm` As `type`, `parm2` As `type2`, ...])`expression`  
  
 函数的签名必须与匹配的委托类型。 有关 lambda 表达式的详细信息，请参阅 [Lambda 表达式](../../../visual-basic/programming-guide/language-features/procedures/lambda-expressions.md)。  
  
 有关委托的详细信息，请参阅[委托](../../../visual-basic/programming-guide/language-features/delegates/index.md)。  
  
## <a name="example"></a>示例  
 下面的示例使用`Delegate`语句来声明一个委托，对两个数字进行运算并返回一个数字。 `DelegateTest`方法采用这种类型的委托的一个实例，并使用它来对数字进行操作。  
  
 [!code-vb[VbVbalrDelegates #&14;](../../../visual-basic/language-reference/operators/codesnippet/VisualBasic/delegate-statement_1.vb)]  
  
## <a name="see-also"></a>另请参阅  
 [AddressOf 运算符](../../../visual-basic/language-reference/operators/addressof-operator.md)   
 [Of](../../../visual-basic/language-reference/statements/of-clause.md)   
 [委托](../../../visual-basic/programming-guide/language-features/delegates/index.md)   
 [如何︰ 使用泛型类](../../../visual-basic/programming-guide/language-features/data-types/how-to-use-a-generic-class.md)   
 [Visual Basic 中的泛型类型](../../../visual-basic/programming-guide/language-features/data-types/generic-types.md)   
 [协变和逆变](http://msdn.microsoft.com/library/a58cc086-276f-4f91-a366-85b7f95f38b8)   
 [在](../../../visual-basic/language-reference/modifiers/in-generic-modifier.md)   
 [扩展](../../../visual-basic/language-reference/modifiers/out-generic-modifier.md)
