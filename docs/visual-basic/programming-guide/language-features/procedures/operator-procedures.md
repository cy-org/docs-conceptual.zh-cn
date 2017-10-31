---
title: "运算符过程 (Visual Basic 中) |Microsoft 文档"
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
- Visual Basic code, procedures
- procedures, operator
- Visual Basic code, operators
- syntax, Operator procedures
- operators [Visual Basic], overloading
- overloaded operators
- operator overloading
- operator procedures
ms.assetid: 8c513d38-246b-4fb7-8b75-29e1364e555b
caps.latest.revision: 17
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
ms.openlocfilehash: a9e86c9c466ba236cc33153f2f341af35c622de6
ms.lasthandoff: 03/13/2017

---
# <a name="operator-procedures-visual-basic"></a>运算符过程 (Visual Basic)
运算符过程是一系列[!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)]定义的行为的标准运算符的语句 (如`*`， `<>`，或`And`) 对类或已定义的结构。 这也称为*运算符重载*。  
  
## <a name="when-to-define-operator-procedures"></a>何时定义运算符过程  
 定义类或结构后，您可以声明为类或结构的类型的变量。 有时这种变量需要参与一个操作作为表达式的一部分。 若要执行此操作，它必须是运算符的操作数。  
  
 [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)]仅在其基本数据类型上定义运算符。 您可以定义运算符之一时的行为或两个操作数均为类或结构的类型。  
  
 有关详细信息，请参阅[Operator 语句](../../../../visual-basic/language-reference/statements/operator-statement.md)。  
  
## <a name="types-of-operator-procedure"></a>运算符过程的类型  
 运算符过程可以是以下类型之一︰  
  
-   一元运算符，其中参数都是类或结构的类型的定义。  
  
-   其中至少一个参数是类或结构的类型的二元运算符的定义。  
  
-   其中的参数是类或结构的类型的转换运算符的定义。  
  
-   转换运算符返回的类或结构类型的定义。  
  
 转换运算符都始终是一元，并且始终将`CType`用作您定义的运算符。  
  
## <a name="declaration-syntax"></a>声明语法  
 声明一个运算符过程的语法如下所示︰  
  
 `Public Shared`   `[Widening | Narrowing]`   `Operator`  *operatorsymbol*  `(` *operand1*  `[,`  *operand2* `]) As`  *datatype*  
  
 `' Statements of the operator procedure.`  
  
 `End Operator`  
  
 您使用`Widening`或`Narrowing`关键字仅在类型转换运算符。 运算符符号始终是[CType 函数](../../../../visual-basic/language-reference/functions/ctype-function.md)有关类型转换运算符。  
  
 声明两个操作数定义二元运算符，并声明一个要定义的一元运算符，包括类型转换运算符的操作数。 所有操作数都必须都声明`ByVal`。  
  
 声明每个操作数相同的方式声明的参数[Sub 过程](./sub-procedures.md)。  
  
### <a name="data-type"></a>数据类型  
 由于您正在对类或已定义的结构定义一个运算符，至少其中一个操作数必须是的该类或结构的数据类型。 对于类型转换运算符，操作数或返回类型必须是数据类型的类或结构。  
  
 有关详细信息，请参阅[Operator 语句](../../../../visual-basic/language-reference/statements/operator-statement.md)。  
  
## <a name="calling-syntax"></a>调用语法  
 通过在表达式中使用运算符的隐式调用运算符过程。 提供对操作数相同的方式相似，预定义的运算符。  
  
 隐式调用运算符过程的语法如下所示︰  
  
 `Dim testStruct As`  *structurename*  
  
 `Dim testNewStruct As`  *structurename*`= testStruct`*operatorsymbol    *  `10`  
  
### <a name="illustration-of-declaration-and-call"></a>声明和调用的插图  
 以下结构存储构成的高序位和低序位部分作为一个 128 位带符号的整数值。 它定义了`+`运算符以添加两个`veryLong`值，并生成生成`veryLong`值。  
  
 [!code-vb[VbVbcnProcedures 第&23;](./codesnippet/VisualBasic/operator-procedures_1.vb)]  
  
 下面的示例演示如何调用典型`+`上定义的运算符`veryLong`。  
  
 [!code-vb[VbVbcnProcedures #&24;](./codesnippet/VisualBasic/operator-procedures_2.vb)]  
  
 有关详细信息和示例，请参阅[Visual Basic 2005 中的运算符重载](http://go.microsoft.com/fwlink/?LinkId=101703)。  
  
## <a name="see-also"></a>另请参阅  
 [过程](./index.md)   
 [Sub 过程](./sub-procedures.md)   
 [Function 过程](./function-procedures.md)   
 [属性过程](./property-procedures.md)   
 [过程参数和变量](./procedure-parameters-and-arguments.md)   
 [Operator 语句](../../../../visual-basic/language-reference/statements/operator-statement.md)   
 [如何︰ 定义运算符](./how-to-define-an-operator.md)   
 [如何︰ 定义转换运算符](./how-to-define-a-conversion-operator.md)   
 [如何︰ 调用运算符过程](./how-to-call-an-operator-procedure.md)   
 [如何：使用定义运算符的类](./how-to-use-a-class-that-defines-operators.md)
