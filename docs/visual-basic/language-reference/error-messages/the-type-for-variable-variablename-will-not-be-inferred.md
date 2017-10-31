---
title: "变量的类型 &quot;&lt;variablename&gt;&quot; 绑定到封闭范围中的字段，因此将不会推断 |Microsoft 文档"
ms.date: 2015-07-20
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology:
- devlang-visual-basic
ms.topic: article
f1_keywords:
- vbc42110
- bc42110
dev_langs:
- VB
helpviewer_keywords:
- BC42110
ms.assetid: ef4442eb-08d1-434f-a03b-4aa2ed4e4414
caps.latest.revision: 33
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
ms.translationtype: Machine Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: ab7d69c34a58dc898553868258c4fdf6b81db343
ms.contentlocale: zh-cn
ms.lasthandoff: 03/13/2017

---
# <a name="the-type-for-variable-39ltvariablenamegt39-will-not-be-inferred-because-it-is-bound-to-a-field-in-an-enclosing-scope"></a>变量的类型 '&lt;variablename&gt;' 绑定到封闭范围中的字段，因此将不会推断
变量的类型 '\<variablename&1;> 绑定到封闭范围中的字段，因此将不会推断。 请更改名称\<variablename&1;>，或使用完全限定的名称 （例如，Me.variablename 或 MyBase.variablename）。  
  
 在代码中的循环控制变量为类或其他封闭范围内的一个字段具有相同的名称。 因为控制变量用而无需`As`子句，它绑定到封闭范围中的字段并且编译器不会为其创建一个新的变量或推断其类型。  
  
 在下面的示例中，`Index`中的控件变量`For`语句中，绑定到`Index`字段中`Customer`类。 编译器不会创建新的变量控制变量`Index`或推断其类型。  
  
```  
Class Customer  
  
    ' The class has a field named Index.  
    Private Index As Integer  
  
    Sub Main()  
  
    ' The following line will raise this warning.  
        For Index = 1 To 10  
            ' ...  
        Next  
  
    End Sub  
End Class  
```  
  
 默认情况下，此消息是一个警告。 有关如何隐藏警告或如何将警告视为错误的信息，请参阅[在 Visual Basic 中配置警告](https://docs.microsoft.com/visualstudio/ide/configuring-warnings-in-visual-basic)。  
  
 **错误 ID:** BC42110  
  
### <a name="to-address-this-warning"></a>解决此警告  
  
-   通过将其名称更改为标识符，也不是类的字段的名称使本地循环控制变量。  
  
    ```  
    For I = 1 To 10  
    ```  
  
-   阐明循环控制变量绑定到类字段，通过使用的前缀`Me.`给变量的名称。  
  
    ```  
    For Me.Index = 1 To 10  
    ```  
  
-   而不是依靠局部类型推理，使用`As`子句，以指定循环控制变量的类型。  
  
    ```  
    For Index As Integer = 1 To 10  
    ```  
  
## <a name="example"></a>示例  
 下面的代码演示在位置中的第一个更正与前面的示例。  
  
```  
Class Customer  
  
    ' The class has a field named Index.  
    Private Index As Integer  
  
    Sub Main()  
  
        For I = 1 To 10  
            ' ...  
        Next  
  
    End Sub  
End Class  
```  
  
## <a name="see-also"></a>另请参阅  
 [Option Infer 语句](../../../visual-basic/language-reference/statements/option-infer-statement.md)   
 [每个...下一条语句](../../../visual-basic/language-reference/statements/for-each-next-statement.md)   
 [有关...下一条语句](../../../visual-basic/language-reference/statements/for-next-statement.md)   
 [如何︰ 引用对象的当前实例](../../../visual-basic/programming-guide/language-features/variables/how-to-refer-to-the-current-instance-of-an-object.md)   
 [局部类型推理](../../../visual-basic/programming-guide/language-features/variables/local-type-inference.md)   
 [Me、My、MyBase 和 MyClass](../../../visual-basic/programming-guide/program-structure/me-my-mybase-and-myclass.md)

