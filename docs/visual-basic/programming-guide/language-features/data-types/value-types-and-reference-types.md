---
title: "值类型和引用类型 |Microsoft 文档"
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
- reference data types
- reference types
- value types
- value data types
- types [Visual Basic]
- data types [Visual Basic], value types
- data types [Visual Basic], reference types
ms.assetid: fc82ce15-5a40-4c5c-a1e1-a556830e7391
caps.latest.revision: 14
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
ms.openlocfilehash: de8016b4b2a5550b32373a41c89a484fa996c596
ms.lasthandoff: 03/13/2017

---
# <a name="value-types-and-reference-types"></a>Value Types and Reference Types
在 Visual Basic 中，基于分类实现数据类型。 [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)]可以根据特定类型的变量存储其自己的数据或指向的数据的数据类型进行分类。 如果将存储其自己的数据则*值类型*; 如果它是的内存中其他位置的数据保留一个指针*引用类型*。  
  
## <a name="value-types"></a>值类型  
 数据类型是*值类型*是否包含在其自己的内存分配中的数据。 值类型包括︰  
  
-   所有数值数据类型  
  
-   `Boolean`、`Char` 和 `Date`  
  
-   所有结构，即使其成员是都引用类型  
  
-   枚举，因为它们的基础类型始终`SByte`， `Short`， `Integer`， `Long`， `Byte`， `UShort`， `UInteger`，或`ULong`  
  
 每个结构是值类型，即使它包含引用类型成员。 出于此原因，值类型，如`Char`和`Integer`由.NET Framework 结构实现。  
  
 您可以通过使用保留的关键字，例如，声明值类型`Decimal`。 您还可以使用`New`关键字来初始化值类型。 这是特别有用，如果该类型具有带参数的构造函数。 此示例是<xref:System.Decimal.%23ctor%28System.Int32%2CSystem.Int32%2CSystem.Int32%2CSystem.Boolean%2CSystem.Byte%29>构造函数，它将生成新`Decimal`值从提供的部分。</xref:System.Decimal.%23ctor%28System.Int32%2CSystem.Int32%2CSystem.Int32%2CSystem.Boolean%2CSystem.Byte%29>  
  
## <a name="reference-types"></a>引用类型  
 一个*引用类型*包含指向另一个保存的数据的内存位置的指针。 引用类型包括︰  
  
-   `String`  
  
-   所有数组，即使其元素是都值类型  
  
-   类类型如<xref:System.Windows.Forms.Form></xref:System.Windows.Forms.Form>  
  
-   委托  
  
 类是*引用类型*。 出于此原因，引用类型如`Object`和`String`支持[!INCLUDE[dnprdnshort](../../../../csharp/getting-started/includes/dnprdnshort_md.md)]类。 请注意每个数组是引用类型，即使其成员都是值类型。  
  
 由于每个引用类型表示基础.NET Framework 类时，必须使用[New 运算符](../../../../visual-basic/language-reference/operators/new-operator.md)关键字时将其初始化。 下面的语句初始化数组。  
  
```  
Dim totals() As Single = New Single(8) {}  
```  
  
## <a name="elements-that-are-not-types"></a>不是类型的元素  
 下面的编程元素不适合作为类型，因为您不能指定其中的任何已声明元素的数据类型︰  
  
-   命名空间  
  
-   模块  
  
-   事件  
  
-   属性和过程  
  
-   变量、 常量和字段  
  
## <a name="working-with-the-object-data-type"></a>使用对象数据类型  
 可以将引用类型还是值类型分配给的变量`Object`数据类型。 `Object`变量始终保留一个指向数据永远不会数据本身。 但是，如果将分配到的值类型`Object`变量时，其行为就像它包含其自己的数据。 有关详细信息，请参阅[Object 数据类型](../../../../visual-basic/language-reference/data-types/object-data-type.md)。  
  
 你可以查明是否`Object`变量作为引用类型或值类型将其传递给<xref:Microsoft.VisualBasic.Information.IsReference%2A>中的方法<xref:Microsoft.VisualBasic.Information>的类<xref:Microsoft.VisualBasic?displayProperty=fullName>命名空间。</xref:Microsoft.VisualBasic?displayProperty=fullName> </xref:Microsoft.VisualBasic.Information> </xref:Microsoft.VisualBasic.Information.IsReference%2A> <xref:Microsoft.VisualBasic.Information.IsReference%2A?displayProperty=fullName>返回`True`如果的内容`Object`变量表示引用类型。</xref:Microsoft.VisualBasic.Information.IsReference%2A?displayProperty=fullName>  
  
## <a name="see-also"></a>另请参阅  
 [可以为 null 的值类型](../../../../visual-basic/programming-guide/language-features/data-types/nullable-value-types.md)   
 [在 Visual Basic 中的类型转换](../../../../visual-basic/programming-guide/language-features/data-types/type-conversions.md)   
 [Structure 语句](../../../../visual-basic/language-reference/statements/structure-statement.md)   
 [有效使用数据类型](../../../../visual-basic/programming-guide/language-features/data-types/efficient-use-of-data-types.md)   
 [Object 数据类型](../../../../visual-basic/language-reference/data-types/object-data-type.md)   
 [数据类型](../../../../visual-basic/programming-guide/language-features/data-types/index.md)
