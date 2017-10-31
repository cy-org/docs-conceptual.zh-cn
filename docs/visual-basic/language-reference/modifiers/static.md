---
title: "Static (Visual Basic) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
f1_keywords: 
  - "vb.Static"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "Static 关键字"
  - "静态修饰符"
ms.assetid: 19013910-4658-47b6-a22e-1744b527979e
caps.latest.revision: 22
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 22
---
# Static (Visual Basic)
[!INCLUDE[vs2017banner](../../../visual-basic/includes/vs2017banner.md)]

指定在其中声明一个或多个局部变量的过程终止后，这些已声明的局部变量继续存在并保留其最新值。  
  
## 备注  
 通常，过程终止后，此过程中的局部变量将立即消失。  静态变量可继续存在，并保留其最新值。  您的代码下次调用该过程时，此变量不会重新初始化，仍然保存已赋给它的最新值。  静态变量在定义它的类或模块的生存期内继续存在。  
  
## 规则  
  
-   **声明上下文。**只能对局部变量使用 `Static`。  这意味着 `Static` 变量的声明上下文必须是一个过程或过程中的块，而不能是源文件、命名空间、类、结构或模块。  
  
     不能在结构过程内使用 `Static`。  
  
-   无法推断出 `Static` 局部变量的数据类型。  有关更多信息，请参见[局部类型推理](../../../visual-basic/programming-guide/language-features/variables/local-type-inference.md)。  
  
-   **组合修饰符。**不能在同一个声明中同时指定 `Static` 与 `ReadOnly`、`Shadows` 或 `Shared`。  
  
## 行为  
 在声明在 `Shared` 程序的静态变量，因此，只有该静态变量的复制为整个应用程序可用。  您调用 `Shared` 程序使用类名称，指向类的实例不是的变量。  
  
 在声明在不是 `Shared`程序的一个静态变量，因此，只有该变量的副本对类的每个实例都可用。  您调用非共享程序以指向特定类实例的变量。  
  
## 示例  
 下面的示例说明 `Static` 的用法。  
  
 [!code-vb[VbVbalrKeywords#5](../../../visual-basic/language-reference/codesnippet/VisualBasic/static_1.vb)]  
  
 `Static` 变量 `totalSales` 只初始化为 0 一次。  每次输入 `updateSales` 时，`totalSales` 仍然包含为其计算的最新值。  
  
 `Static` 修饰符可用于下面的上下文中：  
  
 [Dim 语句](../../../visual-basic/language-reference/statements/dim-statement.md)  
  
## 请参阅  
 [Shadows](../../../visual-basic/language-reference/modifiers/shadows.md)   
 [Shared](../../../visual-basic/language-reference/modifiers/shared.md)   
 [Visual Basic 中的生存期](../../../visual-basic/programming-guide/language-features/declared-elements/lifetime.md)   
 [变量声明](../../../visual-basic/programming-guide/language-features/variables/variable-declaration.md)   
 [结构](../../../visual-basic/programming-guide/language-features/data-types/structures.md)   
 [局部类型推理](../../../visual-basic/programming-guide/language-features/variables/local-type-inference.md)   
 [对象和类](../../../visual-basic/programming-guide/language-features/objects-and-classes/index.md)