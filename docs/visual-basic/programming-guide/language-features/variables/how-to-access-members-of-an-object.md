---
title: "如何：访问对象的成员 (Visual Basic) | Microsoft Docs"
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
  - "成员, 访问"
  - "对象变量, 访问成员"
ms.assetid: a0072514-6a79-4dd6-8d03-ca8c13e61ddc
caps.latest.revision: 20
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 20
---
# 如何：访问对象的成员 (Visual Basic)
[!INCLUDE[vs2017banner](../../../../visual-basic/includes/vs2017banner.md)]

如果有引用某个对象的对象变量，就常常需要处理该对象的成员（如其方法、属性、字段或事件）。  例如，一旦创建一个新的 <xref:System.Windows.Forms.Form> 对象，则可能需要设置其 <xref:System.Windows.Forms.Control.Text%2A> 属性或调用其 <xref:System.Windows.Forms.Control.Focus%2A> 方法。  
  
## 访问成员  
 通过引用对象的变量访问对象的成员。  
  
#### 访问对象的成员  
  
-   在对象变量名称和成员名称之间使用成员访问运算符 \(`.`\)。  
  
    ```  
    currentText = newForm.Text  
    ```  
  
     如果成员是 [Shared](../../../../visual-basic/language-reference/modifiers/shared.md)，则无需变量即可访问。  
  
## 访问已知类型对象的成员  
 如果在编译时知道对象的类型，则可以对引用该对象的变量使用*“早期绑定”*。  
  
#### 访问在编译时知道类型的对象的成员  
  
1.  将对象变量声明为要分配给该变量的对象类型。  
  
    ```  
    Dim extraForm As System.Windows.Forms.Form   
    ```  
  
     使用 `Option Strict On`，则可只将 <xref:System.Windows.Forms.Form> 对象（或从 <xref:System.Windows.Forms.Form> 派生的类型的对象）分配给 `extraForm`。  如果已经使用 `CType` 到 <xref:System.Windows.Forms.Form> 的扩大转换定义了类或结构，也可以将该类或结构分配给 `extraForm`。  
  
2.  在对象变量名称和成员名称之间使用成员访问运算符 \(`.`\)。  
  
    ```  
    extraForm.Show()  
    ```  
  
     无论 `Option Strict` 如何设置，都可以访问所有特定于 <xref:System.Windows.Forms.Form> 类的方法和属性。  
  
## 访问未知类型的对象的成员  
 如果在编译时不知道对象的类型，则必须对引用该对象的所有变量使用*“后期绑定”*。  
  
#### 访问在编译时不知道类型的对象的成员  
  
1.  将对象变量声明为 [Object 数据类型](../../../../visual-basic/language-reference/data-types/object-data-type.md)。  （将变量声明为 `Object` 和声明为 <xref:System.Object?displayProperty=fullName> 是一样的。）  
  
    ```  
    Dim someControl As Object   
    ```  
  
     如果使用 `Option Strict On`，则只能访问 <xref:System.Object> 类定义的成员。  
  
2.  在对象变量名称和成员名称之间使用成员访问运算符 \(`.`\)。  
  
    ```  
    someControl.GetType()  
    ```  
  
     若要能够访问分配给对象变量的任何对象的成员，请务必设置 `Option Strict Off`。  这样编译器不能保证分配给该变量的对象会公开某个给定成员。  如果对象不公开尝试访问的某个成员，则引发 <xref:System.MemberAccessException> 异常。  
  
## 请参阅  
 <xref:System.Object>   
 <xref:System.Windows.Forms.Form>   
 <xref:System.MemberAccessException>   
 [对象变量](../../../../visual-basic/programming-guide/language-features/variables/object-variables.md)   
 [对象变量声明](../../../../visual-basic/programming-guide/language-features/variables/object-variable-declaration.md)   
 [Object 数据类型](../../../../visual-basic/language-reference/data-types/object-data-type.md)   
 [Option Strict 语句](../../../../visual-basic/language-reference/statements/option-strict-statement.md)