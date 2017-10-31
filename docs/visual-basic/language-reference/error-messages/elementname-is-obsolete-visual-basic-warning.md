---
title: "&lt;elementname&gt;是已过时 （Visual Basic 警告） |Microsoft 文档"
ms.date: 2015-07-20
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology:
- devlang-visual-basic
ms.topic: article
f1_keywords:
- vbc40008
- bc40008
dev_langs:
- VB
helpviewer_keywords:
- BC40008
ms.assetid: 729e3eb5-76ac-4c55-9fdd-78350e0de55e
caps.latest.revision: 12
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
ms.openlocfilehash: ccec3b2659502c84dd4db9c9c4d796362958030b
ms.lasthandoff: 03/13/2017

---
# <a name="39ltelementnamegt39-is-obsolete-visual-basic-warning"></a>&lt;elementname&gt;是已过时 （Visual Basic 警告）
语句试图访问的编程元素，它已标记有<xref:System.ObsoleteAttribute>特性，指令会将其视为一条警告。</xref:System.ObsoleteAttribute>  
  
 您可以将标记为不再使用通过将应用<xref:System.ObsoleteAttribute>于它。</xref:System.ObsoleteAttribute>所有编程元素 如果执行此操作，则可以设置该属性的<xref:System.ObsoleteAttribute.IsError%2A>属性设置为任何一个`True`或`False`。</xref:System.ObsoleteAttribute.IsError%2A> 如果设置为 `True`，则编译器将尝试使用该元素的操作视为错误。 如果设置为 `False`，或将其默认为 `False`，则编译器会在有操作尝试使用该元素时发出警告。  
  
 默认情况下，此消息是一个警告，因为<xref:System.ObsoleteAttribute.IsError%2A>属性<xref:System.ObsoleteAttribute>是`False`。</xref:System.ObsoleteAttribute> </xref:System.ObsoleteAttribute.IsError%2A> 有关隐藏警告或将警告视为错误的详细信息，请参阅[在 Visual Basic 中配置警告](https://docs.microsoft.com/visualstudio/ide/configuring-warnings-in-visual-basic)。  
  
 **错误 ID:** BC40008  
  
## <a name="to-correct-this-error"></a>更正此错误  
  
-   确保源代码引用的元素名称拼写正确。  
  
## <a name="see-also"></a>另请参阅  
 [属性概述](../../../visual-basic/programming-guide/concepts/attributes/index.md)

