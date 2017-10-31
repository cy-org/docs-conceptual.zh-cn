---
title: "必须首先用一个“PathName”参数调用“Dir”函数 | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
f1_keywords: 
  - "vbrDIR_IllegalCall"
dev_langs: 
  - "VB"
ms.assetid: 7b5d149f-be91-4ac3-8262-86a360894e7d
caps.latest.revision: 7
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 7
---
# 必须首先用一个“PathName”参数调用“Dir”函数
[!INCLUDE[vs2017banner](../../../visual-basic/includes/vs2017banner.md)]

对 `Dir` 函数的初始调用没有包括 `PathName` 参数。  第一次调用 `Dir` 必须包括 `PathName`，但随后调用 `Dir` 则不需要包括参数即可检索下一项。  
  
### 更正此错误  
  
1.  在函数调用中提供 `PathName` 参数。  
  
## 请参阅  
 <xref:Microsoft.VisualBasic.FileSystem.Dir%2A>