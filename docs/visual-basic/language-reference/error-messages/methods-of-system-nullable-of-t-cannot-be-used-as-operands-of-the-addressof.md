---
title: "“System.Nullable(Of T)”的方法不能用作“AddressOf”运算符的操作数 | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
f1_keywords: 
  - "vbc32126"
  - "bc32126"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "BC32126"
ms.assetid: 2325668b-e2ad-40ee-a1ec-30450236c20d
caps.latest.revision: 5
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 5
---
# “System.Nullable(Of T)”的方法不能用作“AddressOf”运算符的操作数
[!INCLUDE[vs2017banner](../../../visual-basic/includes/vs2017banner.md)]

语句使用 `AddressOf` 运算符和代表 <xref:System.Nullable%601> 结构的过程的操作数。  
  
 **错误 ID：**BC32126  
  
### 更正此错误  
  
-   将 `AddressOf` 子句中的过程名称替换为非 <xref:System.Nullable%601> 成员的操作数。  
  
-   编写一个对要使用的 <xref:System.Nullable%601> 的方法进行包装的类。  在下面的示例中，`NullableWrapper` 类定义一个名为 `GetValueOrDefault` 的新方法。  因为此新方法不是 <xref:System.Nullable%601> 的成员，所以可将其应用于 `nullInstance`（一个可以为 null 的类型的实例）以构成 `AddressOf` 的参数。  
  
    ```vb#  
    Module Module1  
  
        Delegate Function Deleg() As Integer  
  
        Sub Main()  
            Dim nullInstance As New Nullable(Of Integer)(1)  
  
            Dim del As Deleg  
  
            ' GetValueOrDefault is a method of the Nullable generic  
            ' type. It cannot be used as an operand of AddressOf.  
            ' del = AddressOf nullInstance.GetValueOrDefault  
  
            ' The following line uses the GetValueOrDefault method  
            ' defined in the NullableWrapper class.  
            del = AddressOf (New NullableWrapper(  
                Of Integer)(nullInstance)).GetValueOrDefault  
  
            Console.WriteLine(del.Invoke())  
        End Sub  
  
        Class NullableWrapper(Of T As Structure)  
            Private m_Value As Nullable(Of T)  
  
            Sub New(ByVal Value As Nullable(Of T))  
                m_Value = Value  
            End Sub  
  
            Public Function GetValueOrDefault() As T  
                Return m_Value.Value  
            End Function  
        End Class  
    End Module  
    ```  
  
## 请参阅  
 <xref:System.Nullable%601>   
 [AddressOf 运算符](../../../visual-basic/language-reference/operators/addressof-operator.md)   
 [可以为 Null 的值类型](../../../visual-basic/programming-guide/language-features/data-types/nullable-value-types.md)   
 [Visual Basic 中的泛型类型](../../../visual-basic/programming-guide/language-features/data-types/generic-types.md)