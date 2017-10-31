---
title: "ParamArray (Visual Basic) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
f1_keywords: 
  - "vb.ParamArray"
  - "ParamArray"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "ParamArray 关键字"
  - "ParamArray 关键字, 语法"
ms.assetid: a5f18789-92bd-488f-9c7e-cf3719963635
caps.latest.revision: 15
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 15
---
# ParamArray (Visual Basic)
[!INCLUDE[vs2017banner](../../../visual-basic/includes/vs2017banner.md)]

指定过程参数是一个可选的、数据类型为指定类型的元素数组。  `ParamArray` 只可用于参数列表中的最后一个参数。  
  
## 备注  
 `ParamArray` 使您可以将任意数量的参数传递给过程。  `ParamArray` 参数始终使用 [ByVal](../../../visual-basic/language-reference/modifiers/byval.md) 进行声明。  
  
 可以通过传递一组适当的数据类型、以逗号分隔的值列表，或不传递任何内容，来为 `ParamArray` 参数提供一个或多个参数。  有关详细信息，请参见 [参数数组](../../../visual-basic/programming-guide/language-features/procedures/parameter-arrays.md) 中的“Calling a ParamArray”（调用 ParamArray）。  
  
> [!IMPORTANT]
>  每当处理可能变得无限大的数组时，都存在耗尽应用程序的某种内部容量的风险。  如果在调用代码中接受一个参数数组，您应该测试它的长度，如果它对于应用程序而言太大，应采取适当步骤。  
  
 `ParamArray` 修饰符可用于下面的上下文中：  
  
 [Declare 语句](../../../visual-basic/language-reference/statements/declare-statement.md)  
  
 [Function 语句](../../../visual-basic/language-reference/statements/function-statement.md)  
  
 [Property 语句](../../../visual-basic/language-reference/statements/property-statement.md)  
  
 [Sub 语句](../../../visual-basic/language-reference/statements/sub-statement.md)  
  
## 请参阅  
 [关键字](../../../visual-basic/language-reference/keywords/index.md)   
 [参数数组](../../../visual-basic/programming-guide/language-features/procedures/parameter-arrays.md)