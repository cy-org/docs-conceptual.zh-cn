---
title: "结构变量 (Visual Basic) | Microsoft Docs"
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
  - "结构变量"
  - "结构, 结构变量"
  - "结构, 变量"
  - "变量 [Visual Basic], 结构变量"
ms.assetid: 156872f8-aabc-4454-8e2d-f2253c3c13c9
caps.latest.revision: 11
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 11
---
# 结构变量 (Visual Basic)
[!INCLUDE[vs2017banner](../../../../visual-basic/includes/vs2017banner.md)]

创建了结构后，可以声明程序级和模块级变量作为该类型。  例如，您可以创建结构有关记录计算机系统信息的。  下面的示例演示此过程。  
  
```  
Public Structure systemInfo  
    Public cPU As String  
    Public memory As Long  
    Public purchaseDate As Date  
End Structure  
```  
  
 现在可以声明该类型的变量。  下面的声明阐释了这一点。  
  
```  
Dim mySystem, yourSystem As systemInfo  
```  
  
> [!NOTE]
>  在类和模块中，使用声明的结构 [Dim 语句](../../../../visual-basic/language-reference/statements/dim-statement.md) 默认为公共访问。  如果希望结构为私有的，使用关键字，请确保将其声明 [Private](../../../../visual-basic/language-reference/modifiers/private.md) 为。  
  
## 对结构值的访问  
 若要从结构变量的元素中赋值和检索值，请使用与您使用设置和获取对象属性的语法。  将成员访问运算符 \(`.`\) 在结构变量名称和元素名称之间。  先前声明为类型的变量下面的示例访问组件 `systemInfo`。  
  
```  
mySystem.cPU = "486"  
Dim tooOld As Boolean  
If yourSystem.purchaseDate < #1/1/1992# Then tooOld = True  
```  
  
## 结构变量赋值  
 例如，如果两个结构类型相同，也可以将一个变量赋给另一个。  这将一结构中的所有元素对其他任何对应的元素。  下面的声明阐释了这一点。  
  
```  
yourSystem = mySystem  
```  
  
 如果结构元素是引用类型，如 `String`、 `Object`或数组，指向数据的指针被复制。  在前面的示例中，，如果 `systemInfo` 包括了一个对象变量，然后前面的示例中复制 `mySystem` 的指针。 `yourSystem`，因此，对对象数据的更改传递一个结构实际上是访问时，通过另一结构。  
  
## 请参阅  
 [数据类型](../../../../visual-basic/programming-guide/language-features/data-types/index.md)   
 [基本数据类型](../../../../visual-basic/programming-guide/language-features/data-types/elementary-data-types.md)   
 [复合数据类型](../../../../visual-basic/programming-guide/language-features/data-types/composite-data-types.md)   
 [值类型和引用类型](../../../../visual-basic/programming-guide/language-features/data-types/value-types-and-reference-types.md)   
 [结构](../../../../visual-basic/programming-guide/language-features/data-types/structures.md)   
 [数据类型疑难解答](../../../../visual-basic/programming-guide/language-features/data-types/troubleshooting-data-types.md)   
 [如何：声明结构](../../../../visual-basic/programming-guide/language-features/data-types/how-to-declare-a-structure.md)   
 [结构和其他编程元素](../../../../visual-basic/programming-guide/language-features/data-types/structures-and-other-programming-elements.md)   
 [结构和类](../../../../visual-basic/programming-guide/language-features/data-types/structures-and-classes.md)   
 [Structure 语句](../../../../visual-basic/language-reference/statements/structure-statement.md)