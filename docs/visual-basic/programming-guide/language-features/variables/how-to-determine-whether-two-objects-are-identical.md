---
title: "如何︰ 确定两个对象是否相同 (Visual Basic) |Microsoft 文档"
ms.custom: 
ms.date: 2015-07-20
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology:
- devlang-visual-basic
ms.tgt_pltfrm: 
ms.topic: article
dev_langs:
- VB
helpviewer_keywords:
- testing, objects
- objects [Visual Basic], comparing
- object variables, determining identity
ms.assetid: 7829f817-0d1f-4749-a707-de0b95e0cf5c
caps.latest.revision: 19
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
ms.openlocfilehash: 3a853d9f958829eeb0fb42ecbcdae7ba912c89ed
ms.lasthandoff: 03/13/2017

---
# <a name="how-to-determine-whether-two-objects-are-identical-visual-basic"></a>如何：确定两个对象是否相同 (Visual Basic)
在[!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)]，两个变量的引用将被视为相同的指针是相同的也就是说，如果这两个变量指向内存中的同一个类实例。 例如，在 Windows 窗体应用程序中，可能想要进行比较以确定是否当前实例 (`Me`) 等同于一个特定实例，如`Form2`。  
  
 [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)]提供了两个运算符比较指针。 [Is 运算符](../../../../visual-basic/language-reference/operators/is-operator.md)返回`True`如果对象相同的与[IsNot 运算符](../../../../visual-basic/language-reference/operators/isnot-operator.md)返回`True`如果它们不是。  
  
## <a name="determining-if-two-objects-are-identical"></a>确定两个对象是否相同  
  
#### <a name="to-determine-if-two-objects-are-identical"></a>若要确定两个对象是否相同  
  
1.  设置`Boolean`表达式来测试两个对象。  
  
2.  测试表达式中，在使用`Is`两个对象作为操作数的运算符。  
  
     `Is`返回`True`如果指向同一个类实例的对象。  
  
## <a name="determining-if-two-objects-are-not-identical"></a>确定两个对象是否不相同  
 有时您想要执行的操作，如果两个对象不完全相同，并且可以适于组合`Not`和`Is`，例如`If Not obj1 Is obj2`。 在这种情况下可以使用`IsNot`运算符。  
  
#### <a name="to-determine-if-two-objects-are-not-identical"></a>若要确定两个对象是否不相同  
  
1.  设置`Boolean`表达式来测试两个对象。  
  
2.  测试表达式中，在使用`IsNot`两个对象作为操作数的运算符。  
  
     `IsNot`返回`True`如果对象未指向同一类实例。  
  
## <a name="example"></a>示例  
 下面的示例测试对`Object`变量上以查看是否指向同一个类实例。  
  
 [!code-vb[VbVbalrKeywords #&14;](../../../../visual-basic/language-reference/codesnippet/VisualBasic/how-to-determine-whether-two-objects-are-identical_1.vb)]  
  
 前面的示例显示以下输出。  
  
 `objA different from objB? True`  
  
 `objA identical to objC? True`  
  
## <a name="see-also"></a>另请参阅  
 [Object 数据类型](../../../../visual-basic/language-reference/data-types/object-data-type.md)   
 [对象变量](../../../../visual-basic/programming-guide/language-features/variables/object-variables.md)   
 [对象变量值](../../../../visual-basic/programming-guide/language-features/variables/object-variable-values.md)   
 [Is 运算符](../../../../visual-basic/language-reference/operators/is-operator.md)   
 [IsNot 运算符](../../../../visual-basic/language-reference/operators/isnot-operator.md)   
 [如何︰ 确定两个对象是否相关](../../../../visual-basic/programming-guide/language-features/variables/how-to-determine-whether-two-objects-are-related.md)   
 [Me、My、MyBase 和 MyClass](../../../../visual-basic/programming-guide/program-structure/me-my-mybase-and-myclass.md)
