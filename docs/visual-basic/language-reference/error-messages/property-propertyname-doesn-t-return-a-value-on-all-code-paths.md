---
title: "属性 &quot;&lt;propertyname&gt;并非在所有代码路径上都返回值 |Microsoft 文档"
ms.date: 2015-07-20
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology:
- devlang-visual-basic
ms.topic: article
f1_keywords:
- bc42107
- vbc42107
dev_langs:
- VB
helpviewer_keywords:
- BC42107
ms.assetid: 06800966-9c3b-4844-9f13-83ac95607d32
caps.latest.revision: 7
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
ms.openlocfilehash: e7c94d827761ad26d517b44a06734c5db4480a62
ms.lasthandoff: 03/13/2017

---
# <a name="property-39ltpropertynamegt39-doesn39t-return-a-value-on-all-code-paths"></a>属性 '&lt;propertyname&gt;并非在所有代码路径上都返回值
属性 '\<propertyname&1;> 并非在所有代码路径上都返回值。 使用该结果时，可能会在运行时发生 null 引用异常。  
  
 一个属性`Get`过程具有至少一个可能不返回值的代码路径。  
  
 可以从属性中返回值`Get`处于以下任一过程︰  
  
-   将值分配给属性名称，然后执行`Exit Property`语句。  
  
-   将值分配给属性名称，然后执行`End Get`语句。  
  
-   中包括值[Return 语句](../../../visual-basic/language-reference/statements/return-statement.md)。  
  
 控制权将传递给`Exit Property`或`End Get`和您没有分配任何值的属性名称，`Get`过程返回的属性的数据类型的默认值。 详细信息，请参阅"行为"中[Function 语句](../../../visual-basic/language-reference/statements/function-statement.md)。  
  
 默认情况下，此消息是一个警告。 有关隐藏警告或将警告视为错误的详细信息，请参阅[在 Visual Basic 中配置警告](https://docs.microsoft.com/visualstudio/ide/configuring-warnings-in-visual-basic)。  
  
 **错误 ID:** BC42107  
  
## <a name="to-correct-this-error"></a>更正此错误  
  
-   控制流逻辑检查并确保导致返回每个语句之前赋值。  
  
     很容易地保证每一次返回从过程返回一个值，如果始终使用`Return`语句。 如果这样做时之前, 的最后一个语句`End Get`应`Return`语句。  
  
## <a name="see-also"></a>另请参阅  
 [属性过程](../../../visual-basic/programming-guide/language-features/procedures/property-procedures.md)   
 [Property 语句](../../../visual-basic/language-reference/statements/property-statement.md)   
 [Get 语句](../../../visual-basic/language-reference/statements/get-statement.md)
