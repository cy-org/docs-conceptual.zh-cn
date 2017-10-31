---
title: "嵌套的控件结构 (Visual Basic 中) |Microsoft 文档"
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
- Visual Basic code, control flow
- control structures, nested
- conditional statements, nested
- statements [Visual Basic], control flow
- control flow, nested control statements
- structures, nested control
- nested control statements
ms.assetid: cf60b061-65d9-44a8-81f2-b0bdccd23a05
caps.latest.revision: 20
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
ms.openlocfilehash: 4afc0afc2ad63d03f2c4251640d3682b2b184504
ms.lasthandoff: 03/13/2017

---
# <a name="nested-control-structures-visual-basic"></a>嵌套的控件结构 (Visual Basic)
您可以控制将语句放在其他控制语句中，例如`If...Then...Else`中块`For...Next`循环。 说是一个控制语句放在另一个控制语句可*嵌套*。  
  
## <a name="nesting-levels"></a>嵌套级别  
 中的控制结构[!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)]可以嵌套到任意数量的级别。 它是常见的做法使嵌套的结构通过缩进每个正文更具可读性。 集成的开发环境 (IDE) 编辑器自动执行此操作。  
  
 在下面的示例中，该过程`sumRows`相加矩阵的每个行的正元素。  
  
```  
Public Sub sumRows(ByVal a(,) As Double, ByRef r() As Double)  
    Dim i, j As Integer  
    For i = 0 To UBound(a, 1)  
        r(i) = 0  
        For j = 0 To UBound(a, 2)  
            If a(i, j) > 0 Then  
                r(i) = r(i) + a(i, j)  
            End If  
        Next j  
    Next i  
End Sub  
```  
  
 在前面的示例中，第一个`Next`语句关闭内部`For`循环和最后一个`Next`语句关闭外部`For`循环。  
  
 同样，在嵌套`If`语句，`End If`语句自动应用到最近的前`If`语句。 嵌套`Do`循环的工作方式类似，最里层`Loop`语句匹配里面`Do`语句。  
  
> [!NOTE]
>  对于许多控制结构，当您单击某个关键字在结构中的关键字的所有都会突出显示。 例如，当您单击`If`中`If...Then...Else`构造、 的所有实例`If`， `Then`， `ElseIf`， `Else`，和`End If`在构造过程中会突出显示。 若要将移动到下一步或上一个突出显示关键字，按 CTRL + SHIFT + 向下键或 CTRL + SHIFT + 向上键。  
  
## <a name="nesting-different-kinds-of-control-structures"></a>嵌套不同类型的控件结构  
 您可以嵌套在另一种控制结构的一种。 下面的示例使用`With`在此块内`For Each`循环，而且嵌套`If`块内`With`块。  
  
```  
For Each ctl As System.Windows.Forms.Control In Me.Controls  
    With ctl  
        .BackColor = System.Drawing.Color.Yellow  
        .ForeColor = System.Drawing.Color.Black  
        If .CanFocus Then  
            .Text = "Colors changed"  
            If Not .Focus() Then  
                ' Insert code to process failed focus.  
            End If  
        End If  
    End With  
Next ctl  
```  
  
## <a name="overlapping-control-structures"></a>重叠的控件结构  
 不能重叠控制结构。 这意味着，任何嵌套的结构都必须完全包含在下一步最里面的结构。 例如，下面的排列是无效因为`For`循环将终止之前内部`With`块终止。  
  
 ![无效嵌套示意图](../../../../visual-basic/programming-guide/language-features/control-flow/media/nestexampleinvalid.gif "NestExampleInvalid")  
无效嵌套的并且具有结构  
  
 [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)]编译器检测到这种重叠的控制结构和标志编译时错误。  
  
## <a name="see-also"></a>另请参阅  
 [控制流](../../../../visual-basic/programming-guide/language-features/control-flow/index.md)   
 [决策结构](../../../../visual-basic/programming-guide/language-features/control-flow/decision-structures.md)   
 [循环结构](../../../../visual-basic/programming-guide/language-features/control-flow/loop-structures.md)   
 [其他控件结构](../../../../visual-basic/programming-guide/language-features/control-flow/other-control-structures.md)
