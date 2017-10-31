---
title: "安全透明的代码 | Microsoft Docs"
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
  - "安全透明的代码"
  - "透明代码"
ms.assetid: 4f3dd841-82f7-4659-aab0-6d2db2166c65
caps.latest.revision: 24
author: "mairaw"
ms.author: "mairaw"
manager: "wpickett"
caps.handback.revision: 24
---
# 安全透明的代码
<a name="top"></a> [!INCLUDE[net_security_note](../../../includes/net-security-note-md.md)]  
  
 安全性涉及三个交互部分：沙盒处理、权限和强制。 沙盒处理是指创建隔离域的做法，在隔离域中某些代码被视为完全信任，而其他代码则被限制为沙盒授予集中的权限。 在沙盒授予集内运行的应用程序代码被视为透明的，也就是说，它不能执行任何影响安全性的操作。 沙盒的授予集由证据（<xref:System.Security.Policy.Evidence> 类）决定。 证据标识沙盒需要哪些特定权限，以及可以创建哪种沙盒。 强制是指允许透明代码仅在其授予集内执行。  
  
> [!IMPORTANT]
>  安全策略是旧版 .NET Framework 中的关键元素。 从 [!INCLUDE[net_v40_long](../../../includes/net-v40-long-md.md)] 开始，安全策略已过时。 安全策略的取消独立于安全透明度。 有关此更改效果的信息，请参阅 [代码访问安全策略兼容性和迁移](../../../docs/framework/misc/code-access-security-policy-compatibility-and-migration.md)。  
  
 本主题更详细地介绍透明度模型。 它包含下列部分：  
  
-   [透明度模型的用途](#purpose)  
  
-   [指定透明度级别](#level)  
  
-   [透明度强制](#enforcement)  
  
<a name="purpose"></a>   
## 透明度模型的用途  
 透明度是一种强制机制，用于将作为应用程序的一部分运行的代码与作为基础结构的一部分运行代码区分开来。 透明度在可以执行特许事件（例如调用本机代码）的代码（关键代码）和无法执行的代码（透明代码）之间绘制一个屏障。 透明代码可以在其运行的权限集边界内执行命令，但不能执行、派生自或包含关键代码。  
  
 透明度强制的主要目标是提供简单而有效的机制，以基于特权隔离不同的代码组。 在沙盒处理模型的上下文中，这些特权组是完全信任的（即不受限制）或部分信任的（即限于授予沙盒的权限集）。  
  
> [!IMPORTANT]
>  透明度模型优于代码访问安全性。 透明度由实时编译器强制执行，并保持有效，而不考虑程序集的授予集（包括完全信任）。  
  
 .NET Framework 2.0 版中引入了透明度，用于简化安全模型，使其更易于编写和部署安全库和应用程序。 Microsoft Silverlight 中也使用了透明代码，用于简化部分信任的应用程序的开发。  
  
> [!NOTE]
>  当开发部分信任的应用程序时，必须知道目标主机的权限要求。 你可以开发使用某些主机不允许的资源的应用程序。 此应用程序编译时不会出错，但将无法加载到托管环境中。 如果已使用 Visual Studio 开发了应用程序，就可以在部分信任的环境中启用调试或在开发环境中启用受限的权限集。 有关详细信息，请参阅[如何：使用受限权限对 ClickOnce 应用程序进行调试](../Topic/How%20to:%20Debug%20a%20ClickOnce%20Application%20with%20Restricted%20Permissions.md)。 为 ClickOnce 应用程序提供的计算权限功能也可用于部分信任的任何应用程序。  
  
 [返回页首](#top)  
  
<a name="level"></a>   
## 指定透明度级别  
 程序集级别的 <xref:System.Security.SecurityRulesAttribute> 特性显式选择该程序集将遵循的 <xref:System.Security.SecurityRuleSet> 规则。 这些规则在数字级别系统下组织，级别越高表示安全规则的强制性越高。  
  
 级别如下：  
  
-   2 级 \(<xref:System.Security.SecurityRuleSet>\) – [!INCLUDE[net_v40_short](../../../includes/net-v40-short-md.md)] 透明度规则。  
  
-   1 级 \(<xref:System.Security.SecurityRuleSet>\) –.NET Framework 2.0 透明度规则。  
  
 这两个透明度级别之间的主要区别是 1 级不对程序集外部的调用强制实施透明度规则，并且预期仅用于实现兼容性。  
  
> [!IMPORTANT]
>  你应仅出于兼容性目的指定 1 级透明度，也就是说，仅为使用 .NET Framework 3.5 或更早版本（这些版本使用 <xref:System.Security.AllowPartiallyTrustedCallersAttribute> 属性或不使用透明度模型）开发的代码指定 1 级。 例如，对允许从部分信任的调用方 \(APTCA\) 调用的 .NET Framework 2.0 程序集使用 1 级透明度。 有关针对 [!INCLUDE[net_v40_short](../../../includes/net-v40-short-md.md)] 开发的代码，请始终使用 2 级透明度。  
  
### 2 级透明度  
 [!INCLUDE[net_v40_long](../../../includes/net-v40-long-md.md)] 中引入了 2 级透明度。 此模型的三条原则是透明代码、安全可靠关键代码和安全关键代码。  
  
-   透明代码（无论授予什么样的权限）可以调用其他透明代码或安全可靠关键代码。 如果代码是部分信任的代码，那么它只能执行域权限集允许的操作。 透明代码不能：  
  
    -   执行 <xref:System.Security.CodeAccessPermission.Assert%2A> 操作或特权提升。  
  
    -   包含不安全或不可验证的代码。  
  
    -   直接调用关键代码。  
  
    -   调用本机代码或具有 <xref:System.Security.SuppressUnmanagedCodeSecurityAttribute> 特性的代码。  
  
    -   调用受 <xref:System.Security.Permissions.SecurityAction> 保护的成员。  
  
    -   从关键类型继承。  
  
     此外，透明方法不能重写关键虚拟方法或实现关键接口方法。  
  
-   安全可靠关键代码是完全信任的代码，且可被透明代码调用的代码。 它公开完全信任代码的有限外围应用。 可靠关键代码中会进行正确性和安全性验证。  
  
-   安全关键代码可以调用完全信任的任何代码，但不能被透明代码调用。  
  
### 1 级透明度  
 .NET Framework 2.0 版中引入了 1 级透明度模型，目的是便于开发人员减少需要接受安全性审核的代码数量。 虽然 1 级透明度在 2.0 版中公开提供，但它主要仅在 Microsoft 内部用于安全性审核目的。 开发人员可以通过批注声明哪些类型和成员可以执行安全提升和其他信任操作（安全关键），哪些不能执行（安全透明）。 标识为透明的代码不需要高度的安全性审核。 1 级透明度表明透明度强制仅限于程序集内部。 换而言之，标识为安全关键的任何公共类型或成员仅在该程序集内部是安全关键的。 如果希望在从程序集外部调用这些类型和成员时对它们强制实施安全性，则必须使用完全信任的链接要求。 如果不这样做，则公开可见的安全关键类型和成员将被视为安全可靠关键，并且可在程序集外部被部分信任的代码调用。  
  
 1 级透明度模型具有以下限制：  
  
-   安全关键类型和成员是公开的，可从安全透明代码访问。  
  
-   只能在程序集内部强制进行透明度批注。  
  
-   安全关键类型和成员必须使用链接要求才能对程序集外部的调用强制实施安全性。  
  
-   不会强制执行继承规则。  
  
-   在完全信任模式下运行时，透明代码可能会执行有害的操作。  
  
 [返回页首](#top)  
  
<a name="enforcement"></a>   
## 透明度强制  
 在计算透明度之前，不会强制执行透明度规则。 那时，如果违反了透明度规则，则将引发 <xref:System.InvalidOperationException>。 计算透明度的时间取决于多种因素，并且无法预测。 应尽可能晚地计算。 在 [!INCLUDE[net_v40_short](../../../includes/net-v40-short-md.md)] 中，程序集级别的透明度计算比 .NET Framework 2.0 中发生得更快。 只能保证透明度计算将在需要的时间之前发生。 这类似于在编译某种方法且在该方法中检测到错误时实时 \(JIT\) 编译器将如何更改时间点。 如果你的代码没有透明度错误，则透明度计算是不可见的。  
  
## 请参阅  
 [安全透明的代码，级别 1](../../../docs/framework/misc/security-transparent-code-level-1.md)   
 [安全透明的代码，级别 2](../../../docs/framework/misc/security-transparent-code-level-2.md)