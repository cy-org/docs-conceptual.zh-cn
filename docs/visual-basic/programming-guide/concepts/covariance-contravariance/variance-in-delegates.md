---
title: "委托 (Visual Basic 中) 中的变体 |Microsoft 文档"
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
ms.assetid: 38e9353f-74f8-4211-a8f0-7a495414df4a
caps.latest.revision: 3
author: stevehoag
ms.author: shoag
translation.priority.mt:
- cs-cz
- pl-pl
- pt-br
- tr-tr
translationtype: Machine Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: cbab7da8c97ca202f8a4d0a1a65b8fa240cca32d
ms.lasthandoff: 03/13/2017

---
# <a name="variance-in-delegates-visual-basic"></a>委托 (Visual Basic 中) 中的变体
.NET framework 3.5 引入了对匹配方法签名和 C# 和 Visual Basic 中的所有委托中的委托类型的变体支持。 这意味着，可以将分配给委托不仅具有匹配签名，方法还返回多个派生类型 （协变） 或接受具有较少比指定的委托类型的派生的类型 （逆变） 的参数的方法。 这包括泛型和非泛型委托。  
  
 例如，考虑下面的代码，它具有两个类和两个委托︰ 泛型和非泛型。  
  
```vb  
Public Class First  
End Class  
  
Public Class Second  
    Inherits First  
End Class  
  
Public Delegate Function SampleDelegate(ByVal a As Second) As First  
Public Delegate Function SampleGenericDelegate(Of A, R)(ByVal a As A) As R  
```  
  
 当您创建的委托`SampleDelegate`或`SampleDelegate(Of A, R)`类型，可以将以下方法之一分配给这些委托。  
  
```vb  
' Matching signature.  
Public Shared Function ASecondRFirst(  
    ByVal second As Second) As First  
    Return New First()  
End Function  
  
' The return type is more derived.  
Public Shared Function ASecondRSecond(  
    ByVal second As Second) As Second  
    Return New Second()  
End Function  
  
' The argument type is less derived.  
Public Shared Function AFirstRFirst(  
    ByVal first As First) As First  
    Return New First()  
End Function  
  
' The return type is more derived   
' and the argument type is less derived.  
Public Shared Function AFirstRSecond(  
    ByVal first As First) As Second  
    Return New Second()  
End Function  
```  
  
 下面的代码示例说明了方法签名与委托类型之间的隐式转换。  
  
```vb  
' Assigning a method with a matching signature   
' to a non-generic delegate. No conversion is necessary.  
Dim dNonGeneric As SampleDelegate = AddressOf ASecondRFirst  
' Assigning a method with a more derived return type   
' and less derived argument type to a non-generic delegate.  
' The implicit conversion is used.  
Dim dNonGenericConversion As SampleDelegate = AddressOf AFirstRSecond  
  
' Assigning a method with a matching signature to a generic delegate.  
' No conversion is necessary.  
Dim dGeneric As SampleGenericDelegate(Of Second, First) = AddressOf ASecondRFirst  
' Assigning a method with a more derived return type   
' and less derived argument type to a generic delegate.  
' The implicit conversion is used.  
Dim dGenericConversion As SampleGenericDelegate(Of Second, First) = AddressOf AFirstRSecond  
```  
  
 有关更多示例，请参阅[使用委托 (Visual Basic 中) 中的变体](../../../../visual-basic/programming-guide/concepts/covariance-contravariance/using-variance-in-delegates.md)和[对 Func 和 Action 泛型委托 (Visual Basic 中) 的使用方差](../../../../visual-basic/programming-guide/concepts/covariance-contravariance/using-variance-for-func-and-action-generic-delegates.md)。  
  
## <a name="variance-in-generic-type-parameters"></a>泛型类型参数中的变化  
 在.NET Framework 4 及更高版本可以启用之间的代理，而隐式转换，以便具有泛型类型参数所指定的不同类型的泛型委托可以分配给对方，如果这些类型都继承自对方所需的方差。  
  
 若要启用隐式转换，您必须显式声明为协变将委托中的泛型参数或通过使用逆变`in`或`out`关键字。  
  
 下面的代码示例演示如何创建一个具有协变的泛型类型参数的委托。  
  
```vb  
' Type T is declared covariant by using the out keyword.  
Public Delegate Function SampleGenericDelegate(Of Out T)() As T  
Sub Test()  
    Dim dString As SampleGenericDelegate(Of String) = Function() " "  
    ' You can assign delegates to each other,  
    ' because the type T is declared covariant.  
    Dim dObject As SampleGenericDelegate(Of Object) = dString  
End Sub  
```  
  
 如果您使用唯一的变体支持来匹配方法签名和委托类型，且不要使用`in`和`out`关键字，您可能会发现，有时可以实例化委托用相同的 lambda 表达式或方法，但不能将一个委托分配到另一个。  
  
 在下面的代码示例中，`SampleGenericDelegate(Of String)`不能显式转换为`SampleGenericDelegate(Of Object)`，尽管`String`继承`Object`。 可以通过将标记的泛型参数来解决此问题`T`与`out`关键字。  
  
```vb  
Public Delegate Function SampleGenericDelegate(Of T)() As T  
Sub Test()  
    Dim dString As SampleGenericDelegate(Of String) = Function() " "  
  
    ' You can assign the dObject delegate  
    ' to the same lambda expression as dString delegate  
    ' because of the variance support for   
    ' matching method signatures with delegate types.  
    Dim dObject As SampleGenericDelegate(Of Object) = Function() " "  
  
    ' The following statement generates a compiler error  
    ' because the generic type T is not marked as covariant.  
    ' Dim dObject As SampleGenericDelegate(Of Object) = dString  
  
End Sub  
```  
  
### <a name="generic-delegates-that-have-variant-type-parameters-in-the-net-framework"></a>具有 variant 类型的值的泛型委托类型参数在.NET Framework  
 .NET framework 4 中引入了几个现有的泛型委托中的泛型类型参数的变体支持︰  
  
-   `Action`从委托<xref:System>命名空间，例如，<xref:System.Action%601>和<xref:System.Action%602></xref:System.Action%602></xref:System.Action%601></xref:System>  
  
-   `Func`从委托<xref:System>命名空间，例如，<xref:System.Func%601>和<xref:System.Func%602></xref:System.Func%602></xref:System.Func%601></xref:System>  
  
-   <xref:System.Predicate%601>委托</xref:System.Predicate%601>  
  
-   <xref:System.Comparison%601>委托</xref:System.Comparison%601>  
  
-   <xref:System.Converter%602>委托</xref:System.Converter%602>  
  
 有关详细信息和示例，请参阅[对 Func 和 Action 泛型委托 (Visual Basic 中) 的使用方差](../../../../visual-basic/programming-guide/concepts/covariance-contravariance/using-variance-for-func-and-action-generic-delegates.md)。  
  
### <a name="declaring-variant-type-parameters-in-generic-delegates"></a>声明泛型委托中的 Variant 类型参数  
 如果一个泛型委托具有协变或逆变泛型类型参数，它可以被称为*变体泛型委托*。  
  
 可以将泛型类型参数协变的泛型委托声明使用`out`关键字。 可以使用协变类型，只能用作方法的返回类型，不能用作方法参数的类型。 下面的代码示例演示如何声明协变的泛型委托。  
  
<CodeContentPlaceHolder>5</CodeContentPlaceHolder>  
 你可以使用声明为泛型类型参数逆变在泛型委托`in`关键字。 仅为方法参数的类型而不是方法的返回类型，则可以使用逆变类型。 下面的代码示例演示如何声明逆变泛型委托。  
  
<CodeContentPlaceHolder>6</CodeContentPlaceHolder>  
> [!IMPORTANT]
>  `ByRef`在 Visual Basic 中的参数不能将标记作为变体。  
  
 还有可能在同一个委托，但不同的类型参数支持方差和协方差。 这在下面的示例中显示。  
  
<CodeContentPlaceHolder>7</CodeContentPlaceHolder>  
### <a name="instantiating-and-invoking-variant-generic-delegates"></a>实例化和调用变体泛型委托  
 可以实例化并调用变体委托，就像实例化和调用固定委托。 在下面的示例中，lambda 表达式实例化委托。  
  
<CodeContentPlaceHolder>8</CodeContentPlaceHolder>  
### <a name="combining-variant-generic-delegates"></a>组合变体泛型委托  
 不应该组合变体委托。 <xref:System.Delegate.Combine%2A>方法不支持变体委托转换，并且希望委托类型完全相同。</xref:System.Delegate.Combine%2A> 这可能会导致运行时异常时组合使用的委托<xref:System.Delegate.Combine%2A>方法 （在 C# 和 Visual Basic） 或通过使用`+`运算符 （在 C# 中)，如下面的代码示例中所示。</xref:System.Delegate.Combine%2A>  
  
<CodeContentPlaceHolder>9</CodeContentPlaceHolder>  
## <a name="variance-in-generic-type-parameters-for-value-and-reference-types"></a>泛型类型参数中的值和引用类型的方差  
 仅适用于引用类型才支持对泛型类型参数的变体。 例如，`DVariant(Of Int)`不能隐式转换为`DVariant(Of Object)`或`DVariant(Of Long)`，因为整数是值类型。  
  
 下面的示例演示的变体在泛型类型参数不支持对于值类型。  
  
```vb  
' The type T is covariant.  
Public Delegate Function DVariant(Of Out T)() As T  
' The type T is invariant.  
Public Delegate Function DInvariant(Of T)() As T  
Sub Test()  
    Dim i As Integer = 0  
    Dim dInt As DInvariant(Of Integer) = Function() i  
    Dim dVaraintInt As DVariant(Of Integer) = Function() i  
  
    ' All of the following statements generate a compiler error  
    ' because type variance in generic parameters is not supported  
    ' for value types, even if generic type parameters are declared variant.  
    ' Dim dObject As DInvariant(Of Object) = dInt  
    ' Dim dLong As DInvariant(Of Long) = dInt  
    ' Dim dVaraintObject As DInvariant(Of Object) = dInt  
    ' Dim dVaraintLong As DInvariant(Of Long) = dInt  
End Sub  
```  
  
## <a name="relaxed-delegate-conversion-in-visual-basic"></a>在 Visual Basic 中的宽松的委托转换  
 宽松的委托转换，更灵活地匹配方法签名和委托类型。 例如，它允许您忽略参数规范，并省略函数返回值，当为一个委托，分配一个方法。 有关详细信息，请参阅[宽松委托转换](../../../../visual-basic/programming-guide/language-features/delegates/relaxed-delegate-conversion.md)。  
  
## <a name="see-also"></a>另请参阅  
 [泛型](https://msdn.microsoft.com/library/ms172192)   
 [对 Func 和 Action 泛型委托 (Visual Basic 中) 中使用变体](../../../../visual-basic/programming-guide/concepts/covariance-contravariance/using-variance-for-func-and-action-generic-delegates.md)
