---
title: "友元程序集引用 &lt;引用&gt; 无效 | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
f1_keywords: 
  - "vbc31535"
  - "bc31535"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "BC31535"
ms.assetid: 6540c1d0-bb19-4051-a579-2e4f9094585e
caps.latest.revision: 5
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 5
---
# 友元程序集引用 &lt;引用&gt; 无效
[!INCLUDE[vs2017banner](../../../visual-basic/includes/vs2017banner.md)]

友元程序集引用 \<引用\> 无效。强名称签名的程序集必须在其 InternalsVisibleTo 声明中指定一个公钥。  
  
 传递给 <xref:System.Runtime.CompilerServices.InternalsVisibleToAttribute> 特性构造函数的程序集名称标识强名称程序集，但不包含 `PublicKey` 特性。  
  
 **错误 ID：**BC31535  
  
### 更正此错误  
  
1.  确定强名称友元程序集的公钥。  添加此公钥，将其作为使用 `PublicKey` 特性传递给 <xref:System.Runtime.CompilerServices.InternalsVisibleToAttribute> 特性构造函数的程序集名称的一部分。  
  
## 请参阅  
 <xref:System.Reflection.AssemblyName>   
 [友元程序集](../Topic/Friend%20Assemblies%20\(C%23%20and%20Visual%20Basic\).md)   
 [如何：创建签名的友元程序集](../Topic/How%20to:%20Create%20Signed%20Friend%20Assemblies%20\(C%23%20and%20Visual%20Basic\).md)