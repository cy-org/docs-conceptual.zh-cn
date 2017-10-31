---
title: "由于内部错误，无法获取完整的操作系统名 | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
f1_keywords: 
  - "vbrDiagnosticInfo_FullOSName"
ms.assetid: f69da02b-eb9a-4284-bb9e-3025517ae6c1
caps.latest.revision: 9
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 9
---
# 由于内部错误，无法获取完整的操作系统名
由于内部错误，无法获取完整的操作系统名。 这可能由当前计算机上不存在 WMI 导致。  
  
 对 `My.Computer.Info.OSFullName` 属性的调用失败。 此失败的可能原因是当前计算机上是否未安装 Windows Management Instrumentation \(WMI\)。  
  
### 更正此错误  
  
1.  将调用周围的 `Try...Catch` 块添加到 `My.Computer.Info.OSFullName` 属性。  
  
2.  有关 WMI 和如何安装它的详细信息，请转到  并搜索“Windows Management Instrumentation Core”。  
  
## 请参阅  
 [My.Computer.Info.OSFullName 属性](http://msdn.microsoft.com/zh-cn/b3b0fbd1-4dc5-428a-ad04-0d9fc9c2a9be)   
 [Visual Basic 中的异常与错误处理](http://msdn.microsoft.com/zh-cn/3e351e73-cf23-40ab-8b60-05794160529e)   
 [Try...Catch...Finally 语句](../../visual-basic/language-reference/statements/try-catch-finally-statement.md)