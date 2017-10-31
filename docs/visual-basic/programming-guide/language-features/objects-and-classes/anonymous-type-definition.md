---
title: "匿名类型定义 (Visual Basic) | Microsoft Docs"
ms.custom: ""
ms.date: "2015-07-20"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "匿名类型 [Visual Basic], 类型定义"
ms.assetid: 7a8a0ddc-55ba-4d67-869e-87a84d938bac
caps.latest.revision: 21
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 21
---
# 匿名类型定义 (Visual Basic)
[!INCLUDE[vs2017banner](../../../../visual-basic/includes/vs2017banner.md)]

在响应匿名类型的实例声明时，编译器为该类型创建一个包含指定属性的新类定义。  
  
## 编译器生成的代码  
 对于下面的 `product` 定义，编译器创建一个包含 `Name`、`Price` 和 `OnHand` 属性的新类定义。  
  
 [!code-vb[VbVbalrAnonymousTypes#25](../../../../visual-basic/language-reference/modifiers/codesnippet/VisualBasic/anonymous-type-definition_1.vb)]  
  
 类定义包含的属性定义类似于下面的内容。  请注意，键属性没有 `Set` 方法。  键属性的值是只读的。  
  
```vb#  
Public Class $Anonymous1  
    Private _name As String  
    Private _price As Double  
    Private _onHand As Integer  
     Public ReadOnly Property Name() As String  
        Get  
            Return _name  
        End Get  
    End Property  
  
    Public ReadOnly Property Price() As Double  
        Get  
            Return _price  
        End Get  
    End Property  
  
    Public Property OnHand() As Integer  
        Get  
            Return _onHand  
        End Get  
        Set(ByVal Value As Integer)  
            _onHand = Value  
        End Set  
    End Property  
  
End Class  
```  
  
 此外，匿名类型定义还包含一个默认构造函数。  不允许使用需要参数的构造函数。  
  
 如果匿名类型声明至少包含一个键属性，则类型定义将重写三个从 <xref:System.Object> 继承的成员：<xref:System.Object.Equals%2A>、<xref:System.Object.GetHashCode%2A> 和 <xref:System.Object.ToString%2A>。  如果未声明任何键属性，则仅重写 <xref:System.Object.ToString%2A>。  重写的成员提供以下功能：  
  
-   如果两个匿名类型实例是同一实例，则 `Equals` 返回 `True`；否则，如果它们满足下面的条件：  
  
    -   它们具有相同个数的属性。  
  
    -   属性以相同顺序声明，具有相同的名称和相同的推断类型。  名称比较不区分大小写。  
  
    -   至少有一个属性是键属性，并且 `Key` 关键字应用于相同的属性。  
  
    -   如果比较每个相对应的键属性对，则会返回 `True`。  
  
     例如，在下面的示例中，`Equals` 仅对 `employee01` 和 `employee08` 返回 `True`。  每一行前面的注释都指出新实例不匹配 `employee01` 的原因。  
  
     [!code-vb[VbVbalrAnonymousTypes#24](../../../../visual-basic/language-reference/modifiers/codesnippet/VisualBasic/anonymous-type-definition_2.vb)]  
  
-   `GetHashcode` 提供适当的唯一 GetHashCode 算法  该算法仅使用键属性来计算哈希代码。  
  
-   `ToString` 返回相连接的属性值字符串，如下面的示例所示。  既包含键属性也包含非键属性。  
  
     [!code-vb[VbVbalrAnonymousTypes#29](../../../../visual-basic/language-reference/modifiers/codesnippet/VisualBasic/anonymous-type-definition_3.vb)]  
  
 匿名类型的显式命名属性不能与这些生成的方法冲突。  也就是说，不能使用 `.Equals`、`.GetHashCode` 或 `.ToString` 来命名属性。  
  
 此外，至少包含一个键属性的匿名类型定义还实现 <xref:System.IEquatable%601?displayProperty=fullName> 接口，其中 `T` 是匿名类型的类型。  
  
> [!NOTE]
>  仅当满足以下条件时，匿名类型声明才会创建相同的匿名类型：它们出现在相同的程序集中，它们的属性具有相同的名称和相同的推断类型，属性是以相同的顺序声明的，并且相同的属性标记为键属性。  
  
## 请参阅  
 [匿名类型](../../../../visual-basic/programming-guide/language-features/objects-and-classes/anonymous-types.md)   
 [如何：推断匿名类型声明中的属性名和类型](../../../../visual-basic/programming-guide/language-features/objects-and-classes/how-to-infer-property-names-and-types-in-anonymous-type-declarations.md)