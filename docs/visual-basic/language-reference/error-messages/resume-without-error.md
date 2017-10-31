---
title: "无错误继续执行 | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
f1_keywords: 
  - "vbrID20"
dev_langs: 
  - "VB"
ms.assetid: f9631804-fd36-4443-b36c-30db827e6176
caps.latest.revision: 8
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 8
---
# 无错误继续执行
[!INCLUDE[vs2017banner](../../../visual-basic/includes/vs2017banner.md)]

`Resume` 语句出现在错误处理代码之外，或代码在未发生错误时跳转到错误处理程序中。  
  
### 更正此错误  
  
1.  将 `Resume` 语句移到错误处理程序内，或将其删除。  
  
2.  过程中不能出现到标签的跳转，因此，请搜索过程中是否有标识错误处理程序的标签。  如果找到一个重复标签且被指定为 `GoTo` 语句而非 `On Error GoTo` 语句的目标，则请更改行标签使其与相应的目标对应。  
  
## 请参阅  
 [Resume 语句](../../../visual-basic/language-reference/statements/resume-statement.md)   
 [On Error 语句](../../../visual-basic/language-reference/statements/on-error-statement.md)