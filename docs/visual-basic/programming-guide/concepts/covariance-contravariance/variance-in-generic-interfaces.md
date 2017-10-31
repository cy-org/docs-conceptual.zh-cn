---
title: "泛型接口 (Visual Basic 中) 中的变体 |Microsoft 文档"
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
ms.assetid: cf4096d0-4bb3-45a9-9a6b-f01e29a60333
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
ms.openlocfilehash: c53c27bdb085213046553fc4b08f11336880a7c2
ms.lasthandoff: 03/13/2017

---
# <a name="variance-in-generic-interfaces-visual-basic"></a>泛型接口 (Visual Basic 中) 中的变体
.NET framework 4 中引入了多个现有的泛型接口的变体支持。 变体支持允许实现这些接口的类的隐式转换。 下面的接口是现在为变体︰  
  
-   <xref:System.Collections.Generic.IEnumerable%601>（T 是协变）</xref:System.Collections.Generic.IEnumerable%601>  
  
-   <xref:System.Collections.Generic.IEnumerator%601>（T 是协变）</xref:System.Collections.Generic.IEnumerator%601>  
  
-   <xref:System.Linq.IQueryable%601>（T 是协变）</xref:System.Linq.IQueryable%601>  
  
-   <xref:System.Linq.IGrouping%602>(`TKey`和`TElement`都是协变)</xref:System.Linq.IGrouping%602>  
  
-   <xref:System.Collections.Generic.IComparer%601>（T 是逆变）</xref:System.Collections.Generic.IComparer%601>  
  
-   <xref:System.Collections.Generic.IEqualityComparer%601>（T 是逆变）</xref:System.Collections.Generic.IEqualityComparer%601>  
  
-   <xref:System.IComparable%601>（T 是逆变）</xref:System.IComparable%601>  
  
 协变允许具有派生程度更大的返回类型相比，通过该接口的泛型类型参数定义的方法。 若要阐释了协变功能，请考虑以下泛型接口︰`IEnumerable(Of Object)`和`IEnumerable(Of String)`。 `IEnumerable(Of String)`接口不会继承`IEnumerable(Of Object)`接口。 但是，`String`类型会继承`Object`类型，在某些情况下，可能想要将这些接口的对象分配给彼此。 下面的代码示例所示。  
  
<CodeContentPlaceHolder>0</CodeContentPlaceHolder>  
 在.NET framework 的早期版本，此代码会导致编译错误，在 Visual Basic 中的`Option Strict On`。 但现在，您可以使用`strings`而不是`objects`，前面的示例中所示，因为<xref:System.Collections.Generic.IEnumerable%601>接口是协变。</xref:System.Collections.Generic.IEnumerable%601>  
  
 逆变允许方法具有比指定的接口的泛型参数的派生程度更小的参数类型。 为了说明逆变，假设您已创建`BaseComparer`类来比较的实例`BaseClass`类。 `BaseComparer` 类实现 `IEqualityComparer(Of BaseClass)` 接口。 因为<xref:System.Collections.Generic.IEqualityComparer%601>接口现在为逆变接口，则可以使用`BaseComparer`比较继承的类的实例`BaseClass`类</xref:System.Collections.Generic.IEqualityComparer%601> 下面的代码示例所示。  
  
<CodeContentPlaceHolder>1</CodeContentPlaceHolder>  
 有关更多示例，请参阅[使用泛型集合 (Visual Basic 中) 的接口中的变体](../../../../visual-basic/programming-guide/concepts/covariance-contravariance/using-variance-in-interfaces-for-generic-collections.md)。  
  
 仅适用于引用类型才支持变体泛型接口中。 值类型不支持差异。 例如，`IEnumerable(Of Integer)`不能隐式转换为`IEnumerable(Of Object)`，这是因为整数表示由值类型。  
  
<CodeContentPlaceHolder>2</CodeContentPlaceHolder>  
 它还是一定要记住，实现变体接口的类仍然是固定的。 例如，尽管<xref:System.Collections.Generic.List%601>实现协变接口<xref:System.Collections.Generic.IEnumerable%601>，你不能隐式转换`List(Of Object)`到`List(Of String)`。</xref:System.Collections.Generic.IEnumerable%601> </xref:System.Collections.Generic.List%601> 下面的代码示例所示。  
  
```vb  
' The following statement generates a compiler error  
' because classes are invariant.  
' Dim list As List(Of Object) = New List(Of String)  
  
' You can use the interface object instead.  
Dim listObjects As IEnumerable(Of Object) = New List(Of String)  
```  
  
## <a name="see-also"></a>另请参阅  
 [泛型集合 (Visual Basic 中) 的接口中使用变体](../../../../visual-basic/programming-guide/concepts/covariance-contravariance/using-variance-in-interfaces-for-generic-collections.md)   
 [创建变体泛型接口 (Visual Basic)](../../../../visual-basic/programming-guide/concepts/covariance-contravariance/creating-variant-generic-interfaces.md)   
 [泛型接口](http://msdn.microsoft.com/library/88bf5b04-d371-4edb-ba38-01ec7cabaacf)   
 [委托 (Visual Basic 中) 中的变体](../../../../visual-basic/programming-guide/concepts/covariance-contravariance/variance-in-delegates.md)
