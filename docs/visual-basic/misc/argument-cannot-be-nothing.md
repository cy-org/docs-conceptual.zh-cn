---
title: "参数不能为 Nothing | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
f1_keywords: 
  - "vbrGeneral_ArgumentNullException"
ms.assetid: 2abd995b-36a5-45f0-b3c1-6e0c3b31a875
caps.latest.revision: 8
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 8
---
# 参数不能为 Nothing
向必须具有值的参数提供了 null 值。  
  
### 更正此错误  
  
-   你可能试图在未先提供对象的实例的情况下使用对象。 在这种情况下，请使用 `New` 关键字创建实例。  
  
-   检查值是否计算正确。  
  
## 请参阅  
 [关于异常的疑难解答：System.NullReferenceException](../Topic/Troubleshooting%20Exceptions:%20System.NullReferenceException.md)