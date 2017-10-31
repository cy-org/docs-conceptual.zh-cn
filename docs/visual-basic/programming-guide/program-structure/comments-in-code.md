---
title: "代码 (Visual Basic 中) 中的注释 |Microsoft 文档"
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
- Uncomment button
- REM statement
- comments, in code
- comments, Visual Basic code
- Comment button
- buttons, Uncomment
- buttons, Comment
- code comments, Visual Basic
- Visual Basic code, comments
- comments
- code comments
ms.assetid: 90136fba-22eb-49f9-ba81-63db629b4a47
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
ms.openlocfilehash: 9663d83903ba2f9dcf93ecb5c293ac479e7dc175
ms.lasthandoff: 03/13/2017

---
# <a name="comments-in-code-visual-basic"></a>代码中的注释 (Visual Basic)
阅读代码示例时，经常会遇到注释符号 (`'`)。 此符号通知[!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)]编译器忽略它，后面的文本或*注释*。 注释是为了方便阅读而为代码添加的简短的解释性说明。  
  
 在所有过程的开头加入一段说明过程功能特征（过程的作用）的简短注释是一个很好的编程做法。 这对您自己和检查代码的任何其他人都有好处。 应该把实现的详细信息（过程实现的方式）与描述功能特征的注释分开。 若给说明加入了实现的详细信息，切记在更新函数时对这些详细信息进行更新。  
  
 注释可以和语句同行并跟随其后，也可以另占一整行。 以下代码阐释了这两种情况。  
  
 [!code-vb[VbVbcnConventions #&16;](../../../visual-basic/programming-guide/language-features/codesnippet/VisualBasic/comments-in-code_1.vb)]  
  
 如果注释需要多行，请在每行的前面使用注释符号，如以下示例所示。  
  
 [!code-vb[VbVbcnConventions #&17;](../../../visual-basic/programming-guide/language-features/codesnippet/VisualBasic/comments-in-code_2.vb)]  
  
## <a name="commenting-guidelines"></a>注释原则  
 下表提供了在一段代码前可以加上哪些类型的注释的一般原则。 这些准则仅仅是一些建议；[!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] 并未强制实施有关添加注释的规则。 编写注释时，应编写对您和代码的任何其他读者都最为有效的注释。  
  
|||  
|---|---|  
|注释类型|注释说明|  
|用途|描述过程的用途（而不是其实现方式）|  
|假设|列举每个外部变量、控件、打开的文件或过程访问的其他元素|  
|效果|列举每个受影响的外部变量、控件、文件以及它的作用（仅在作用不明显时列举）|  
|输入|指定参数的用途|  
|返回|说明过程返回的值|  
  
 请记住以下几点：  
  
-   每个重要的变量声明前都应有注释，用以描述被声明变量的用途。  
  
-   变量、控件和过程的命名应当足够清楚，使得只在遇到复杂的实现详细情况时才使用注释。  
  
-   注释不能与行继续符同行。  
  
 您可以添加或删除选择的代码的一个或多个行，然后选择一个代码块的注释符**注释**(![VisualBasicWinAppCodeEditorCommentButton](../../../visual-basic/programming-guide/program-structure/media/vacommentbutton.gif "vaCommentButton")) 和**取消注释**(![VisualStudioWinAppProjectUncommentButton](../../../visual-basic/programming-guide/program-structure/media/vauncommentbutton.gif "vaUncommentButton")) 上的按钮**编辑**工具栏。  
  
> [!NOTE]
>  也可以用在文本前加关键字 `REM` 的方式给代码添加注释。 但是，`'`符号和**注释**/**取消注释**按钮可以更轻松地使用，并且需要更少的空间和内存。  
  
## <a name="see-also"></a>另请参阅  
 [使用 XML 注释将代码文档化](http://msdn.microsoft.com/magazine/dd722812.aspx)   
 [如何︰ 创建 XML 文档](../../../visual-basic/programming-guide/program-structure/how-to-create-xml-documentation.md)   
 [XML 注释标记](../../../visual-basic/language-reference/xmldoc/recommended-xml-tags-for-documentation-comments.md)   
 [程序结构和代码约定](../../../visual-basic/programming-guide/program-structure/program-structure-and-code-conventions.md)   
 [REM 语句](../../../visual-basic/language-reference/statements/rem-statement.md)
