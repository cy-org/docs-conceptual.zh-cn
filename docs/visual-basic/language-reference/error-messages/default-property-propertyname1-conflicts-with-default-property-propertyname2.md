---
title: "默认属性&lt;propertyname1&gt;与默认属性冲突&lt;propertyname2&gt;in&lt;classname&gt;，因此应声明为 Shadows |Microsoft 文档"
ms.date: 2015-07-20
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology:
- devlang-visual-basic
ms.topic: article
f1_keywords:
- vbc40007
- bc40007
dev_langs:
- VB
helpviewer_keywords:
- BC40007
ms.assetid: 692ccf76-5715-4f11-a972-84cf9de30bc1
caps.latest.revision: 9
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
ms.openlocfilehash: 803b42b7659c16fd97251635e4b6ba49362e0a02
ms.lasthandoff: 03/13/2017

---
# <a name="default-property-39ltpropertyname1gt39-conflicts-with-default-property-39ltpropertyname2gt39-in-39ltclassnamegt39-and-so-should-be-declared-39shadows39"></a>默认属性&lt;propertyname1&gt;与默认属性冲突&lt;propertyname2&gt;in&lt;classname&gt;，因此应声明为 Shadows
使用与基类中定义的属性相同的名称所声明的属性。 在这种情况下，此类中的属性应隐藏基类属性。  
  
 此消息是一个警告。 `Shadows`默认情况下，则假定。 有关隐藏警告或将警告视为错误的详细信息，请参阅[在 Visual Basic 中配置警告](https://docs.microsoft.com/visualstudio/ide/configuring-warnings-in-visual-basic)。  
  
 **错误 ID:** BC40007  
  
## <a name="to-correct-this-error"></a>更正此错误  
  
-   添加`Shadows`关键字来声明中或更改所声明的属性名称。  
  
## <a name="see-also"></a>另请参阅  
 [阴影](../../../visual-basic/language-reference/modifiers/shadows.md)   
 [Visual Basic 中的隐藏](../../../visual-basic/programming-guide/language-features/declared-elements/shadowing.md)
