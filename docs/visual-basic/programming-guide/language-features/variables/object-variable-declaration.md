---
title: "对象变量声明 (Visual Basic) | Microsoft Docs"
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
  - "绑定, 后期和早期"
  - "类 [Visual Basic], 声明"
  - "声明, class"
  - "声明类"
  - "声明变量, 对象变量"
  - "早期绑定"
  - "后期绑定"
  - "对象变量, 声明"
  - "变量 [Visual Basic], 对象"
ms.assetid: 2a5a41a3-1aa8-4236-b1f0-2382af7bf715
caps.latest.revision: 33
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 33
---
# 对象变量声明 (Visual Basic)
[!INCLUDE[vs2017banner](../../../../visual-basic/includes/vs2017banner.md)]

可使用普通声明语句声明对象变量。  对于数据类型，可指定 `Object`（即 [Object 数据类型](../../../../visual-basic/language-reference/data-types/object-data-type.md)）或要从中创建对象的更具体的类。  
  
 将变量声明为 `Object` 与将其声明为 <xref:System.Object?displayProperty=fullName> 相同。  
  
 用特定的对象类声明变量时，变量可以访问由该类以及它所继承的类公开的所有方法和属性。  如果使用 <xref:System.Object> 声明变量，则该变量只能访问 <xref:System.Object> 类的成员，除非打开 `Option Strict Off` 选项以允许后期绑定。  
  
## 声明语法  
 使用下面的语法声明对象变量：  
  
```  
Dim variablename As [New] { objectclass | Object }  
```  
  
 也可以在声明中指定 [Public](../../../../visual-basic/language-reference/modifiers/public.md)、[Protected](../../../../visual-basic/language-reference/modifiers/protected.md)、[Friend](../../../../visual-basic/language-reference/modifiers/friend.md)、`Protected Friend`、[Private](../../../../visual-basic/language-reference/modifiers/private.md)、[Shared](../../../../visual-basic/language-reference/modifiers/shared.md) 或 [Static](../../../../visual-basic/language-reference/modifiers/static.md)。  下面的示例声明是有效的：  
  
```  
Private objA As Object  
Static objB As System.Windows.Forms.Label  
Dim objC As System.OperatingSystem  
```  
  
## 后期绑定和早期绑定  
 有时，直到代码运行时才知道特定类。  这种情况下，必须用 `Object` 数据类型声明对象变量。  这会创建对任何类型的对象的常规引用，并在运行时分配特定类。  这称为“后期绑定”。  后期绑定需要附加的执行时间，  它还会将您的代码局限于某个类的方法和属性，该类是您最近为其分配的。  如果您的代码尝试访问其他类的成员，这就可能导致运行时错误。  
  
 当在编译时知道特定类时，应将对象变量声明为属于该类。  这称为*“早期绑定”*。  早期绑定可提高性能并保证您的代码访问特定类的所有方法和属性。  在前面的示例声明中，如果变量 `objA` 只使用 <xref:System.Windows.Forms.Label?displayProperty=fullName> 类的对象，则应在它的声明中指定 `As System.Windows.Forms.Label`。  
  
### 早期绑定的优点  
 将对象变量声明为特定类具有若干优点：  
  
-   自动类型检查  
  
-   保证了对特定类的所有成员的访问  
  
-   代码编辑器中具有 Microsoft IntelliSense 支持  
  
-   改进了代码的可读性  
  
-   代码中的错误更少  
  
-   在编译时而不是运行时捕获错误  
  
-   更快地执行代码  
  
## 访问对象变量成员  
 当 `Option Strict` 处于 `On` 状态时，对象变量只能访问用于声明它的类的方法和属性。  下面的示例阐释了这一点。  
  
```  
' Option statements must precede all other source file lines.  
Option Strict On  
' Imports statement must precede all declarations in the source file.  
Imports System.Windows.Forms  
Public Sub accessMembers()  
    Dim p As Object  
    Dim q As System.Windows.Forms.Label  
    p = New System.Windows.Forms.Label  
    q = New System.Windows.Forms.Label  
    Dim j, k As Integer  
    ' The following statement generates a compiler ERROR.  
    j = p.Left  
    ' The following statement retrieves the left edge of the label in pixels.  
    k = q.Left  
End Sub  
```  
  
 在本示例中，`p` 只能使用 <xref:System.Object> 类本身的成员，其中不包括 `Left` 属性。  另一方面，`q` 被声明为 <xref:System.Windows.Forms.Label> 类型，因此它可以使用 <xref:System.Windows.Forms> 命名空间中 <xref:System.Windows.Forms.Label> 类的所有方法和属性。  
  
## 对象变量的灵活性  
 在处理继承层次结构中的对象时，可以选择使用哪个类来声明对象变量。  在进行这种选择时，必须在对象赋值的灵活性和类成员的可访问性之间权衡。  例如，请考虑通向 <xref:System.Windows.Forms.Form?displayProperty=fullName> 类的继承层次结构：  
  
 <xref:System.Object>  
  
 `` <xref:System.ComponentModel.Component>  
  
 `` <xref:System.Windows.Forms.Control>  
  
 `` <xref:System.Windows.Forms.ScrollableControl>  
  
 `` <xref:System.Windows.Forms.ContainerControl>  
  
 `` <xref:System.Windows.Forms.Form>  
  
 假设应用程序定义了一个从 <xref:System.Windows.Forms.Form> 类继承的名为 `specialForm` 的窗体类。  可以声明一个专门引用 `specialForm` 的对象变量，如下例所示。  
  
<CodeContentPlaceHolder>3</CodeContentPlaceHolder>  
 前面示例中的声明将变量 `nextForm` 限制为 `specialForm` 类的对象，但也使得以下两项可用于 `nextForm`：一是 `specialForm` 的所有方法和属性；二是 `specialForm` 从中继承的所有类的所有成员。  
  
 可以将对象变量声明为 <xref:System.Windows.Forms.Form> 类型，使之更加通用，如下例所示。  
  
<CodeContentPlaceHolder>4</CodeContentPlaceHolder>  
 通过前面示例中的声明，可以将应用程序中的任何窗体赋值给 `anyForm`。  但是，虽然 `anyForm` 可以访问 <xref:System.Windows.Forms.Form> 类的所有成员，但它无法使用为 `specialForm` 等特定窗体定义的任何其他方法或属性。  
  
 基类的所有成员均可用于派生类，但是派生类的其他成员不可用于基类。  
  
## 请参阅  
 [对象变量](../../../../visual-basic/programming-guide/language-features/variables/object-variables.md)   
 [对象变量赋值](../../../../visual-basic/programming-guide/language-features/variables/object-variable-assignment.md)   
 [对象变量值](../../../../visual-basic/programming-guide/language-features/variables/object-variable-values.md)   
 [如何：在 Visual Basic 中声明对象变量并为它分配对象](../../../../visual-basic/programming-guide/language-features/variables/how-to-declare-an-object-variable-and-assign-an-object-to-it.md)   
 [如何：访问对象的成员](../../../../visual-basic/programming-guide/language-features/variables/how-to-access-members-of-an-object.md)   
 [New 运算符](../../../../visual-basic/language-reference/operators/new-operator.md)   
 [Option Strict 语句](../../../../visual-basic/language-reference/statements/option-strict-statement.md)   
 [局部类型推理](../../../../visual-basic/programming-guide/language-features/variables/local-type-inference.md)