---
title: "GetType 运算符 (Visual Basic) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
f1_keywords: 
  - "vb.GetType"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "GetType 关键字"
  - "GetType 运算符"
ms.assetid: 4f733297-2503-4607-850c-15eba65fff90
caps.latest.revision: 17
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 17
---
# GetType 运算符 (Visual Basic)
[!INCLUDE[vs2017banner](../../../visual-basic/includes/vs2017banner.md)]

返回指定类型的 <xref:System.Type> 对象。  <xref:System.Type> 对象提供有关类型的信息，如类型的属性、方法和事件。  
  
## 语法  
  
```  
GetType(typename)  
```  
  
#### 参数  
  
|||  
|-|-|  
|Parameter|说明|  
|`typename`|需要获取其信息的类型的名称。|  
  
## 备注  
 `GetType` 运算符返回指定的 `typename` 的 <xref:System.Type> 对象。  您可以在 `typename` 中传递任何已定义的类型的名称。  这包括：  
  
-   任何 Visual Basic 数据类型，如 `Boolean` 或 `Date`。  
  
-   任何 .NET Framework 类、结构、模块或接口，如 <xref:System.ArgumentException?displayProperty=fullName> 或 <xref:System.Double?displayProperty=fullName>。  
  
-   由您的应用程序定义的任何类、结构、模块或接口。  
  
-   由您的应用程序定义的任何数组。  
  
-   由您的应用程序定义的任何委托。  
  
-   由 Visual Basic、.NET Framework 或您的应用程序定义的任何枚举。  
  
 如果要获取对象变量的类型对象，请使用 <xref:System.Type.GetType%2A?displayProperty=fullName> 方法。  
  
 `GetType` 运算符在下列情况下非常有用：  
  
-   在运行时必须访问某个类型的元数据。  <xref:System.Type> 对象提供了类型成员和部署信息等元数据。  例如，您需要使用这些元数据在程序集上进行反射。  有关更多信息，请参见 <xref:System.Reflection?displayProperty=fullName>。  
  
-   需要比较两个对象引用，以了解它们是否引用了同一个类型的实例。  如果是，`GetType` 将返回对同一个 <xref:System.Type> 对象的引用。  
  
## 示例  
 下面的示例显示正在使用的 `GetType` 操作符。  
  
 [!code-vb[VbVbalrOperators#26](../../../visual-basic/language-reference/operators/codesnippet/VisualBasic/gettype-operator_1.vb)]  
  
## 请参阅  
 [Visual Basic 中的运算符优先级](../../../visual-basic/language-reference/operators/operator-precedence.md)   
 [按功能列出的运算符](../../../visual-basic/language-reference/operators/operators-listed-by-functionality.md)   
 [运算符和表达式](../../../visual-basic/programming-guide/language-features/operators-and-expressions/index.md)