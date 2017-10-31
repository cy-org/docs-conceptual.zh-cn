---
title: "加载 DLL 时出错 (Visual Basic) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
f1_keywords: 
  - "vbrID48"
dev_langs: 
  - "VB"
ms.assetid: 4226cd1f-028c-477d-88a5-cb57f7e0cdc8
caps.latest.revision: 8
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 8
---
# 加载 DLL 时出错 (Visual Basic)
[!INCLUDE[vs2017banner](../../../visual-basic/includes/vs2017banner.md)]

动态链接库 \(DLL\) 是在 `Declare` 语句的 `Lib` 子句中指定的库。  该错误可能的原因包括：  
  
-   文件不是 DLL 可执行文件。  
  
-   文件不是 Microsoft Windows DLL。  
  
-   DLL 引用不存在的其他 DLL。  
  
-   DLL 或引用的 DLL 不在路径中指定的目录中。  
  
### 更正此错误  
  
-   如果文件是源文本文件而非 DLL 可执行文件，必须将其编译并链接为 DLL 可执行文件格式。  
  
-   如果文件不是 Microsoft Windows DLL，则获取相应的 Microsoft Windows 文件。  
  
-   如果 DLL 引用了另一个不存在的 DLL，则获取引用的 DLL 并使其可用。  
  
-   如果 DLL 或引用的 DLL 不在路径所指定的目录中，则将 DLL 移到引用的目录中。  
  
## 请参阅  
 [Declare 语句](../../../visual-basic/language-reference/statements/declare-statement.md)