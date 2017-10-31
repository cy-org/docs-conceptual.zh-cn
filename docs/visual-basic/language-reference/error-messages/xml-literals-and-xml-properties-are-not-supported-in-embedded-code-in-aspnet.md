---
title: "ASP.NET 中的嵌入式代码不支持 XML 文本和 XML 属性 | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
f1_keywords: 
  - "vbc31200"
  - "bc31200"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "BC31200"
ms.assetid: 053e8cba-8584-45cc-9fa0-43d122779772
caps.latest.revision: 9
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 9
---
# ASP.NET 中的嵌入式代码不支持 XML 文本和 XML 属性
[!INCLUDE[vs2017banner](../../../visual-basic/includes/vs2017banner.md)]

ASP.NET 中的嵌入式代码不支持 XML 文本和 XML 属性。若要使用 XML 功能，请将代码移到代码隐藏文件中。  
  
 在 ASP.NET 文件中的嵌入式代码（`<%= =>`）内定义 XML 文本或 XML 轴属性。  
  
 **错误 ID：**BC31200  
  
### 更正此错误  
  
-   将包括 XML 文本或 XML 轴属性的代码移到 ASP.NET 代码隐藏文件中。  
  
## 请参阅  
 [XML 文本](../../../visual-basic/language-reference/xml-literals/index.md)   
 [XML 轴属性](../../../visual-basic/language-reference/xml-axis/xml-axis-properties.md)   
 [XML](../../../visual-basic/programming-guide/language-features/xml/index.md)