---
title: "如何：在 Visual Basic 中初始化数组变量 | Microsoft Docs"
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
  - "数组 [Visual Basic], 声明"
  - "数组 [Visual Basic], 初始化"
  - "数组 [Visual Basic], 变量"
  - "变量 [Visual Basic], 初始化"
ms.assetid: aadd7a60-7ca4-4608-b986-091f19e7fc10
caps.latest.revision: 42
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 42
---
# 如何：在 Visual Basic 中初始化数组变量
[!INCLUDE[vs2017banner](../../../../visual-basic/includes/vs2017banner.md)]

通过在 `New` 子句中加入数组文本并指定数组的初始值，可以初始化数组变量。  可以指定类型或允许它从数组文本中的值推断出来。  有关如何推断类型的更多信息，请参见 [数组](../../../../visual-basic/programming-guide/language-features/arrays/index.md) 中的“为数组填充初始值”。  
  
### 使用数组文本初始化数组变量  
  
-   可在 `New` 子句中或在为数组赋值时，在大括号 \(`{}`\) 内提供元素值。  下面的示例通过多种方式演示如何声明、创建和初始化一个变量，使其包含一个具有 `Char` 类型元素的数组。  
  
     [!code-vb[VbVbalrArrays#16](../../../../visual-basic/programming-guide/language-features/arrays/codesnippet/VisualBasic/how-to-initialize-an-array-variable_1.vb)]  
  
     执行每个语句后，将创建一个数组，其长度为 3，初始值包含在索引 0 到 2 的元素中。  如果您同时提供了上限和值，则必须为从索引 0 到上限的每个元素都包括一个值。  
  
     请注意，如果在数组文本中提供了元素值，则无需指定索引上限。  如果不指定上限，将根据数组文本中值的数量来推断数组大小。  
  
### 使用数组文本初始化多维数组变量  
  
-   将值放在嵌套的大括号 \(`{}`\) 中。  确保嵌套的数组文本全都推断为类型和长度相同的数组。  下面的代码示例演示了多维数组的几种初始化方式。  
  
     [!code-vb[VbVbalrArrays#17](../../../../visual-basic/programming-guide/language-features/arrays/codesnippet/VisualBasic/how-to-initialize-an-array-variable_2.vb)]  
  
-   可以显式指定数组界限；也可以不指定数组界限，让编译器根据数组文本中的值来推断数组界限。  如果同时提供上限和值，则必须在每一个维度上为从索引 0 到索引上限的每个元素提供一个值。  下面的示例通过多种方式演示如何声明、创建和初始化一个变量，使其包含一个具有 `Short` 类型元素的二维数组。  
  
     [!code-vb[VbVbalrArrays#18](../../../../visual-basic/programming-guide/language-features/arrays/codesnippet/VisualBasic/how-to-initialize-an-array-variable_3.vb)]  
  
     执行每个语句后，将创建一个数组，其中包含六个初始化的元素，它们的索引分别为：`(0,0)`、`(0,1)`、`(0,2)`、`(1,0)`、`(1,1)` 和 `(1,2)`。  每个数组位置都包含值 `10`。  
  
-   下面的示例通过多维数组重复。  在用 Visual Basic 编写的 Windows 控制台应用程序中，将代码粘贴到 `Sub Main()` 方法内部。  最后一个注释显示输出。  
  
     [!code-vb[VbVbalrArrays#31](../../../../visual-basic/programming-guide/language-features/arrays/codesnippet/VisualBasic/how-to-initialize-an-array-variable_4.vb)]  
  
### 使用数组文本初始化交错数组变量  
  
-   将对象值嵌套在大括号 \(`{}`\) 中。  虽然对于交错数组，也可以嵌套指定不同长度数组的数组文本，但请确保将嵌套的数组文本括在小括号 \(`()`\) 中。  小括号将强制对嵌套的数组文本求值，得到的数组将用作交错数组的初始值。  下面的代码示例演示了交错数组的两种初始化方式。  
  
     [!code-vb[VbVbalrArrays#19](../../../../visual-basic/programming-guide/language-features/arrays/codesnippet/VisualBasic/how-to-initialize-an-array-variable_5.vb)]  
  
-   下面的示例通过交错数组重复。  在用 Visual Basic 编写的 Windows 控制台应用程序中，将代码粘贴到 `Sub Main()` 方法内部。代码中的最后一个注释显示输出。  
  
     [!code-vb[VbVbalrArrays#32](../../../../visual-basic/programming-guide/language-features/arrays/codesnippet/VisualBasic/how-to-initialize-an-array-variable_6.vb)]  
  
## 请参阅  
 [数组](../../../../visual-basic/programming-guide/language-features/arrays/index.md)   
 [数组疑难解答](../../../../visual-basic/programming-guide/language-features/arrays/troubleshooting-arrays.md)