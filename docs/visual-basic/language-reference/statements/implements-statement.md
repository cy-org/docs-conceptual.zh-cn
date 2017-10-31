---
title: "Implements 语句 | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
f1_keywords: 
  - "vb.Implements"
  - "Implements"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "Implements 语句"
  - "Implements 语句, 语法"
  - "接口实现, Implements 语句"
ms.assetid: 1fafb83f-f55a-4215-8ea9-681e8622613d
caps.latest.revision: 17
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 17
---
# Implements 语句
[!INCLUDE[vs2017banner](../../../visual-basic/includes/vs2017banner.md)]

指定一个或多个接口或接口成员，这些接口或接口成员必须在它们所在的类或结构定义中实现。  
  
## 语法  
  
```  
Implements interfacename [, ...]  
-or-  
Implements interfacename.interfacemember [, ...]  
```  
  
## 部件  
 `interfacename`  
 必选。  一个接口，其属性、过程和事件将由类或结构中对应的成员来实现。  
  
 `interfacemember`  
 必选。  正被实现的接口的成员。  
  
## 备注  
 接口是表示该接口封装的成员（属性、过程和事件）的原型集合。  接口只包含成员的声明；类和结构实现这些成员。  有关更多信息，请参见 [接口](../../../visual-basic/programming-guide/language-features/interfaces/index.md)。  
  
 `Implements` 语句必须紧跟在 `Class` 或 `Structure` 语句的后面。  
  
 当实现接口时，必须实现该接口中声明的所有成员。  省略任何成员被认为是语法错误。  若要实现单个成员，您在类或结构中声明该成员时要指定 [Implements](../../../visual-basic/language-reference/statements/implements-clause.md) 关键字（它与 `Implements` 语句是分离的）。  有关更多信息，请参见 [接口](../../../visual-basic/programming-guide/language-features/interfaces/index.md)。  
  
 类可以使用属性和过程的 [Private](../../../visual-basic/language-reference/modifiers/private.md) 实现，但只能通过将实现类的实例转换为被声明为接口类型的变量来访问这些成员。  
  
## 示例  
 下面的示例演示如何使用 `Implements` 语句来实现接口的成员。  该示例使用事件、属性和过程定义一个名为 `ICustomerInfo` 的接口。  类 `customerInfo` 实现该接口中定义的所有成员。  
  
 [!code-vb[VbVbalrStatements#33](../../../visual-basic/language-reference/error-messages/codesnippet/VisualBasic/implements-statement_1.vb)]  
  
 请注意，类 `customerInfo` 在单独的源代码行上使用 `Implements` 语句，以指示该类实现 `ICustomerInfo` 接口的所有成员。  然后，该类中的每个成员使用 `Implements` 关键字作为其成员声明的一部分，以指示它实现该接口成员。  
  
## 示例  
 下面的两个过程演示如何使用上例中实现的接口。  若要测试该实现，请将这些过程添加到项目中并调用 `testImplements` 过程。  
  
 [!code-vb[VbVbalrStatements#34](../../../visual-basic/language-reference/error-messages/codesnippet/VisualBasic/implements-statement_2.vb)]  
  
## 请参阅  
 [Implements](../../../visual-basic/language-reference/statements/implements-clause.md)   
 [Interface 语句](../../../visual-basic/language-reference/statements/interface-statement.md)   
 [接口](../../../visual-basic/programming-guide/language-features/interfaces/index.md)