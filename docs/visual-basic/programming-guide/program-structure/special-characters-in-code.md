---
title: "在代码 (Visual Basic 中) 中的特殊字符 |Microsoft 文档"
ms.custom: 
ms.date: 2015-07-20
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology:
- devlang-visual-basic
ms.topic: article
f1_keywords:
- vb.)
- vb.(
- vb.colon
- vb.!
- vb..
- 'vb.:'
dev_langs:
- VB
helpviewer_keywords:
- special characters, in code
- parentheses, using in code
- colons (:)
- period character in code
- dot operator (.)
- dictionary access operator
- concatenation operators, special characters in code
- concatenation operators, vs. addition operator
- '! operator'
- separators, using in code
- operators [Visual Basic], dictionary access
- ': separator character'
- member access operator
- addition operator
- operators [Visual Basic], member access
- . operator
- exclamation points
- separators
- exclamation point operator (!)
- Visual Basic code, special characters
ms.assetid: 310dce0c-45b5-4e0d-83e9-32df258d2a3e
caps.latest.revision: 21
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
ms.openlocfilehash: 6d4b6e74ef3dfab3a7174da07cff7100fa4b2a2f
ms.lasthandoff: 03/13/2017

---
# <a name="special-characters-in-code-visual-basic"></a>代码中的特殊字符 (Visual Basic)
有时您必须使用特殊字符，在代码中，即，不是字母或数字的字符。 标点和特殊字符在[!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)]字符集各有其用途，从组织程序文本到定义编译器或已编译的程序执行的任务。 它们不指定要执行的操作。  
  
## <a name="parentheses"></a>括号  
 使用括号时定义一个过程，如`Sub`或`Function`。 必须将所有过程参数列表都括在括号中。 您还使用括号为将变量或参数放入逻辑组，特别是可重写中的复杂表达式的运算符优先级的默认顺序。 下面的示例阐释了这一点。  
  
 [!code-vb[VbVbcnConventions #&11;](../../../visual-basic/programming-guide/language-features/codesnippet/VisualBasic/special-characters-in-code_1.vb)]  
  
 在前面的代码的值执行`d`8.225 和的值是`e`为 3。 用于计算`d`使用默认优先顺序，`/`通过`+`，等同于`d = b + (c / a)`。 在计算中使用的括号`e`重写默认的优先级。  
  
## <a name="separators"></a>分隔符  
 分隔符执行其名称所示︰ 它们分隔各部分代码。 在[!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)]，分隔符为冒号 (`:`)。 当你想要包括在单独的行，而不是单独的行的多个语句时可以使用分隔符。 这可节省空间，并提高代码的可读性。 下面的示例演示由冒号分隔的三个语句。  
  
 [!code-vb[VbVbcnConventions #&12;](../../../visual-basic/programming-guide/language-features/codesnippet/VisualBasic/special-characters-in-code_2.vb)]  
  
 有关详细信息，请参阅[如何︰ 中断并组合在代码中的语句](../../../visual-basic/programming-guide/program-structure/how-to-break-and-combine-statements-in-code.md)。  
  
 冒号 (`:`) 字符也用于标识语句标签。 有关详细信息，请参阅[How to︰ 标签语句](../../../visual-basic/programming-guide/program-structure/how-to-label-statements.md)。  
  
## <a name="concatenation"></a>串联  
 使用`&`运算符*串联*，或将字符串链接在一起。 不要将其与混淆`+`运算符，将数值相加。 如果您使用`+`运算符可串联在基于数值，运行时可以获得不正确的结果。 下面的示例演示这一操作。  
  
 [!code-vb[VbVbcnConventions #&13;](../../../visual-basic/programming-guide/language-features/codesnippet/VisualBasic/special-characters-in-code_3.vb)]  
  
 在前面的代码的值执行`resultA`为 21.01，而值`resultB`为"10.0111"。  
  
## <a name="member-access-operators"></a>成员访问运算符  
 若要访问的一种类型的成员，您使用圆点 (`.`) 或感叹号 (`!`) 之间的类型名称和成员名称的运算符。  
  
### <a name="dot--operator"></a>点 （.）运算符  
 使用`.`运算符是成员访问运算符作为类、 结构、 接口或枚举。 成员可以是字段、 属性、 事件或方法。 下面的示例阐释了这一点。  
  
 [!code-vb[VbVbcnConventions #&14;](../../../visual-basic/programming-guide/language-features/codesnippet/VisualBasic/special-characters-in-code_4.vb)]  
  
### <a name="exclamation-point--operator"></a>惊叹号 （！）运算符  
 使用`!`运算符仅对类或接口用作字典访问运算符。 类或接口必须具有一个接受单个的默认属性`String`参数。 紧随`!`运算符将成为传递给默认属性的字符串形式的参数值。 下面的示例演示这一操作。  
  
 [!code-vb[VbVbcnConventions #&15;](../../../visual-basic/programming-guide/language-features/codesnippet/VisualBasic/special-characters-in-code_5.vb)]  
  
 三个输出行的`MsgBox`所有显示的值`32856`。 第一行使用传统属性的访问权限`index`，第二个利用了这一事实，`index`是类的默认属性`hasDefault`，并且第三个使用字典访问该类。  
  
 请注意，第二个操作数的`!`运算符必须是有效的 Visual Basic 标识符不括在双引号内 (`" "`)。 换而言之，不能使用字符串文字或字符串变量。 下面的最后一个更改行`MsgBox`调用生成一个错误，因为`"X"`是括起来的字符串。  
  
 `"Dictionary access returns " & hD!"X")`  
  
> [!NOTE]
>  必须显式默认集合的引用。 具体而言，不能使用`!`运算符后期绑定变量。  
  
 `!`字符也用作`Single`键入字符。  
  
## <a name="see-also"></a>另请参阅  
 [程序结构和代码约定](../../../visual-basic/programming-guide/program-structure/program-structure-and-code-conventions.md)   
 [类型字符](../../../visual-basic/programming-guide/language-features/data-types/type-characters.md)
