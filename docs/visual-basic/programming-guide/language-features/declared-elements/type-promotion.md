---
title: "类型提升 (Visual Basic 中) |Microsoft 文档"
ms.custom: 
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
- declared elements, scope
- visibility, declared elements
- Partial keyword, unexpected results with type promotion
- scope, declared elements
- scope, Visual Basic
- type promotion
- declared elements, visibility
ms.assetid: 035eeb15-e4c5-4288-ab3c-6bd5d22f7051
caps.latest.revision: 17
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
ms.openlocfilehash: d732e765fc28eaedc0deab477dbf9955a40e97c9
ms.lasthandoff: 03/13/2017

---
# <a name="type-promotion-visual-basic"></a>类型提升 (Visual Basic)
当您声明一个模块中的编程元素时[!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)]将提升其作用域限制为包含该模块的命名空间。 这称为*类型提升*。  
  
 下面的示例演示一个模块的主干定义和该模块的两个成员。  
  
 [!code-vb[VbVbalrDeclaredElements #&1;](../../../../visual-basic/programming-guide/language-features/declared-elements/codesnippet/VisualBasic/type-promotion_1.vb)]  
  
 在`projModule`、 编程在模块级别声明的元素将被提升到`projNamespace`。 在前面的示例中，`basicEnum`和`innerClass`进行升级，但`numberSub`无效，因为它不在模块级别声明。  
  
## <a name="effect-of-type-promotion"></a>类型提升的结果  
 类型提升的结果是一个限定字符串不需要包括该模块名称。 下面的示例调用两个过程在前面的示例。  
  
 [!code-vb[VbVbalrDeclaredElements #&2;](../../../../visual-basic/programming-guide/language-features/declared-elements/codesnippet/VisualBasic/type-promotion_2.vb)]  
  
 在前面的示例中，第一次调用使用完全限定字符串。 但是，这是不必要由于类型提升。 第二个调用也访问该模块的成员而不包括`projModule`限定字符串中。  
  
## <a name="defeat-of-type-promotion"></a>类型提升的失效  
 如果命名空间已具有相同的名称作为模块成员的成员，类型提升则会对该模块成员失效。 下面的示例演示了框架的枚举和同一命名空间中的模块定义。  
  
 [!code-vb[VbVbalrDeclaredElements #&3;](../../../../visual-basic/programming-guide/language-features/declared-elements/codesnippet/VisualBasic/type-promotion_3.vb)]  
  
 在前面的示例中，[!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)]无法提升类`abc`到`thisNameSpace`原因是已经存在具有相同的名称在命名空间级别的枚举。 访问`abcSub`，必须使用完全限定字符串`thisNamespace.thisModule.abc.abcSub`。 但是，类`xyz`仍会提升，并且可以访问`xyzSub`较短的限定字符串`thisNamespace.xyz.xyzSub`。  
  
### <a name="defeat-of-type-promotion-for-partial-types"></a>分部类型的类型提升的失效  
 如果某个类或模块内的结构使用[部分](../../../../visual-basic/language-reference/modifiers/partial.md)关键字，类型提升自动失效该类或结构中，无论是命名空间包含具有相同名称的成员。 该模块中的其他元素都仍可进行类型提升。  
  
 **后果。** 部分定义的类型提升的失效可能导致意外的结果和甚至编译器错误。 下面的示例演示一个类，其中之一是模块内的主干分部定义。  
  
 [!code-vb[VbVbalrDeclaredElements #&4;](../../../../visual-basic/programming-guide/language-features/declared-elements/codesnippet/VisualBasic/type-promotion_4.vb)]  
  
 在前面的示例中，开发人员可能期望编译器要合并的两个部分定义`sampleClass`。 但是，编译器不会考虑的促销内分部定义`sampleModule`。 结果是，它尝试编译两个独立但截然不同的类，名为`sampleClass`但具有不同限定路径。  
  
 仅当其完全限定的路径相同时，编译器才将合并分部定义。  
  
## <a name="recommendations"></a>建议  
 下面的建议提供良好编程习惯。  
  
-   **唯一的名称。** 如果必须对编程元素的命名的完全控制，并总是最好是不同的场合使用唯一的名称。 相同的名称需要额外的限定，并且会导致代码更难读懂。 它们也可能会带来细微错误和意外的结果。  
  
-   **完全限定。** 当您正在使用模块和相同的命名空间中的其他元素时，最安全的方法是始终使用完全限定的所有编程元素。 如果使某个模块成员的类型提升无效，并且不完全限定该成员，您可能无意中访问不同的编程元素。  
  
## <a name="see-also"></a>另请参阅  
 [Module 语句](../../../../visual-basic/language-reference/statements/module-statement.md)   
 [Namespace 语句](../../../../visual-basic/language-reference/statements/namespace-statement.md)   
 [部分](../../../../visual-basic/language-reference/modifiers/partial.md)   
 [在 Visual Basic 中的作用域](../../../../visual-basic/programming-guide/language-features/declared-elements/scope.md)   
 [如何︰ 控制变量的作用域](../../../../visual-basic/programming-guide/language-features/declared-elements/how-to-control-the-scope-of-a-variable.md)   
 [对已声明元素的引用](../../../../visual-basic/programming-guide/language-features/declared-elements/references-to-declared-elements.md)
