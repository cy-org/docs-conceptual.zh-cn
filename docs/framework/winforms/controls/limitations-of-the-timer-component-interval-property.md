---
title: "Windows 窗体 Timer 组件的 Interval 属性的限制 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-winforms"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "jsharp"
helpviewer_keywords: 
  - "“间隔”属性, 限制"
  - "Timer 组件 [Windows 窗体], “间隔”属性的限制"
  - "计时器, 事件间隔"
  - "计时器, 基于 Windows 的"
ms.assetid: 7e5fb513-77e7-4046-a8e8-aab94e61ca0f
caps.latest.revision: 10
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 10
---
# Windows 窗体 Timer 组件的 Interval 属性的限制
Windows 窗体 <xref:System.Windows.Forms.Timer> 组件具有一个 <xref:System.Windows.Forms.Timer.Interval%2A> 属性，该属性指定一个计时器事件与下一个计时器事件之间间隔的毫秒数。  除非该组件被禁用，否则计时器会以大致相等的时间间隔继续接收 <xref:System.Windows.Forms.Timer.Tick> 事件。  
  
 该组件是为 Windows 窗体环境设计的。  如果您需要适合服务器环境的计时器，请参见 [Introduction to Server\-Based Timers](http://msdn.microsoft.com/zh-cn/adc0bc0a-a519-4812-bafc-fb9d1a5801fc)。  
  
## Interval 属性  
 当编写 <xref:System.Windows.Forms.Timer> 组件时，需要考虑 <xref:System.Windows.Forms.Timer.Interval%2A> 属性的几点限制：  
  
-   如果应用程序或另一个应用程序对系统需求很大（如长循环、大量的计算或驱动程序、网络或端口访问），那么应用程序可能无法以 <xref:System.Windows.Forms.Timer.Interval%2A> 属性指定的频率来获取计时器事件。  
  
-   不能保证间隔所精确经过的时间。  若要确保精确，计时器应根据需要检查系统时钟，而不是尝试在内部跟踪所积累的时间。  
  
-   <xref:System.Windows.Forms.Timer.Interval%2A> 属性的精度为毫秒。  某些计算机提供分辨率高于毫秒的高分辨率计数器。  是否具有这种计数器取决于计算机的处理器硬件。  有关更多信息，请参见位于 http:\/\/support.microsoft.com 上的 Microsoft 知识库文章 172338“How To Use QueryPerformanceCounter to Time Code”（如何使用 QueryPerformanceCounter 对代码计时）。  
  
## 请参阅  
 <xref:System.Windows.Forms.Timer>   
 [Timer 组件](../../../../docs/framework/winforms/controls/timer-component-windows-forms.md)   
 [Timer 组件概述](../../../../docs/framework/winforms/controls/timer-component-overview-windows-forms.md)