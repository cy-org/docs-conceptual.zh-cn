---
title: "程序集 (Visual Basic 中) |Microsoft 文档"
ms.date: 2015-07-20
ms.prod: .net
ms.suite: 
ms.technology:
- devlang-visual-basic
ms.topic: article
f1_keywords:
- vb.Assembly
- vb.AssemblyAttribute
- Assembly
dev_langs:
- VB
helpviewer_keywords:
- Assembly modifier
- Assembly keyword
- attribute blocks, Assembly keyword
ms.assetid: 925e7471-3bdf-4b51-bb93-cbcfc6efc52f
caps.latest.revision: 15
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
ms.openlocfilehash: b496b96360ff891554ab71ba2b3227b2dabbc416
ms.lasthandoff: 03/13/2017

---
# <a name="assembly-visual-basic"></a>程序集 (Visual Basic)
指定源文件开头特性应用于整个程序集。  
  
## <a name="remarks"></a>备注  
 很多特性适用于单个的编程元素，例如一个类或属性。 通过将附加特性块，在尖括号中的应用此类属性 (`< >`)，直接到声明语句。  
  
 如果属性不仅到下面的元素，而且整个程序集，源文件开头插入分特性块和标识与该特性`Assembly`关键字。 如果它适用于当前程序集模块，则使用[模块](../../../visual-basic/language-reference/modifiers/module-keyword.md)关键字。  
  
 您还可以将属性为程序集在 AssemblyInfo.vb 文件中，在这种情况下不需要使用主源代码文件中的属性块。  
  
## <a name="see-also"></a>另请参阅  
 [模块\<关键字&1;>](../../../visual-basic/language-reference/modifiers/module-keyword.md)   
 [属性概述](../../../visual-basic/programming-guide/concepts/attributes/index.md)


