---
title: "没有鼠标滚轮 | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
f1_keywords: 
  - "vbrMouse_NoWheelIsPresent"
ms.assetid: e924ffba-4af1-4247-9a6f-d19a03738f62
caps.latest.revision: 10
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 10
---
# 没有鼠标滚轮
调用了 `My.Computer.Mouse.WheelScrollLines` 属性，但鼠标没有滚轮。  
  
### 更正此错误  
  
-   检查 `My.Computer.Mouse.WheelExists` 属性，以查看鼠标是否有滚轮，然后再调用 `My.Computer.Mouse.WheelScrollLines` 属性。  
  
     \- 或 \-  
  
-   在计算机上安装带滚轮的鼠标。  
  
## 请参阅  
 [My.Computer.Mouse.WheelScrollLines 属性](http://msdn.microsoft.com/zh-cn/67600f96-25d7-4dd9-946a-b46e1fc6a57f)   
 [My.Computer.Mouse.WheelExists 属性](http://msdn.microsoft.com/zh-cn/332d44f7-0b66-4eaa-b4ce-d7f161bfbd07)   
 [Visual Basic 中的异常与错误处理](http://msdn.microsoft.com/zh-cn/3e351e73-cf23-40ab-8b60-05794160529e)