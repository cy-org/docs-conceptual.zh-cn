---
title: "&lt;typename&gt;是委托类型 |Microsoft 文档"
ms.date: 2015-07-20
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology:
- devlang-visual-basic
ms.topic: article
f1_keywords:
- bc32008
- vbc32008
dev_langs:
- VB
helpviewer_keywords:
- BC32008
ms.assetid: dc6abba0-a9ad-450f-8899-87265bc84abc
caps.latest.revision: 11
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
ms.openlocfilehash: 3d6cc283f7e9815eb9b723a450731998f14b3424
ms.lasthandoff: 03/13/2017

---
# <a name="39lttypenamegt39-is-a-delegate-type"></a>&lt;typename&gt;是委托类型
\<typename&1;> 是委托类型。 委托构造允许只能将单个 AddressOf 表达式作为参数列表。 通常 AddressOf 表达式可用来代替委托构造。  
  
 一个`New`子句创建委托类的实例为提供了无效的参数列表的委托构造函数。  
  
 您可以提供只有一个`AddressOf`表达式时创建新的委托实例。  
  
 如果您不传递任何参数给委托构造函数，如果传递的多个参数，或者如果传递单个参数，不是有效，则可能发生此错误`AddressOf`表达式。  
  
 **错误 ID:** BC32008  
  
## <a name="to-correct-this-error"></a>更正此错误  
  
-   使用单个`AddressOf`参数列表中的代理类中的表达式`New`子句。  
  
## <a name="see-also"></a>另请参阅  
 [New 运算符](../../../visual-basic/language-reference/operators/new-operator.md)   
 [AddressOf 运算符](../../../visual-basic/language-reference/operators/addressof-operator.md)   
 [委托](../../../visual-basic/programming-guide/language-features/delegates/index.md)   
 [如何：调用委托方法](../../../visual-basic/programming-guide/language-features/delegates/how-to-invoke-a-delegate-method.md)
