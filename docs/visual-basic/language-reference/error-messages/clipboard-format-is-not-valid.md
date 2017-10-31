---
title: "剪贴板格式无效 | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
f1_keywords: 
  - "vbrID460"
dev_langs: 
  - "VB"
ms.assetid: 71a4a045-65bb-417d-b3bd-99a9fa3c53f6
caps.latest.revision: 10
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 10
---
# 剪贴板格式无效
[!INCLUDE[vs2017banner](../../../visual-basic/includes/vs2017banner.md)]

指定的剪贴板格式与所执行的方法不兼容。  该错误可能的原因包括：  
  
-   对剪贴板格式使用了剪贴板的 `GetText` 或 `SetText` 方法，而不是 `vbCFText` 或 `vbCFLink`。  
  
-   对剪贴板格式使用了剪贴板的 `GetData` 或 `SetData` 方法，而不是 `vbCFBitmap`、`vbCFDIB` 或 `vbCFMetafile`。  
  
-   当 Microsoft Windows 为注册格式保留的范围 \(&HC000\-&HFFFF\) 中的某个剪贴板格式尚未向 Microsoft Windows 注册时，对该剪贴板格式使用了 `DataObject` `GetData` 方法或 `SetData` 方法。  
  
### 更正此错误  
  
-   移除无效格式并指定一种有效格式。  
  
## 请参阅  
 [剪贴板：添加其他格式](../Topic/Clipboard:%20Adding%20Other%20Formats.md)