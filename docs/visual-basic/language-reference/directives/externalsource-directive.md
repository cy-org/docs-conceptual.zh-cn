---
title: "#ExternalSource 指令 | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
f1_keywords: 
  - "#Externalsource"
  - "#ExternalSource"
  - "vb.ExternalSource"
  - "Externalsource"
  - "vb.#ExternalSource"
  - "ExternalSource"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "#ExternalSource 指令"
  - "ExternalSource 指令 (#ExternalSource)"
ms.assetid: 243bc6a2-34c3-4eeb-a776-9fd2bf988149
caps.latest.revision: 160
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 160
---
# #ExternalSource 指令
[!INCLUDE[vs2017banner](../../../visual-basic/includes/vs2017banner.md)]

指示特定的源代码行与源外部的文本之间的映射。  
  
## 语法  
  
```  
#ExternalSource( StringLiteral , IntLiteral )  
    [ LogicalLine+ ]  
#End ExternalSource  
```  
  
## 部件  
 `StringLiteral`  
 外部源的路径。  
  
 `IntLiteral`  
 外部源第一行的行号。  
  
 `LogicalLine`  
 外部源中发生错误的行。  
  
 `#End ExternalSource`  
 终止 `#ExternalSource` 块。  
  
## 备注  
 此指令仅供编译器和调试器使用。  
  
 源文件可以包含外部源指令，这些指令指示源文件中的特定代码行与源外部的文本（如 .aspx 文件）的映射。  如果编译期间在指定的源代码中遇到错误，则会将这些错误标识为来自外部源。  
  
 外部源指令对编译无效，而且不能嵌套。  它们仅供应用程序内部使用。  
  
## 请参阅  
 [条件编译](../../../visual-basic/programming-guide/program-structure/conditional-compilation.md)