---
title: "扩大转换和收缩转换 (Visual Basic 中) |Microsoft 文档"
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
- widening conversions
- narrowing conversions
- conversions, type
- data types [Visual Basic], changing
- variables [Visual Basic], changing data type
- conversions, exceptions during conversion
- type conversion, exceptions during conversion
- conversions, data type
- conversions, narrowing
- type conversion, narrowing
- data type conversion, widening
- data type conversion, narrowing
- changing data types
- type conversion, widening
- data type conversion, exceptions during conversion
- conversions, widening
ms.assetid: 058c3152-6c28-4268-af44-2209e774f0bd
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
ms.openlocfilehash: 88c5db6e7e82a88ae8015b581e5a795ec389d003
ms.lasthandoff: 03/13/2017

---
# <a name="widening-and-narrowing-conversions-visual-basic"></a>扩大转换和收缩转换 (Visual Basic)
通过类型转换的一个重要注意事项是转换的结果是否在目标数据类型的范围内。  
  
 一个*扩大转换*将值更改为数据类型，可允许的任何可能的值的原始数据。  扩大转换保留源值，但可以更改它的表示形式。 发生这种情况是如果你转换为整数类型转换`Decimal`，或从`Char`到`String`。  
  
 *“收缩转换”* 将值更改为可能无法保存某些可能值的数据类型。 例如，小数部分的值将舍入转换为整数类型，而转换为数值类型时`Boolean`缩减为`True`或`False`。  
  
## <a name="widening-conversions"></a>扩大转换  
 下表显示了标准的扩大转换。  
  
|数据类型|为数据类型加宽<sup>1</sup>|  
|---|---|  
|[SByte](../../../../visual-basic/language-reference/data-types/sbyte-data-type.md)|`SByte`, `Short`, `Integer`, `Long`, `Decimal`, `Single`, `Double`|  
|[Byte](../../../../visual-basic/language-reference/data-types/byte-data-type.md)|`Byte`, `Short`, `UShort`, `Integer`, `UInteger`, `Long`, `ULong`, `Decimal`, `Single`, `Double`|  
|[短](../../../../visual-basic/language-reference/data-types/short-data-type.md)|`Short`, `Integer`, `Long`, `Decimal`, `Single`, `Double`|  
|[UShort](../../../../visual-basic/language-reference/data-types/ushort-data-type.md)|`UShort`, `Integer`, `UInteger`, `Long`, `ULong`, `Decimal`, `Single`, `Double`|  
|[整数](../../../../visual-basic/language-reference/data-types/integer-data-type.md)|`Integer`, `Long`, `Decimal`, `Single`, `Double`<sup>2</sup>|  
|[UInteger](../../../../visual-basic/language-reference/data-types/uinteger-data-type.md)|`UInteger`, `Long`, `ULong`, `Decimal`, `Single`, `Double`<sup>2</sup>|  
|[长时间](../../../../visual-basic/language-reference/data-types/long-data-type.md)|`Long`, `Decimal`, `Single`, `Double`<sup>2</sup>|  
|[ULong](../../../../visual-basic/language-reference/data-types/ulong-data-type.md)|`ULong`, `Decimal`, `Single`, `Double`<sup>2</sup>|  
|[小数](../../../../visual-basic/language-reference/data-types/decimal-data-type.md)|`Decimal`, `Single`, `Double`<sup>2</sup>|  
|[单精度](../../../../visual-basic/language-reference/data-types/single-data-type.md)|`Single`, `Double`|  
|[双精度](../../../../visual-basic/language-reference/data-types/double-data-type.md)|`Double`|  
|任何枚举类型 ([枚举](../../../../visual-basic/language-reference/statements/enum-statement.md))|其基础的整型类型和可以扩大的基础类型的任何类型。|  
|[Char](../../../../visual-basic/language-reference/data-types/char-data-type.md)|`Char`, `String`|  
|`Char` 数组|`Char`数组中，`String`|  
|任何类型|[对象](../../../../visual-basic/language-reference/data-types/object-data-type.md)|  
|任何派生的类型|任何基的类型从其派生<sup>3</sup>。|  
|任何类型|它实现任何接口。|  
|[Nothing](../../../../visual-basic/language-reference/nothing.md)|任何数据类型或对象类型。|  
  
 <sup>1</sup>根据定义，每种数据类型加宽到本身。  
  
 <sup>2</sup>从转换`Integer`， `UInteger`， `Long`， `ULong`，或`Decimal`到`Single`或`Double`可能导致丢失精度，但永远不会导致丢失量级。 在这个意义上讲它们不会产生信息丢失。  
  
 <sup>3</sup>它可能看起来很奇怪从派生类型到它的基类型的转换扩大转换。 原因是派生的类型包含基类型的所有成员，因此它有资格作为基类型的实例。 以相反方向的基类型不包含由派生类型定义的任何新成员。  
  
 扩大转换始终在运行时失败，并且永远不会导致数据丢失。 始终可以隐式执行它们，无论[Option Strict 语句](../../../../visual-basic/language-reference/statements/option-strict-statement.md)设置类型检查切换到`On`或`Off`。  
  
## <a name="narrowing-conversions"></a>收缩转换  
 标准的收缩转换包括︰  
  
-   在前面的扩大转换的相反方向表 （只不过每个类型都扩大到自身）  
  
-   在任一方向之间的转换[布尔](../../../../visual-basic/language-reference/data-types/boolean-data-type.md)和任何数值类型  
  
-   从任何数字类型转换为任何枚举类型 (`Enum`)  
  
-   在任一方向之间的转换[字符串](../../../../visual-basic/language-reference/data-types/string-data-type.md)和任何数值类型`Boolean`，或[日期](../../../../visual-basic/language-reference/data-types/date-data-type.md)  
  
-   从数据类型或对象类型到派生自它的类型转换  
  
 收缩转换执行并非总是在运行时成功和可能失败或导致数据丢失。 如果目标数据类型不能接收要转换的值，就会出错。 例如，数值的转换导致溢出。 编译器不允许您可以隐式执行收缩转换，除非[Option Strict 语句](../../../../visual-basic/language-reference/statements/option-strict-statement.md)设置类型检查切换到`Off`。  
  
> [!NOTE]
>  收缩转换错误则会取消对转换中的元素从`For Each…Next`循环控制变量的集合。 有关详细信息和示例，请参阅中的"收缩转换"一节[为每个...下一条语句](../../../../visual-basic/language-reference/statements/for-each-next-statement.md)。  
  
### <a name="when-to-use-narrowing-conversions"></a>何时使用收缩转换  
 当您知道源值可以转换为目标的数据类型，而不会错误或数据丢失时，可使用收缩转换。 例如，如果您有`String`，您知道包含"True"False"，您可以使用`CBool`关键字来将其转换为`Boolean`。  
  
## <a name="exceptions-during-conversion"></a>转换期间的异常  
 由于扩大转换始终会成功，它们不会引发异常。 收缩转换，当它们失败时，通常会引发以下异常︰  
  
-   <xref:System.InvalidCastException>-如果未定义转换两个类型之间</xref:System.InvalidCastException>  
  
-   <xref:System.OverflowException>--（仅限整型） 如果转换后的值对于目标类型来说太大</xref:System.OverflowException>  
  
 如果某个类或结构定义[CType 函数](../../../../visual-basic/language-reference/functions/ctype-function.md)作为与该类或结构之间的来回转换运算符，`CType`可能会引发任何它认为适当的异常。 此外，该`CType`可能调用[!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)]函数或[!INCLUDE[dnprdnshort](../../../../csharp/getting-started/includes/dnprdnshort_md.md)]又可能引发多种异常的方法。  
  
## <a name="changes-during-reference-type-conversions"></a>引用类型转换过程中的更改  
 从转换*引用类型*只复制的指针的值。 值本身不复制也不以任何方式更改。 唯一可以更改是变量的存放指针的数据类型。 在下面的示例中，数据类型从派生类转换为它的基类，但两个变量现在指向的对象保持不变。  
  
```  
' Assume class cSquare inherits from class cShape.  
Dim shape As cShape  
Dim square As cSquare = New cSquare  
' The following statement performs a widening  
' conversion from a derived class to its base class.  
shape = square  
```  
  
## <a name="see-also"></a>另请参阅  
 [数据类型](../../../../visual-basic/programming-guide/language-features/data-types/index.md)   
 [在 Visual Basic 中的类型转换](../../../../visual-basic/programming-guide/language-features/data-types/type-conversions.md)   
 [隐式和显式转换](../../../../visual-basic/programming-guide/language-features/data-types/implicit-and-explicit-conversions.md)   
 [字符串和其他类型之间的转换](../../../../visual-basic/programming-guide/language-features/data-types/conversions-between-strings-and-other-types.md)   
 [如何︰ 将对象转换为另一种类型在 Visual Basic 中](../../../../visual-basic/programming-guide/language-features/data-types/how-to-convert-an-object-to-another-type.md)   
 [数组转换](../../../../visual-basic/programming-guide/language-features/data-types/array-conversions.md)   
 [数据类型](../../../../visual-basic/language-reference/data-types/data-type-summary.md)   
 [类型转换函数](../../../../visual-basic/language-reference/functions/type-conversion-functions.md)
