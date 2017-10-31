---
title: "代码安全维护指南 | Microsoft Docs"
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
  - "代码安全性"
  - "代码安全性, 选项"
  - "代码, 安全性"
  - "组件 [.NET Framework], 安全性"
  - "用于公开受保护资源的库代码"
  - "本机代码实现的托管包装"
  - "可重复使用的组件"
  - "安全编码"
  - "安全编码, 选项"
  - "安全性 [.NET Framework], 编码原则"
  - "非特定于安全性的代码"
ms.assetid: 4f882d94-262b-4494-b0a6-ba9ba1f5f177
caps.latest.revision: 20
author: "mairaw"
ms.author: "mairaw"
manager: "wpickett"
caps.handback.revision: 17
---
# 代码安全维护指南
基于证据的安全性和代码访问安全性提供非常强大的显式机制来实现安全。 大多数应用程序代码就可以使用由 .NET Framework 实现的基础结构。 在某些情况下，需要额外的应用程序特定的安全性，或通过扩展安全系统或通过使用全新临时方法构建。  
  
 在代码中使用 .NET Framework 强制实施的权限和其他强制，则应建立屏障，以防止恶意代码获取不希望其具有的信息或执行其他不需要的操作。 此外，必须在使用受信任代码的所有预期方案中平衡安全性和可用性。  
  
 本概述介绍代码可以用于处理安全系统的不同方式。  
  
> [!NOTE]
>  在 [!INCLUDE[net_v40_long](../../../includes/net-v40-long-md.md)] 中，已对 .NET Framework 安全模型和术语作出重要更改。 有关这些更改的详细信息，请参阅 [安全更改](../../../docs/framework/security/security-changes.md)。  
  
## 代码访问安全性和部分受信任的代码  
 .NET Framework 提供一种机制，对在相同应用程序中运行的不同代码强制实施不同的信任级别，该机制称为代码访问安全性 \(CAS\)。  因为 .NET Framework 中的代码访问安全性并不保证代码隔离，所以它不应用作部分受信任代码（特别是未知来源代码）的安全边界。 建议在未实施其他安全措施的情况下，不要加载和执行未知来源的代码。  
  
 此策略适用于 .NET Framework 的所有版本，但不适用于 Silverlight 中所含的 .NET Framework。  
  
## 非特定于安全性的代码  
 非特定于安全性的代码不对任何安全系统进行显示处理。 它通过所接收的任何权限来运行。 虽然无法捕获与受保护操作（例如使用文件、网络等）相关联安全异常的应用程序可导致未经处理的异常，但非特定于安全性的代码还是利用 .NET Framework 安全技术。  
  
 非特定于安全性的库具有你应了解的特殊性质。 假设你的库提供了使用文件或调用非托管代码的 API 元素；如果你的代码没有相应的权限，则不会如所述运行。 但是，即使代码具有权限，调用它的任何应用程序代码必须具有相同的权限才能正常运行。 如果调用代码没有正确的权限，则 <xref:System.Security.SecurityException> 将作为代码访问安全堆栈审核的结果显示。  
  
## 不是可重用组件的应用程序代码  
 如果代码是不会由其他代码调用的应用程序的一部分，则实现安全很简单，可能不需要特殊的编码。 但请记住，恶意代码可以调用你的代码。 代码访问安全性可能会阻止恶意代码访问资源，而此类代码仍然可以读取你的字段或可能包含敏感信息的属性的值。  
  
 此外，如果你的代码接受来自 Internet 或其他不可靠来源的用户输入，则务必要小心恶意输入。  
  
## 本机代码实现的托管包装  
 通常在这种情况下，某些有用功能是在你想要提供给托管代码的本机代码中实现的。 托管包装器可通过使用平台调用或 COM 互操作轻松写入。 但如果你这样做，包装器的调用方必须具有非托管代码权限才能成功。 在默认策略下，这意味着从 Intranet 或 Internet 下载的代码不适用于此包装器。  
  
 相较于为所有使用这些包装器的应用程序提供非托管代码权限而言，仅对包装器代码提供这些权限是更好的做法。 如果基础功能没有公开任何资源，且实现同样也安全，则包装器只需断言其权限，这可使任何代码通过它进行调用。 当涉及资源时，安全编码应该与下一节中所述的库代码案例相同。 因为包装器可能对这些资源公开调用方，所以仔细验证本机代码的安全性是必要的，这是包装器的责任。  
  
## 用于公开受保护资源的库代码  
 这是最强大的，因而对安全编码具有潜在的危险性（如未正确执行）：你的库作为其他代码访问某些资源的接口（否则无法访问该资源），就像 .NET Framework 的类强制执行所使用资源的权限。 只要公开资源，你的代码首先就必须要求相应资源的权限（也就是说，必须执行安全检查），然后通常断言其权限来执行实际的操作。  
  
## 相关主题  
  
|标题|描述|  
|--------|--------|  
|[如何：运行沙盒中部分受信任的代码](../../../docs/framework/misc/how-to-run-partially-trusted-code-in-a-sandbox.md)|说明如何在受限制的安全环境中运行部分受信任的应用程序，限制授予给它的代码访问权限。|  
|[保护状态数据](../../../docs/standard/security/securing-state-data.md)|说明如何保护私有成员。|  
|[保护方法访问](../../../docs/framework/misc/securing-method-access.md)|说明如何帮助保护方法免受部分受信任代码的调用。|  
|[保护包装代码](../../../docs/framework/misc/securing-wrapper-code.md)|说明包装其他代码的代码安全问题。|  
|[安全和公共只读数组字段](../../../docs/framework/misc/security-and-public-read-only-array-fields.md)|说明使用在 .NET Framework 库中找到的公共只读数组的代码的安全问题。|  
|[保护异常处理](../../../docs/framework/misc/securing-exception-handling.md)|说明用于处理异常的安全问题。|  
|[安全性和用户输入](../../../docs/standard/security/security-and-user-input.md)|说明用于接受用户输入的应用程序的安全问题。|  
|[安全性和远程处理注意事项](../../../docs/framework/misc/security-and-remoting-considerations.md)|说明在应用程序域之间通信的应用程序的安全问题。|  
|[安全和序列化](../../../docs/framework/misc/security-and-serialization.md)|说明序列化对象时的安全问题。|  
|[安全和争用条件](../../../docs/standard/security/security-and-race-conditions.md)|说明如何避免代码中的争用条件。|  
|[安全性和进行中的代码生成](../../../docs/standard/security/security-and-on-the-fly-code-generation.md)|说明用于生成动态代码的应用程序的安全问题。|  
|[安全性和安装问题](../Topic/Security%20and%20Setup%20Issues.md)|说明用于测试和安装应用程序的注意事项。|  
|[代码访问安全性](../../../docs/framework/misc/code-access-security.md)|详细说明 .NET Framework 代码访问安全，并提供有关在代码中使用的说明。|  
|[基于角色的安全性](../../../docs/standard/security/role-based-security.md)|详细说明 .NET Framework 中基于角色的安全性，并提供有关在代码中使用的说明。|