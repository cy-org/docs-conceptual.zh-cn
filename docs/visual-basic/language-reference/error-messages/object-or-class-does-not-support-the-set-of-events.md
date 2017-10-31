---
title: "对象或类不支持事件集 | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
f1_keywords: 
  - "vbrID459"
dev_langs: 
  - "VB"
ms.assetid: 785df3f3-2aae-4a25-af36-1f9879d4e5fd
caps.latest.revision: 8
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 8
---
# 对象或类不支持事件集
[!INCLUDE[vs2017banner](../../../visual-basic/includes/vs2017banner.md)]

尝试对不能作为指定事件集的事件源的组件使用 `WithEvents` 变量。  例如，您希望接收某个对象的事件，然后，创建了 `Implements` 该对象的另一个对象。  虽然您可能认为您可以接收实现的对象的事件，但情况并非总是这样。  `Implements` 只实现方法和属性的接口。  专用 `UserControls` 不支持 `WithEvents`，因为引发 `ObjectEvent` 所需的类型信息在运行时不可用。  
  
### 更正此错误  
  
1.  无法接收不发起事件的组件的事件。  
  
## 请参阅  
 [WithEvents](../../../visual-basic/language-reference/modifiers/withevents.md)   
 [Implements 语句](../../../visual-basic/language-reference/statements/implements-statement.md)