---
title: "复合数据类型 (Visual Basic 中) |Microsoft 文档"
ms.custom: 
ms.date: 2015-07-20
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology:
- devlang-visual-basic
ms.topic: article
dev_langs:
- VB
helpviewer_keywords:
- classes [Visual Basic], composite data types
- composite types
- composite data types
- data types [Visual Basic], composite
- arrays [Visual Basic], composite data types
- structures, composite data types
- classes [Visual Basic], composite types
- types [Visual Basic], composite
ms.assetid: 62970f2e-52c0-4369-8963-613820f1f434
caps.latest.revision: 19
author: dotnet-bot
ms.author: dotnetcontent
translation.priority.ht:
- cs-cz
- de-de
- es-es
- fr-fr
- it-it
- ja-jp
- ko-kr
- pl-pl
- pt-br
- ru-ru
- tr-tr
- zh-cn
- zh-tw
translationtype: Machine Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: d81b2c08155cb16754e780fdfb341b596322302d
ms.lasthandoff: 03/13/2017

---
# <a name="composite-data-types-visual-basic"></a>复合数据类型 (Visual Basic)
除了基本数据类型[!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)]供应品，你可以还将组合来创建不同类型的项*复合数据类型*如结构、 数组和类。 从基本类型和其他复合类型，您可以构建复合数据类型。 例如，可以具有数组成员中定义的结构元素的数组或结构。  
  
## <a name="data-types"></a>数据类型  
 复合类型是不同于其任意组件的数据类型。 例如，数组的`Integer`元素不属于`Integer`数据类型。  
  
 数组数据类型通常是根据需要使用元素类型、 括号和逗号表示的。 例如的一维数组`String`元素表示为`String()`，和一个二维数组`Boolean`元素表示为`Boolean(,)`。  
  
## <a name="structure-types"></a>结构化类型  
 没有一种数据类型包含所有结构。 相反，每个定义的结构表示唯一的数据类型，即使两个结构定义相同的元素以相同的顺序。 但是，如果创建两个或多个实例相同的结构，[!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)]认为它们是相同的数据类型。  
  
## <a name="array-types"></a>数组类型  
 不存在包含所有数组的单个数据类型。 数组的特定实例的数据类型是由以下方面确定︰  
  
-   确实为数组  
  
-   数组的秩 （维数）  
  
-   数组的元素类型  
  
 具体而言，给定维度的长度不是该实例的数据类型的一部分。 下面的示例阐释了这一点。  
  
```  
Dim arrayA( ) As Byte = New Byte(12) {}  
Dim arrayB( ) As Byte = New Byte(100) {}  
Dim arrayC( ) As Short = New Short(100) {}  
Dim arrayD( , ) As Short  
Dim arrayE( , ) As Short = New Short(4, 10) {}  
```  
  
 在前面的示例中，数组变量`arrayA`和`arrayB`被认为是相同的数据类型 — `Byte()` — 即使它们被初始化为不同的长度也是如此。 变量`arrayB`和`arrayC`不相同类型的因为它们的元素类型不同。 变量`arrayC`和`arrayD`不相同类型的因为它们的秩不同。 变量`arrayD`和`arrayE`具有相同的类型 — `Short(,)` — 因为它们的秩和元素类型是相同的即使`arrayD`尚未初始化。  
  
 在阵列上的详细信息，请参阅[数组](../../../../visual-basic/programming-guide/language-features/arrays/index.md)。  
  
## <a name="class-types"></a>类类型  
 没有一种数据类型组成的所有类。 尽管一个类可以从另一个类继承的每个是单独的数据类型。 同一个类的多个实例是相同的数据类型。 如果将一个类实例变量分配到另一个，不仅它们具有相同的数据类型，它们指向内存中的同一个类实例。  
  
 类的详细信息，请参阅[对象和类](../../../../visual-basic/programming-guide/language-features/objects-and-classes/index.md)。  
  
## <a name="see-also"></a>另请参阅  
 [数据类型](../../../../visual-basic/programming-guide/language-features/data-types/index.md)   
 [基本数据类型](../../../../visual-basic/programming-guide/language-features/data-types/elementary-data-types.md)   
 [Visual Basic 中的泛型类型](../../../../visual-basic/programming-guide/language-features/data-types/generic-types.md)   
 [值类型和引用类型](../../../../visual-basic/programming-guide/language-features/data-types/value-types-and-reference-types.md)   
 [在 Visual Basic 中的类型转换](../../../../visual-basic/programming-guide/language-features/data-types/type-conversions.md)   
 [结构](../../../../visual-basic/programming-guide/language-features/data-types/structures.md)   
 [数据类型疑难解答](../../../../visual-basic/programming-guide/language-features/data-types/troubleshooting-data-types.md)   
 [如何：在一个变量中保存多个值](../../../../visual-basic/programming-guide/language-features/data-types/how-to-hold-more-than-one-value-in-a-variable.md)
