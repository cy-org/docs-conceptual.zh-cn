---
title: "/ 运算符 (Visual Basic 中) |Microsoft 文档"
ms.date: 2015-07-20
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology:
- devlang-visual-basic
ms.topic: article
f1_keywords:
- vb./
dev_langs:
- VB
helpviewer_keywords:
- division operator, floating point
- floating-point numbers, division operator
- slash (/) operator
- zero, division by zero
- operators [Visual Basic], arithmetic
- arithmetic operators, division
- division, by zero
- operators [Visual Basic], division
- division operator, syntax
- / operator [Visual Basic]
- math operators
ms.assetid: 335e97f2-c434-439e-9064-76973a051101
caps.latest.revision: 18
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
ms.openlocfilehash: 71b4f64f6deeb334412c87131ccd9480620f284f
ms.contentlocale: zh-cn
ms.lasthandoff: 03/13/2017

---
# <a name="-operator-visual-basic"></a>/ 运算符 (Visual Basic)
使两个数字相除，返回浮点结果。  
  
## <a name="syntax"></a>语法  
  
```  
expression1 / expression2  
```  
  
## <a name="parts"></a>部件  
 `expression1`  
 必需。 任何数值表达式。  
  
 `expression2`  
 必需。 任何数值表达式。  
  
## <a name="supported-types"></a>支持的类型  
 所有数值类型，包括无符号和浮点类型和`Decimal`。  
  
## <a name="result"></a>结果  
 结果是完整的商`expression1`除以`expression2`，包括任何余数。  
  
 [\ 运算符 (Visual Basic)](../../../visual-basic/language-reference/operators/integer-division-operator.md)返回整数的商，将删除其余部分。  
  
## <a name="remarks"></a>备注  
 结果的数据类型取决于操作数的类型。 下表显示如何确定结果的数据类型。  
  
|操作数数据类型|结果数据类型|  
|------------------------|----------------------|  
|这两个表达式都是整数数据类型 ([SByte](../../../visual-basic/language-reference/data-types/sbyte-data-type.md)，[字节](../../../visual-basic/language-reference/data-types/byte-data-type.md)，[短](../../../visual-basic/language-reference/data-types/short-data-type.md)， [UShort](../../../visual-basic/language-reference/data-types/ushort-data-type.md)，[整数](../../../visual-basic/language-reference/data-types/integer-data-type.md)， [UInteger](../../../visual-basic/language-reference/data-types/uinteger-data-type.md)，[长](../../../visual-basic/language-reference/data-types/long-data-type.md)， [ULong](../../../visual-basic/language-reference/data-types/ulong-data-type.md))|`Double`|  
|一个表达式是[单个](../../../visual-basic/language-reference/data-types/single-data-type.md)数据类型，另一个不是[Double](../../../visual-basic/language-reference/data-types/double-data-type.md)|`Single`|  
|一个表达式是[十进制](../../../visual-basic/language-reference/data-types/decimal-data-type.md)数据类型，另一个不是[单个](../../../visual-basic/language-reference/data-types/single-data-type.md)或[Double](../../../visual-basic/language-reference/data-types/double-data-type.md)|`Decimal`|  
|其中任何一个表达式是[Double](../../../visual-basic/language-reference/data-types/double-data-type.md)数据类型|`Double`|  
  
 执行除法运算之前，将任何整数数值表达式被扩展为`Double`。 如果将结果分配给整型数据类型，请尝试将转换的结果 Visual Basic`Double`为该类型。 如果结果无法容纳在该类型，这可以引发异常。 请参见此帮助页上的"尝试用零作除数"。  
  
 如果`expression1`或`expression2`的计算结果为[Nothing](../../../visual-basic/language-reference/nothing.md)，它将被视为零。  
  
## <a name="attempted-division-by-zero"></a>尝试被零除  
 如果`expression2`计算结果为零，`/`运算符的操作数数据类型不同的行为以不同的方式。 下表显示可能的行为。  
  
|操作数数据类型|行为如果`expression2`为零|  
|------------------------|---------------------------------------|  
|浮点 (`Single`或`Double`)|返回无穷大 (<xref:System.Double.PositiveInfinity>或<xref:System.Double.NegativeInfinity>)，或<xref:System.Double.NaN>（而不是数字） 如果`expression1`也为零</xref:System.Double.NaN></xref:System.Double.NegativeInfinity></xref:System.Double.PositiveInfinity>|  
|`Decimal`|将引发<xref:System.DivideByZeroException></xref:System.DivideByZeroException>|  
|整数 （有符号或无符号）|尝试转换回整数类型，则会引发<xref:System.OverflowException>因为整数类型不能接受<xref:System.Double.PositiveInfinity>， <xref:System.Double.NegativeInfinity>，或<xref:System.Double.NaN></xref:System.Double.NaN></xref:System.Double.NegativeInfinity></xref:System.Double.PositiveInfinity></xref:System.OverflowException>|  
  
> [!NOTE]
>  `/`运算符可以被*重载*，这意味着，某个类或结构可以重新定义其行为时，操作数的类或结构的类型。 如果您的代码对这样的类或结构中使用此运算符，请确保您了解其被重新定义的行为。 有关详细信息，请参阅[运算符过程](../../../visual-basic/programming-guide/language-features/procedures/operator-procedures.md)。  
  
## <a name="example"></a>示例  
 此示例使用`/`运算符执行浮点除法运算。 结果是两个操作数的商。  
  
 [!code-vb[VbVbalrOperators #&16;](../../../visual-basic/language-reference/operators/codesnippet/VisualBasic/floating-point-division-operator_1.vb)]  
  
 在前面的示例表达式返回 2.5 和 3.333333 的值。 请注意，结果始终是浮点 (`Double`)，即使这两个操作数都是整数常量。  
  
## <a name="see-also"></a>另请参阅  
 [/ = 运算符 (Visual Basic)](../../../visual-basic/language-reference/operators/floating-point-division-assignment-operator.md)   
 [\ 运算符 (Visual Basic)](../../../visual-basic/language-reference/operators/integer-division-operator.md)   
 [运算符结果的数据类型](../../../visual-basic/language-reference/operators/data-types-of-operator-results.md)   
 [算术运算符](../../../visual-basic/language-reference/operators/arithmetic-operators.md)   
 [在 Visual Basic 中的运算符优先级](../../../visual-basic/language-reference/operators/operator-precedence.md)   
 [按功能列出的运算符](../../../visual-basic/language-reference/operators/operators-listed-by-functionality.md)   
 [在 Visual Basic 中的算术运算符](../../../visual-basic/programming-guide/language-features/operators-and-expressions/arithmetic-operators.md)

