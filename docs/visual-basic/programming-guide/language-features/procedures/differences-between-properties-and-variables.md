---
title: "Visual Basic 中属性和变量的差异 | Microsoft Docs"
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
  - "属性 [Visual Basic], 和变量"
  - "属性 [Visual Basic], 已定义"
  - "属性 [Visual Basic], values"
  - "属性值"
  - "values, 属性"
  - "变量 [Visual Basic]"
  - "变量 [Visual Basic], 和属性"
  - "变量 [Visual Basic], 定义"
  - "Visual Basic 代码, 过程"
  - "Visual Basic 代码, 属性"
  - "Visual Basic 代码, 变量"
ms.assetid: 7a03a8be-5381-431f-bd7c-16e887e4e07b
caps.latest.revision: 14
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 14
---
# Visual Basic 中属性和变量的差异
[!INCLUDE[vs2017banner](../../../../visual-basic/includes/vs2017banner.md)]

变量和属性都表示可以访问的值。  但在存储和实现方面有所不同。  
  
## 变量  
 “变量”直接对应于内存位置。  可以使用单个声明语句定义变量。  变量可以是“局部变量”，在过程中定义且仅可用于该过程；它也可以是“成员变量”，在模块、类或结构中定义，但不在任何过程中定义。  成员变量又称“字段”。  
  
## 属性  
 “属性”是在模块、类或结构中定义的数据元素。  使用 `Property` 和 `End Property` 语句之间的代码块定义属性。  此代码块包含一个 `Get` 过程或一个 `Set` 过程，或两者都包含。  这两个过程称为“属性过程”或“属性访问器”。  除了检索或存储属性的值外，它们还可以执行自定义操作，如更新访问计数器。  
  
## 不同点  
 下表指出了变量和属性之间的一些重要差异。  
  
|差异点|变量|属性|  
|---------|--------|--------|  
|声明|单个声明语句|代码块中的一系列语句|  
|实现|单个存储位置|可执行代码（属性过程）|  
|存储|直接与变量的值关联|通常包含内部存储；在属性的包含类或模块外部，这些内部存储不可用<br /><br /> 属性的值可能作为也可能不作为一个存储元素<sup>1</sup>存在|  
|可执行代码|无|至少必须有一个过程|  
|读写访问权限|读\/写或只读|读\/写、只读或只写|  
|自定义操作（接受或返回值以外）|不可能|可以当作部分设置或检索属性值执行|  
  
 <sup>1</sup> 和变量不同，属性的值可能不直接对应于单个存储项。  为方便或安全起见，存储可能拆分为几块；也可能以加密格式存储值。  在这些情况下，`Get` 过程将汇编这些块或解密存储值，然后 `Set` 过程会加密新值或将其拆分到构成存储的各个组成部分中。  属性值可以是临时的，如一天中的某个时间，在这种情况下，每次访问此属性时，`Get` 过程将及时计算此属性。  
  
## 请参阅  
 [Property 过程](../../../../visual-basic/programming-guide/language-features/procedures/property-procedures.md)   
 [过程参数和自变量](../../../../visual-basic/programming-guide/language-features/procedures/procedure-parameters-and-arguments.md)   
 [Property 语句](../../../../visual-basic/language-reference/statements/property-statement.md)   
 [Dim 语句](../../../../visual-basic/language-reference/statements/dim-statement.md)   
 [如何：创建属性](../../../../visual-basic/programming-guide/language-features/procedures/how-to-create-a-property.md)   
 [如何：声明具有混合访问级别的属性](../../../../visual-basic/programming-guide/language-features/procedures/how-to-declare-a-property-with-mixed-access-levels.md)   
 [如何：调用 Property 过程](../../../../visual-basic/programming-guide/language-features/procedures/how-to-call-a-property-procedure.md)   
 [如何：在 Visual Basic 中声明和调用默认属性](../../../../visual-basic/programming-guide/language-features/procedures/how-to-declare-and-call-a-default-property.md)   
 [如何：在属性中放置值](../../../../visual-basic/programming-guide/language-features/procedures/how-to-put-a-value-in-a-property.md)   
 [如何：从属性获取值](../../../../visual-basic/programming-guide/language-features/procedures/how-to-get-a-value-from-a-property.md)