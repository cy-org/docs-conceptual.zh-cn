---
title: "在自定义日志名称中，只有前八个字符是有意义的 | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
ms.assetid: db2a0252-9ddd-4e93-a239-6a690cc09557
caps.latest.revision: 10
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 10
---
# 在自定义日志名称中，只有前八个字符是有意义的
在检查事件日志名称的唯一性时，仅考虑前八个字符。 当事件日志共享前八个字符时，则可能会导致冲突。  
  
### 更正此错误  
  
-   为事件日志命名，其中前八个字符是唯一的。  
  
## 请参阅  
 [How to: Create and Remove Custom Event Logs](http://msdn.microsoft.com/zh-cn/af9b7da0-80c7-46ac-b7f7-897063ddd503)   
 [Administering Event Logs](http://msdn.microsoft.com/zh-cn/35f53238-bdd2-417b-acd8-2fd9f7397f18)