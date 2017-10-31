---
title: "创建变体泛型接口 (Visual Basic 中) |Microsoft 文档"
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
ms.assetid: d4037dd2-dfe9-4811-9150-93d4e8b20113
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
ms.openlocfilehash: 324e2a906e84950aa9019bbf68a524458492646e
ms.lasthandoff: 03/13/2017

---
# <a name="creating-variant-generic-interfaces-visual-basic"></a>创建变体泛型接口 (Visual Basic)
您可以声明为协变的接口中的泛型类型参数或逆变。 *协变*允许接口方法更派生了比定义的泛型类型参数的返回类型。 *逆变*允许接口方法具有比指定的泛型参数的派生程度更小的参数类型。 泛型接口具有协变或逆变的泛型类型参数称为*变体*。  
  
> [!NOTE]
>  .NET framework 4 中引入了多个现有的泛型接口的变体支持。 .NET Framework 中的变体接口的列表，请参阅[泛型接口 (Visual Basic 中) 中的变体](../../../../visual-basic/programming-guide/concepts/covariance-contravariance/variance-in-generic-interfaces.md)。  
  
## <a name="declaring-variant-generic-interfaces"></a>声明的变体泛型接口  
 你可以使用声明变体泛型接口`in`和`out`对于泛型类型参数的关键字。  
  
> [!IMPORTANT]
>  `ByRef`在 Visual Basic 中的参数不能为 variant 类型的值。 值类型也不支持差异。  
  
 可以将泛型类型参数协变声明使用`out`关键字。 协变类型必须满足以下条件︰  
  
-   类型是只用作接口方法的返回类型，不用作方法参数的类型。 在下面的示例中，在其中阐释了这类型`R`声明为协变。  
  
    ```vb  
    Interface ICovariant(Of Out R)  
        Function GetSomething() As R  
        ' The following statement generates a compiler error.  
        ' Sub SetSomething(ByVal sampleArg As R)  
    End Interface  
    ```  
  
     此规则有一个例外。 如果您具有作为方法参数的逆变泛型委托，可以为委托作为泛型类型参数使用类型。 阐释了这一点由类型`R`在下面的示例。 有关详细信息，请参阅[委托 (Visual Basic 中) 中的变体](../../../../visual-basic/programming-guide/concepts/covariance-contravariance/variance-in-delegates.md)和[对 Func 和 Action 泛型委托 (Visual Basic 中) 的使用方差](../../../../visual-basic/programming-guide/concepts/covariance-contravariance/using-variance-for-func-and-action-generic-delegates.md)。  
  
    ```vb  
    Interface ICovariant(Of Out R)  
        Sub DoSomething(ByVal callback As Action(Of R))  
    End Interface  
    ```  
  
-   类型不用作接口方法的泛型约束。 下面的代码所示。  
  
    ```vb  
    Interface ICovariant(Of Out R)  
        ' The following statement generates a compiler error  
        ' because you can use only contravariant or invariant types  
        ' in generic contstraints.  
        ' Sub DoSomething(Of T As R)()  
    End Interface  
    ```  
  
 你可以使用声明为泛型类型参数逆变`in`关键字。 可以使用逆变类型，只能用作方法参数的类型，不能用作接口方法的返回类型。 逆变类型还可用于泛型约束。 下面的代码演示如何声明逆变接口和泛型约束用于其方法之一。  
  
```vb  
Interface IContravariant(Of In A)  
    Sub SetSomething(ByVal sampleArg As A)  
    Sub DoSomething(Of T As A)()  
    ' The following statement generates a compiler error.  
    ' Function GetSomething() As A  
End Interface  
```  
  
 它还有可能以中相同的接口，但对于不同的类型参数支持协变和逆变，如下面的代码示例中所示。  
  
```vb  
Interface IVariant(Of Out R, In A)  
    Function GetSomething() As R  
    Sub SetSomething(ByVal sampleArg As A)  
    Function GetSetSomething(ByVal sampleArg As A) As R  
End Interface  
```  
  
 在 Visual Basic 中不能声明变体接口中的事件，而不指定委托类型。 此外，不能包含嵌套变体接口，类、 枚举或结构，但它可以有嵌套接口。 下面的代码所示。  
  
```vb  
Interface ICovariant(Of Out R)  
    ' The following statement generates a compiler error.  
    ' Event SampleEvent()  
    ' The following statement specifies the delegate type and   
    ' does not generate an error.  
    Event AnotherEvent As EventHandler  
  
    ' The following statements generate compiler errors,  
    ' because a variant interface cannot have  
    ' nested enums, classes, or structures.  
  
    'Enum SampleEnum : test : End Enum  
    'Class SampleClass : End Class  
    'Structure SampleStructure : Dim value As Integer : End Structure  
  
    ' Variant interfaces can have nested interfaces.  
    Interface INested : End Interface  
End Interface  
```  
  
## <a name="implementing-variant-generic-interfaces"></a>实现的变体泛型接口  
 通过使用相同的语法，用于固定接口，可以在类中实现变体泛型接口。 下面的代码示例演示如何实现泛型类中的协变的接口。  
  
```vb  
Interface ICovariant(Of Out R)  
    Function GetSomething() As R  
End Interface  
  
Class SampleImplementation(Of R)  
    Implements ICovariant(Of R)  
    Public Function GetSomething() As R _  
    Implements ICovariant(Of R).GetSomething  
        ' Some code.  
    End Function  
End Class  
```  
  
 实现变体接口的类是不变。 例如，考虑下面的代码。  
  
```vb  
 The interface is covariant.  
Dim ibutton As ICovariant(Of Button) =  
    New SampleImplementation(Of Button)  
Dim iobj As ICovariant(Of Object) = ibutton  
  
' The class is invariant.  
Dim button As SampleImplementation(Of Button) =  
    New SampleImplementation(Of Button)  
' The following statement generates a compiler error  
' because classes are invariant.  
' Dim obj As SampleImplementation(Of Object) = button  
```  
  
## <a name="extending-variant-generic-interfaces"></a>扩展的变体泛型接口  
 在扩展变体泛型接口时，您必须使用`in`和`out`关键字来显式指定派生的接口是否支持变体。 编译器无法推断从正在扩展的接口的方差。 例如，考虑下面的接口。  
  
```vb  
Interface ICovariant(Of Out T)  
End Interface  
  
Interface IInvariant(Of T)  
    Inherits ICovariant(Of T)  
End Interface  
  
Interface IExtCovariant(Of Out T)  
    Inherits ICovariant(Of T)  
End Interface  
```  
  
 在`Invariant(Of T)`接口的泛型类型参数`T`固定不变，而在`IExtCovariant (Of Out T)`该类型参数是协变的虽然这两个界面扩展相同的接口。 相同的规则应用于逆变泛型类型参数。  
  
 您可以创建可同时扩展接口的泛型类型参数的其中一个接口`T`是协变和其中如果处于扩展是逆变的接口的接口的泛型类型参数`T`是固定不变。 下面的代码示例所示。  
  
```vb  
Interface ICovariant(Of Out T)  
End Interface  
  
Interface IContravariant(Of In T)  
End Interface  
  
Interface IInvariant(Of T)  
    Inherits ICovariant(Of T), IContravariant(Of T)  
End Interface  
```  
  
 但是，如果泛型类型参数`T`是声明为协变在一个界面，您不能将其声明逆变中扩展接口，反之亦然。 下面的代码示例所示。  
  
```vb  
Interface ICovariant(Of Out T)  
End Interface  
  
' The following statements generate a compiler error.  
' Interface ICoContraVariant(Of In T)  
'     Inherits ICovariant(Of T)  
' End Interface  
```  
  
### <a name="avoiding-ambiguity"></a>避免不明确性  
 当您实现变体泛型接口时，方差有时可能导致不明确。 应避免这种情况。  
  
 例如，如果在一个类显式实现相同的变体泛型接口，使用不同的泛型类型参数，它可以创建二义性。 在这种情况下，编译器不会产生一个错误，但未指定将在运行时选择的接口的实现。 这可能导致您的代码中出现细微错误。 请考虑下面的代码示例。  
  
> [!NOTE]
>  与`Option Strict Off`，Visual Basic 会生成编译器警告，当不明确的接口的实现。 与`Option Strict On`，Visual Basic 生成一个编译器错误。  
  
```vb  
' Simple class hierarchy.  
Class Animal  
End Class  
  
Class Cat  
    Inherits Animal  
End Class  
  
Class Dog  
    Inherits Animal  
End Class  
  
' This class introduces ambiguity  
' because IEnumerable(Of Out T) is covariant.  
Class Pets  
    Implements IEnumerable(Of Cat), IEnumerable(Of Dog)  
  
    Public Function GetEnumerator() As IEnumerator(Of Cat) _  
        Implements IEnumerable(Of Cat).GetEnumerator  
        Console.WriteLine("Cat")  
        ' Some code.  
    End Function  
  
    Public Function GetEnumerator1() As IEnumerator(Of Dog) _  
        Implements IEnumerable(Of Dog).GetEnumerator  
        Console.WriteLine("Dog")  
        ' Some code.  
    End Function  
  
    Public Function GetEnumerator2() As IEnumerator _  
        Implements IEnumerable.GetEnumerator  
        ' Some code.  
    End Function  
End Class  
  
Sub Main()  
    Dim pets As IEnumerable(Of Animal) = New Pets()  
    pets.GetEnumerator()  
End Sub  
```  
  
 在此示例中，它是未指定如何`pets.GetEnumerator`方法选择之间`Cat`和`Dog`。 在代码中，这可能导致问题。  
  
## <a name="see-also"></a>另请参阅  
 [泛型接口 (Visual Basic 中) 中的变体](../../../../visual-basic/programming-guide/concepts/covariance-contravariance/variance-in-generic-interfaces.md)   
 [对 Func 和 Action 泛型委托 (Visual Basic 中) 中使用变体](../../../../visual-basic/programming-guide/concepts/covariance-contravariance/using-variance-for-func-and-action-generic-delegates.md)
