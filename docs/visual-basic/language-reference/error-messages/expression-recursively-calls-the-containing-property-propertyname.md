---
title: "表达式递归调用包含的属性 &quot;&lt;propertyname&gt;&quot; |Microsoft 文档"
ms.date: 2015-07-20
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology:
- devlang-visual-basic
ms.topic: article
f1_keywords:
- vbc42026
- BC42026
dev_langs:
- VB
helpviewer_keywords:
- BC42026
ms.assetid: 4fde9db6-3bf3-48dc-8e05-981bf08969da
caps.latest.revision: 10
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
ms.openlocfilehash: ca20bf1a539f2727a80f8e781c1e9ebc5a4a253d
ms.lasthandoff: 03/13/2017

---
# <a name="expression-recursively-calls-the-containing-property-39ltpropertynamegt39"></a>表达式递归调用包含的属性 '&lt;propertyname&gt;
中的语句`Set`属性定义的过程将一个值存储到属性的名称。  
  
 包含属性的值的建议的方法是定义`Private`变量属性的容器中并将其同时`Get`和`Set`过程。 `Set`过程然后应将传入的值存储在此`Private`变量。  
  
 `Get`过程的行为类似`Function`的过程中，以便可以将值分配给属性名称并将控制权返回在遇到`End Get`语句。 建议的方法，但是，是包括`Private`变量中的值作为[Return 语句](../../../visual-basic/language-reference/statements/return-statement.md)。  
  
 `Set`过程的行为类似`Sub`过程，不返回值。 因此，过程或属性名称具有中的没有特殊含义`Set`过程中，并且您不能将一个值存储到其中。  
  
 下面的示例说明了可能会导致此错误消息，然后建议的方法的方法。  
  
```  
Public Class illustrateProperties  
' The code in the following property causes this error.  
    Public Property badProp() As Char  
        Get  
            Dim charValue As Char  
            ' Insert code to update charValue.  
            badProp = charValue  
        End Get  
        Set(ByVal Value As Char)  
            ' The following statement causes this error.  
            badProp = Value  
            ' The value stored in the local variable badProp  
            ' is not used by the Get procedure in this property.  
        End Set  
    End Property  
' The following code uses the recommended approach.  
    Private propValue As Char  
    Public Property goodProp() As Char  
        Get  
            ' Insert code to update propValue.  
            Return propValue  
        End Get  
        Set(ByVal Value As Char)  
            propValue = Value  
        End Set  
    End Property  
End Class  
```  
  
 默认情况下，此消息是一个警告。 有关隐藏警告或将警告视为错误的详细信息，请参阅[在 Visual Basic 中配置警告](https://docs.microsoft.com/visualstudio/ide/configuring-warnings-in-visual-basic)。  
  
 **错误 ID:** BC42026  
  
## <a name="to-correct-this-error"></a>更正此错误  
  
-   重写属性定义，以便使用建议的方法，如在前面的示例所示。  
  
## <a name="see-also"></a>另请参阅  
 [属性过程](../../../visual-basic/programming-guide/language-features/procedures/property-procedures.md)   
 [Property 语句](../../../visual-basic/language-reference/statements/property-statement.md)   
 [Set 语句](../../../visual-basic/language-reference/statements/set-statement.md)
