---
title: "在使用 &quot;Object&quot; 类型的参数时，请使用 &quot;FileGetObject&quot;，而不要使用 &quot;FileGet&quot; | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
ms.assetid: 090b8088-895a-482a-9362-606596bac304
caps.latest.revision: 9
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 9
---
# 在使用 &quot;Object&quot; 类型的参数时，请使用 &quot;FileGetObject&quot;，而不要使用 &quot;FileGet&quot;
`FileGet` 方法包含 `Object` 类型的参数。 应使用 `FileGetObject` 替代 `FileGet`，以避免多义性。  
  
 请注意，与 `FileGet` 或 `FileGetObject` 相比，`My.Computer.Filesystem` 提供的功能更易于使用且性能更高。  
  
### 更正此错误  
  
1.  将 `FileGet` 替换为 `FileGetObject`。  
  
2.  将 `Object` 参数强制转换为一个更明确的类型。  
  
## 请参阅  
 [不在生成中：FileGetObject 函数](http://msdn.microsoft.com/zh-cn/3eda786b-d1ee-4b44-9dd7-0ea6bff072c0)   
 [My.Computer.FileSystem 对象](../../visual-basic/language-reference/objects/my-computer-filesystem-object.md)