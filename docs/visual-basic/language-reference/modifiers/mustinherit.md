---
title: "MustInherit (Visual Basic) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
f1_keywords: 
  - "MustInherit"
  - "vb.MustInherit"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "抽象类, MustInherit 类"
  - "类 [Visual Basic], abstract"
  - "MustInherit 类, MustInherit 关键字"
  - "MustInherit 关键字"
ms.assetid: b8f05185-90e3-4dd7-adc2-90d852fab5b4
caps.latest.revision: 15
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 15
---
# MustInherit (Visual Basic)
[!INCLUDE[vs2017banner](../../../visual-basic/includes/vs2017banner.md)]

指定某个类只能用作基类，您不能直接从该类创建对象。  
  
## 备注  
 基类（也称为“抽象类”）的用途就是定义从此基类派生的所有类所共同拥有的功能，  这样派生类将不必重新定义这些公共元素。  某些情况下，此公共功能不够完整，无法生成一个可用的对象，因此每个派生类都需要单独定义所缺少的功能。  此时，您需要让使用代码仅从派生类创建对象。  您可以对基类使用 `MustInherit` 来强制执行此操作。  
  
 `MustInherit` 类的另一个用途是限定一个变量仅用于一组相关类。  您可以先定义一个基类，然后从此基类派生出所有这些相关的类。  此基类无需提供所有派生类所共同拥有的任何功能，但它可以作为一个筛选器，将值分配给变量。  如果您的使用代码将一个变量声明为基类，Visual Basic 将允许您仅将这些派生类中的某个类的对象分配给该变量。  
  
 .NET Framework 定义多个 `MustInherit` 类，其中包括 <xref:System.Array>、<xref:System.Enum> 和 <xref:System.ValueType>。  <xref:System.ValueType> 就是限制变量的基类的一个示例。  所有值类型均从 <xref:System.ValueType> 派生。  如果将一个变量声明为 <xref:System.ValueType>，则可以仅将值类型分配给该变量。  
  
## 规则  
  
-   **声明上下文。**只能在 `Class` 语句中使用 `MustInherit`。  
  
-   **组合修饰符。**不能在同一声明中同时指定 `MustInherit` 和 `NotInheritable`。  
  
## 示例  
 下面的示例演示强制继承和强制重写。  基类 `shape` 定义变量 `acrossLine`。  类 `circle` 和 `square` 从 `shape` 派生。  这两个类继承 `acrossLine` 的定义，但它们必须单独定义 `area` 函数，这是因为每种形状的面积计算方法不同。  
  
 [!code-vb[VbVbalrKeywords#2](../../../visual-basic/language-reference/codesnippet/VisualBasic/mustinherit_1.vb)]  
  
 您可以将 `shape1` 和 `shape2` 声明为 `shape` 类型。  但是，您不能从 `shape` 创建对象，因为它缺少 `area` 函数的功能并且被标记为 `MustInherit`。  
  
 由于变量 `shape1` 和 `shape2` 被声明为 `shape` 类型，因此它们被限定为仅使用派生类 `circle` 和 `square` 中的对象。  Visual Basic 不允许您将任何其他对象分配给这些变量，这样您就可以获得很高的类型安全级别。  
  
## 用法  
 `MustInherit` 修饰符可用于下面的上下文中：  
  
 [Class 语句](../../../visual-basic/language-reference/statements/class-statement.md)  
  
## 请参阅  
 [Inherits 语句](../../../visual-basic/language-reference/statements/inherits-statement.md)   
 [NotInheritable](../../../visual-basic/language-reference/modifiers/notinheritable.md)   
 [关键字](../../../visual-basic/language-reference/keywords/index.md)   
 [继承的基础知识](../../../visual-basic/programming-guide/language-features/objects-and-classes/inheritance-basics.md)