---
title: "安全性的基础概念 | Microsoft Docs"
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
  - "权限 [.NET Framework]"
  - "安全性 [.NET Framework], 关于安全性"
  - "未经授权的访问"
ms.assetid: 3cfced4f-ea02-4e66-ae98-d69286363e98
caps.latest.revision: 22
author: "mairaw"
ms.author: "mairaw"
manager: "wpickett"
caps.handback.revision: 20
---
# 安全性的基础概念
Microsoft .NET Framework 可提供安全透明度、代码访问安全性和基于角色的安全性，有助于解决有关移动代码的安全性问题，并提供支持，使组件可以决定用户有权执行的操作。  这些安全机制使用一种简单一致的模型，以便熟悉代码访问安全性的开发人员可以轻松使用基于角色的安全性，反之亦然。  代码访问安全性和基于角色的安全性均使用公共语言运行时提供的公共基础结构实现。  
  
> [!NOTE]
>  从 [!INCLUDE[net_v40_long](../../../includes/net-v40-long-md.md)] 开始，安全透明度为默认的强制机制。  安全透明度将作为应用程序的一部分运行的代码与作为基础结构的一部分运行的代码分离。  有关详细信息，请参阅[安全透明的代码](../../../docs/framework/misc/security-transparent-code.md)。  
  
 因为它们使用相同的模型和基础结构，代码访问安全性和基于角色的安全性将共享若干基础概念，本节对这些概念进行了介绍。  请确保在阅读有关 .NET Framework 代码访问安全性和基于角色的安全性的文档之前，已熟悉这些概念。  
  
## 安全权限  
 公共语言运行时仅允许代码执行代码具有执行权限的那些操作。  运行时使用称为权限的对象强制对托管代码的限制。  运行时提供多个命名空间中的内置权限类，同时支持设计和实现自定义权限类。  
  
 存在两种权限，每种都有特定用途：  
  
-   代码访问权限表示对受保护资源的访问权限或执行受保护操作的能力。  
  
-   基于角色的安全权限提供一种机制，用于发现用户（或代表该用户的代理）是否具有特定标识或者是否是指定角色的成员。  <xref:System.Security.Permissions.PrincipalPermission> 是唯一的基于角色的安全权限。  
  
 安全权限的形式可以是权限类（命令性安全）或表示权限类（声明性安全）的特性。  安全权限的基类是 <xref:System.Security.CodeAccessPermission?displayProperty=fullName>；安全权限特性的基类是 <xref:System.Security.Permissions.CodeAccessSecurityAttribute?displayProperty=fullName>。  
  
 一个形式为程序集的应用程序将在加载到应用程序域内时被授予一组权限。  通常通过使用由 <xref:System.Security.SecurityManager.GetStandardSandbox%2A?displayProperty=fullName> 方法确定的预定义权限集进行授予。  授予集确定代码可以使用的权限。  运行时基于代码的原始位置授予权限（例如，本地计算机、本地 Intranet 或 Internet）。  如果将代码加载到沙盒中，还将向代码授予特殊权限。  有关在沙盒中运行代码的详细信息，请参阅[如何：运行沙盒中部分受信任的代码](../../../docs/framework/misc/how-to-run-partially-trusted-code-in-a-sandbox.md)。  
  
 权限的主要用途如下：  
  
-   库代码可要求其调用方拥有特定权限。  如果在代码中为权限放置一个 <xref:System.Security.CodeAccessPermission.Demand%2A>，所有使用你的代码的代码都必须具有该权限才能运行。  可使用需求来确定调用方是否有权访问特定资源或发现调用方的标识。  
  
-   代码可使用权限来拒绝对其需保护的资源的访问。  可以使用 <xref:System.Security.Permissions.SecurityAction?displayProperty=fullName> 指定一个有限权限集，隐式拒绝所有其他权限。  但是，我们不建议出于防止故意误用这一目的而使用 <xref:System.Security.Permissions.SecurityAction> 来禁止访问。  调用的程序集（在其授予集中具有被隐式拒绝的权限）可以通过执行对它们需使用的任何权限执行 <xref:System.Security.Permissions.SecurityAction?displayProperty=fullName> 来重写被拒绝的权限。  例如，如果仅允许 <xref:System.Security.Permissions.UIPermission> 并调用了一个本身就具有 <xref:System.Security.Permissions.FileIOPermission> 的程序集，则该程序集可只需针对 <xref:System.Security.Permissions.FileIOPermission> 执行 <xref:System.Security.Permissions.SecurityAction> 并执行文件操作。  安全保护引用程序集中不受信任代码中的资源的唯一方式是：使用不包括这些权限的授予集执行此代码。  
  
### 代码访问权限  
 代码访问权限是权限对象，用于帮助防止在未经授权的情况下使用资源和操作。  它们是公共语言运行时用于对托管代码强制安全限制的机制的一个基础部分。  
  
 每个代码访问权限均表示下列权限之一：  
  
-   访问受保护资源（如文件或环境变量）的权限。  
  
-   执行受保护操作（如访问非托管代码）的权限。  
  
 代码可请求或要求所有的代码访问权限，运行时决定向代码授予哪些权限（如果有）。  
  
 每个代码访问权限均派生自 <xref:System.Security.CodeAccessPermission> 类，这意味着所有代码访问权限都具有共同的方法，如 **Demand**、**Assert**、**Deny**、**PermitOnly**、**IsSubsetOf**、**Intersect** 和 **Union**。  
  
> [!IMPORTANT]
>  在 [!INCLUDE[net_v40_long](../../../includes/net-v40-long-md.md)] 中，为强制 <xref:System.Security.Permissions.SecurityAction>、<xref:System.Security.Permissions.SecurityAction>、<xref:System.Security.Permissions.SecurityAction> 和 <xref:System.Security.Permissions.SecurityAction> 权限请求而删除了运行时支持。  这些请求不应用于基于 [!INCLUDE[net_v40_short](../../../includes/net-v40-short-md.md)] 或更高版本的代码中。  有关此信息及其他更改的详细信息，请参阅 [安全更改](../../../docs/framework/security/security-changes.md)。  
  
### 基于角色的安全权限  
 <xref:System.Security.Permissions.PrincipalPermission> 是基于角色的安全权限，可用于确定用户是否具有指定标识或是否是指定角色的成员。  **PrincipalPermission** 是 .NET Framework 类库提供的唯一基于角色的安全权限。  
  
## 类型安全和安全性  
 类型安全代码只访问其有权访问的内存位置。  （对于本次讨论，类型安全特指内存类型安全，不应与更广义的类型安全混淆。） 例如，类型安全代码无法从另一个对象的私有字段读取值。  它仅以明确定义且经允许的方式访问类型。  
  
 在实时 \(JIT\) 编译期间，一个可选的验证过程将检查方法（该方法将被实时编译为本机代码）的元数据和 Microsoft 中间语言 \(MSIL\)，以验证它们是否类型安全。  如果代码有权绕过验证，则将跳过此过程。  有关验证的详细信息，请参阅[托管执行过程](../../../docs/standard/managed-execution-process.md)。  
  
 虽然类型安全验证并不强制性要求运行托管代码，但类型安全在程序集隔离和安全性强制中扮演着重要角色。  代码类型安全时，公共语言运行时可以将程序集彼此完全隔离。  这种隔离可帮助确保程序集不能对彼此产生负面影响，同时可增加应用程序的可靠性。  类型安全组件可在相同进程中安全地执行，即使它们的信任级别不同。  代码不是类型安全的代码时，可能会产生意外的副作用。  例如，运行时无法阻止托管代码调用到本机（非托管）代码中和执行恶意操作。  代码是类型安全的代码时，运行时的安全强制机制可确保它不会访问本机代码，除非它有权这么做。  非类型安全的所有代码都必须被授予 <xref:System.Security.Permissions.SecurityPermission> 和传递的枚举成员 <xref:System.Security.Permissions.SecurityPermissionAttribute.SkipVerification%2A>才能运行。  
  
 有关详细信息，请参阅[NIB: Writing Verifiably Type\-Safe Code](http://msdn.microsoft.com/zh-cn/d18f10ef-3b48-4f47-8726-96714021547b)。  
  
## 主体  
 主体表示用户的标识和角色，并代表用户进行操作。  .NET Framework 中基于角色的安全性支持三种主体：  
  
-   泛型主体表示独立于 Windows 用户和角色存在的用户和角色。  
  
-   Windows 主体表示 Windows 用户及其角色（或其 Windows 组）。  Windows 主体可以模拟其他用户，这意味着当代表属于一个用户的标识时，主体可代表该用户访问资源。  
  
-   应用程序可以用任何所需的方式自定义主体。  它们可以扩展该主体的标识和角色的基本概念。  
  
 更多详细信息，请参阅[主体和标识对象](../../../docs/standard/security/principal-and-identity-objects.md)。  
  
## 身份验证  
 身份验证是通过检查用户凭据和针对某些颁发机构对这些凭据进行验证来发现和验证主体的标识的过程。  身份验证期间获取的信息可直接为你的代码所用。  还可以使用 .NET Framework 基于角色的安全性对当前用户进行身份验证并确定是否允许该主体访问代码。  请参阅 <xref:System.Security.Principal.WindowsPrincipal.IsInRole%2A?displayProperty=fullName> 方法的重载，了解有关如何对特定角色的主体进行身份验证的示例。  例如，可以使用 <xref:System.Security.Principal.WindowsPrincipal.IsInRole%28System.String%29?displayProperty=fullName> 重载确定当前用户是否是“Administrators”组的成员。  
  
 现今使用的身份验证机制多种多样，其中许多可与 .NET Framework 基于角色的安全性配合使用。  最常用的一些机制包括 basic、digest、Passport、操作系统（例如，NTLM 或 Kerberos）或应用程序定义的机制。  
  
### 示例  
 下面的示例要求活动主体是管理员。  `name` 参数为 `null`，这使任何身份为管理员的用户均满足该要求。  
  
> [!NOTE]
>  在 Windows Vista 中，用户帐户控制 \(UAC\) 决定用户的特权。  如果您是内置的 Administrators 组的成员，将为您分配两个运行时访问令牌：一个标准用户访问令牌和一个管理员访问令牌。  默认情况下，您拥有标准用户角色。  要执行需要管理员身份的代码，必须首先将你的特权从标准用户提升至管理员。  你可以通过以下方式执行此操作：右键单击应用程序图标并指示需以管理员身份运行。  
  
 [!code-cpp[Classic PrincipalPermission Example#1](../../../samples/snippets/cpp/VS_Snippets_CLR_Classic/classic PrincipalPermission Example/CPP/source.cpp#1)]
 [!code-csharp[Classic PrincipalPermission Example#1](../../../samples/snippets/csharp/VS_Snippets_CLR_Classic/classic PrincipalPermission Example/CS/source.cs#1)]
 [!code-vb[Classic PrincipalPermission Example#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR_Classic/classic PrincipalPermission Example/VB/source.vb#1)]  
  
 下面的示例演示如何确定主体的标识和该主体可用的角色。  该示例的应用可能是：确认当前用户为你允许使用你的应用程序的角色。  
  
 [!code-cpp[System.Security.Principal.WindowsBuiltInRole Example#1](../../../samples/snippets/cpp/VS_Snippets_CLR_System/system.Security.Principal.WindowsBuiltInRole Example/CPP/source.cpp#1)]
 [!code-csharp[System.Security.Principal.WindowsBuiltInRole Example#1](../../../samples/snippets/csharp/VS_Snippets_CLR_System/system.Security.Principal.WindowsBuiltInRole Example/CS/source.cs#1)]
 [!code-vb[System.Security.Principal.WindowsBuiltInRole Example#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR_System/system.Security.Principal.WindowsBuiltInRole Example/VB/source.vb#1)]  
  
## 授权  
 授权是确定是否同意主体执行所请求的操作的过程。  授权发生在身份验证之后，并使用有关主体的标识和角色的信息来确定主体可以访问的资源。  可使用 .NET Framework 基于角色的安全性实现授权。  
  
## Internal Virtual 关键字的安全问题  
 绝不应将 C\# 中标记为 [internal](../Topic/internal%20\(C%23%20Reference\).md) [virtual](../Topic/virtual%20\(C%23%20Reference\).md) 修饰符（Visual Basic 中的 [Overloads](../Topic/Overloads%20\(Visual%20Basic\).md) [Overridable](../Topic/Overridable%20\(Visual%20Basic\).md) [Friend](../Topic/Friend%20\(Visual%20Basic\).md) 修饰符）的成员作为建立应用程序安全性的基础。  虽然标记为这些修饰符的成员只能被当前程序集内的其他成员重写，但仅 C\# 和 Visual Basic 语言强制执行此规则。  运行时不强制执行此规则。  因此，可以使用 Microsoft 中间语言或任何其他不强制执行此规则的语言重写 C\# 中标记为 **internal virtual** 的成员或 Visual Basic 中标记为 **Overloads Overridable Friend** 的成员。  
  
## 请参阅  
 [安全性的基础概念](../../../docs/standard/security/key-security-concepts.md)