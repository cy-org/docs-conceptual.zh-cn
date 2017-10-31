---
title: "不支持 XML 实体引用 | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
f1_keywords: 
  - "vbc31180"
  - "bc31180"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "BC31180"
ms.assetid: 2a393327-d8e2-4187-85b1-642b4f53b4ae
caps.latest.revision: 6
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 6
---
# 不支持 XML 实体引用
[!INCLUDE[vs2017banner](../../../visual-basic/includes/vs2017banner.md)]

以 XML 文本值形式添加了未在 XML 1.0 规范中定义的实体引用（例如 `©`）。  在 XML 文本中仅支持 `&`、`"`、`<`、`>` 和 `'` XML 实体引用。  
  
 **错误 ID：**BC31180  
  
### 更正此错误  
  
-   移除不受支持的实体引用。  
  
## 请参阅  
 [XML 文本和 XML 1.0 规范](../../../visual-basic/programming-guide/language-features/xml/xml-literals-and-the-xml-1-0-specification.md)   
 [XML 文本](../../../visual-basic/language-reference/xml-literals/index.md)   
 [XML](../../../visual-basic/programming-guide/language-features/xml/index.md)