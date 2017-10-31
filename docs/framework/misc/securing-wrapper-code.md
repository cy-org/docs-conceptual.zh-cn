---
title: "保护包装代码 | Microsoft Docs"
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
  - "代码安全性, 包装代码"
  - "安全编码, 包装代码"
  - "安全性 [.NET Framework], 包装代码"
  - "包装代码, 保护"
ms.assetid: 1df6c516-5bba-48bd-b450-1070e04b7389
caps.latest.revision: 11
author: "mairaw"
ms.author: "mairaw"
manager: "wpickett"
caps.handback.revision: 9
---
# 保护包装代码
包装代码，特别是在包装的信任级别比使用它的代码的信任级别更高时，可以打开一组唯一的安全漏洞。 代表调用方完成的任何操作都是被利用的潜在漏洞，其中进行适当安全检查时不包括调用方的有限权限。  
  
 请勿通过包装启用调用方无法自行执行的任何操作。 相对于完整堆栈遍历需求，在进行牵涉到限制安全性检查的操作时，这项操作特别危险。 当涉及到单级别检查时，在实际调用方和正在讨论的 API 元素之间干预包装代码很容易导致本应失败的安全检查成功，从而便削弱了安全性。  
  
> [!CAUTION]
>  代码访问安全性和部分受信任的代码  
>   
>  .NET Framework 提供一种机制，对在相同应用程序中运行的不同代码强制实施不同的信任级别，该机制称为代码访问安全性 \(CAS\)。  .NET Framework 中的代码访问安全性不应用作部分受信任的代码（特别是未知来源的代码）的安全边界。 建议在未实施其他安全措施的情况下，不要加载和执行未知来源的代码。  
>   
>  此策略适用于 .NET Framework 的所有版本，但不适用于 Silverlight 中所含的 .NET Framework。  
  
## 委托  
 委托安全性因 .NET Framework 的版本而异。  本节介绍了不同的委托行为和相关的安全注意事项。  
  
### .NET Framework 1.0 版和 1.1 版  
 .NET Framework 1.0 版和 1.1 版可执行以下针对委托创建者和委托调用方的安全性操作。  
  
-   当创建委托时，将针对委托创建者的权限集执行对委托目标方法的安全链接要求。  未遵循安全操作将导致 <xref:System.Security.SecurityException>。  
  
-   当调用委托时，将执行对委托调用方的任何现有的安全需求。  
  
 无论何时，当代码从可能调用它的不太受信任代码中提取 <xref:System.Delegate> 时，确保不会启用不太受信任代码提升其权限。 如果提取委托想在以后使用，则创建委托的代码不会出现在调用堆栈之上，并且其权限也得不到测试（如果委托中或以下的代码尝试执行受保护操作）。 如果你的代码和调用方的代码其特权比创建者更高，则创建者可以安排调用路径，使其不作为调用堆栈的一部分。  
  
### .NET Framework 2.0 版及更高版本  
 不像之前的版本，.NET Framework 2.0 版可执行针对创建和调用委托的委托创建者的安全操作。  
  
-   当创建委托时，将针对委托创建者的权限集执行对委托目标方法的安全链接要求。  未遵循安全操作将导致 <xref:System.Security.SecurityException>。  
  
-   在创建委托期间还会捕获委托创建者的权限集并存储在委托中。  
  
-   待用委托时，如果委托创建者和调用方属于不同的程序集，则将针对当前内容中的任何需求首先评估委托创建者捕获的权限集。  然后才是执行针对委托调用方的现有安全需求。  
  
## 链接需求和包装  
 在安全性基础结构中，已经对链接需求加强了特殊保护，但它依然是代码中潜在的漏洞源。  
  
 如果完全受信任代码调用受 [LinkDemand](../../../docs/framework/misc/link-demands.md) 保护的属性、事件或方法，则调用成功，前提是对调用方的 **LinkDemand** 权限检查令人满意。 并且，如果完全受信任代码公共采用某个属性名称的类并使用反射调用其 **get** 访问器，则可成功调用 **get** 访问器，即使用户代码无权访问此属性。 这是因为 **LinkDemand** 仅检查直接调用方，而直接调用方是完全受信任的代码。 从根本上而言，完全受信任的代码可代表用户代码发出特权调用，而无需确保用户代码是否有权发出该调用。  
  
 为了帮助防止此类安全漏洞，公共语言运行时都会将检查范围扩展至对 **LinkDemand** 保护的方法、构造函数、属性或事件的直接调用的完整堆栈遍历需求。 这种保护会带来一些性能损失，并更改安全检查语义；完整的堆栈遍历需求可能会失败，其中会通过速度更快的单一级别检查。  
  
> [!NOTE]
>  在 [!INCLUDE[net_v40_long](../../../includes/net-v40-long-md.md)] 中，已将部分受信任的代码重新定义为透明代码。 透明模型会在可以执行特许事件（例如调用本机代码）的代码（关键代码）和无法执行的代码（透明代码）之间绘制一个屏障。 透明性可代替使用 <xref:System.Security.Permissions.SecurityAction> f或完全信任以识别具有 <xref:System.Security.SecurityCriticalAttribute> 的完全受信任代码。 有关此更改以及其他更改的详细信息，请参阅 [安全更改](../../../docs/framework/security/security-changes.md)。  
  
## 加载包装的程序集  
 用于加载托管代码的几种方法，包括 <xref:System.Reflection.Assembly.Load%2A?displayProperty=fullName>使用调用方的证据加载程序集。 如果包装任何这些方法，安全系统将使用代码的授予权限（而不是使用包装其调用方的权限）加载程序集。 不应使用不太受信任代码加载比包装器调用方的权限更高的代码。  
  
 否则，将会降低任何具有完全信任或比潜在调用方（）的信任程度明显更高的代码的安全性。 如果代码有一个公共方法，它接受字节数组，并将其传递给 **Assembly.Load**，从而代表调用方创建程序集，则可能会破坏安全性。  
  
 此问题适用于以下 API 元素：  
  
-   <xref:System.AppDomain.DefineDynamicAssembly%2A?displayProperty=fullName>  
  
-   <xref:System.AppDomain.Load%2A?displayProperty=fullName>  
  
-   <xref:System.Reflection.Assembly.LoadFrom%2A?displayProperty=fullName>  
  
-   <xref:System.Reflection.Assembly.Load%2A?displayProperty=fullName>  
  
## Demand VS LinkDemand  
 声明性安全提供了两种类型相似但执行方法完全不同的安全检查。 你应该了解这两种形式，因为选择错误可能导安全性降低或性能受损。  
  
 声明性安全提供了下列安全检查：  
  
-   <xref:System.Security.Permissions.SecurityAction> 指示代码访问安全堆栈审核。 堆栈上的所有调用方必须具有特定权限或标识才能通过。 每次调用都会发生 **Demand**，因为堆栈可能包含不同的调用方。 如果重复调用一种方法，则每次都会执行安全检查。**Demand** 是对引诱攻击的有效保护方式；它可以检测尝试侵入的未授权代码。  
  
-   [LinkDemand](../../../docs/framework/misc/link-demands.md) 发生在实时 \(JIT\) 编译时，并且检查仅限直接调用方。 这种安全检查不会检查调用方的调用方。 一旦此项检查成功，无论调用方调用的次数为多少，都无需任何其他安全性开销。 但是，这种方法没有对引诱攻击提供保护。 使用 **LinkDemand**，通过检查并可以引用代码的任何代码，都可能通过允许恶意代码利用已授权的代码进行调用的方式破坏安全性。 因此，请勿使用 **LinkDemand**，除非可以彻底避免所有可能的漏洞。  
  
    > [!NOTE]
    >  在 [!INCLUDE[net_v40_long](../../../includes/net-v40-long-md.md)] 中，链接要求已被 <xref:System.Security.SecurityRuleSet> 程序集中的 <xref:System.Security.SecurityCriticalAttribute> 属性所取代。<xref:System.Security.SecurityCriticalAttribute> 等同于完全信任的链接要求；但是，它也会影响继承规则。 有关这一更改的详细信息，请参阅 [安全透明的代码，级别 2](../../../docs/framework/misc/security-transparent-code-level-2.md)。  
  
 必须对使用 **LinkDemand** 时要求执行的其他预防措施进行单独编程；安全系统可以帮助执行这一点。 任何错误都会打开安全漏洞。 利用你的代码的所有授权代码都必须负责执行以下操作实现其他安全性：  
  
-   限制调用代码对类或程序集的访问权限。  
  
-   对显示在将被调用的代码上的调用代码施行相同的安全检查并负责让其调用方也执行这种检查。 例如，你要编写代码，使其可以调用受 <xref:System.Security.Permissions.SecurityPermission> 的 **LinkDemand**（具有指定的 <xref:System.Security.Permissions.SecurityPermissionFlag> 标记）保护的方法，则你的方法还应采用 **LinkDemand**（或效果更强的 **Demand**）执行此权限。 例外情况是，如果你的代码以你认为安全的有限方式使用 **LinkDemand** 保护的方法，则会在你的代码中指定其他保护机制（例如“Demand”）。 对于这种例外情况，调用方需对削弱基础代码的安全性保护负责。  
  
-   确保你的代码调用方无法欺骗你的代码代表自己调用受保护的代码。 换言之，调用方不能强制授权代码向受保护的代码传递特定参数，或从受保护的代码中得到返回结果。  
  
### 接口和链接需求  
 如果使用 **LinkDemand** 的虚拟方法、属性或事件重写了基类方法，则基类方法还必须具有重写方法的相同 **LinkDemand** 才能有效。 当然，恶意代码重新强制转换为基类并调用基类方法的这种情况也是有可能的。 另请注意，可以将链接需求以隐式方式添加到不包含 <xref:System.Security.AllowPartiallyTrustedCallersAttribute> 程序集级别属性的程序集。  
  
 当接口方法也具有链接需求时，使用链接需求实现保护方法也是不错的选择。 请注意下列有关使用链接需求的接口：  
  
-   **AllowPartiallyTrustedCallersAttribute** 属性也适用于接口。  
  
-   你可以将链接需求放放置在接口上以选择性地保护某些接口不被部分受信任的代码所使用（例如使用 **AllowPartiallyTrustedCallersAttribute**  属性时）。  
  
-   如果你的接口是在程序集中定义的，并且该程序集不包含 **AllowPartiallyTrustedCallersAttribute**  属性，则可以在部分受信任类中实现该接口。  
  
-   如果你将 **LinkDemand** 放置在可实现接口方法的类的公共方法中，之后你又强制转换为接口并调用该方法，则不会执行 **LinkDemand**。 在这种情况下，由于你是针对接口进行的链接，因此只会认可该接口上的 **LinkDemand**。  
  
 审阅安全性问题的以下各项：  
  
-   接口方法上的显式链接需求。 确保这些链接需求提供预期保护。 确定恶意代码是否可以使用强制转换来避开链接需求，如前面所述。  
  
-   应用了包含链接需求的虚拟方法。  
  
-   它们实现的类型和接口。 这些应使用相一致的链接需求。  
  
## 请参阅  
 [代码安全维护指南](../../../docs/standard/security/secure-coding-guidelines.md)