---
title: "不能删除系统事件日志 | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
ms.assetid: 26ca8819-4ce5-49c6-98f3-27fe9e2e8e3d
caps.latest.revision: 8
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 8
---
# 不能删除系统事件日志
试图删除系统事件日志（该日志是不能被删除的）。 系统日志跟踪系统事件（如系统启动和硬件故障）。  
  
### 更正此错误  
  
-   请考虑让应用程序写入应用程序或自定义日志，而不是系统事件日志。  
  
-   请勿试图删除系统事件日志。  
  
## 请参阅  
 [Administering Event Logs](http://msdn.microsoft.com/zh-cn/35f53238-bdd2-417b-acd8-2fd9f7397f18)   
 [How to: Create and Remove Custom Event Logs](http://msdn.microsoft.com/zh-cn/af9b7da0-80c7-46ac-b7f7-897063ddd503)