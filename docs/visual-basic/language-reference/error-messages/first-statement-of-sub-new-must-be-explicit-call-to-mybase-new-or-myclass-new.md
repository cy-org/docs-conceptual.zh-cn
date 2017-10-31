---
title: "此 Sub New 的第一条语句必须是对 MyBase.New 或 MyClass.New 的显式调用，因为&lt;constructorname&gt;in 基类&lt;baseclassname&gt;of&lt;derivedclassname&gt;标记为已过时:&lt;errormessage&gt;&quot; |Microsoft 文档"
ms.date: 2015-07-20
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology:
- devlang-visual-basic
ms.topic: article
f1_keywords:
- vbc30920
- bc30920
dev_langs:
- VB
helpviewer_keywords:
- BC30920
ms.assetid: e47dc755-4294-4368-b813-2177b7677957
caps.latest.revision: 10
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
ms.openlocfilehash: feb04d426b7e050b7ad05cdfd4d481172dda3a49
ms.lasthandoff: 03/13/2017

---
# <a name="first-statement-of-this-39sub-new39-must-be-an-explicit-call-to-39mybasenew39-or-39myclassnew39-because-the-39ltconstructornamegt39-in-the-base-class-39ltbaseclassnamegt39-of-39ltderivedclassnamegt39-is-marked-obsolete-39lterrormessagegt39"></a>此 Sub New 的第一条语句必须是对 MyBase.New 或 MyClass.New 的显式调用，因为&lt;constructorname&gt;in 基类&lt;baseclassname&gt;of&lt;derivedclassname&gt;标记为已过时:&lt;errormessage&gt;
类构造函数不显式调用基类构造函数，并且隐式基类构造函数标有<xref:System.ObsoleteAttribute>特性，指令会将其视为错误。</xref:System.ObsoleteAttribute>  
  
 在派生的类构造函数未调用基类构造函数，[!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)]尝试生成隐式调用无参数的基类构造函数。 如果没有可访问的构造函数可以调用不带参数，基类中[!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)]无法生成的隐式调用。 在这种情况下，需要的构造函数标有<xref:System.ObsoleteAttribute>属性，因此[!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)]不能调用它。</xref:System.ObsoleteAttribute>  
  
 您可以将标记为不再使用通过将应用<xref:System.ObsoleteAttribute>于它。</xref:System.ObsoleteAttribute>所有编程元素 如果执行此操作，则可以设置该属性的<xref:System.ObsoleteAttribute.IsError%2A>属性设置为任何一个`True`或`False`。</xref:System.ObsoleteAttribute.IsError%2A> 如果设置为 `True`，则编译器将尝试使用该元素的操作视为错误。 如果设置为 `False`，或将其默认为 `False`，则编译器会在有操作尝试使用该元素时发出警告。  
  
 **错误 ID:** BC30920  
  
## <a name="to-correct-this-error"></a>更正此错误  
  
1.  检查引用的错误信息并采取相应的操作。  
  
2.  将对 `MyBase.New()` 或 `MyClass.New()` 的调用包括为派生类中 `Sub New` 的第一个语句。  
  
## <a name="see-also"></a>另请参阅  
 [属性概述](../../../visual-basic/programming-guide/concepts/attributes/index.md)
 
