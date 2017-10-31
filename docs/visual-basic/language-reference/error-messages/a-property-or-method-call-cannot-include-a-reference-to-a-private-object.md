---
title: "无论是作为参数还是作为返回值，属性或方法调用都不能包括对私有对象的引用 | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
f1_keywords: 
  - "vbrID98"
dev_langs: 
  - "VB"
ms.assetid: 059b43e1-202d-4fa2-806b-7bad63c1e7ca
caps.latest.revision: 8
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 8
---
# 无论是作为参数还是作为返回值，属性或方法调用都不能包括对私有对象的引用
[!INCLUDE[vs2017banner](../../../visual-basic/includes/vs2017banner.md)]

此错误的可能原因包括：  
  
-   客户端调用了进程外组件的属性或方法，并且试图将对私有对象的引用作为参数之一进行传递。  
  
-   进程外组件调用了其客户端上的回调方法，并试图传递对私有对象的引用。  
  
-   进程外组件试图将对私有对象的引用作为它所引发的事件的参数进行传递。  
  
-   客户端试图将私有对象引用赋给它正在处理的事件的 `ByRef` 参数。  
  
### 更正此错误  
  
1.  删除引用。  
  
## 请参阅  
 [Private](../../../visual-basic/language-reference/modifiers/private.md)