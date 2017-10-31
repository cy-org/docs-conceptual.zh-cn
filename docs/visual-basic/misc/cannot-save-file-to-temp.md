---
title: "无法将文件保存到 TEMP | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
f1_keywords: 
  - "vbrID735"
ms.assetid: 1055fc15-9641-43b2-a40c-a0a9fbbb34b2
caps.latest.revision: 7
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 7
---
# 无法将文件保存到 TEMP
组件找不到名为 TEMP 目录，或者包含 TEMP 目录的驱动器或分区的空间不足，不能保存信息。  
  
### 更正此错误  
  
1.  创建一个名为“TEMP”目录，并将 TEMP 环境变量设置为它的路径。  
  
2.  通过清除不必要的文件增加驱动器空间，或者在另一个分区上创建一个临时目录，然后将 TEMP 环境变量设置为它的路径。  
  
## 请参阅  
 [错误类型](../../visual-basic/programming-guide/language-features/error-types.md)