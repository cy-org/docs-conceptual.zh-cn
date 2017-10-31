---
title: "属性列表 (Visual Basic 中) |Microsoft 文档"
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
- attribute list
- attributes [Visual Basic], applying
ms.assetid: 5880073a-68a4-4b6b-8a07-ace32959a4e2
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
ms.openlocfilehash: e360794ad217784e2358967bfbcc03959cd043b1
ms.contentlocale: zh-cn
ms.lasthandoff: 03/13/2017

---
# <a name="attribute-list-visual-basic"></a>特性列表 (Visual Basic)
指定要应用于声明的编程元素的属性。 用逗号分隔多个属性。 下面是一个属性的语法。  
  
## <a name="syntax"></a>语法  
  
```  
[ attributemodifier ] attributename [ ( attributearguments | attributeinitializer ) ]  
```  
  
## <a name="parts"></a>部件  
 `attributemodifier`  
 所需的应用的源代码文件开头的属性。 可以是[程序集](../../../visual-basic/language-reference/modifiers/assembly.md)或[模块](../../../visual-basic/language-reference/modifiers/module-keyword.md)。  
  
 `attributename`  
 必需。 属性名称。  
  
 `attributearguments`  
 可选。 此属性的位置参数的列表。 用逗号分隔多个参数。  
  
 `attributeinitializer`  
 可选。 此属性的变量或属性初始值设定项的列表。 用逗号分隔多个初始值设定项。  
  
## <a name="remarks"></a>备注  
 可以将一个或多个特性应用于几乎所有编程元素 （类型、 过程、 属性和等）。 属性出现在程序集的元数据，并且它们可以帮助您为您的代码添加批注或指定如何使用特定的编程元素。 您可以应用属性定义的 Visual Basic 和.NET Framework 中，并且可以定义您自己的属性。  

 有关何时使用属性的详细信息，请参阅[属性概述](../../../visual-basic/programming-guide/concepts/attributes/index.md)。 属性名称的信息，请参阅[声明元素名称](../../../visual-basic/programming-guide/language-features/declared-elements/declared-element-names.md)。  
  
## <a name="rules"></a>规则  
  
-   **处的位置。** 可以将特性应用于大多数已声明的编程元素。 若要将应用一个或多个属性，将放*特性块*元素声明的开头。 每个条目的属性列表中指定您要将应用的属性、 修饰符和参数将用于调用该属性。  
  
-   **尖括号。** 如果您提供的属性列表，则必须将其括在尖括号中 ("`<`"和"`>`")。  
  
-   **声明的一部分。** 该属性必须是元素声明，而不是单独语句的一部分。 您可以使用行继续符序列 (" `_`") 来扩展到多个源代码行上的声明语句。  
  
-   **修饰符。** 属性修饰符 (`Assembly`或`Module`) 需要在每个特性应用于源代码文件开头的编程元素上。 应用于不源文件中的开始处的元素特性不允许使用属性修饰符。  
  
-   **参数。** 属性的所有位置参数必须优先任何变量或属性初始值设定项。  
  
## <a name="example"></a>示例  
 下面的示例应用<xref:System.Runtime.InteropServices.DllImportAttribute>属性的主干定义为`Function`过程。</xref:System.Runtime.InteropServices.DllImportAttribute>  
  
 [!code-vb[VbVbalrStatements #&1;](../../../visual-basic/language-reference/error-messages/codesnippet/VisualBasic/attribute-list_1.vb)]  
  
 <xref:System.Runtime.InteropServices.DllImportAttribute>指示特性化的过程表示非托管动态链接库 (DLL) 中的入口点。</xref:System.Runtime.InteropServices.DllImportAttribute> 该属性提供了位置参数作为 DLL 的名称和作为变量的初始值设定项的其他信息。  
  
## <a name="see-also"></a>请参见  
 [程序集](../../../visual-basic/language-reference/modifiers/assembly.md)   
 [模块\<关键字&1;>](../../../visual-basic/language-reference/modifiers/module-keyword.md)   
 [属性概述](../../../visual-basic/programming-guide/concepts/attributes/index.md)   
 [如何：在代码中拆分和合并语句](../../../visual-basic/programming-guide/program-structure/how-to-break-and-combine-statements-in-code.md)

