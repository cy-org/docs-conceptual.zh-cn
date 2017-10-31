---
title: "其他数据类型 (Visual Basic 中) |Microsoft 文档"
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
- Object data type, data types
- data types [Visual Basic], choosing
ms.assetid: 64c71a12-9057-4dbf-baca-7379c4aada69
caps.latest.revision: 22
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
ms.openlocfilehash: 2de377fa9dfd7ec13cdbb9b700f8485b0c0e2106
ms.lasthandoff: 03/13/2017

---
# <a name="miscellaneous-data-types-visual-basic"></a>其他数据类型 (Visual Basic)
[!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)]提供几个不是针对数字或字符的数据类型。 相反，它们处理专用数据如是/否值、 日期/时间值和对象地址。  
  
 显示通过并行进行比较的表为[!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)]数据类型，请参阅[数据类型](../../../../visual-basic/language-reference/data-types/data-type-summary.md)。  
  
## <a name="boolean-type"></a>布尔值类型  
 [布尔数据类型](../../../../visual-basic/language-reference/data-types/boolean-data-type.md)是解释为无符号的值`True`或`False`。 其数据宽度取决于实现的平台。 如果一个变量可以包含如 true/false 时，只有两种状态值是/否，或打开/关闭，将其声明为`Boolean`。  
  
## <a name="date-type"></a>日期类型  
 [Date 数据类型](../../../../visual-basic/language-reference/data-types/date-data-type.md)是包含日期和时间信息的 64 位值。 每个增量之初 (12:00 AM) 表示已用时间的 100 纳的秒的 1 公历日历中每 1 年月 1 日。 如果日期值和 / 或时间值，可以包含一个变量，将其声明为`Date`。  
  
## <a name="object-type"></a>对象类型  
 [Object 数据类型](../../../../visual-basic/language-reference/data-types/object-data-type.md)是指向对象实例在您的应用程序或其他一些应用程序中的 32 位地址。 `Object`变量可引用的应用程序识别，任何对象或对任何数据类型的数据。 这包括这两个*值类型*，如`Integer`， `Boolean`，以及结构的实例，并*引用类型*，后者是如从类创建的对象的实例`String`和<xref:System.Windows.Forms.Form>，以及数组实例。</xref:System.Windows.Forms.Form>  
  
 如果一个变量存储在编译时，不知道您的类的实例的指针，或者它可以指向各种数据类型的数据，将其声明为`Object`。  
  
 利用`Object`数据类型是，可以使用它来存储任何数据类型的数据。 其缺点在于，您会产生额外的操作，需要更多的执行时间，使得应用程序执行速度慢。 如果您使用`Object`对于值类型变量，则会导致*装箱*和*取消装箱*。 如果您将它用于引用类型，则会引发*后期绑定*。  
  
## <a name="see-also"></a>另请参阅  
 [类型字符](../../../../visual-basic/programming-guide/language-features/data-types/type-characters.md)   
 [基本数据类型](../../../../visual-basic/programming-guide/language-features/data-types/elementary-data-types.md)   
 [数值数据类型](../../../../visual-basic/programming-guide/language-features/data-types/numeric-data-types.md)   
 [字符数据类型](../../../../visual-basic/programming-guide/language-features/data-types/character-data-types.md)   
 [数据类型疑难解答](../../../../visual-basic/programming-guide/language-features/data-types/troubleshooting-data-types.md)   
 [早期绑定和后期绑定](../../../../visual-basic/programming-guide/language-features/early-late-binding/index.md)
