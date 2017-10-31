---
title: "End &lt;关键字&gt; 语句 (Visual Basic) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
f1_keywords: 
  - "vb.EndDefinition"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "End 关键字"
ms.assetid: 42d6e088-ab0f-4cda-88e8-fdce3e5fcf4f
caps.latest.revision: 17
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 17
---
# End &lt;关键字&gt; 语句 (Visual Basic)
[!INCLUDE[vs2017banner](../../../visual-basic/includes/vs2017banner.md)]

当后接其他关键字时，它终止由该关键字引入的语句块的定义。  
  
## 语法  
  
```  
End AddHandler  
End Class   
End Enum   
End Event   
End Function   
End Get   
End If   
End Interface   
End Module   
End Namespace   
End Operator   
End Property   
End RaiseEvent  
End RemoveHandler  
End Select   
End Set   
End Structure   
End Sub   
End SyncLock   
End Try   
End While   
End With  
```  
  
## 部件  
 `End`  
 必选。  终止编程元素的定义。  
  
 `AddHandler`  
 必选。用于终止在自定义的 [Event 语句](../../../visual-basic/language-reference/statements/event-statement.md)中由匹配的 `AddHandler` 语句开始的 `AddHandler` 访问器。  
  
 `Class`  
 必选。用于终止由匹配的 [Class 语句](../../../visual-basic/language-reference/statements/class-statement.md)开始的类定义。  
  
 `Enum`  
 必选。用于终止由匹配的 [Enum 语句](../../../visual-basic/language-reference/statements/enum-statement.md)开始的枚举定义。  
  
 `Event`  
 必选。用于终止由匹配的 [Event 语句](../../../visual-basic/language-reference/statements/event-statement.md)开始的`Custom`事件定义。  
  
 `Function`  
 必选。用于终止由匹配的 [Function 语句](../../../visual-basic/language-reference/statements/function-statement.md)开始的 `Function` 过程定义。  如果执行时遇到 `End` `Function` 语句，控制将返回到调用代码。  
  
 `Get`  
 必选。用于终止由匹配的 [Get 语句](../../../visual-basic/language-reference/statements/get-statement.md)开始的 `Property` 过程定义。  如果执行时遇到 `End` `Get` 语句，控制将返回到请求该属性值的语句。  
  
 `If`  
 必选。用于终止由匹配的 `If` 语句开始的 `If`...`Then`...`Else` 块定义。  请参见 [If...Then...Else 语句](../../../visual-basic/language-reference/statements/if-then-else-statement.md)。  
  
 `Interface`  
 必选。用于终止由匹配的 [Interface 语句](../../../visual-basic/language-reference/statements/interface-statement.md)开始的接口定义。  
  
 `Module`  
 必选。用于终止由匹配的 [Module 语句](../../../visual-basic/language-reference/statements/module-statement.md)开始的模块定义。  
  
 `Namespace`  
 必选。用于终止由匹配的 [Namespace 语句](../../../visual-basic/language-reference/statements/namespace-statement.md)开始的命名空间定义。  
  
 `Operator`  
 必选。用于终止由匹配的 [Operator 语句](../../../visual-basic/language-reference/statements/operator-statement.md)开始的运算符定义。  
  
 `Property`  
 必选。用于终止由匹配的 [Property 语句](../../../visual-basic/language-reference/statements/property-statement.md)开始的属性定义。  
  
 `RaiseEvent`  
 必选。用于终止在自定义的 [Event 语句](../../../visual-basic/language-reference/statements/event-statement.md)中由匹配的 `RaiseEvent` 语句开始的 `RaiseEvent` 访问器。  
  
 `RemoveHandler`  
 必选。用于终止在自定义的 [Event 语句](../../../visual-basic/language-reference/statements/event-statement.md)中由匹配的 `RemoveHandler` 语句开始的 `RemoveHandler` 访问器。  
  
 `Select`  
 必选。用于终止由匹配的 `Select` 语句开始的 `Select`...`Case` 块定义。  请参见 [Select...Case 语句](../../../visual-basic/language-reference/statements/select-case-statement.md)。  
  
 `Set`  
 必选。用于终止由匹配的 [Set 语句](../../../visual-basic/language-reference/statements/set-statement.md)开始的 `Property` 过程定义。  如果执行时遇到 `End` `Set` 语句，控制将返回到设置该属性值的语句。  
  
 `Structure`  
 必选。用于终止由匹配的 [Structure 语句](../../../visual-basic/language-reference/statements/structure-statement.md)开始的结构定义。  
  
 `Sub`  
 必选。用于终止由匹配的 [Sub 语句](../../../visual-basic/language-reference/statements/sub-statement.md)开始的 `Sub` 过程定义。  如果执行时遇到 `End` `Sub` 语句，则控制将返回到调用代码。  
  
 `SyncLock`  
 必选。用于终止由匹配的 `SyncLock` 语句开始的 `SyncLock` 块定义。  请参见 [SyncLock 语句](../../../visual-basic/language-reference/statements/synclock-statement.md)。  
  
 `Try`  
 必选。用于终止由匹配的 `Try` 语句开始的 `Try`...`Catch`...`Finally` 块定义。  请参见 [Try...Catch...Finally 语句](../../../visual-basic/language-reference/statements/try-catch-finally-statement.md)。  
  
 `While`  
 必选。用于终止由匹配的 `While` 语句开始的 `While` 循环定义。  请参见 [While...End While 语句](../../../visual-basic/language-reference/statements/while-end-while-statement.md)。  
  
 `With`  
 必选。用于终止由匹配的 `With` 语句开始的 `With` 块定义。  请参见 [With...End With 语句](../../../visual-basic/language-reference/statements/with-end-with-statement.md)。  
  
## 备注  
 没有附加关键字的 [End 语句](../../../visual-basic/language-reference/statements/end-statement.md)语句会立即终止执行。  
  
 前接数字标记 \(`#`\) 时，`End` 关键字会终止由相应的指令引入的预处理块。  
  
 `#End`  
 必选。  终止预处理块的定义。  
  
 `#ExternalSource`  
 必选。用于终止由匹配的 [\#ExternalSource 指令](../../../visual-basic/language-reference/directives/externalsource-directive.md)开始的外部源块。  
  
 `#If`  
 必选。用于终止由匹配的 `#If` 指令开始的条件编译块。  请参见 [\#If...Then...\#Else 指令](../../../visual-basic/language-reference/directives/if-then-else-directives.md)。  
  
 `#Region`  
 必选。用于终止由匹配的 [\#Region 指令](../../../visual-basic/language-reference/directives/region-directive.md)开始的源区域块。  
  
## 智能设备开发人员说明  
 不支持无附加关键字的 `End` 语句。  
  
## 请参阅  
 [End 语句](../../../visual-basic/language-reference/statements/end-statement.md)