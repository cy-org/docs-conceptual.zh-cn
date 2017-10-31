---
title: "Of 子句 (Visual Basic) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
f1_keywords: 
  - "Of"
  - "vb.Of"
  - "vb.of"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "变量 [Visual Basic], 数据类型"
  - "约束, Visual Basic 泛型类型"
  - "数据类型参数"
  - "泛型参数"
  - "泛型 [Visual Basic], 约束"
  - "Of 关键字"
  - "参数, 泛型"
  - "参数, 类型"
  - "类型参数"
  - "类型 [Visual Basic], 泛型"
ms.assetid: 0db8f65c-65af-4089-ab7f-6fcfecb60444
caps.latest.revision: 17
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 17
---
# Of 子句 (Visual Basic)
[!INCLUDE[vs2017banner](../../../visual-basic/includes/vs2017banner.md)]

引入 `Of` 子句，该子句在泛型类、结构、接口、委托或过程上标识类型参数。  有关泛型类型的信息，请参见 [Visual Basic 中的泛型类型](../../../visual-basic/programming-guide/language-features/data-types/generic-types.md)。  
  
## 使用 Of 关键字  
 下面的代码示例使用 `Of` 关键字定义采用两个类型参数的类的大纲。  它会按 <xref:System.IComparable> 接口约束 `keyType` 参数，这意味着使用代码必须提供用于实现 <xref:System.IComparable> 的类型参数。  这非常有必要，使得 `add` 过程可以调用 <xref:System.IComparable.CompareTo%2A?displayProperty=fullName> 方法。  有关约束的更多信息，请参见 [类型列表](../../../visual-basic/language-reference/statements/type-list.md)。  
  
```  
Public Class Dictionary(Of entryType, keyType As IComparable)  
    Public Sub add(ByVal e As entryType, ByVal k As keyType)  
        Dim dk As keyType  
        If k.CompareTo(dk) = 0 Then  
        End If  
    End Sub  
    Public Function find(ByVal k As keyType) As entryType  
    End Function  
End Class  
```  
  
 如果完成了上面的类定义，就可以根据它构造各种 `dictionary` 类。  为 `entryType` 和 `keyType` 提供的类型确定该类存储的项类型以及它与各项关联的关键字类型。  因为有此项约束，所以必须为 `keyType` 提供用于实现 <xref:System.IComparable> 的类型。  
  
 下面的代码示例创建了对象，该对象具有 `String` 条目，并将 `Integer` 项与每一个关联。  `Integer` 可以实现 <xref:System.IComparable>，因此满足对 `keyType` 的约束。  
  
```  
Dim d As New dictionary(Of String, Integer)  
```  
  
 `Of` 关键字可用于下面的上下文中：  
  
 [Class 语句](../../../visual-basic/language-reference/statements/class-statement.md)  
  
 [Delegate 语句](../../../visual-basic/language-reference/statements/delegate-statement.md)  
  
 [Function 语句](../../../visual-basic/language-reference/statements/function-statement.md)  
  
 [Interface 语句](../../../visual-basic/language-reference/statements/interface-statement.md)  
  
 [Structure Statement](../../../visual-basic/language-reference/statements/structure-statement.md)  
  
 [Sub 语句](../../../visual-basic/language-reference/statements/sub-statement.md)  
  
## 请参阅  
 <xref:System.IComparable>   
 [类型列表](../../../visual-basic/language-reference/statements/type-list.md)   
 [Visual Basic 中的泛型类型](../../../visual-basic/programming-guide/language-features/data-types/generic-types.md)   
 [In](../../../visual-basic/language-reference/modifiers/in-generic-modifier.md)   
 [Out](../../../visual-basic/language-reference/modifiers/out-generic-modifier.md)