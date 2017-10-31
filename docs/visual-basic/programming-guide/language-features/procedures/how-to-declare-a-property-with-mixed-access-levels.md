---
title: "如何：声明具有混合访问级别的属性 (Visual Basic) | Microsoft Docs"
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
  - "访问级别, 属性"
  - "混合访问级别"
  - "过程, 定义"
  - "属性 [Visual Basic], 访问级别"
  - "Property 语句, 声明混合访问级别"
  - "Visual Basic 代码, 过程"
  - "Visual Basic 代码, 属性"
ms.assetid: fdbb2d97-279a-4956-b26c-cbdfbc34915a
caps.latest.revision: 16
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 16
---
# 如何：声明具有混合访问级别的属性 (Visual Basic)
[!INCLUDE[vs2017banner](../../../../visual-basic/includes/vs2017banner.md)]

如果需要属性上的 `Get` 和 `Set` 过程具有不同的访问级别，可以对 `Property` 语句使用更高的许可级别，对 `Get` 或 `Set` 语句使用更高的限制级别。  如果希望代码的某些部分能够获取属性值，而其他某些部分能够更改属性值，则可以在属性上使用混合访问级别。  
  
 有关访问级别的更多信息，请参见 [Visual Basic 中的访问级别](../../../../visual-basic/programming-guide/language-features/declared-elements/access-levels.md)。  
  
### 声明带有混合访问级别的属性  
  
1.  按通常的方法声明属性，在 `Property` 语句中指定较低的限制访问级别（例如 `Public`）。  
  
2.  声明 `Get` 或 `Set` 过程，指定更高的限制访问级别（例如 `Friend`）。  
  
3.  不要在其他属性过程上指定访问级别。  它假定已在 `Property` 语句中声明了访问级别。  可以仅在一个属性过程上限制访问权限。  
  
     [!code-vb[VbVbcnProcedures#10](./codesnippet/VisualBasic/how-to-declare-a-property-with-mixed-access-levels_1.vb)]  
  
     在前面的示例中，`Get` 过程具有与属性自身相同的 `Protected` 访问权限，而 `Set` 过程具有 `Private` 访问权限。  派生自 `employee` 的类可以读取 `salary` 值，但只有 `employee` 类可以对它进行设置。  
  
## 请参阅  
 [过程](../../../../visual-basic/programming-guide/language-features/procedures/index.md)   
 [Property 过程](../../../../visual-basic/programming-guide/language-features/procedures/property-procedures.md)   
 [过程参数和自变量](../../../../visual-basic/programming-guide/language-features/procedures/procedure-parameters-and-arguments.md)   
 [Property 语句](../../../../visual-basic/language-reference/statements/property-statement.md)   
 [Visual Basic 中属性和变量的差异](../../../../visual-basic/programming-guide/language-features/procedures/differences-between-properties-and-variables.md)   
 [如何：创建属性](../../../../visual-basic/programming-guide/language-features/procedures/how-to-create-a-property.md)   
 [如何：调用 Property 过程](../../../../visual-basic/programming-guide/language-features/procedures/how-to-call-a-property-procedure.md)   
 [如何：在 Visual Basic 中声明和调用默认属性](../../../../visual-basic/programming-guide/language-features/procedures/how-to-declare-and-call-a-default-property.md)   
 [如何：在属性中放置值](../../../../visual-basic/programming-guide/language-features/procedures/how-to-put-a-value-in-a-property.md)   
 [如何：从属性获取值](../../../../visual-basic/programming-guide/language-features/procedures/how-to-get-a-value-from-a-property.md)