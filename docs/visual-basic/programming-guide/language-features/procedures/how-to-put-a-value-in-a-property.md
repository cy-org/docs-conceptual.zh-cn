---
title: "如何︰ 将值放属性 (Visual Basic 中) |Microsoft 文档"
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
- property values
- Visual Basic code, procedures
- values, properties
- Visual Basic code, properties
- properties [Visual Basic], values
ms.assetid: c39401e5-b5fc-4439-8f31-ed640f7ce6ed
caps.latest.revision: 13
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
ms.openlocfilehash: e3b2336589b525756a92cb3e26ab6c1950118b01
ms.lasthandoff: 03/13/2017

---
# <a name="how-to-put-a-value-in-a-property-visual-basic"></a>如何：在属性中放置值 (Visual Basic)
通过将属性名称放在赋值语句的左侧，可以在属性中存储一个值。  
  
 该属性的`Set`过程存储一个值，但并不按名称显式调用它。 就像您使用一个变量，您可以使用该属性。 [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)]调用该属性的过程。  
  
### <a name="to-store-a-value-in-a-property"></a>在属性中存储的值  
  
1.  在赋值语句左侧使用的属性名称。  
  
     下面的示例设置的值[!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)]`TimeOfDay`属性设置为中午，隐式调用其`Set`过程。  
  
     [!code-vb[VbVbcnProcedures #&11;](./codesnippet/VisualBasic/how-to-put-a-value-in-a-property_1.vb)]  
  
2.  如果该属性接受参数，请按照用括号括起的参数列表的属性名称。 如果不有任何参数，可以选择省略括号。  
  
3.  将参数放在括号内，用逗号分隔参数列表中。 请确保您的属性定义的相应参数的相同顺序的参数提供。  
  
4.  生成的赋值语句右侧的值存储在该属性。  
  
## <a name="see-also"></a>另请参阅  
 <xref:Microsoft.VisualBasic.DateAndTime.TimeOfDay%2A></xref:Microsoft.VisualBasic.DateAndTime.TimeOfDay%2A>   
 [属性过程](./property-procedures.md)   
 [过程参数和变量](./procedure-parameters-and-arguments.md)   
 [Property 语句](../../../../visual-basic/language-reference/statements/property-statement.md)   
 [在 Visual Basic 中属性和变量之间的差异](./differences-between-properties-and-variables.md)   
 [如何︰ 创建属性](./how-to-create-a-property.md)   
 [如何︰ 声明具有混合的访问级别的属性](./how-to-declare-a-property-with-mixed-access-levels.md)   
 [如何︰ 调用 Property 过程](./how-to-call-a-property-procedure.md)   
 [如何︰ 声明和调用默认属性在 Visual Basic 中](./how-to-declare-and-call-a-default-property.md)   
 [如何：从属性获取值](./how-to-get-a-value-from-a-property.md)
