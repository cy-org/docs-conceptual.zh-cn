---
title: "WithEvents (Visual Basic 中) |Microsoft 文档"
ms.date: 2015-07-20
ms.prod: .net
ms.suite: 
ms.technology:
- devlang-visual-basic
ms.topic: article
f1_keywords:
- vb.WithEvents
- WithEvents
dev_langs:
- VB
helpviewer_keywords:
- WithEvents keyword
ms.assetid: 19d461f5-d72f-4de9-8c1d-0a6650316990
caps.latest.revision: 17
author: dotnet-bot
ms.author: dotnetcontent
translation.priority.ht:
- cs-cz
- de-de
- es-es
- fr-fr
- it-it
- ja-jp
- ko-kr
- pl-pl
- pt-br
- ru-ru
- tr-tr
- zh-cn
- zh-tw
translationtype: Machine Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: 708cf6fec78faf2c7a5959a3a2694d237d728882
ms.lasthandoff: 03/13/2017

---
# <a name="withevents-visual-basic"></a>WithEvents (Visual Basic)
指定一个或多个声明的成员变量指可以引发事件的类的实例。  
  
## <a name="remarks"></a>备注  
 当使用定义一个变量`WithEvents`，您可以以声明方式指定一种方法，可使用的变量的事件处理`Handles`关键字。  
  
 您可以使用`WithEvents`只能在类或模块级别。 这意味着的声明上下文`WithEvents`变量必须是类或模块，且不能为源文件、 命名空间、 结构或过程。  
  
 不能使用`WithEvents`对结构成员。  
  
 您可以声明只有单个变量-不数组 — 与`WithEvents`。  
  
## <a name="rules"></a>规则  
  
-   **元素类型。** 您必须声明`WithEvents`变量为对象变量，以使它们可以接受类实例。 但是，您无法声明这些变量作为`Object`。 您必须将它们声明为可引发事件的特定类。  
  
 `WithEvents`修饰符可用于在此上下文中︰ [Dim 语句](../../../visual-basic/language-reference/statements/dim-statement.md)  
  
## <a name="see-also"></a>另请参阅  
 [句柄](../../../visual-basic/language-reference/statements/handles-clause.md)   
 [关键字](../../../visual-basic/language-reference/keywords/index.md)   
 [事件](../../../visual-basic/programming-guide/language-features/events/index.md)
