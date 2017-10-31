---
title: "Object 数据类型 | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
f1_keywords: 
  - "vb.Object"
  - "vb.Variant"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "数据类型 [Visual Basic], 分配"
  - "Object 数据类型"
  - "Object 数据类型, 参考"
  - "对象变量, 对象类型"
ms.assetid: 61ea4a7c-3b3d-48d4-adc4-eacfa91779b2
caps.latest.revision: 19
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 19
---
# Object 数据类型
[!INCLUDE[vs2017banner](../../../visual-basic/includes/vs2017banner.md)]

保存引用对象的地址。  可以为 `Object` 的变量分配任何引用类型（字符串、数组、类或接口）。  `Object` 变量还可以引用任何值类型（数值、`Boolean`、`Char`、`Date`、结构或枚举）的数据。  
  
## 备注  
 `Object` 数据类型可以指向任意数据类型的数据，包括您的应用程序识别的任意对象实例。  当您在编译时不知道变量可能指向哪种数据类型时，请使用 `Object`。  
  
 `Object` 的默认值为 `Nothing`（null 引用）。  
  
## 数据类型  
 可以将任何数据类型的变量、常数或表达式赋给 `Object` 变量。  若要确定 `Object` 变量当前引用的数据类型，您可以使用 <xref:System.Type?displayProperty=fullName> 类的 <xref:System.Type.GetTypeCode%2A> 方法。  下面的示例阐释了这一点。  
  
```  
Dim myObject As Object  
' Suppose myObject has now had something assigned to it.  
Dim datTyp As Integer  
datTyp = Type.GetTypeCode(myObject.GetType())  
```  
  
 `Object` 数据类型为引用类型。  但是，当 `Object` 变量引用值类型的数据时，Visual Basic 将此变量视为一个值类型。  
  
## 存储  
 无论它引用什么数据类型，`Object` 变量都不包含数据值本身，而是指向该值的一个指针。  它总是在计算机内存中使用四个字节，但这不包括表示变量值的数据的存储。  由于使用指针定位数据的代码的缘故，访问持有值类型的 `Object` 变量比访问显式声明类型的变量速度稍慢。  
  
## 编程提示  
  
-   **互操作注意事项。**如果您正连接到不是为 .NET Framework 编写的组件，例如 Automation 或 COM 对象，请记住其他环境中的指针类型与 Visual Basic `Object` 类型不兼容。  
  
-   **性能。**用 `Object` 类型声明的变量足够灵活，可以包含对任何对象的引用。  但是，在这样一个变量上调用方法或属性时，总是会遇到*后期绑定*（在运行时）。  若要强制*前期绑定*（在编译时）和提高性能，请用特定的类名称声明变量，或将它强制转换为特定数据类型。  
  
     当您声明一个对象变量时，请尝试使用特定的类类型，例如 <xref:System.OperatingSystem>，而不是普通的 `Object` 类型。  还应使用可用的最具体的类，例如 <xref:System.Windows.Forms.TextBox> 而不是 <xref:System.Windows.Forms.Control>，这样就可以访问其属性和方法。  通常可以使用**“对象浏览器”**中的**“类”**列表来查找可用的类名。  
  
-   **扩大。**所有数据类型和所有引用类型均扩大至 `Object` 数据类型。  这意味着您可以将任意类型转换为 `Object`，而不会遇到 <xref:System.OverflowException?displayProperty=fullName> 错误。  
  
     但是，如果您在值类型和 `Object` 之间转换，Visual Basic 会执行称为*装箱*和*取消装箱*的操作，这将减慢执行速度。  
  
-   **类型字符。** `Object` 不包含文本类型字符或标识符类型字符。  
  
-   **Framework 类型。**.NET Framework 中的对应类型是 <xref:System.Object?displayProperty=fullName> 类。  
  
## 示例  
 下面的示例演示一个 `Object` 变量，它指向一个对象实例。  
  
```  
Dim objDb As Object  
Dim myCollection As New Collection()  
' Suppose myCollection has now been populated.  
objDb = myCollection.Item(1)  
```  
  
## 请参阅  
 <xref:System.Object>   
 [数据类型](../../../visual-basic/language-reference/data-types/data-type-summary.md)   
 [类型转换函数](../../../visual-basic/language-reference/functions/type-conversion-functions.md)   
 [转换摘要](../../../visual-basic/language-reference/keywords/conversion-summary.md)   
 [有效使用数据类型](../../../visual-basic/programming-guide/language-features/data-types/efficient-use-of-data-types.md)   
 [如何：确定两个对象是否相关](../../../visual-basic/programming-guide/language-features/variables/how-to-determine-whether-two-objects-are-related.md)   
 [如何：确定两个对象是否相同](../../../visual-basic/programming-guide/language-features/variables/how-to-determine-whether-two-objects-are-identical.md)