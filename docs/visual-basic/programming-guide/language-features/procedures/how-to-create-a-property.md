---
title: "如何：创建属性 (Visual Basic) | Microsoft Docs"
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
  - "过程, 定义"
  - "属性 [Visual Basic]"
  - "Visual Basic 代码, 过程"
  - "Visual Basic 代码, 属性"
ms.assetid: 4d229712-6be8-4c5c-bac5-06995ce9185a
caps.latest.revision: 15
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 15
---
# 如何：创建属性 (Visual Basic)
[!INCLUDE[vs2017banner](../../../../visual-basic/includes/vs2017banner.md)]

属性定义位于 `Property` 语句和 `End Property` 语句之间。  在此定义中，可以定义 `Get` 过程、`Set` 过程，或者同时定义两者。  属性的所有代码均位于这些过程内。  
  
 `Get` 过程检索属性的值，`Set` 过程存储一个值。  如果想要属性可读和可写，这两个过程都必须定义。  对于只读属性，只需定义 `Get`，对于只写属性，只需定义 `Set`。  
  
### 创建属性  
  
1.  在任何属性或过程之外，使用一条 [Property 语句](../../../../visual-basic/language-reference/statements/property-statement.md) 语句，后跟一条 `End Property` 语句。  
  
2.  如果属性带有参数，则在 `Property` 关键字后接该过程的名称，然后是置于括号中的参数列表。  
  
3.  在括号后使用一个 `As` 子句，以指定属性值的数据类型。  即使对于只写属性也必须指定数据类型。  
  
4.  根据相应的情况，添加 `Get` 和 `Set` 过程。  请参见以下说明。  
  
### 创建检索属性值的 Get 过程  
  
1.  在 `Property` 和 `End Property` 语句之间，加入一条 [Get 语句](../../../../visual-basic/language-reference/statements/get-statement.md) 语句，后跟一条 `End Get` 语句。  无需为 `Get` 过程定义任何参数。  
  
2.  在 `Get` 和 `End Get` 语句之间放置检索属性值的代码语句。  除了生成和返回属性的值之外，该代码还可以包括其他计算和数据操作。  
  
3.  使用 `Return` 语句可将属性的值返回到调用代码。  
  
 对于读写属性和只读属性，必须编写一个 `Get` 过程。  对于只写属性，无需定义 `Get` 过程。  
  
### 创建写入属性值的 Set 过程  
  
1.  在 `Property` 和 `End Property` 之间，加入一条 [Set 语句](../../../../visual-basic/language-reference/statements/set-statement.md) 语句，然后加入一条 `End Set` 语句。  
  
2.  在 `Set` 语句中，参数列表置于 `Set` 关键字后面的括号中。  该参数列表至少必须包括一个值参数，该参数的值由调用代码传递。  该值参数的默认名称为 `Value`，但是如果需要，也可以使用其他名称。  值参数的数据类型必须与属性本身相同。  
  
3.  用于将值存储在属性中的代码语句放在 `Set` 和 `End Set` 语句之间。  除了验证和存储属性值之外，该代码还可以包括其他计算和数据操作。  
  
4.  使用值参数接受调用代码提供的值。  可以直接通过赋值语句存储该值，或者在表达式中使用它计算出要存储的内部值。  
  
 对于读写属性和只写属性，必须编写一个 `Set` 过程。  对于只读属性，无需定义 `Set` 过程。  
  
## 示例  
 下面的示例创建一个读\/写属性，将一个全名存储为两个组成部分（名和姓）。  当调用代码读取 `fullName` 时，`Get` 过程将姓名的两个组成部分组合在一起，并返回全名。  当调用代码赋予一个新的全名时，`Set` 过程尝试将其分割为姓名的两个组成部分。  如果它没有找到空格，它将整个名称存储为名。  
  
 [!code-vb[VbVbcnProcedures#8](./codesnippet/VisualBasic/how-to-create-a-property_1.vb)]  
  
 下面的示例演示对 `fullName` 属性过程的典型调用。  第一个调用设置属性值，第二个调用检索该值。  
  
 [!code-vb[VbVbcnProcedures#9](./codesnippet/VisualBasic/how-to-create-a-property_2.vb)]  
  
## 请参阅  
 [过程](../../../../visual-basic/programming-guide/language-features/procedures/index.md)   
 [Property 过程](../../../../visual-basic/programming-guide/language-features/procedures/property-procedures.md)   
 [过程参数和自变量](../../../../visual-basic/programming-guide/language-features/procedures/procedure-parameters-and-arguments.md)   
 [Visual Basic 中属性和变量的差异](../../../../visual-basic/programming-guide/language-features/procedures/differences-between-properties-and-variables.md)   
 [如何：声明具有混合访问级别的属性](../../../../visual-basic/programming-guide/language-features/procedures/how-to-declare-a-property-with-mixed-access-levels.md)   
 [如何：调用 Property 过程](../../../../visual-basic/programming-guide/language-features/procedures/how-to-call-a-property-procedure.md)   
 [如何：在 Visual Basic 中声明和调用默认属性](../../../../visual-basic/programming-guide/language-features/procedures/how-to-declare-and-call-a-default-property.md)   
 [如何：在属性中放置值](../../../../visual-basic/programming-guide/language-features/procedures/how-to-put-a-value-in-a-property.md)   
 [如何：从属性获取值](../../../../visual-basic/programming-guide/language-features/procedures/how-to-get-a-value-from-a-property.md)