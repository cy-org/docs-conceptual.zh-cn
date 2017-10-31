---
title: "无法获取日志的流 | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
f1_keywords: 
  - "vbrApplicationLog_ExhaustedPossibleStreamNames"
ms.assetid: 33994f52-8efb-4790-a459-033e5c1db632
caps.latest.revision: 8
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 8
---
# 无法获取日志的流
无法获取日志的流。 可能基于 \<name\> 的文件名已在使用中。  
  
 <xref:Microsoft.VisualBasic.Logging.FileLogTraceListener> 类未能创建新日志文件，原因是基于 \<name\> 的所有可能的日志文件名都已在使用中。  
  
 具有过多的日志文件可能表明应用程序存在结构问题。 有关详细信息，请参阅 <xref:Microsoft.VisualBasic.Logging.FileLogTraceListener> 类的文档。  
  
### 更正此错误  
  
1.  将 <xref:Microsoft.VisualBasic.Logging.FileLogTraceListener.LogFileCreationSchedule%2A> 属性设置为 <xref:Microsoft.VisualBasic.Logging.LogFileCreationScheduleOption> 或 <xref:Microsoft.VisualBasic.Logging.LogFileCreationScheduleOption>，以便在日志文件名中包含日期戳。  
  
2.  将现有日志存档后将其从计算机中删除，以允许 <xref:Microsoft.VisualBasic.Logging.FileLogTraceListener> 对象创建新日志。  
  
## 请参阅  
 <xref:Microsoft.VisualBasic.Logging.FileLogTraceListener>   
 <xref:Microsoft.VisualBasic.Logging.FileLogTraceListener.LogFileCreationSchedule%2A>   
 [My.Application.Log 对象](../../visual-basic/language-reference/objects/my-application-log-object.md)   
 [My.Log 对象](../../visual-basic/language-reference/objects/my-log-object.md)