---
title: "主体和标识对象 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-standard"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "VB"
  - "CSharp"
  - "C++"
  - "jsharp"
helpviewer_keywords: 
  - "GenericIdentity 对象"
  - "GenericPrincipal 对象"
  - "标识对象, 关于标识对象"
  - "主体对象, 关于主体对象"
  - "安全性 [.NET Framework], 标识对象"
  - "安全性 [.NET Framework], 用户"
  - "WindowsIdentity 对象"
  - "WindowsPrincipal 对象"
ms.assetid: aa5930ad-f3d7-40aa-b6f6-c6edcd5c64f7
caps.latest.revision: 9
author: "mairaw"
ms.author: "mairaw"
manager: "wpickett"
caps.handback.revision: 8
---
# 主体和标识对象
托管代码可通过 [Principal](frlrfSystemSecurityPrincipalIPrincipalClassTopic) 对象发现主体的标识或角色，该对象包含对 [Identity](frlrfSystemSecurityPrincipalIIdentityClassTopic) 对象的引用。  将标识和主体对象同用户与组帐户这样常见的概念进行比较，可能会有所帮助。  在多数网络环境中，用户帐户表示人员或程序，而组帐户表示特定类别的用户及其拥有的权限。  同样，.NET Framework 中的标识对象表示用户，而角色表示成员条件与安全性上下文。  在 .NET Framework 中，主体对象同时封装标识对象和角色。.NET Framework 应用程序根据主体的标识或角色成员条件（后者更常见）来向主体授予权限。  
  
## 标识对象  
 标识对象封装有关正在验证的用户或实体的信息。  在最基本的级别上，标识对象包含名称和身份验证类型。  名称可以是用户名或 Windows 帐户名，而身份验证类型可以是所支持的登录协议（如 Kerberos V5）或自定义值。  .NET Framework 定义了一个 <xref:System.Security.Principal.GenericIdentity> 对象和一个更专用的 <xref:System.Security.Principal.WindowsIdentity> 对象，前者可用于大多数自定义登录方案，后者可用于希望应用程序依赖 Windows 身份验证的情况。  此外，您还可以定义自己的标识类来封装自定义用户信息。  
  
 <xref:System.Security.Principal.IIdentity> 接口定义用于访问名称和身份验证类型（例如 Kerberos V5 或 NTLM）的属性。  所有 **Identity** 类均实现 **IIdentity** 接口。  **Identity** 对象同执行当前线程所用的 Windows NT 进程标记之间不需要有什么关系。  但是，如果 **Identity** 对象是 **WindowsIdentity** 对象，则假定标识表示 Windows NT 安全标记。  
  
## 主体对象  
 主体对象表示代码运行时所在的安全上下文。  实现基于角色的安全性的应用程序将基于与主体对象关联的角色来授予权限。  与标识对象相似，.NET Framework 也提供了 <xref:System.Security.Principal.GenericPrincipal> 对象和 <xref:System.Security.Principal.WindowsPrincipal> 对象。  您还可以定义自己的自定义主体类。  
  
 <xref:System.Security.Principal.IPrincipal> 接口定义一个属性和一个方法，前者用于访问关联的 **Identity** 对象，后者用于确定 **Principal** 对象所标识的用户是否为给定角色的成员。  所有 **Principal** 类都实现 **IPrincipal** 接口以及任何必需的附加属性和方法。  例如，公共语言运行时提供了 **WindowsPrincipal** 类，该类实现将 Windows NT 或 Windows 2000 组成员条件映射到角色的附加功能。  
  
 **Principal** 对象将被绑定到应用程序域 \(<xref:System.AppDomain>\) 内部的调用上下文 \(<xref:System.Runtime.Remoting.Messaging.CallContext>\) 对象。  默认的调用上下文总是用每个新的 **AppDomain** 创建的，因此总是存在可用于接受 **Principal** 对象的调用上下文。  创建新线程的同时也为该线程创建 **CallContext** 对象。  **Principal** 对象引用从创建线程自动复制到新线程的 **CallContext** 中。  如果运行时无法确定哪个 **Principal** 对象属于线程的创建者，它将遵循 **Principal** 和 **Identity** 对象创建的默认策略。  
  
 可配置的应用程序域特定策略定义了一些规则，用以决定同新的应用程序域关联的 **Principal** 对象类型。  在安全策略的允许范围内，运行时可创建 **Principal** 和 **Identity** 对象来反射同当前执行线程关联的操作系统标记。  默认情况下，运行时使用 **Principal** 和 **Identity** 对象表示未经身份验证的用户。  运行时不创建这些默认的 **Principal** 和 **Identity** 对象，除非代码尝试访问它们。  
  
 创建应用程序域的受信任代码可设置应用程序域策略，以控制默认 **Principal** 和 **Identity** 对象的构造。  此应用程序域特定的策略适用于该应用程序域中的所有执行线程。  非托管的受信任宿主本身就具有设置此策略的能力，但托管代码必须具有控制域策略的 <xref:System.Security.Permissions.SecurityPermission?displayProperty=fullName> 才能设置此策略。  
  
 在不同的应用程序域之间、但在同一进程内（因此在同一台计算机上）传输 **Principal** 对象时，远程基础结构将同调用方上下文相关联的、对 **Principal** 对象的引用复制到被调用方的上下文中。  
  
## 请参阅  
 [如何：创建 WindowsPrincipal 对象](../../../docs/standard/security/how-to-create-a-windowsprincipal-object.md)   
 [如何：创建 GenericPrincipal 和 GenericIdentity 对象](../../../docs/standard/security/how-to-create-genericprincipal-and-genericidentity-objects.md)   
 [替换 Principal 对象](../../../docs/standard/security/replacing-a-principal-object.md)   
 [模拟与恢复](../../../docs/standard/security/impersonating-and-reverting.md)   
 [基于角色的安全性](../../../docs/standard/security/role-based-security.md)   
 [安全性的基础概念](../../../docs/standard/security/key-security-concepts.md)