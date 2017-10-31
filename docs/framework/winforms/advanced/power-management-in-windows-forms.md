---
title: "Windows 窗体中的电源管理 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-winforms"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "jsharp"
helpviewer_keywords: 
  - "电池状态"
  - "电源状态"
ms.assetid: ad04a801-5682-4d88-92c5-26eb9cdb209a
caps.latest.revision: 18
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 18
---
# Windows 窗体中的电源管理
Windows 窗体应用程序可以使用 Windows 操作系统中的电源管理功能。  应用程序可以监视计算机的电源状态，并在发生状态更改时采取措施。  例如，如果应用程序在便携式计算机上运行，则可能需要在计算机的电池电量低于某一特定水平时禁用应用程序的某些功能。  
  
 [!INCLUDE[dnprdnshort](../../../../includes/dnprdnshort-md.md)] 提供了 <xref:Microsoft.Win32.SystemEvents.PowerModeChanged> 事件，一旦电源状态更改时（例如，当用户挂起或继续操作系统时，或者当交流电源状态或电池状态更改时），此事件就会发生。  <xref:System.Windows.Forms.SystemInformation> 类的 <xref:System.Windows.Forms.SystemInformation.PowerStatus%2A> 属性可以用来查询当前状态，如下面的代码示例所示：  
  
 [!code-csharp[PowerMode#1](../../../../samples/snippets/csharp/VS_Snippets_Winforms/powermode/cs/form1.cs#1)]
 [!code-vb[PowerMode#1](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/powermode/vb/form1.vb#1)]  
  
 除 <xref:System.Windows.Forms.BatteryChargeStatus> 枚举外，<xref:System.Windows.Forms.SystemInformation.PowerStatus%2A> 属性还包含用于确定电池容量 \(<xref:System.Windows.Forms.PowerStatus.BatteryFullLifetime%2A>\) 和电池电量百分比（<xref:System.Windows.Forms.PowerStatus.BatteryLifePercent%2A>、<xref:System.Windows.Forms.PowerStatus.BatteryLifeRemaining%2A>）的枚举。  
  
 可以使用 <xref:System.Windows.Forms.Application> 的 <xref:System.Windows.Forms.Application.SetSuspendState%2A> 方法将计算机置于休眠或挂起模式。  如果将 `force` 参数设置为 `false`，操作系统将向所有请求挂起权限的应用程序广播事件。  如果将 `disableWakeEvent` 参数设置为 `true`，操作系统将禁用所有唤醒事件。  
  
 下面的代码示例演示如何将计算机置于休眠模式。  
  
 [!code-csharp[PowerMode#2](../../../../samples/snippets/csharp/VS_Snippets_Winforms/powermode/cs/form1.cs#2)]
 [!code-vb[PowerMode#2](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/powermode/vb/form1.vb#2)]  
  
## 请参阅  
 <xref:Microsoft.Win32.SystemEvents.PowerModeChanged>   
 <xref:System.Windows.Forms.SystemInformation.PowerStatus%2A>   
 <xref:System.Windows.Forms.Application.SetSuspendState%2A>   
 <xref:Microsoft.Win32.SystemEvents.SessionSwitch>