---
title: "如何：确定两个对象是否相关 (Visual Basic) | Microsoft Docs"
ms.custom: ""
ms.date: "2015-07-20"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "继承, Visual Basic 对象"
  - "对象变量, 确定关系"
  - "对象 [Visual Basic], 继承"
ms.assetid: da002e3f-6616-4bad-a229-f842d06652bb
caps.latest.revision: 7
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 7
---
# 如何：确定两个对象是否相关 (Visual Basic)
[!INCLUDE[vs2017banner](../../../../visual-basic/includes/vs2017banner.md)]

可以对两个对象进行比较，以确定用于创建这两个对象的类之间的关系（如果有）。  如果指定的类从当前类继承，或者如果当前类型是由指定的类支持的接口，则 <xref:System.Type?displayProperty=fullName> 类的 <xref:System.Type.IsInstanceOfType%2A> 方法返回 `True`。  
  
### 确定一个对象是否从另一个对象的类或接口继承  
  
1.  对您认为可能是基类型的对象，调用 <xref:System.Object.GetType%2A> 方法。  
  
2.  对 <xref:System.Object.GetType%2A> 返回的 <xref:System.Type?displayProperty=fullName> 对象，调用 <xref:System.Type.IsInstanceOfType%2A> 方法。  
  
3.  在 <xref:System.Type.IsInstanceOfType%2A> 的参数列表中，指定您认为可能是派生类型的对象。  
  
     如果 <xref:System.Type.IsInstanceOfType%2A> 的参数类型从 <xref:System.Type?displayProperty=fullName> 对象类型继承，它就会返回 `True`。  
  
## 示例  
 下面的示例确定一个对象是否表示从另一个对象的类派生的类。  
  
```  
Public Class baseClass  
End Class  
Public Class derivedClass : Inherits baseClass  
End Class  
Public Class testTheseClasses  
    Public Sub seeIfRelated()  
        Dim baseObj As Object = New baseClass()  
        Dim derivedObj As Object = New derivedClass()  
        Dim related As Boolean  
        related = baseObj.GetType().IsInstanceOfType(derivedObj)  
        MsgBox(CStr(related))  
    End Sub  
End Class  
```  
  
 请注意，<xref:System.Type.IsInstanceOfType%2A> 调用中的两个对象变量的位置不符合要求。  假定的基类型用于生成 <xref:System.Type?displayProperty=fullName> 类，而假定的派生类型则作为参数传递给 <xref:System.Type.IsInstanceOfType%2A> 方法。  
  
## 请参阅  
 <xref:System.Object.GetType%2A>   
 <xref:System.Type?displayProperty=fullName>   
 <xref:System.Type.IsInstanceOfType%2A>   
 [Object 数据类型](../../../../visual-basic/language-reference/data-types/object-data-type.md)   
 [对象变量](../../../../visual-basic/programming-guide/language-features/variables/object-variables.md)   
 [对象变量值](../../../../visual-basic/programming-guide/language-features/variables/object-variable-values.md)   
 [如何：确定两个对象是否相同](../../../../visual-basic/programming-guide/language-features/variables/how-to-determine-whether-two-objects-are-identical.md)