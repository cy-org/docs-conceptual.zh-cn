---
title: "如何：确定对象变量引用的类型 (Visual Basic) | Microsoft Docs"
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
  - "对象变量, 确定类型"
  - "TypeOf 运算符 [Visual Basic], 确定对象变量类型"
  - "变量 [Visual Basic], 对象"
ms.assetid: 6f6a138d-58a4-40d1-9f4e-0a3c598eaf81
caps.latest.revision: 13
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 13
---
# 如何：确定对象变量引用的类型 (Visual Basic)
[!INCLUDE[vs2017banner](../../../../visual-basic/includes/vs2017banner.md)]

对象变量包含一个指针，它指向存储在其他位置的数据。  该数据的类型可在运行时更改。  任何时候，都可以使用 <xref:System.Type.GetTypeCode%2A> 方法确定当前运行时类型，或者使用 [TypeOf 运算符](../../../../visual-basic/language-reference/operators/typeof-operator.md) 检查当前运行时类型是否与指定类型兼容。  
  
### 确定对象变量当前引用的精确类型  
  
1.  在对象变量上，调用 <xref:System.Object.GetType%2A> 方法检索 <xref:System.Type?displayProperty=fullName> 对象。  
  
    ```  
    Dim myObject As Object  
    myObject.GetType()  
    ```  
  
2.  在 <xref:System.Type?displayProperty=fullName> 类上，调用共享方法 <xref:System.Type.GetTypeCode%2A> 检索对象类型的 <xref:System.TypeCode> 枚举值。  
  
    ```  
    Dim myObject As Object  
    Dim datTyp As Integer = Type.GetTypeCode(myObject.GetType())  
    MsgBox("myObject currently has type code " & CStr(datTyp))  
    ```  
  
     对任何感兴趣的枚举成员都可以测试 <xref:System.TypeCode> 枚举值，例如 `Double`。  
  
### 确定对象变量的类型是否与指定类型兼容  
  
-   组合使用 `TypeOf` 运算符和 [Is 运算符](../../../../visual-basic/language-reference/operators/is-operator.md)，使用 `TypeOf`...`Is` 表达式测试对象。  
  
    ```  
    If TypeOf objA Is System.Windows.Forms.Control Then  
        MsgBox("objA is compatible with the Control class")  
    End If  
    ```  
  
     如果对象的运行时类型和指定类型兼容，则 `TypeOf`...`Is` 表达式返回 `True`。  
  
     兼容性标准取决于指定类型是类、结构还是接口。  通常，如果对象的类型与指定类型相同，或者，继承或实现了指定类型，则类型是兼容的。  有关更多信息，请参见 [TypeOf 运算符](../../../../visual-basic/language-reference/operators/typeof-operator.md)。  
  
## 编译代码  
 注意，指定类型不能是变量或表达式。  它必须是已定义类型（例如，类、结构或接口）的名称。  包括内部类型，例如 `Integer` 和 `String`。  
  
## 请参阅  
 <xref:System.Object.GetType%2A>   
 <xref:System.Type?displayProperty=fullName>   
 <xref:System.Type.GetTypeCode%2A>   
 <xref:System.TypeCode>   
 [对象变量](../../../../visual-basic/programming-guide/language-features/variables/object-variables.md)   
 [对象变量值](../../../../visual-basic/programming-guide/language-features/variables/object-variable-values.md)   
 [Object 数据类型](../../../../visual-basic/language-reference/data-types/object-data-type.md)