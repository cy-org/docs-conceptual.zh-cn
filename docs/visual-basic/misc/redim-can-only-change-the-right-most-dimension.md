---
title: "“ReDim”只能更改最右边的维度 | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
f1_keywords: 
  - "vbrArray_TypeMismatch"
ms.assetid: d53cf41b-7a7a-466c-a29a-920d99698fa9
caps.latest.revision: 9
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 9
---
# “ReDim”只能更改最右边的维度
`ReDim` 语句尝试使用 `Preserve` 关键字来更改一个数组的维度，它不是最后一个维度。 使用 `Preserve` 时，只能调整数组最后一个维度的大小。 对于其他所有维度，必须指定与现有数组相同的大小。  
  
### 更正此错误  
  
-   删除 `Preserve` 关键字。  
  
## 请参阅  
 [NOTINBUILD Visual Basic 中的数组概述](http://msdn.microsoft.com/zh-cn/ca50e2f2-b4d2-4c57-9169-9abbcc3392d8)   
 [NOTINBUILD Visual Basic 中的多维数组](http://msdn.microsoft.com/zh-cn/d92cad25-07e2-4d79-8ea4-ab269700f5de)   
 [ReDim 语句](../../visual-basic/language-reference/statements/redim-statement.md)   
 [Dim 语句](../../visual-basic/language-reference/statements/dim-statement.md)   
 [保留 \- 删除](http://msdn.microsoft.com/zh-cn/91badeab-b4e0-48b6-92c9-9f0c8f995d81)