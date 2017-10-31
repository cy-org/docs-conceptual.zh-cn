---
title: "Property 过程 (Visual Basic 中) |Microsoft 文档"
ms.custom: 
ms.date: 2015-07-20
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology:
- devlang-visual-basic
ms.topic: article
dev_langs:
- VB
helpviewer_keywords:
- Set statement, Property procedures
- Visual Basic code, procedures
- return values, Property procedures
- syntax, Property procedures
- procedures, property
- Visual Basic code, properties
- procedures, calling
- properties [Visual Basic], custom
- property procedures
- Get statement, property procedures
ms.assetid: 46a98379-e1a2-45dd-a48c-b51213f5ab07
caps.latest.revision: 22
author: dotnet-bot
ms.author: dotnetcontent
translation.priority.ht:
- de-de
- es-es
- fr-fr
- it-it
- ja-jp
- ko-kr
- ru-ru
- zh-cn
- zh-tw
translation.priority.mt:
- cs-cz
- pl-pl
- pt-br
- tr-tr
translationtype: Machine Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: f21d4c7d9bd8f14bbe7284bc08399e7ba6b466c3
ms.lasthandoff: 03/13/2017

---
# <a name="property-procedures-visual-basic"></a>Property 过程 (Visual Basic)
Property 过程是一系列[!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)]操作上模块、 类或结构的自定义属性的语句。 属性过程也被称为*属性访问器*。  
  
 [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)]提供了以下属性过程︰  
  
-   一个`Get`过程将返回属性的值。 访问在表达式中的属性时调用它。  
  
-   一个`Set`过程将属性设置为某个值，包括的对象引用。 将值分配给属性时调用它。  
  
 通常要定义属性过程中使用的对`Get`和`Set`语句中，但您可以定义单独无论哪一过程，如果该属性是只读的 ([Get 语句](../../../../visual-basic/language-reference/statements/get-statement.md)) 或只写 ([Set 语句](../../../../visual-basic/language-reference/statements/set-statement.md))。  
  
 可以省略`Get`和`Set`过程时使用自动实现的属性。 有关详细信息，请参阅[类属性](./auto-implemented-properties.md)。  
  
 可以在类、 结构和模块中定义属性。 属性是`Public`默认情况下，这意味着可以从任何位置进行调用的应用程序可以访问该属性的容器中。  
  
 属性和变量的比较，请参阅[属性之间的差异和 Visual Basic 中的变量](./differences-between-properties-and-variables.md)。  
  
## <a name="declaration-syntax"></a>声明语法  
 由内包含的代码块中定义的属性本身[属性语句](../../../../visual-basic/language-reference/statements/property-statement.md)和`End Property`语句。 在此块中，内部形式出现作为内部块括在声明语句内的每个 property 过程 (`Get`或`Set`) 和匹配`End`声明。  
  
 声明的属性和它的过程的语法如下所示︰  
  
```  
[Default] [Modifiers] Property PropertyName[(ParameterList)] [As DataType]  
    [AccessLevel] Get  
        ' Statements of the Get procedure.  
        ' The following statement returns an expression as the property's value.  
        Return Expression  
    End Get  
    [AccessLevel] Set[(ByVal NewValue As DataType)]  
        ' Statements of the Set procedure.  
        ' The following statement assigns newvalue as the property's value.  
        LValue = NewValue  
    End Set  
End Property  
- or -  
[Default] [Modifiers] Property PropertyName [(ParameterList)] [As DataType]  
```  
  
 `Modifiers`可以指定访问级别以及与重载、 重写、 共享、 隐藏的比较，相关的信息以及该属性是只读的还是只写。 `AccessLevel`上`Get`或`Set`过程可以是任何级别的限制性强于属性自身为指定的访问级别。 有关详细信息，请参阅[属性语句](../../../../visual-basic/language-reference/statements/property-statement.md)。  
  
### <a name="data-type"></a>数据类型  
 在中定义属性的数据类型和主体的访问级别`Property`语句不在的属性过程。 属性可以具有一种数据类型。 例如，不能定义属性存储`Decimal`值而检索`Double`值。  
  
### <a name="access-level"></a>访问级别  
 但是，您可以定义主要访问级别的属性和一个它的属性过程中的访问级别来进一步限制。 例如，您可以定义`Public`属性，然后定义`Private Set`过程。 `Get`过程保持`Public`。 可以更改属性的过程之一中的访问级别，您可以只是使其限制性强于主体的访问级别。 有关详细信息，请参阅[如何︰ 声明具有混合访问级别的属性](./how-to-declare-a-property-with-mixed-access-levels.md)。  
  
## <a name="parameter-declaration"></a>参数声明  
 声明每个参数相同的方式相似， [Sub 过程](./sub-procedures.md)，只不过必须传递机制`ByVal`。  
  
 参数列表中每个参数的语法是，如下所示︰  
  
 `[Optional] ByVal [ParamArray] parametername As datatype`  
  
 如果该参数是可选的您还必须提供默认值作为其声明的一部分。 用于指定默认值的语法如下所示︰  
  
 `Optional ByVal parametername As datatype = defaultvalue`  
  
## <a name="property-value"></a>属性值  
 在`Get`的过程中，则返回值提供给调用表达式的值的属性。  
  
 在`Set`的过程中，新的属性值传递给参数`Set`语句。 如果显式声明一个参数，您必须使用相同的数据类型作为属性声明它。 如果不声明一个参数，编译器将使用隐式参数`Value`来表示要分配给属性的新值。  
  
## <a name="calling-syntax"></a>调用语法  
 通过使对该属性引用的隐式调用 property 过程。 您的属性名称相同的方式使用您将使用变量的名称，只不过你必须为不是可选的所有参数提供值，则必须将参数列表括在括号中。 如果未不提供任何参数，可以选择省略括号。  
  
 隐式调用的语法`Set`过程是，如下所示︰  
  
 `propertyname[(argumentlist)] = expression`  
  
 隐式调用的语法`Get`过程是，如下所示︰  
  
 `lvalue = propertyname[(argumentlist)]`  
  
 `Do While (propertyname[(argumentlist)] > expression)`  
  
### <a name="illustration-of-declaration-and-call"></a>声明和调用的插图  
 以下属性将存储为两个构成的名称、 名字和姓氏的完整名称。 当调用的代码中读取`fullName`、`Get`过程将组合构成的两个名称，并返回的完整名称。 当调用代码将分配一个新的完整名称，`Set`过程尝试将其分解为两个构成的名称。 如果找不到一个空间，它可以将其存储所有作为第一个名称。  
  
 [!code-vb[VbVbcnProcedures #&8;](./codesnippet/VisualBasic/property-procedures_1.vb)]  
  
 下面的示例显示的属性过程的典型调用`fullName`。  
  
 [!code-vb[VbVbcnProcedures #&9;](./codesnippet/VisualBasic/property-procedures_2.vb)]  
  
## <a name="see-also"></a>另请参阅  
 [过程](./index.md)   
 [Function 过程](./function-procedures.md)   
 [运算符过程](./operator-procedures.md)   
 [过程参数和变量](./procedure-parameters-and-arguments.md)   
 [在 Visual Basic 中属性和变量之间的差异](./differences-between-properties-and-variables.md)   
 [如何︰ 创建属性](./how-to-create-a-property.md)   
 [如何︰ 调用 Property 过程](./how-to-call-a-property-procedure.md)   
 [如何︰ 声明和调用默认属性在 Visual Basic 中](./how-to-declare-and-call-a-default-property.md)   
 [如何︰ 在属性中放置值](./how-to-put-a-value-in-a-property.md)   
 [如何：从属性获取值](./how-to-get-a-value-from-a-property.md)
