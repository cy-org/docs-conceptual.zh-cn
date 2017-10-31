---
title: "疑难解答：调试 Windows 服务 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "调试 [Visual Studio], Windows 服务"
  - "调试 Windows 服务应用程序"
  - "服务, 调试"
  - "服务, 疑难解答"
  - "调试疑难解答, Windows 服务"
  - "服务应用程序疑难解答"
  - "Windows 服务应用程序, 调试"
  - "Windows 服务应用程序, 疑难解答"
ms.assetid: cf859d4c-f04c-4cb7-81e3-bc7de8bea190
caps.latest.revision: 8
author: "ghogen"
ms.author: "ghogen"
manager: "douge"
caps.handback.revision: 8
---
# 疑难解答：调试 Windows 服务
调试 Windows 服务应用程序时，服务与**“Windows 服务管理器”**进行交互。  **“服务管理器”**通过调用 <xref:System.ServiceProcess.ServiceBase.OnStart%2A> 方法启动服务，然后花 30 秒时间等待 <xref:System.ServiceProcess.ServiceBase.OnStart%2A> 方法返回。  如果在这段时间内方法没有返回，管理器将显示一个服务无法启动的错误。  
  
 按 [如何：调试 Windows 服务应用程序](../../../docs/framework/windows-services/how-to-debug-windows-service-applications.md) 中的介绍调试 <xref:System.ServiceProcess.ServiceBase.OnStart%2A> 方法时，必须注意这 30 秒的时间。  如果在 <xref:System.ServiceProcess.ServiceBase.OnStart%2A> 方法中放置一个断点并且在 30 秒内不通过该断点，则管理器不会启动服务。  
  
## 请参阅  
 [如何：调试 Windows 服务应用程序](../../../docs/framework/windows-services/how-to-debug-windows-service-applications.md)   
 [Windows 服务应用程序介绍](../../../docs/framework/windows-services/introduction-to-windows-service-applications.md)