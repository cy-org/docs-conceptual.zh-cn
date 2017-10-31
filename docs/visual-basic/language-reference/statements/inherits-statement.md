---
title: "Inherits 语句 | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
f1_keywords: 
  - "vb.Inherits"
  - "Inherits"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "Inherits 语句"
  - "Inherits 语句, 语法"
ms.assetid: 9e6fe042-9af3-4341-8093-fc3537770cf2
caps.latest.revision: 16
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 16
---
# Inherits 语句
[!INCLUDE[vs2017banner](../../../visual-basic/includes/vs2017banner.md)]

使当前类或接口继承另一个类或一组接口的特性、变量、属性、过程和事件。  
  
## 语法  
  
```  
Inherits basetypenames  
```  
  
## 部件  
  
|||  
|-|-|  
|术语|定义|  
|`basetypenames`|必选。  派生此类的类的名称。<br /><br /> \- 或 \-<br /><br /> 此接口派生自的接口的名称。  可使用逗号分隔多个名称。|  
  
## 备注  
 如果使用 `Inherits` 语句，则该语句必须是类或接口定义中的第一个非空白的非注释行。  它应紧接在 `Class` 或 `Interface` 语句之后。  
  
 只能在类或接口中使用 `Inherits`。  这意味着继承的声明上下文不能是源文件、命名空间、结构、模块、过程或块。  
  
## 规则  
  
-   **类继承。**如果类使用 `Inherits` 语句，则只能指定一个基类。  
  
     类不能从嵌套在该类中的类继承。  
  
-   **接口继承。**如果接口使用 `Inherits` 语句，则可以指定一个或多个基接口。  可以从两个接口继承，即使它们各自定义了名称相同的成员也是如此。  如果这样做，则实现代码必须使用名称限定来指定它实现的是哪个成员。  
  
     接口无法从另一个具有限制性更高的访问级别的接口继承。  例如，`Public` 接口不能从 `Friend` 接口继承。  
  
     接口不能从其内部嵌套的接口继承。  
  
 .NET Framework 中的类继承示例是 <xref:System.ArgumentException> 类，它从 <xref:System.SystemException> 类继承。  这向 <xref:System.ArgumentException> 提供了系统异常所需的所有预定义属性和过程，如 <xref:System.Exception.Message%2A> 属性和 <xref:System.Exception.ToString%2A> 方法。  
  
 .NET Framework 中的接口继承示例是 <xref:System.Collections.ICollection> 接口，它从 <xref:System.Collections.IEnumerable> 接口继承。  这导致 <xref:System.Collections.ICollection> 继承在遍历集合时所需的枚举数定义。  
  
## 示例  
 下面的示例使用 `Inherits` 语句来演示名为 `thisClass` 的类如何继承名为 `anotherClass` 的基类的所有成员。  
  
 [!code-vb[VbVbalrStatements#37](../../../visual-basic/language-reference/error-messages/codesnippet/VisualBasic/inherits-statement_1.vb)]  
  
## 示例  
 下面的示例演示多个接口的继承。  
  
 [!code-vb[VbVbalrStatements#38](../../../visual-basic/language-reference/error-messages/codesnippet/VisualBasic/inherits-statement_2.vb)]  
  
 现在，名为 `thisInterface` 的接口包含 <xref:System.IComparable>、<xref:System.IDisposable> 和 <xref:System.IFormattable> 接口中的所有定义。继承的成员分别提供这些功能：对两个对象进行特定于类型的比较、释放分配的资源，以及将对象的值表示为 `String`。  实现 `thisInterface` 的类必须实现每个基接口的每个成员。  
  
## 请参阅  
 [MustInherit](../../../visual-basic/language-reference/modifiers/mustinherit.md)   
 [NotInheritable](../../../visual-basic/language-reference/modifiers/notinheritable.md)   
 [对象和类](../../../visual-basic/programming-guide/language-features/objects-and-classes/index.md)   
 [继承的基础知识](../../../visual-basic/programming-guide/language-features/objects-and-classes/inheritance-basics.md)   
 [接口](../../../visual-basic/programming-guide/language-features/interfaces/index.md)