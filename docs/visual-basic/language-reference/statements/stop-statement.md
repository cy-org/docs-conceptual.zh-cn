---
title: "Stop 语句 (Visual Basic) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
f1_keywords: 
  - "vb.Stop"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "断点, Stop 语句"
  - "执行, stopping"
  - "执行, 挂起"
  - "进程, 中断"
  - "处理, 中断"
  - "Stop 语句"
  - "Stop 语句, 语法"
ms.assetid: c9a9fde0-d649-4662-9bef-bd0146ebc2a7
caps.latest.revision: 9
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 9
---
# Stop 语句 (Visual Basic)
[!INCLUDE[vs2017banner](../../../visual-basic/includes/vs2017banner.md)]

中止执行。  
  
## 语法  
  
```  
Stop  
```  
  
## 备注  
 可以将 `Stop` 语句放在过程的任何地方以中止执行。  使用 `Stop` 语句类似于在代码中设置断点。  
  
 `Stop` 语句中止执行，但与 `End` 不同，它不关闭任何文件或清除任何变量，除非在已编译的可执行 \(.exe\) 文件中遇到它。  
  
> [!NOTE]
>  如果在集成开发环境 \(IDE\) 之外运行的代码中遇到 `Stop` 语句，将调用调试器。  不论代码是以调试模式编译还是以发布模式编译，都将如此。  
  
## 示例  
 本示例使用 `Stop` 语句中止执行 `For...Next` 循环里的每一次迭代。  
  
 [!code-vb[VbVbalrStatements#56](../../../visual-basic/language-reference/error-messages/codesnippet/VisualBasic/stop-statement_1.vb)]  
  
## 请参阅  
 [End 语句](../../../visual-basic/language-reference/statements/end-statement.md)