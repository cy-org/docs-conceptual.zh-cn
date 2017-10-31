---
title: "无法建立必要的临时文件。 | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
f1_keywords: 
  - "vbrID322"
dev_langs: 
  - "VB"
ms.assetid: 53617b5b-eb06-4188-b4c2-8607cb9fbc79
caps.latest.revision: 6
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 6
---
# 无法建立必要的临时文件。
[!INCLUDE[vs2017banner](../../../visual-basic/includes/vs2017banner.md)]

由 TEMP 环境变量指定的目录所在的驱动器已满，或者 TEMP 环境变量指定了无效或只读的驱动器或目录。  
  
### 更正此错误  
  
1.  如果驱动器已满，请删除驱动器中的部分文件。  
  
2.  在 TEMP 环境变量中指定其他驱动器。  
  
3.  为 TEMP 环境变量指定有效的驱动器。  
  
4.  从当前指定的驱动器或目录中，移除只读限制。  
  
## 请参阅  
 [错误类型](../../../visual-basic/programming-guide/language-features/error-types.md)