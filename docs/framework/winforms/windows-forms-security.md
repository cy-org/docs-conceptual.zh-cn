---
title: "Windows 窗体安全 | Microsoft Docs"
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
  - "访问控制, Windows 窗体"
  - "设计器访问安全性"
  - "权限, Windows 窗体"
  - "安全性 [Windows 窗体]"
  - "安全策略, Windows 窗体"
  - "Windows 窗体, 安全性"
ms.assetid: 932d438a-5285-46d8-a958-8c93d0ad6cae
caps.latest.revision: 8
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 8
---
# Windows 窗体安全
Windows 窗体以一种基于代码的安全模型为特色（为代码设置了安全性级别，而不论运行代码的用户是什么人）。  这种安全模型会加强计算机系统上已有的任何安全性架构。  这些架构包括浏览器中或操作系统中的安全性架构，例如 Internet Explorer 中提供的基于区域的安全性就属于浏览器中的安全性架构，Windows NT 的基于凭据的安全性就属于操作系统中的安全性架构。  
  
## 本节内容  
 [Windows 窗体中的安全性概述](../../../docs/framework/winforms/security-in-windows-forms-overview.md)  
 简要说明 .NET Framework 的安全模型以及确保应用程序中的 Windows 窗体安全所需的基本步骤。  
  
 [Windows 窗体中更加安全的文件和数据访问](../../../docs/framework/winforms/more-secure-file-and-data-access-in-windows-forms.md)  
 描述如何在不完全受信任的环境中访问文件和数据。  
  
 [Windows 窗体中的更加安全的打印](../../../docs/framework/winforms/more-secure-printing-in-windows-forms.md)  
 描述如何在不完全受信任的环境中访问打印功能。  
  
 [Windows 窗体中额外的安全注意事项](../../../docs/framework/winforms/additional-security-considerations-in-windows-forms.md)  
 介绍在不完全受信任的环境中如何执行窗口管理、使用剪贴板以及调用非托管代码。  
  
## 相关章节  
 [NIB: Default Security Policy](http://msdn.microsoft.com/zh-cn/2c086873-0894-4f4d-8f7e-47427c1a3b55)  
 列出了在 Full Trust、Local Intranet 和 Internet 权限集中授予的默认权限。  
  
 [NIB: General Security Policy Administration](http://msdn.microsoft.com/zh-cn/5121fe35-f0e3-402c-94ab-4f35b0a87b4b)  
 提供了有关如何管理 .NET Framework 安全策略和如何提升权限的信息。  
  
 [危险权限和策略管理](../../../docs/framework/misc/dangerous-permissions-and-policy-administration.md)  
 讨论某些可能允许安全系统被避开的 .NET Framework 权限。  
  
 [代码安全维护指南](../../../docs/standard/security/secure-coding-guidelines.md)  
 链接到解释在 .NET Framework 中编写安全代码的最佳方法的主题。  
  
 [NIB: Requesting Permissions](http://msdn.microsoft.com/zh-cn/0447c49d-8cba-45e4-862c-ff0b59bebdc2)  
 讨论一些特性的用法，这些特性告知运行时，代码的运行需要哪些权限。  
  
 [安全性的基础概念](../../../docs/standard/security/key-security-concepts.md)  
 链接到探讨代码安全性基础概念的主题。  
  
 [代码访问安全性基础知识](../../../docs/framework/misc/code-access-security-basics.md)  
 讨论使用 .NET Framework 运行时安全策略的基础知识。  
  
 [NIB: Determining When to Modify Security Policy](http://msdn.microsoft.com/zh-cn/af749b17-e461-409d-84b9-a3d44789db16)  
 解释如何确定应用程序需要修改默认安全策略的时机。  
  
 [NIB: Deploying Security Policy](http://msdn.microsoft.com/zh-cn/f936c1e5-033b-4bd9-a3bd-a39ba733a681)  
 讨论部署安全策略更改的最佳方式。