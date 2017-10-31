---
title: "未定义 Property Let 过程，并且 Property Get 过程未返回对象 | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
f1_keywords: 
  - "vbrID451"
dev_langs: 
  - "VB"
ms.assetid: 8542382a-689f-4e1b-abc0-c1e2dadb92f4
caps.latest.revision: 8
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 8
---
# 未定义 Property Let 过程，并且 Property Get 过程未返回对象
[!INCLUDE[vs2017banner](../../../visual-basic/includes/vs2017banner.md)]

某些属性、方法和操作只能应用于 `Collection` 对象。  指定的操作或属性专用于集合，但此对象不是集合。  
  
### 更正此错误  
  
1.  检查对象或属性名称的拼写是否正确，或验证对象是否为 `Collection` 对象。  
  
2.  查看用于将对象添加到集合中的 `Add`方法，确保语法正确且所有标识符拼写正确。  
  
## 请参阅  
 <xref:Microsoft.VisualBasic.Collection>