---
title: "在委托 (Visual Basic 中) 中使用变体 |Microsoft 文档"
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
ms.assetid: 7b5c20f1-6416-46a3-94b6-f109c31c842c
caps.latest.revision: 3
author: dotnet-bot
ms.author: dotnetcontent
translation.priority.mt:
- cs-cz
- pl-pl
- pt-br
- tr-tr
translationtype: Machine Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: 5bd3e60031eac713cee3dee1399af8c6b83e6656
ms.lasthandoff: 03/13/2017

---
# <a name="using-variance-in-delegates-visual-basic"></a>在委托 (Visual Basic 中) 中使用变体
当将一种方法分配给一个委托，委托*协方差*和*逆变*为匹配方法签名与委托类型提供的灵活性。 协变允许方法具有返回类型为于在委托中定义的派生程度更大。 逆变允许具有比委托类型中派生程度更小的参数类型的方法。  
  
## <a name="example-1-covariance"></a>示例 1︰ 协方差  
  
### <a name="description"></a>描述  
 此示例演示如何使用具有返回类型的派生自委托签名中的返回类型的方法使用委托。 返回的数据类型`DogsHandler`属于类型`Dogs`，它派生自`Mammals`委托中定义的类型。  
  
### <a name="code"></a>代码  
  
```vb  
Class Mammals  
End Class  
  
Class Dogs  
    Inherits Mammals  
End Class  
Class Test  
    Public Delegate Function HandlerMethod() As Mammals  
    Public Shared Function MammalsHandler() As Mammals  
        Return Nothing  
    End Function  
    Public Shared Function DogsHandler() As Dogs  
        Return Nothing  
    End Function  
    Sub Test()  
        Dim handlerMammals As HandlerMethod = AddressOf MammalsHandler  
        ' Covariance enables this assignment.  
        Dim handlerDogs As HandlerMethod = AddressOf DogsHandler  
    End Sub  
End Class  
```  
  
## <a name="example-2-contravariance"></a>示例 2︰ 逆变  
  
### <a name="description"></a>描述  
 此示例演示如何使用具有一种类型的基类型的委托签名参数类型的参数的方法使用委托。 逆变，您可以使用一个事件处理程序而不是单独的处理程序。 例如，您可以创建的事件处理程序接受`EventArgs`输入参数并将其用于`Button.MouseClick`发送的事件`MouseEventArgs`类型作为参数，以及与`TextBox.KeyDown`发送的事件`KeyEventArgs`参数。  
  
### <a name="code"></a>代码  
  
```vb  
' Event hander that accepts a parameter of the EventArgs type.  
Private Sub MultiHandler(ByVal sender As Object,  
                         ByVal e As System.EventArgs)  
    Label1.Text = DateTime.Now  
End Sub  
  
Private Sub Form1_Load(ByVal sender As System.Object,  
    ByVal e As System.EventArgs) Handles MyBase.Load  
  
    ' You can use a method that has an EventArgs parameter,  
    ' although the event expects the KeyEventArgs parameter.  
    AddHandler Button1.KeyDown, AddressOf MultiHandler  
  
    ' You can use the same method   
    ' for the event that expects the MouseEventArgs parameter.  
    AddHandler Button1.MouseClick, AddressOf MultiHandler  
End Sub  
```  
  
## <a name="see-also"></a>另请参阅  
 [委托 (Visual Basic 中) 中的变体](../../../../visual-basic/programming-guide/concepts/covariance-contravariance/variance-in-delegates.md)   
 [对 Func 和 Action 泛型委托 (Visual Basic 中) 中使用变体](../../../../visual-basic/programming-guide/concepts/covariance-contravariance/using-variance-for-func-and-action-generic-delegates.md)
