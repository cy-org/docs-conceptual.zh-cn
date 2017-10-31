---
title: "一个实例; 通过共享成员访问将不计算限定表达式 |Microsoft 文档"
ms.date: 2015-07-20
ms.prod: .net
ms.suite: 
ms.technology:
- devlang-visual-basic
ms.topic: article
f1_keywords:
- vbc42025
- BC42025
dev_langs:
- VB
helpviewer_keywords:
- BC42025
ms.assetid: db3337e5-c349-42bf-86df-d9c1e00952a5
caps.latest.revision: 23
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
ms.openlocfilehash: 39be3c95d5acc20afe3a33be9d4db48c09f99a9c
ms.lasthandoff: 03/13/2017

---
# <a name="access-of-shared-member-through-an-instance-qualifying-expression-will-not-be-evaluated"></a>通过实例访问共享成员；将不计算限定表达式
使用类或结构的实例变量访问`Shared`变量、 属性、 过程中或在该类或结构中定义的事件。 如果实例变量用于访问类或结构，例如常量或枚举中，或一个嵌套的类或结构的隐式共享的成员，也可能发生此警告。  
  
 共享某个成员的目的是创建仅该成员的单个副本并将该单一副本提供给类或结构声明它的每个实例。 它具有一致性具有访问该目的`Shared`通过其类或结构的名称而不是通过变量包含的单独实例，该类或结构的成员。  
  
 访问`Shared`通过实例变量的成员可以使代码更加难以理解通过隐藏该成员是事实`Shared`。 此外，如果此类访问是表达式的一部分执行其他操作，如`Function`返回共享成员实例的过程[!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)]绕过表达式，否则，它会执行任何其他操作。  
  
 有关详细信息和示例，请参阅[共享](../../../visual-basic/language-reference/modifiers/shared.md)。  
  
 默认情况下，此消息是一个警告。 有关隐藏警告或将警告视为错误的详细信息，请参阅[在 Visual Basic 中配置警告](https://docs.microsoft.com/visualstudio/ide/configuring-warnings-in-visual-basic)。  
  
 **错误 ID:** BC42025  
  
## <a name="to-correct-this-error"></a>更正此错误  
  
-   使用类或结构，它定义的名称`Shared`成员来访问它，如下面的示例中所示。  
  
```vb  
Public Class testClass  
    Public Shared Sub sayHello()  
        MsgBox("Hello")  
    End Sub  
End Class  
  
Module testModule  
    Public Sub Main()  
        ' Access a shared method through an instance variable.  
        ' This generates a warning.  
        Dim tc As New testClass  
        tc.sayHello()  
  
        ' Access a shared method by using the class name.  
        ' This does not generate a warning.  
        testClass.sayHello()  
    End Sub  
End Module  
```  
  
> [!NOTE]
>  当两个编程元素具有相同的名称，则发出警报的作用域的效果。 在上一示例中，如果通过使用声明实例`Dim testClass as testClass = Nothing`，则编译器将调用`testClass.sayHello()`发生时通过类名，并不会出现警告的方法的访问。  
  
## <a name="see-also"></a>另请参阅  
 [共享](../../../visual-basic/language-reference/modifiers/shared.md)   
 [在 Visual Basic 中的作用域](../../../visual-basic/programming-guide/language-features/declared-elements/scope.md)
