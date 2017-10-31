---
title: "特性“&lt;特性名&gt;”不能应用多次 | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
f1_keywords: 
  - "bc30663"
  - "vbc30663"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "BC30663"
ms.assetid: 3760e7ff-7238-40a1-8676-77d858a64fc0
caps.latest.revision: 9
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 9
---
# 特性“&lt;特性名&gt;”不能应用多次
[!INCLUDE[vs2017banner](../../../visual-basic/includes/vs2017banner.md)]

此特性只能应用一次。  `AttributeUsage` 特性决定了某个特性是否可以应用多次。  
  
 **错误 ID：**BC30663  
  
### 更正此错误  
  
1.  确保特性只应用一次。  
  
2.  如果使用的是自已开发的自定义特性，请考虑更改其 `AttributeUsage` 特性，以允许特性使用多次，如下面的示例所示。  
  
    ```  
    <AttributeUsage(AllowMultiple := True)>  
    ```  
  
## 请参阅  
 <xref:System.AttributeUsageAttribute>   
 [创建自定义特性](../Topic/Creating%20Custom%20Attributes%20\(C%23%20and%20Visual%20Basic\).md)   
 [AttributeUsage](../Topic/AttributeUsage%20\(C%23%20and%20Visual%20Basic\).md)