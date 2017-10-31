---
title: "Windows 窗体和非托管应用程序 | Microsoft Docs"
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
  - "ActiveX 控件 [Windows 窗体]"
  - "COM [Windows 窗体]"
  - "COM 互操作, Windows 窗体"
  - "Windows 窗体, 互操作"
  - "Windows 窗体, 非托管"
ms.assetid: 81bc100c-fa49-4614-85a6-0f7ab59eac8a
caps.latest.revision: 12
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 12
---
# Windows 窗体和非托管应用程序
Windows 窗体应用程序和控件可以与非托管应用程序进行互操作，但有一些需要注意的问题。  以下各节将介绍 Windows 窗体应用程序和控件支持和不支持的方案和配置。  
  
## 本节内容  
 [Windows 窗体和非托管应用程序概述](../../../../docs/framework/winforms/advanced/windows-forms-and-unmanaged-applications-overview.md)  
 提供有关如何使用和实现运用非托管应用程序的 Windows 窗体控件的常规信息。  
  
 [如何：通过使用 ShowDialog 方法显示 Windows 窗体来支持 COM 互操作](../../../../docs/framework/winforms/advanced/com-interop-by-displaying-a-windows-form-shadow.md)  
 提供显示如何使用 <xref:System.Windows.Forms.Form.ShowDialog%2A?displayProperty=fullName> 方法在非托管应用程序中运行 Windows 窗体的代码示例。  
  
 [如何：通过在每个 Windows 窗体各自的线程上显示该 Windows 窗体来支持 COM 互操作](../../../../docs/framework/winforms/advanced/how-to-support-com-interop-by-displaying-each-windows-form-on-its-own-thread.md)  
 提供显示如何在各自的线程上运行 Windows 窗体的代码示例。  
  
 另请参阅[演练：通过在各自的线程上显示每个 Windows 窗体来支持 COM 互操作](http://msdn.microsoft.com/library/ms233639\(v=vs.110\))。  
  
## 参考  
 <xref:System.Windows.Forms.Form.ShowDialog%2A?displayProperty=fullName>  
 用于为 Windows 窗体中创建单独线程。  
  
 <xref:System.Windows.Forms.Application.Run%2A?displayProperty=fullName>  
 启动线程的消息循环。  
  
 <xref:System.Windows.Forms.Control.Invoke%2A>  
 将来自非托管应用程序的调用封送到窗体。  
  
## 相关章节  
 [向 COM 公开 .NET Framework 组件](../../../../docs/framework/interop/exposing-dotnet-components-to-com.md)  
 提供有关如何在非托管应用程序中使用 .NET Framework 类型的常规信息。