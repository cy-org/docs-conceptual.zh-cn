---
title: "在 Visual Basic 中的变量声明 |Microsoft 文档"
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
- variables [Visual Basic], declaring
- member variables, declarations
- Dim statement, variable declaration
- declaring variables
- variables [Visual Basic], scope
- variables [Visual Basic], data types
- data types [Visual Basic], variable declarations
- lifetime, variables
- variables [Visual Basic], lifetime
- access levels, variables
- scope, declaration statements
- variables [Visual Basic], access level
- local variables, declarations
- scope, variables
ms.assetid: d8f10226-92b1-480f-9f53-df377b2d7e15
caps.latest.revision: 31
author: dotnet-bot
ms.author: dotnetcontent
translation.priority.ht:
- de-de
- es-es
- fr-fr
- it-it
- ja-jp
- ko-kr
- ru-ru
- zh-cn
- zh-tw
translation.priority.mt:
- cs-cz
- pl-pl
- pt-br
- tr-tr
translationtype: Machine Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: 8cabb2d319288653c80099c816e46e822429d6ec
ms.lasthandoff: 03/13/2017

---
# <a name="variable-declaration-in-visual-basic"></a>Visual Basic 中的变量声明
声明一个变量来指定其名称和特性。 变量的声明语句是[Dim 语句](../../../../visual-basic/language-reference/statements/dim-statement.md)。 其位置和内容确定变量的特征。  
  
 有关变量的命名规则和注意事项，请参阅[声明元素名称](../../../../visual-basic/programming-guide/language-features/declared-elements/declared-element-names.md)。  
  
## <a name="declaration-levels"></a>声明级别  
  
### <a name="local-and-member-variables"></a>本地和成员变量  
 一个*局部变量*是指在过程内声明。 一个*成员变量*属于[!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)]类型; 它在模块级别，在类、 结构或模块，但不是能在内部的类、 结构或模块的任何过程声明。  
  
### <a name="shared-and-instance-variables"></a>共享变量和实例变量  
 在类或结构中，成员变量的类别取决于共享它。 如果使用声明[共享](../../../../visual-basic/language-reference/modifiers/shared.md)关键字，它是*共享的变量*，并且它存在于类或结构的所有实例都共享的单个副本中。  
  
 否则，很*实例变量*，并为类或结构的每个实例创建的单独副本。 给定的实例变量副本是仅对类或结构在其中创建的实例可用。 它不依赖于类或结构的任何其他实例中实例变量的副本。  
  
## <a name="declaring-data-type"></a>将数据类型声明  
 [作为](../../../../visual-basic/language-reference/statements/as-clause.md)声明语句中的子句可用于定义数据类型或所声明的变量的对象类型。 你可以指定任何以下类型的变量︰  
  
-   基本数据类型，如`Boolean`， `Long`，或`Decimal`  
  
-   复合数据类型，如数组或结构  
  
-   对象类型或在您的应用程序或其他应用程序中定义的类  
  
-   一个[!INCLUDE[dnprdnshort](../../../../csharp/getting-started/includes/dnprdnshort_md.md)]类，如<xref:System.Windows.Forms.Label>或<xref:System.Windows.Forms.TextBox></xref:System.Windows.Forms.TextBox></xref:System.Windows.Forms.Label>  
  
-   接口类型，如<xref:System.IComparable>或<xref:System.IDisposable></xref:System.IDisposable></xref:System.IComparable>  
  
 您可以声明在一个语句中的几个变量，而无需重复的数据类型。 在下面的语句中，变量`i`， `j`，和`k`都声明为类型`Integer`，`l`和`m`作为`Long`，和`x`和`y`作为`Single`:  
  
```  
Dim i, j, k As Integer  
' All three variables in the preceding statement are declared as Integer.  
Dim l, m As Long, x, y As Single  
' In the preceding statement, l and m are Long, x and y are Single.  
```  
  
 数据类型的详细信息，请参阅[数据类型](../../../../visual-basic/programming-guide/language-features/data-types/index.md)。 对象的详细信息，请参阅[对象和类](../../../../visual-basic/programming-guide/language-features/objects-and-classes/index.md)和[使用组件编程](http://msdn.microsoft.com/library/d4d4fcb4-e0b8-46b3-b679-7ee0026eb9e3)。  
  
## <a name="local-type-inference"></a>局部类型推理  
 *类型推理*用来确定未声明的局部变量的数据类型`As`子句。 编译器推断出类型的变量的初始化表达式的类型。 这使您无需显式声明一个类型声明变量。 在下面的示例中，同时`num1`和`num2`强类型化为整数。  
  
 [!code-vb[VbVbalrTypeInference #&1;](../../../../visual-basic/language-reference/statements/codesnippet/VisualBasic/variable-declaration_1.vb)]  
  
 如果你想要使用局部类型推理`Option Infer`必须设置为`On`。 有关详细信息，请参阅[本地类型推理](../../../../visual-basic/programming-guide/language-features/variables/local-type-inference.md)和[Option Infer 语句](../../../../visual-basic/language-reference/statements/option-infer-statement.md)。  
  
## <a name="characteristics-of-declared-variables"></a>已声明的变量的特征  
 *生存期*的变量是一段时间期间它是可供使用。 一般情况下，变量存在，只要继续存在 （如过程或类） 中声明的元素。 如果该变量并不需要它的包含元素的生存期过后继续存在，您不需要执行任何特殊的声明中。 如果变量需要继续存在时间超过其包含元素，则可以包括`Static`或`Shared`关键字在其`Dim`语句。 有关详细信息，请参阅[Visual Basic 中的生存期](../../../../visual-basic/programming-guide/language-features/declared-elements/lifetime.md)。  
  
 *范围*的变量是一组的所有代码都可以引用它，而不用限定其名称。 声明位置取决于该变量的作用域。 位于某个给定区域中的代码可以使用而不必限定它们的名称在该区域中定义的变量。 有关详细信息，请参阅[在 Visual Basic 中的作用域](../../../../visual-basic/programming-guide/language-features/declared-elements/scope.md)。  
  
 变量的*访问级别*是有权访问它的代码的范围。 这由访问修饰符 (如[公共](../../../../visual-basic/language-reference/modifiers/public.md)或[专用](../../../../visual-basic/language-reference/modifiers/private.md)) 中使用`Dim`语句。 有关详细信息，请参阅[Visual Basic 中的访问级别](../../../../visual-basic/programming-guide/language-features/declared-elements/access-levels.md)。  
  
## <a name="see-also"></a>另请参阅  
 [如何︰ 创建新变量](../../../../visual-basic/programming-guide/language-features/variables/how-to-create-a-new-variable.md)   
 [如何︰ 将数据移入和移出变量](../../../../visual-basic/programming-guide/language-features/variables/how-to-move-data-into-and-out-of-a-variable.md)   
 [数据类型](../../../../visual-basic/language-reference/data-types/data-type-summary.md)   
 [受保护](../../../../visual-basic/language-reference/modifiers/protected.md)   
 [友元](../../../../visual-basic/language-reference/modifiers/friend.md)   
 [静态](../../../../visual-basic/language-reference/modifiers/static.md)   
 [已声明的元素的特性](../../../../visual-basic/programming-guide/language-features/declared-elements/declared-element-characteristics.md)   
 [局部类型推理](../../../../visual-basic/programming-guide/language-features/variables/local-type-inference.md)   
 [Option Infer 语句](../../../../visual-basic/language-reference/statements/option-infer-statement.md)
