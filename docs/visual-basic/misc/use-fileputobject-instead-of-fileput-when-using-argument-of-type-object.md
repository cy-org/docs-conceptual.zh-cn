---
title: "在使用 &quot;Object&quot; 类型的参数时，请使用 &quot;FilePutObject&quot;，而不要使用 &quot;FilePut&quot; | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
f1_keywords: 
  - "vbrUseFilePutObject"
ms.assetid: d207b9b7-5898-4c13-8b03-9feefac5f726
caps.latest.revision: 8
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 8
---
# 在使用 &quot;Object&quot; 类型的参数时，请使用 &quot;FilePutObject&quot;，而不要使用 &quot;FilePut&quot;
`FilePut` 方法包含`Object` 类型的参数。 应使用 `FilePutObject` 替代 `FilePut`，以避免多义性。  
  
### 更正此错误  
  
-   将 `FilePut` 替换为 `FilePutObject`。  
  
-   将 `Object` 参数强制转换为一个更明确的类型。  
  
-   使用 `My.Computer.FileSystem` 对象中的可用功能。  
  
## 请参阅  
 [不在生成中：FilePutObject 函数](http://msdn.microsoft.com/zh-cn/a0f52a1c-5ecc-4945-b18c-03147af61d6b)   
 [My.Computer.FileSystem 对象](../../visual-basic/language-reference/objects/my-computer-filesystem-object.md)   
 [My.Computer.FileSystem.WriteAllBytes 方法](http://msdn.microsoft.com/zh-cn/b1a24dc1-eac8-4e22-8ffa-cc3bacbaf826)