---
title: "XML 注释异常必须具有“cref”特性 | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
f1_keywords: 
  - "bc42319"
  - "vbc42319"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "BC42319"
ms.assetid: 62eeeba3-6811-48be-b1ef-c2e4feda3177
caps.latest.revision: 13
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 13
---
# XML 注释异常必须具有“cref”特性
[!INCLUDE[vs2017banner](../../../visual-basic/includes/vs2017banner.md)]

\<exception\> 标记提供一种方法以记录可能由方法引发的异常。  必选的 `cref` 特性指定成员的名称，它由文档生成器检查。  如果该成员存在，它将被转换为文档文件中的规范化元素名称。  
  
 **错误 ID：** BC42319  
  
### 更正此错误  
  
-   将 `cref` 特性添加至下面的异常：  
  
    ```  
    '''<exception cref="member">description</exception>  
    ```  
  
## 请参阅  
 [\<exception\>](../../../visual-basic/language-reference/xmldoc/exception.md)   
 [如何：创建 XML 文档](../../../visual-basic/programming-guide/program-structure/how-to-create-xml-documentation.md)   
 [XML 注释标记](../../../visual-basic/language-reference/xmldoc/recommended-xml-tags-for-documentation-comments.md)