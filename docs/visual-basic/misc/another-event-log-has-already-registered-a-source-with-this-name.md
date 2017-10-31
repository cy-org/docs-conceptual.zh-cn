---
title: "另一个事件日志已使用该名称注册了一个源 | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
ms.assetid: e6f5cd95-bb3f-4845-84fb-ae623a9bd44e
caps.latest.revision: 13
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 13
---
# 另一个事件日志已使用该名称注册了一个源
已尝试向事件日志写入条目，其中指定的源使用其他事件日志进行注册。  
  
 在组件将条目写入日志前，必须设置 <xref:System.Diagnostics.EventLog> 组件实例的 <xref:System.Diagnostics.EventLog.Source%2A> 属性。 发生此情况时，系统将检查所指定的源是否使用写入该组件的事件日志进行注册，并在需要时调用 <xref:System.Diagnostics.EventLog.CreateEventSource%2A>。  
  
### 更正此错误  
  
1.  使用 <xref:System.Diagnostics.EventLog.DeleteEventSource%2A> 或 <xref:System.Diagnostics.EventLog.DeleteEventSource%2A> 方法删除源与第一个日志之间的关联。  
  
2.  使用新的日志注册源。  
  
## 请参阅  
 [My.Application.Log 对象](../../visual-basic/language-reference/objects/my-application-log-object.md)   
 [How to: Remove an Event Source](http://msdn.microsoft.com/zh-cn/bc66c900-4b8a-426a-b8e2-17031a20167e)   
 [How to: Add Your Application as a Source of Event Log Entries](http://msdn.microsoft.com/zh-cn/948ff920-a739-4e66-a191-ee951512d42c)