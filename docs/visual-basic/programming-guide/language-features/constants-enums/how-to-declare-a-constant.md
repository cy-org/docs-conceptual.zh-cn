---
title: "如何︰ 声明常量 (Visual Basic 中) |Microsoft 文档"
ms.custom: 
ms.date: 2015-07-20
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology:
- devlang-visual-basic
ms.topic: article
f1_keywords:
- vb.constant
dev_langs:
- VB
helpviewer_keywords:
- Integer data type, declaring constants
- Single data type, declaring constants
- Const statement [Visual Basic], declaring constants
- procedures, declaration
- data types [Visual Basic], constants
- Long data type, declaring constants
- Visual Basic code, declaring variables and constants
- Double data type, declaring constants
- Boolean data type, declaring constants
- modules, declaring constants
- Byte data type, declaring constants
- constants, declaring
- Date data type, declaring constants
- String data type, declaring constants
- declaring constants, const keyword
- Currency data type, declaring constants and variants
- module-level constants and variables
- Object data type, declaring constants
ms.assetid: f901b4fa-481f-4621-822e-427060577ad1
caps.latest.revision: 20
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
ms.openlocfilehash: 401d0feb85fccf94a25308d38c3c75198ef9294c
ms.contentlocale: zh-cn
ms.lasthandoff: 03/13/2017

---
# <a name="how-to-declare-a-constant-visual-basic"></a>如何：声明常量 (Visual Basic)
您使用`Const`语句声明一个常量，并将其值设置。 通过声明一个常量，您将有意义的名称分配给一个值。 一旦声明为一个常量，不能修改或分配一个新值。  
  
 声明是固定的过程中或在模块、 类或结构的声明部分。 类或结构级常量`Private`默认情况下，但也可能声明为`Public`， `Friend`， `Protected`，或`Protected Friend`为相应的代码访问级别。  
  
 常量必须具有有效的符号名称 （都具有相同规则与用于创建变量的名称） 和构成的数值或字符串常量及操作 （但不包括函数调用） 表达式。  
  
[!INCLUDE[note_settings_general](~/includes/note-settings-general-md.md)]  
  
### <a name="to-declare-a-constant"></a>若要声明常量  
  
-   编写一个包含访问说明符的声明`Const`关键字和一个表达式，如下面的示例中所示︰  
  
     [!code-vb[VbEnumsTask #&8;](../../../../visual-basic/language-reference/statements/codesnippet/VisualBasic/how-to-declare-a-constant_1.vb)]  
  
     当[Option Infer](../../../../visual-basic/language-reference/statements/option-infer-statement.md)是`Off`和[Option Strict](../../../../visual-basic/language-reference/statements/option-strict-statement.md)是`On`，您必须通过指定数据类型显式声明一个常量 (`Boolean`， `Byte`， `Char`， `DateTime`， `Decimal`， `Double`， `Integer`， `Long`， `Short`， `Single`，或`String`)。  
  
     当`Option Infer`是`On`或`Option Strict`是`Off`，您可以声明变量，而无需指定数据类型为`As`子句。 编译器确定的常量表达式的类型的类型。 有关详细信息，请参阅[常量和文本数据类型](constant-and-literal-data-types.md)。  
  
### <a name="to-declare-a-constant-that-has-an-explicitly-stated-data-type"></a>若要声明一个常量，它具有显式声明的数据类型  
  
-   编写一个包含的声明`As`关键字和显式数据类型，如下面的示例中所示︰  
  
     [!code-vb[VbEnumsTask #&9;](../../../../visual-basic/language-reference/statements/codesnippet/VisualBasic/how-to-declare-a-constant_2.vb)]  
  
     尽管您的代码的可读性更高，如果您声明单个常量每行，您可以在单独的行，声明多个常量。 如果您在单独的行声明多个常数，它们必须都具有相同的访问级别 (`Public`， `Private`， `Friend`， `Protected`，或`Protected Friend`)。  
  
### <a name="to-declare-multiple-constants-on-a-single-line"></a>若要在单独的行声明多个常数  
  
-   分隔声明用逗号和空格，如以下示例所示︰  
  
    ```  
    Public Const Four As Integer = 4, Five As Integer = 5, Six As Integer = 44  
    ```  
  
## <a name="see-also"></a>另请参阅  
 [Const 语句](../../../../visual-basic/language-reference/statements/const-statement.md)   
 [常量和 Literal 数据类型](constant-and-literal-data-types.md)   
 [常量概述](constants-overview.md)
 [如何︰ 声明常量](how-to-declare-a-constant.md)
 [用户定义的常量](user-defined-constants.md)
 [常量和 Literal 数据类型](constant-and-literal-data-types.md)
 [How to︰ 相关的常量值组合在一起](how-to-group-related-constant-values-together.md)
 [枚举概述](enumerations-overview.md)
 [如何︰ 声明枚举](how-to-declare-enumerations.md)
 [如何︰ 为枚举成员，请参阅](how-to-refer-to-an-enumeration-member.md)
 [枚举和名称限定](enumerations-and-name-qualification.md)
 [如何︰ 循环访问枚举](how-to-iterate-through-an-enumeration.md)
 [如何︰ 确定字符串枚举值相关联](how-to-determine-the-string-associated-with-an-enumeration-value.md)
 [何时使用枚举](when-to-use-an-enumeration.md)

 [枚举概述](enumerations-overview.md)   
 [常量概述](constants-overview.md)   
 [如何︰ 声明枚举](how-to-declare-enumerations.md)   
 [枚举和名称限定](enumerations-and-name-qualification.md)   
 [Option Strict 语句](../../../../visual-basic/language-reference/statements/option-strict-statement.md)   
 [常量和枚举](../../../../visual-basic/language-reference/constants-and-enumerations.md)

