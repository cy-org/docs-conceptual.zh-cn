---
title: "Visual Basic 中的访问级别 | Microsoft Docs"
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
  - "访问级别"
  - "访问级别, 已声明的元素"
  - "访问修饰符"
  - "已声明的元素, 访问级别"
  - "Friend 访问修饰符"
  - "成员, 在 Visual Basic 中访问"
  - "私有访问修饰符"
  - "Protected 访问修饰符"
  - "Protected Friend 访问修饰符"
  - "公共访问修饰符"
ms.assetid: 6e06c1ab-fd78-47f0-83a8-1152780b5e1a
caps.latest.revision: 16
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 16
---
# Visual Basic 中的访问级别
[!INCLUDE[vs2017banner](../../../../visual-basic/includes/vs2017banner.md)]

已声明元素的*“访问级别”*是指能够对其进行访问的程度，即什么代码对其具有读取或写入权限。  这不仅取决于元素本身的声明方式，还取决于元素容器的访问级别。  不能访问包含元素的代码也不能访问该元素中包含的任何元素，甚至那些声明为 `Public` 的元素也不例外。  例如，`Private` 结构中的 `Public` 变量可从包含该结构的类内部访问，但不能从该类的外部访问。  
  
## Public  
 声明语句中的 [Public](../../../../visual-basic/language-reference/modifiers/public.md) 关键字指定可从以下位置访问元素：同一项目中任意位置的代码、引用该项目的其他项目以及由该项目生成的任何程序集。  下面的代码显示一个 `Public` 声明的示例。  
  
```  
Public Class classForEverybody  
```  
  
 仅可以在模块、接口或命名空间级别使用 `Public`。  这意味着可以在源文件级别或命名空间级别，或者在接口、模块、类或结构内部声明 public 元素，但不能在过程内声明它。  
  
## Protected  
 声明语句中的 [Protected](../../../../visual-basic/language-reference/modifiers/protected.md) 关键字指定仅可以从同一个类内部或从此类派生的类中访问元素。  下面的代码显示一个 `Protected` 声明的示例。  
  
```  
Protected Class classForMyHeirs  
```  
  
 仅可以在类级别并且仅在声明类的成员时使用 `Protected`。  这意味着可以在类中声明 protected 元素，但不能在源文件级或命名空间级，或者在接口、模块、结构或过程内部声明它。  
  
## Friend  
 声明语句中的 [Friend](../../../../visual-basic/language-reference/modifiers/friend.md) 关键字指定可以从同一程序集内部访问元素，而不能从程序集外部访问。  下面的代码显示一个 `Friend` 声明的示例。  
  
```  
Friend stringForThisProject As String  
```  
  
 仅可以在模块、接口或命名空间级别使用 `Friend`。  这意味着您可以在源文件级别或命名空间级别，或者在接口、模块、类或结构内部声明 friend 元素，但不能在过程内声明它。  
  
## Protected Friend  
 声明语句中同时出现 `Protected` 和 `Friend` 关键字时，指定可从以下位置访问元素：派生类或同一程序集内，或两者皆可。  下面的代码显示示例 `Protected` `Friend` 声明。  
  
```  
Protected Friend stringForProjectAndHeirs As String  
```  
  
 仅可以在类级别并且仅在声明类的成员时使用 `Protected` `Friend`。  这意味着可以在类中声明 protected friend 元素，但不能在源文件级别或命名空间级别，或者在接口、模块、结构或过程内声明它。  
  
## Private  
 声明语句中的 [Private](../../../../visual-basic/language-reference/modifiers/private.md) 关键字指定仅可以从同一模块、类或结构内访问元素。  下面的代码显示一个 `Private` 声明的示例。  
  
```  
Private numberForMeOnly As Integer  
```  
  
 仅可以在模块级别使用 `Private`。  这意味着可以在模块、类或结构内部声明 private 元素，但不能在源文件级别或命名空间级别、接口内部或者过程内声明它。  
  
 在模块级别，不带任何访问级别关键字的 `Dim` 语句与 `Private` 声明等效。  但是，您可能希望使用 `Private` 关键字使代码更容易阅读和解释。  
  
## 访问修饰符  
 指定访问级别的关键字称为*“访问修饰符”*。  下表对访问修饰符进行了比较。  
  
|访问修饰符|授予的访问级别|可以用此访问级别声明的元素|可以在其中使用此修饰符的声明上下文|  
|-----------|-------------|-------------------|-----------------------|  
|`Public`|无限制：<br /><br /> 可看到 public 元素的任何代码均可以访问它|接口<br /><br /> 模块<br /><br /> 类<br /><br /> 结构<br /><br /> 结构成员<br /><br /> 过程<br /><br /> 属性<br /><br /> 成员变量<br /><br /> 常量<br /><br /> 枚举<br /><br /> 事件<br /><br /> 外部声明<br /><br /> 委托|源文件<br /><br /> 命名空间<br /><br /> 接口<br /><br /> 模块<br /><br /> 类<br /><br /> 结构|  
|`Protected`|派生的：<br /><br /> 声明 protected 元素的类（或该类的派生类）中的代码可访问该元素|接口<br /><br /> 类<br /><br /> 结构<br /><br /> 过程<br /><br /> 属性<br /><br /> 成员变量<br /><br /> 常量<br /><br /> 枚举<br /><br /> 事件<br /><br /> 外部声明<br /><br /> 委托|类|  
|`Friend`|程序集：<br /><br /> 声明 friend 元素的程序集中的代码可以访问该元素|接口<br /><br /> 模块<br /><br /> 类<br /><br /> 结构<br /><br /> 结构成员<br /><br /> 过程<br /><br /> 属性<br /><br /> 成员变量<br /><br /> 常量<br /><br /> 枚举<br /><br /> 事件<br /><br /> 外部声明<br /><br /> 委托|源文件<br /><br /> 命名空间<br /><br /> 接口<br /><br /> 模块<br /><br /> 类<br /><br /> 结构|  
|`Protected` `Friend`|`Protected` 和 `Friend` 的联合：<br /><br /> 与 protected friend 元素位于同一个类或同一个程序集中的代码，或者从该元素的类派生的任何类中的代码均可访问该元素|接口<br /><br /> 类<br /><br /> 结构<br /><br /> 过程<br /><br /> 属性<br /><br /> 成员变量<br /><br /> 常量<br /><br /> 枚举<br /><br /> 事件<br /><br /> 外部声明<br /><br /> 委托|类|  
|`Private`|声明上下文：<br /><br /> 声明 private 元素的类型（包括该类型的子类型）中的代码可访问该元素|接口<br /><br /> 类<br /><br /> 结构<br /><br /> 结构成员<br /><br /> 过程<br /><br /> 属性<br /><br /> 成员变量<br /><br /> 常量<br /><br /> 枚举<br /><br /> 事件<br /><br /> 外部声明<br /><br /> 委托|模块<br /><br /> 类<br /><br /> 结构|  
  
## 请参阅  
 [Dim 语句](../../../../visual-basic/language-reference/statements/dim-statement.md)   
 [Static](../../../../visual-basic/language-reference/modifiers/static.md)   
 [已声明的元素名称](../../../../visual-basic/programming-guide/language-features/declared-elements/declared-element-names.md)   
 [对已声明元素的引用](../../../../visual-basic/programming-guide/language-features/declared-elements/references-to-declared-elements.md)   
 [已声明元素的特性](../../../../visual-basic/programming-guide/language-features/declared-elements/declared-element-characteristics.md)   
 [Visual Basic 中的生存期](../../../../visual-basic/programming-guide/language-features/declared-elements/lifetime.md)   
 [Visual Basic 中的范围](../../../../visual-basic/programming-guide/language-features/declared-elements/scope.md)   
 [如何：控制变量的可用性](../../../../visual-basic/programming-guide/language-features/declared-elements/how-to-control-the-availability-of-a-variable.md)   
 [变量](../../../../visual-basic/programming-guide/language-features/variables/index.md)   
 [变量声明](../../../../visual-basic/programming-guide/language-features/variables/variable-declaration.md)