---
title: "如何：使用对象初始值设定项声明对象 (Visual Basic) | Microsoft Docs"
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
  - "使用对象初始值设定项声明对象"
  - "初始值设定项 [Visual Basic]"
  - "对象初始值设定项 [Visual Basic]"
  - "视频帮助, Visual Basic"
ms.assetid: 0f53a553-efd6-466d-80bf-6b679e5cd174
caps.latest.revision: 20
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 20
---
# 如何：使用对象初始值设定项声明对象 (Visual Basic)
[!INCLUDE[vs2017banner](../../../../visual-basic/includes/vs2017banner.md)]

使用对象初始值设定项可以在单个语句中声明并实例化类的实例。  此外，还可以同时初始化该实例的一个或多个成员，而无需调用参数化构造函数。  
  
 使用对象初始值设定项创建命名类型的实例时，将调用类的默认构造函数，然后按指定顺序初始化指定的成员。  
  
 下面的过程演示如何以三种不同方式创建 `Student` 类的实例。  该类具有名字、姓氏和年级等属性。  三个声明各自创建 `Student` 的一个新实例，并且将属性 `First` 设置为“Michael”，将属性 `Last` 设置为“Tucker”，将所有其他成员设置为各自的默认值。  过程中每个声明的结果等效于下面的示例，该示例未使用对象初始值设定项。  
  
 [!code-vb[VbVbalrObjectInit#20](../../../../visual-basic/programming-guide/language-features/objects-and-classes/codesnippet/VisualBasic/how-to-declare-an-object-by-using-an-object-initializer_1.vb)]  
  
 有关 `Student` 类的实现，请参见[How to: Create a List of Items](../../../../visual-basic/programming-guide/concepts/linq/how-to-create-a-list-of-items.md)。  您可以从该主题中复制代码来设置类以及创建要使用的 `Student` 对象列表。  
  
### 使用对象初始值设定项创建命名类的对象  
  
1.  就像您计划使用构造函数一样开始声明。  
  
     `Dim student1 As New Student`  
  
2.  键入关键字 `With`，后面跟一个括在大括号内的初始化列表。  
  
     `Dim student1 As New Student With { <initialization list> }`  
  
3.  在初始化列表中包含要初始化并向其分配初始值的每个属性。  属性名称以句点开头。  
  
     [!code-vb[VbVbalrObjectInit#21](../../../../visual-basic/programming-guide/language-features/objects-and-classes/codesnippet/VisualBasic/how-to-declare-an-object-by-using-an-object-initializer_2.vb)]  
  
     您可以初始化类的一个或多个成员。  
  
4.  或者，可以声明类的新实例，然后为其赋值。  首先，声明一个 `Student` 实例：  
  
     `Dim student2 As Student`  
  
5.  以常规方式开始创建 `Student` 的实例。  
  
     `Dim student2 As Student = New Student`  
  
6.  依次键入 `With` 和对象初始值设定项，以初始化新实例的一个或多个成员。  
  
     [!code-vb[VbVbalrObjectInit#22](../../../../visual-basic/programming-guide/language-features/objects-and-classes/codesnippet/VisualBasic/how-to-declare-an-object-by-using-an-object-initializer_3.vb)]  
  
7.  可以省略 `As Student` 以简化上一步中的定义。  如果这样做，编译器将使用局部类型推理来确定 `student3` 是 `Student` 的实例。  
  
     [!code-vb[VbVbalrObjectInit#23](../../../../visual-basic/programming-guide/language-features/objects-and-classes/codesnippet/VisualBasic/how-to-declare-an-object-by-using-an-object-initializer_4.vb)]  
  
     有关更多信息，请参见[局部类型推理](../../../../visual-basic/programming-guide/language-features/variables/local-type-inference.md)。  
  
## 请参阅  
 [局部类型推理](../../../../visual-basic/programming-guide/language-features/variables/local-type-inference.md)   
 [How to: Create a List of Items](../../../../visual-basic/programming-guide/concepts/linq/how-to-create-a-list-of-items.md)   
 [对象初始值设定项：命名类型和匿名类型](../../../../visual-basic/programming-guide/language-features/objects-and-classes/object-initializers-named-and-anonymous-types.md)   
 [匿名类型](../../../../visual-basic/programming-guide/language-features/objects-and-classes/anonymous-types.md)