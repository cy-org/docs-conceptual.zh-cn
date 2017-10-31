---
title: "如何︰ 拆分和合并代码 (Visual Basic 中) 中的语句 |Microsoft 文档"
ms.custom: 
ms.date: 2015-07-20
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology:
- devlang-visual-basic
ms.topic: article
f1_keywords:
- vb._
dev_langs:
- VB
helpviewer_keywords:
- colons (:)
- line continuation
- _ line-continuation character
- ': line separator character'
- Visual Basic code, line breaks in
- Visual Basic code, line breaks
- Visual Basic code, line continuation
- long lines of code
- line terminator
- line-continuation sequence
- underscores, in code
- statements [Visual Basic], line continuation in
- line breaks, in code
- line-continuation character
- Visual Basic code, line continuation in
- statements [Visual Basic], line breaks in
ms.assetid: dea01dad-a8ac-484a-bb3a-8c45a1b1eccc
caps.latest.revision: 21
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
ms.openlocfilehash: 840036a91f430f72e0258b8be466770f2855a58f
ms.lasthandoff: 03/13/2017

---
# <a name="how-to-break-and-combine-statements-in-code-visual-basic"></a>如何：在代码中拆分和合并语句 (Visual Basic)
时编写代码时，有时可能要创建一些冗长的语句都必须采取措施水平滚动在代码编辑器中。 尽管这不会影响的方式代码运行，这使得困难为你或其他任何人阅读该代码，因为其出现在显示器上。 在这种情况下，应考虑将单个的长语句分成多个行。  
  
### <a name="to-break-a-single-statement-into-multiple-lines"></a>若要拆分为多行的一条语句  
  
-   使用行继续符，它是一个下划线 (`_`)，您想要中断的行的时刻。 该下划线必须紧跟在空格后，并且在它后面紧跟行终止符（回车）。  
  
    > [!NOTE]
    >  在某些情况下，如果您忽略行继续符，Visual Basic 编译器将隐式 continue 语句在下一行代码上。 有关可以为其省略行继续符的语法元素的列表，请参阅"隐式行继续符"[语句](../../../visual-basic/programming-guide/language-features/statements.md)。  
  
     在下面的示例中，该语句分成四行终止所有的行继续符，但最后一行。  
  
     [!code-vb[VbVbcnConventions #&20;](../../../visual-basic/programming-guide/language-features/codesnippet/VisualBasic/how-to-break-and-combine-statements-in-code_1.vb)]  
  
     这样可以使代码易于阅读，在线和当打印。  
  
     行继续符必须在行上的最后一个字符。 您不能与任何其他内容按照其在同一行。  
  
     存在一些限制，您可以使用行继续符字符;例如，不能使用它的参数名的中间。 您可以中断参数列表与行继续符，但参数的各个名称必须保持不变。  
  
     通过使用行继续符，无法继续注释。 编译器不会检查具有特殊含义的注释中的字符。 对于多行注释，请重复注释符号 (`'`) 在每一行上。  
  
 将每个语句放在单独的行是推荐的方法，尽管[!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)]还允许您在同一行上放置多个语句。  
  
### <a name="to-place-multiple-statements-on-the-same-line"></a>若要在同一行上放置多个语句  
  
-   将语句分隔冒号开头 (`:`)，如下面的示例。  
  
     [!code-vb[VbVbcnConventions #&10;](../../../visual-basic/programming-guide/language-features/codesnippet/VisualBasic/how-to-break-and-combine-statements-in-code_2.vb)]  
  
## <a name="see-also"></a>请参见  
 [程序结构和代码约定](../../../visual-basic/programming-guide/program-structure/program-structure-and-code-conventions.md)   
 [语句](../../../visual-basic/programming-guide/language-features/statements.md)
