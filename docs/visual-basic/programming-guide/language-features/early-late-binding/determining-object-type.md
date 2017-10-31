---
title: "确定对象类型 (Visual Basic 中) |Microsoft 文档"
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
- classes [Visual Basic], discovering which an object belongs to
- types [Visual Basic], determining Visual Basic object types
- object variables, testing values
- TypeOf...Is expression, object type at run time
- TypeName function
- objects [Visual Basic], type determining
ms.assetid: d95e7ad1-cd63-41d6-9a28-d7a1380d49c1
caps.latest.revision: 13
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
ms.openlocfilehash: 2486d989801fc4866a50747aa963b509a627994d
ms.lasthandoff: 03/13/2017

---
# <a name="determining-object-type-visual-basic"></a>确定对象类型 (Visual Basic)
一般对象变量 (即，变量声明为`Object`) 可以包含来自任何类对象。 使用类型的变量时`Object`，您可能需要采取不同的操作，在基于对象的类; 例如，某些对象可能不支持特定属性或方法。 [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)]提供了以下两种方法可以确定哪种类型的对象存储在一个对象变量︰`TypeName`函数和`TypeOf...Is`运算符。  
  
## <a name="typename-and-typeofis"></a>TypeName 和 TypeOf...是  
 `TypeName`函数将返回一个字符串，而是最佳选择，当您需要时存储或显示类对象的名称，如下面的代码段中所示︰  
  
 [!code-vb[VbVbalrOOP #&92;](../../../../visual-basic/misc/codesnippet/VisualBasic/determining-object-type_1.vb)]  
  
 `TypeOf...Is`运算符是用于测试的对象类型的最佳选择，因为它是比等效的字符串比较使用更快`TypeName`。 下面的代码片段使用`TypeOf...Is`内`If...Then...Else`语句︰  
  
 [!code-vb[VbVbalrOOP #&93;](../../../../visual-basic/misc/codesnippet/VisualBasic/determining-object-type_2.vb)]  
  
 需要注意的一点就到期。 `TypeOf...Is`运算符将返回`True`如果属于特定类型或派生自某个特定类型的对象。 几乎所有操作都与[!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)]涉及到对象，其中包括一些通常不被视为对象，如字符串和整数的元素。 这些对象派生自和继承从<xref:System.Object>。</xref:System.Object>方法 当传递`Integer`和计算与`Object`、`TypeOf...Is`运算符将返回`True`。 下面的示例报告参数`InParam`既是`Object`和`Integer`:  
  
 [!code-vb[VbVbalrOOP #&94;](../../../../visual-basic/misc/codesnippet/VisualBasic/determining-object-type_3.vb)]  
  
 下面的示例使用这两个`TypeOf...Is`和`TypeName`来确定对象中传递给它的类型`Ctrl`参数。 `TestObject`过程调用`ShowType`使用三种不同的控件。  
  
#### <a name="to-run-the-example"></a>运行示例  
  
1.  创建新的 Windows 应用程序项目并添加<xref:System.Windows.Forms.Button>控件，<xref:System.Windows.Forms.CheckBox>控件，和一个<xref:System.Windows.Forms.RadioButton>到窗体的控件。</xref:System.Windows.Forms.RadioButton> </xref:System.Windows.Forms.CheckBox> </xref:System.Windows.Forms.Button>  
  
2.  从你的窗体上的按钮，调用`TestObject`过程。  
  
3.  将以下代码添加到你的窗体︰  
  
     [!code-vb[VbVbalrOOP #&95;](../../../../visual-basic/misc/codesnippet/VisualBasic/determining-object-type_4.vb)]  
  
## <a name="see-also"></a>另请参阅  
 <xref:Microsoft.VisualBasic.Information.TypeName%2A></xref:Microsoft.VisualBasic.Information.TypeName%2A>   
 [使用字符串名调用属性或方法](../../../../visual-basic/programming-guide/language-features/early-late-binding/calling-a-property-or-method-using-a-string-name.md)   
 [Object 数据类型](../../../../visual-basic/language-reference/data-types/object-data-type.md)   
 [如果...然后...Else 语句](../../../../visual-basic/language-reference/statements/if-then-else-statement.md)   
 [String 数据类型](../../../../visual-basic/language-reference/data-types/string-data-type.md)   
 [Integer 数据类型](../../../../visual-basic/language-reference/data-types/integer-data-type.md)
