---
title: "安全性和进行中的代码生成 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-standard"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "VB"
  - "CSharp"
  - "C++"
  - "jsharp"
helpviewer_keywords: 
  - "代码安全性, 快速代码生成"
  - "快速代码生成"
  - "安全编码, 快速代码生成"
  - "安全性 [.NET Framework], 快速代码生成"
ms.assetid: 6d221724-bb21-4d76-90c3-0ee2a2e69be2
caps.latest.revision: 10
author: "mairaw"
ms.author: "mairaw"
manager: "wpickett"
caps.handback.revision: 8
---
# 安全性和进行中的代码生成
某些库的操作方式是通过生成代码并运行它执行调用方的某项操作。  基本问题是代表信任级别较低的代码生成代码，并在更高的信任级别运行它。  当调用方可影响代码生成时，问题更为恶化，因此必须确保仅生成认为安全的代码。  
  
 需要随时了解正在生成的具体代码。  这意味着必须严格控制从用户获取的任何值，无论它们是带引号的字符串（应转义以便不包含意外代码元素）、标识符（应检查以验证是否为有效标识符）或任何其他内容。  标识符可能很危险，因为可能修改已编译的程序集，使其标识符包含可能损程序集的奇怪字符（尽管此类安全漏洞很少见）。  
  
 建议用反射发出生成代码，这通常有助于避免很多此类问题。  
  
 编译代码时，请注意恶意程序是否可以某种方式修改它。  在编译器读取磁盘上的源代码或代码加载 .dll 文件之前，是否存在一小段时间窗口使恶意代码可在此期间修改此源代码？  若如此，必须适当使用文件系统中的代码访问安全性或访问控制列表保护包含这些文件的目录。  
  
 如果调用方可以引起编译器错误的方式影响生成的代码，则此处还可能存在安全漏洞。  
  
 使用 <xref:System.Security.Permissions.SecurityAction> 或 [Deny](http://msdn.microsoft.com/zh-cn/6b4d2e01-c504-4ac3-b50e-d6f5e7f5df25) 以尽可能最低的权限设置运行生成的代码。  
  
## 请参阅  
 [代码安全维护指南](../../../docs/standard/security/secure-coding-guidelines.md)