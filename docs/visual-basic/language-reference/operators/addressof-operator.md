---
title: "AddressOf 运算符 (Visual Basic 中) |Microsoft 文档"
ms.date: 2015-07-20
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology:
- devlang-visual-basic
ms.topic: article
f1_keywords:
- AddressOf
- vb.AddressOf
dev_langs:
- VB
helpviewer_keywords:
- AddressOf operator
- addresses, passing to API procedures
ms.assetid: 8105a59d-60d8-4ab5-b221-5899cdfacbf4
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
ms.translationtype: Machine Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: 04a7c5be9b890faea561c28715093a271cf9eaa8
ms.contentlocale: zh-cn
ms.lasthandoff: 03/13/2017

---
# <a name="addressof-operator-visual-basic"></a>AddressOf 运算符 (Visual Basic)
创建引用的特定过程的过程委托实例。  
  
## <a name="syntax"></a>语法  
  
```  
AddressOf procedurename  
```  
  
## <a name="parts"></a>部件  
 `procedurename`  
 必需。 指定由新创建的过程委托引用的过程。  
  
## <a name="remarks"></a>备注  
 `AddressOf`运算符创建一个指向由指定的函数的函数委托`procedurename`。 当指定的过程是实例方法则此函数委托引用实例和方法。 然后，调用的函数委托时调用的指定实例的指定的方法。  
  
 `AddressOf`运算符可以用作委托构造函数的操作数，或者可在其中可以由编译器确定的委托类型的上下文中。  
  
## <a name="example"></a>示例  
 此示例使用`AddressOf`运算符来指定一个委托来处理`Click`按钮事件。  
  
 [!code-vb[VbVbalrDelegates #&8;](../../../visual-basic/language-reference/operators/codesnippet/VisualBasic/addressof-operator_1.vb)]  
  
## <a name="example"></a>示例  
 下面的示例使用`AddressOf`运算符来指定线程的启动函数。  
  
 [!code-vb[VbVbalrDelegates #&9;](../../../visual-basic/language-reference/operators/codesnippet/VisualBasic/addressof-operator_2.vb)]  
  
## <a name="see-also"></a>另请参阅  
 [Declare 语句](../../../visual-basic/language-reference/statements/declare-statement.md)   
 [Function 语句](../../../visual-basic/language-reference/statements/function-statement.md)   
 [Sub 语句](../../../visual-basic/language-reference/statements/sub-statement.md)   
 [委托](../../../visual-basic/programming-guide/language-features/delegates/index.md)

