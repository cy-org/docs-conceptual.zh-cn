---
title: "程序集绑定重定向安全权限 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "VB"
  - "CSharp"
  - "C++"
  - "jsharp"
helpviewer_keywords: 
  - "程序集 [.NET Framework], 绑定重定向"
  - "并行执行, 程序集绑定重定向"
ms.assetid: 24a5cdff-7ed9-4195-93f3-edf6899019fc
caps.latest.revision: 9
author: "mcleblanc"
ms.author: "markl"
manager: "markl"
caps.handback.revision: 8
---
# 程序集绑定重定向安全权限
应用程序配置文件中的显式程序集绑定重定向需要安全权限。  这适用于对 .NET Framework 程序集和来自第三方的程序集的重定向。  该权限可通过针对 [SecurityPermission Class](frlrfSystemSecurityPermissionsSecurityPermissionClassTopic)设置 [BindingRedirects](frlrfSystemSecurityPermissionsSecurityPermissionFlagClassTopic)标志来授予。  默认情况下，托管程序集没有任何权限。  
  
 安全权限应授予受信任的区域（本地计算机）内和 Intranet 区域内运行的应用程序。  严禁在 Internet 区域内运行的应用程序执行程序集绑定重定向。  
  
 如果在由组件发行者控制的发行者策略文件中执行程序集重定向，或者，在管理员控制的计算机配置文件中执行程序集重定向，则不需要这一权限。  然而，应用程序需要一个权限通过使用应用程序配置文件中[\<publisherPolicy apply\="no"\/\>](../../../docs/framework/configure-apps/file-schema/runtime/publisherpolicy-element.md)元素来显式地忽略版权政策。  
  
 下表显示了 **BindingRedirect** 标志的默认安全设置。  
  
|区域|BindingRedirect 标志设置|  
|--------|--------------------------|  
|受信任的区域（本地计算机）|**ON**|  
|Intranet 区域|**ON**|  
|Internet 区域|**OFF**|  
|不受信任的区域|**OFF**|  
  
 管理员可以更改这些安全设置，以支持或限制给定计算机上的特定方案。  没有工具可用来更改 **BindingRedirect** 标志的默认设置；管理员必须手动编辑用户计算机上的 Security.config 文件。  
  
## 请参阅  
 [Publisher Policy Files and Side\-by\-Side Execution](http://msdn.microsoft.com/zh-cn/97a042be-4d72-40c3-91c0-76fd36bdf133)   
 [如何：启用和禁用自动绑定重定向](../../../docs/framework/configure-apps/how-to-enable-and-disable-automatic-binding-redirection.md)   
 [并行执行](../../../docs/framework/deployment/side-by-side-execution.md)