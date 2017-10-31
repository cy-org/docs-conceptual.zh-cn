---
title: "已声明元素的特性 (Visual Basic) | Microsoft Docs"
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
  - "访问级别, 已声明的元素"
  - "数据类型 [Visual Basic], 已声明的元素"
  - "已声明的元素, 访问级别"
  - "已声明的元素, 生存期"
  - "已声明的元素, 范围"
  - "已声明的元素, 可见性"
  - "元素, 编程"
  - "生存期, 已声明的元素"
  - "范围, 已声明的元素"
  - "可见性, 已声明的元素"
ms.assetid: 1bc40fb8-b67c-4428-90a4-76b630ae2583
caps.latest.revision: 16
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 16
---
# 已声明元素的特性 (Visual Basic)
[!INCLUDE[vs2017banner](../../../../visual-basic/includes/vs2017banner.md)]

已声明元素的“特性”是该元素影响代码可以如何与自己进行交互的方面。  每个已声明元素都具有以下一个或多个与之关联的特性：  
  
-   数据类型 \- 元素可以持有的值，及其存储这些值的方式。  有关更多信息，请参见[数据类型](../../../../visual-basic/language-reference/data-types/data-type-summary.md)。  
  
-   生存期 \- 执行时间的周期，元素在此期间可供使用。  有关更多信息，请参见 [Visual Basic 中的生存期](../../../../visual-basic/programming-guide/language-features/declared-elements/lifetime.md)。  
  
-   范围 \- 所有无需限定元素名称即可引用元素的代码的集合。  有关更多信息，请参见[如何：控制变量的范围](../../../../visual-basic/programming-guide/language-features/declared-elements/how-to-control-the-scope-of-a-variable.md)。  
  
-   访问级别 \- 代码使用元素的权限。  有关更多信息，请参见[如何：控制变量的可用性](../../../../visual-basic/programming-guide/language-features/declared-elements/how-to-control-the-availability-of-a-variable.md)。  
  
## 元素的特性  
 下表显示了已声明元素和适用于各个元素的特性。  
  
|元素|数据类型|生存期|范围 <sup>1</sup>|访问级别|  
|--------|----------|---------|---------------------|----------|  
|变量|是|是|是|是|  
|常量|是|否|是|是|  
|Enumeration|是|否|是|是|  
|结构|否|否|是|是|  
|属性|是|是|是|是|  
|方法|否|是|是|是|  
|过程（`Sub` 或 `Function`）|否|是|是|是|  
|过程参数|是|是|是|否|  
|函数返回值|是|是|是|否|  
|运算符|是|否|是|是|  
|接口|否|否|是|是|  
|类|否|否|是|是|  
|Event|否|否|是|是|  
|委托|否|否|是|是|  
  
 <sup>1</sup> 范围有时被称为“可见性”。  
  
## 请参阅  
 [已声明的元素](../../../../visual-basic/programming-guide/language-features/declared-elements/index.md)   
 [已声明的元素名称](../../../../visual-basic/programming-guide/language-features/declared-elements/declared-element-names.md)   
 [对已声明元素的引用](../../../../visual-basic/programming-guide/language-features/declared-elements/references-to-declared-elements.md)   
 [Visual Basic 中的生存期](../../../../visual-basic/programming-guide/language-features/declared-elements/lifetime.md)   
 [Visual Basic 中的范围](../../../../visual-basic/programming-guide/language-features/declared-elements/scope.md)   
 [Visual Basic 中的访问级别](../../../../visual-basic/programming-guide/language-features/declared-elements/access-levels.md)   
 [数据类型](../../../../visual-basic/programming-guide/language-features/data-types/index.md)   
 [变量声明](../../../../visual-basic/programming-guide/language-features/variables/variable-declaration.md)