---
title: "隐藏和重写之间的差异 (Visual Basic) | Microsoft Docs"
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
  - "重写, 与隐藏的比较"
  - "阴影操作, 与重写的比较"
ms.assetid: 2d014a0b-7630-407d-8f4e-24bd87987923
caps.latest.revision: 24
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 24
---
# 隐藏和重写之间的差异 (Visual Basic)
[!INCLUDE[vs2017banner](../../../../visual-basic/includes/vs2017banner.md)]

当您定义从基类继承的类时，有时会需要重定义派生类中的一个或多个基类元素。  隐藏和重写均可用于此目的。  
  
## 比较  
 隐藏和重写都在派生类继承基类时使用，并且都是用另外的元素重定义一个已声明的元素。  但二者之间有重大区别。  
  
 下表对隐藏和重写进行了比较。  
  
||||  
|-|-|-|  
|比较点|Shadowing|重写|  
|用途|防止后续的基类修改引入已在派生类中定义的成员|通过用同一调用序列定义不同的过程或属性实现来获得多态性<sup>1</sup>|  
|重定义的元素|任何声明的元素类型|只能是过程（`Function`、`Sub` 或 `Operator`）或属性|  
|重定义元素|任何声明的元素类型|只能是具备相同的调用序列的过程或属性<sup>1</sup>|  
|重定义元素的访问级别|任何访问级别|不能更改被重写的元素的访问级别|  
|重定义元素的可读性和可写性|任何组合|不能更改被重写的属性的可读性或可写性|  
|控制重定义|基类元素不能强制或禁止隐藏|基类元素可以指定 `MustOverride`、`NotOverridable` 或 `Overridable`|  
|关键字的用法|建议在派生类中使用 `Shadows`；若既没有指定 `Shadows` 也没有指定 `Overrides`，则假定为 `Shadows`<sup>2</sup>|基类中要求 `Overridable` 或 `MustOverride`；派生类中要求 `Overrides`|  
|由派生类派生的类实现的重定义元素继承|隐藏其他派生类继承的元素；隐藏的元素仍被隐藏<sup>3</sup>|重写其他派生类继承的元素；重写的元素仍被重写|  
  
 <sup>1</sup>“调用序列”包括元素类型（`Function`、`Sub`、`Operator` 或 `Property`）、名称、参数列表和返回类型。  不能用属性重写过程，或是用过程重写属性。  您不能用一种过程重写另一种过程（`Function`、`Sub` 或 `Operator`）。  
  
 <sup>2</sup> 如果不指定 `Shadows` 或 `Overrides`，则编译器会发出一条警告消息，以帮助您确定要使用哪种重定义。  如果忽略该警告，则使用隐藏机制。  
  
 <sup>3</sup> 若隐藏元素在后来的派生类中不可访问，则没有继承隐藏。  例如，如果将隐藏元素声明为 `Private`，则从派生类派生的类就会继承原始元素而不是隐藏元素。  
  
## 准则  
 重写通常用在以下情况下：  
  
-   您要定义多态性派生类。  
  
-   您需要安全地让编译器强制执行相同元素类型和调用序列。  
  
 隐藏通常用在以下情况下：  
  
-   您希望可以修改基类并使用您的名称定义元素。  
  
-   您希望可以随意更改元素类型或调用序列。  
  
## 请参阅  
 [对已声明元素的引用](../../../../visual-basic/programming-guide/language-features/declared-elements/references-to-declared-elements.md)   
 [Visual Basic 中的隐藏](../../../../visual-basic/programming-guide/language-features/declared-elements/shadowing.md)   
 [如何：隐藏与您的变量同名的变量](../../../../visual-basic/programming-guide/language-features/declared-elements/how-to-hide-a-variable-with-the-same-name-as-your-variable.md)   
 [如何：隐藏继承的变量](../../../../visual-basic/programming-guide/language-features/declared-elements/how-to-hide-an-inherited-variable.md)   
 [如何：访问被派生类隐藏的变量](../../../../visual-basic/programming-guide/language-features/declared-elements/how-to-access-a-variable-hidden-by-a-derived-class.md)   
 [Shadows](../../../../visual-basic/language-reference/modifiers/shadows.md)   
 [Overrides](../../../../visual-basic/language-reference/modifiers/overrides.md)