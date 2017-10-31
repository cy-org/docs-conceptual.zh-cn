---
title: "结构和其他编程元素 (Visual Basic) | Microsoft Docs"
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
  - "数组 [Visual Basic], 结构元素"
  - "嵌套结构"
  - "对象 [Visual Basic], 结构元素"
  - "过程, 作为参数的结构"
  - "结构, 数组"
ms.assetid: 0f849313-ccd2-4c9a-acb9-69de6751c088
caps.latest.revision: 13
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 13
---
# 结构和其他编程元素 (Visual Basic)
[!INCLUDE[vs2017banner](../../../../visual-basic/includes/vs2017banner.md)]

可以将结构与数组、对象和程序一起，以及其他。  交互使用与这些元素单独使用的语法。  
  
> [!NOTE]
>  无法初始化任何一个在结构声明的结构元素。  只能将值分配给声明为结构类型的变量的元素。  
  
## 结构和数组  
 结构可以包含数组作为它的一个或多个元素。  下面的示例阐释了这一点。  
  
```vb#  
Public Structure systemInfo  
    Public cPU As String  
    Public memory As Long  
    Public diskDrives() As String  
    Public purchaseDate As Date  
End Structure   
```  
  
 您访问一个结构内数组的值的方式与访问对象的属性。  下面的示例阐释了这一点。  
  
```vb#  
Dim mySystem As systemInfo  
ReDim mySystem.diskDrives(3)  
mySystem.diskDrives(0) = "1.44 MB"  
```  
  
 还可以声明结构数组。  下面的示例阐释了这一点。  
  
```vb#  
Dim allSystems(100) As systemInfo  
```  
  
 要遵循相同的规则访问此数据结构元素。  下面的示例阐释了这一点。  
  
```vb#  
ReDim allSystems(5).diskDrives(3)  
allSystems(5).CPU = "386SX"  
allSystems(5).diskDrives(2) = "100M SCSI"  
```  
  
## 结构和对象  
 结构可以包含对象作为它的一个或多个元素。  下面的示例阐释了这一点。  
  
```vb#  
Protected Structure userInput  
    Public userName As String  
    Public inputForm As System.Windows.Forms.Form  
    Public userFileNumber As Integer  
End Structure  
```  
  
 在这样的声明中使用特定的对象类，而不是 `Object`。  
  
## 结构和过程  
 可以将结构作为过程参数。  下面的示例阐释了这一点。  
  
```vb#  
Public currentCPUName As String = "700MHz Pentium compatible"  
Public currentMemorySize As Long = 256  
Public Sub fillSystem(ByRef someSystem As systemInfo)  
    someSystem.cPU = currentCPUName  
    someSystem.memory = currentMemorySize  
    someSystem.purchaseDate = Now  
End Sub  
```  
  
 前面的示例通过 *引用*来传递结构，这允许过程修改其元素，以使更改生效在调用代码中。  如果要保护结构避免这种修改，将它值。  
  
 还可以从返回 `Function` 程序的结构。  下面的示例阐释了这一点。  
  
```vb#  
Dim allSystems(100) As systemInfo  
Function findByDate(ByVal searchDate As Date) As systemInfo  
    Dim i As Integer  
    For i = 1 To 100  
        If allSystems(i).purchaseDate = searchDate Then Return allSystems(i)  
    Next i  
   ' Process error: system with desired purchase date not found.  
End Function  
```  
  
## 结构中的结构  
 结构可以包含其他结构。  下面的示例阐释了这一点。  
  
```vb#  
Public Structure driveInfo  
    Public type As String  
    Public size As Long  
End Structure  
Public Structure systemInfo  
    Public cPU As String  
    Public memory As Long  
    Public diskDrives() As driveInfo  
    Public purchaseDate As Date  
End Structure  
```  
  
```vb#  
Dim allSystems(100) As systemInfo  
ReDim allSystems(1).diskDrives(3)  
allSystems(1).diskDrives(0).type = "Floppy"  
```  
  
 也可以使用此方法封装在另的模块中定义的结构中的一个模块中定义的结构。  
  
 结构可以包含其他结构到任意深度。  
  
## 请参阅  
 [数据类型](../../../../visual-basic/programming-guide/language-features/data-types/index.md)   
 [基本数据类型](../../../../visual-basic/programming-guide/language-features/data-types/elementary-data-types.md)   
 [复合数据类型](../../../../visual-basic/programming-guide/language-features/data-types/composite-data-types.md)   
 [值类型和引用类型](../../../../visual-basic/programming-guide/language-features/data-types/value-types-and-reference-types.md)   
 [结构](../../../../visual-basic/programming-guide/language-features/data-types/structures.md)   
 [数据类型疑难解答](../../../../visual-basic/programming-guide/language-features/data-types/troubleshooting-data-types.md)   
 [如何：声明结构](../../../../visual-basic/programming-guide/language-features/data-types/how-to-declare-a-structure.md)   
 [结构变量](../../../../visual-basic/programming-guide/language-features/data-types/structure-variables.md)   
 [结构和类](../../../../visual-basic/programming-guide/language-features/data-types/structures-and-classes.md)   
 [Structure 语句](../../../../visual-basic/language-reference/statements/structure-statement.md)