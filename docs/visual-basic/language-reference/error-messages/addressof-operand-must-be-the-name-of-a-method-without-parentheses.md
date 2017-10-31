---
title: "AddressOf 操作数必须是 （不带括号） 方法的名称 |Microsoft 文档"
ms.date: 2015-07-20
ms.prod: .net
ms.suite: 
ms.technology:
- devlang-visual-basic
ms.topic: article
f1_keywords:
- vbc30577
- bc30577
dev_langs:
- VB
helpviewer_keywords:
- BC30577
ms.assetid: c2c55640-5c61-4e66-97a4-4322020c6001
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
ms.openlocfilehash: 04103fe23ee55bb751d9604ef74614edeead8886
ms.lasthandoff: 03/13/2017

---
# <a name="39addressof39-operand-must-be-the-name-of-a-method-without-parentheses"></a>AddressOf 操作数必须是 （不带括号） 方法的名称
`AddressOf` 运算符创建引用特定过程的过程委托实例。 语法是，如下所示。  
  
 `AddressOf` `procedurename`  
  
 插入后面的参数两边的括号`AddressOf`，这里不需要。  
  
 **错误 ID:** BC30577  
  
## <a name="to-correct-this-error"></a>更正此错误  
  
1.  删除后面的参数两边的括号`AddressOf`。  
  
2.  请确保该参数的方法名称。  
  
## <a name="see-also"></a>另请参阅  
 [AddressOf 运算符](../../../visual-basic/language-reference/operators/addressof-operator.md)   
 [委托](../../../visual-basic/programming-guide/language-features/delegates/index.md)
