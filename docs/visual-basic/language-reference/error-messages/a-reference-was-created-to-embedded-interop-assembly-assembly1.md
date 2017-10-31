---
title: "创建了对嵌入的互操作程序集“&lt;assembly1&gt;”的引用，因为程序集“&lt;assembly2&gt;”间接引用了该程序集 | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
f1_keywords: 
  - "vbc40059"
  - "bc40059"
helpviewer_keywords: 
  - "BC40059"
  - "VBC40059"
ms.assetid: 520e39cb-8ab6-46f5-aa00-08afd51b4b7c
caps.latest.revision: 9
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 9
---
# 创建了对嵌入的互操作程序集“&lt;assembly1&gt;”的引用，因为程序集“&lt;assembly2&gt;”间接引用了该程序集
[!INCLUDE[vs2017banner](../../../visual-basic/includes/vs2017banner.md)]

创建了对嵌入的互操作程序集“\<assembly1\>”的引用，因为程序集“\<assembly2\>”间接引用了该程序集。请考虑更改任一程序集的“嵌入互操作类型”属性。  
  
 您已添加了一个对 `Embed Interop Types` 属性设置为 `True` 的程序集 \(assembly1\) 的引用。  这将指示编译器嵌入该程序集中的互操作类型信息。  但是，编译器无法嵌入该程序集中的互操作类型信息，因为您已引用的另一个程序集 \(assembly2\) 也引用了该程序集 \(assembly1\) 并且它的 `Embed Interop Types` 属性设置为 `False`。  
  
> [!NOTE]
>  将某个程序集引用的 `Embed Interop Types` 属性设置为 `True` 相当于通过使用命令行编译器的 `/link` 选项来引用该程序集。  
  
 **错误 ID：**BC40059  
  
### 处理此警告  
  
-   若要嵌入这两个程序集的互操作类型信息，请将对 assembly1 的所有引用的 `Embed Interop Types` 属性设置为 `True`。  
  
-   若要移除此警告，您可以将 assembly1 的 `Embed Interop Types` 属性设置为 `False`。  在这种情况下，互操作类型信息由主互操作程序集 \(PIA\) 提供。  
  
## 请参阅  
 [\/link](../../../visual-basic/reference/command-line-compiler/link.md)   
 [Programming with Primary Interop Assemblies](http://msdn.microsoft.com/zh-cn/306fa1d6-0703-4004-9e93-d0a57f1be81e)