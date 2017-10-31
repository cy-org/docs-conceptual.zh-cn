---
title: "模拟与恢复 | Microsoft Docs"
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
  - "模拟 Windows 帐户"
  - "安全性 [.NET Framework], 模拟 Windows 帐户"
  - "WindowsIdentity 对象, 模拟"
ms.assetid: b93d402c-6c28-4f50-b2bc-d9607dc3e470
caps.latest.revision: 13
author: "mairaw"
ms.author: "mairaw"
manager: "wpickett"
caps.handback.revision: 11
---
# 模拟与恢复
有时你可能需要获取 Windows NT 帐户标记来模拟 Windows 帐户。 例如，基于 ASP.NET 的应用程序可能需要在不同时间代表多个用户进行工作。 应用程序可以从 Internet 信息服务 \(IIS\) 接受一个表示管理员的标记，模拟该用户，执行一项操作，然后还原到以前的身份。 然后，可以从 IIS 接受一个表示拥有较少权限的用户的标记，执行某项操作，并再次还原。  
  
 如果应用程序必须模拟一个未通过 IIS 附加到当前线程的 Windows 帐户，则必须检索该帐户的标记并用它来激活该帐户。 通过执行下列任务可实现这一目的：  
  
1.  通过调用非托管的 **LogonUser** 方法，检索特定用户的帐户标记。 此方法不在.NET Framework 基类库中，但在非托管 **advapi32.dll** 中。 访问非托管代码中的方法是一项高级的操作，不在本文的讨论范围之内。 有关详细信息，请参阅[与非托管代码交互操作](../../../docs/framework/interop/index.md)。 有关 **LogonUser** 方法和 **advapi32.dll** 的详细信息，请参阅平台 SDK 文档。  
  
2.  创建 **WindowsIdentity** 类的新实例，并向其传递标记。 下面的代码演示此调用，其中 `hToken` 表示 Windows 标记。  
  
    ```csharp  
    WindowsIdentity ImpersonatedIdentity = new WindowsIdentity(hToken);  
  
    ```  
  
    ```vb  
    Dim ImpersonatedIdentity As New WindowsIdentity(hToken)  
    ```  
  
3.  创建 <xref:System.Security.Principal.WindowsImpersonationContext> 类的新实例，并用已初始化类的 <xref:System.Security.Principal.WindowsIdentity.Impersonate%2A?displayProperty=fullName> 方法对它进行初始化，以开始模拟，如以下代码所示。  
  
    ```csharp  
    WindowsImpersonationContext MyImpersonation = ImpersonatedIdentity.Impersonate();  
  
    ```  
  
    ```vb  
    WindowsImpersonationContext MyImpersonation = ImpersonatedIdentity.Impersonate()  
    ```  
  
4.  当不再需要进行模拟时，调用 <xref:System.Security.Principal.WindowsImpersonationContext.Undo%2A?displayProperty=fullName> 方法还原模拟，如以下代码所示。  
  
    ```csharp  
    MyImpersonation.Undo();  
  
    ```  
  
    ```vb  
    MyImpersonation.Undo()  
    ```  
  
 如果受信任的代码已将 <xref:System.Security.Principal.WindowsPrincipal> 对象附加到线程，则可调用不采用帐户标记的 **Impersonate** 实例方法。 请注意，仅当线程上的 **WindowsPrincipal** 对象所表示的用户不是当前正在执行进程的用户时，此操作才有用。 例如，如果在使用 ASP.NET 时打开 Windows 身份验证并关闭模拟，则可能遇到此情形。 这时，进程在 Internet Information Services \(IIS\) 中配置的帐户下运行，而当前主体表示正在访问页面的 Windows 用户。  
  
 请注意，**Impersonate** 和 **Undo** 都不更改与当前调用上下文关联的 **Principal** 对象 \(<xref:System.Security.Principal.IPrincipal>\)。 相反，模拟和还原会更改与当前操作系统进程关联的标记。  
  
## 请参阅  
 <xref:System.Security.Principal.WindowsIdentity>   
 <xref:System.Security.Principal.WindowsImpersonationContext>   
 [主体和标识对象](../../../docs/standard/security/principal-and-identity-objects.md)   
 [与非托管代码交互操作](../../../docs/framework/interop/index.md)