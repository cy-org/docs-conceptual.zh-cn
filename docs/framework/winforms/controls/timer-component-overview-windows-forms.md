---
title: "Timer 组件概述（Windows 窗体） | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-winforms"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "Timer"
dev_langs: 
  - "jsharp"
helpviewer_keywords: 
  - "Timer 组件 [Windows 窗体], 关于 Timer 组件"
  - "计时器, 关于计时器"
ms.assetid: e672c05b-a8b6-4b26-9e4d-9223aa9e3873
caps.latest.revision: 9
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 9
---
# Timer 组件概述（Windows 窗体）
Windows 窗体 <xref:System.Windows.Forms.Timer> 是定期引发事件的组件。  该组件是为 Windows 窗体环境设计的。  如果您需要适合服务器环境的计时器，请参见 [Introduction to Server\-Based Timers](http://msdn.microsoft.com/zh-cn/adc0bc0a-a519-4812-bafc-fb9d1a5801fc)。  
  
## 主要属性、方法和事件  
 时间间隔的长度由 <xref:System.Windows.Forms.Timer.Interval%2A> 属性定义，其值以毫秒为单位。  若启用了该组件，则每个时间间隔引发一个 <xref:System.Windows.Forms.Timer.Tick> 事件。  这是添加要执行的代码的位置。  有关更多信息，请参见 [如何：使用 Windows 窗体计时器组件以设置的间隔运行过程](../../../../docs/framework/winforms/controls/run-procedures-at-set-intervals-with-wf-timer-component.md)。  <xref:System.Windows.Forms.Timer> 组件的主要方法包括 <xref:System.Windows.Forms.Timer.Start%2A> 和 <xref:System.Windows.Forms.Timer.Stop%2A>，这两种方法可打开和关闭计时器。  计时器在关闭时重置；不存在暂停 <xref:System.Windows.Forms.Timer> 组件的方法。  
  
## 请参阅  
 <xref:System.Windows.Forms.Timer>   
 [Timer 组件](../../../../docs/framework/winforms/controls/timer-component-windows-forms.md)   
 [Windows 窗体 Timer 组件的 Interval 属性的限制](../../../../docs/framework/winforms/controls/limitations-of-the-timer-component-interval-property.md)