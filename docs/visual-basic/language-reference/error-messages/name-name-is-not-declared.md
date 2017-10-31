---
title: "名称 &quot;&lt;名称&gt;未声明 |Microsoft 文档"
ms.date: 2015-07-20
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology:
- devlang-visual-basic
ms.topic: article
f1_keywords:
- bc30451
- vbc30451
dev_langs:
- VB
helpviewer_keywords:
- BC30451
ms.assetid: 765f099b-e21e-47c6-a906-a065444e56b3
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
ms.openlocfilehash: 81b6862a7f8ceb7998b2ea53336ed3af46b1db5f
ms.lasthandoff: 03/13/2017

---
# <a name="name-39ltnamegt39-is-not-declared"></a>名称 '&lt;名称&gt;未声明
语句引用的编程元素，但编译器找不到具有该准确名称的元素。  
  
 **错误 ID:** BC30451  
  
## <a name="to-correct-this-error"></a>更正此错误  
  
1.  检查引用语句中名称的拼写。 [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)]不区分大小写，但是拼写中的任何其他变化都会被视为完全不同的名称。 请注意，下划线 (`_`) 是名称的一部分，因此也是拼写的一部分。  
  
2.  检查您是否具有成员访问运算符 (`.`) 对象及其成员之间。 例如，如果您有<xref:System.Windows.Forms.TextBox>控件名为`TextBox1`，以访问其<xref:System.Windows.Forms.TextBoxBase.Text%2A>属性应键入`TextBox1.Text`。</xref:System.Windows.Forms.TextBoxBase.Text%2A> </xref:System.Windows.Forms.TextBox> 如果你转而键入 `TextBox1Text`，则会创建不同的名称。  
  
3.  如果任何对象成员访问的语法正确的拼写正确，请验证已声明元素。 有关详细信息，请参阅[声明元素](../../../visual-basic/programming-guide/language-features/declared-elements/index.md)。  
  
4.  如果已声明的编程元素，检查它是否在范围。 如果引用的语句声明的编程元素的区域外，您可能需要限定该元素名称。 有关详细信息，请参阅[在 Visual Basic 中的作用域](../../../visual-basic/programming-guide/language-features/declared-elements/scope.md)。  
  
## <a name="see-also"></a>另请参阅  
 [声明和常量摘要](../../../visual-basic/language-reference/keywords/declarations-and-constants-summary.md)   
 [Visual Basic 命名约定](../../../visual-basic/programming-guide/program-structure/naming-conventions.md)   
 [已声明的元素名称](../../../visual-basic/programming-guide/language-features/declared-elements/declared-element-names.md)   
 [对已声明元素的引用](../../../visual-basic/programming-guide/language-features/declared-elements/references-to-declared-elements.md)
