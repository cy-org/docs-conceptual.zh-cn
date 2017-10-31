---
title: "托管代码的安全编码指南"
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology:
- dotnet-clr
ms.tgt_pltfrm: 
ms.topic: article
dev_langs:
- VB
- CSharp
- C++
- jsharp
helpviewer_keywords:
- code security, unmanaged code
- unmanaged code, securing
- security [.NET Framework], unmanaged code
- secure coding, unmanaged code
ms.assetid: a8d15139-d368-4c9c-a747-ba757781117c
caps.latest.revision: 13
author: mairaw
ms.author: mairaw
manager: wpickett
ms.translationtype: HT
ms.sourcegitcommit: 306c608dc7f97594ef6f72ae0f5aaba596c936e1
ms.openlocfilehash: 5ebd50589c1ee2710e9d5dfe2c5110554be19ca5
ms.contentlocale: zh-cn
ms.lasthandoff: 08/21/2017

---
# <a name="secure-coding-guidelines-for-unmanaged-code"></a>托管代码的安全编码指南
有些库代码需要调入非托管代码（如本机代码 API（如 Win32））。 因为这意味着超出托管代码的安全外围，所以需要适当小心。 如果你的代码在安全性方面是非特定的，你的代码和调用它的任何代码都必须具有非托管代码权限（指定了<xref:System.Security.Permissions.SecurityPermission> 标志的 <xref:System.Security.Permissions.SecurityPermissionFlag.UnmanagedCode> ）。  
  
 但是，调用方具有如此强大的权限通常是不合理的。 在这种情况下，受信任的代码可充当中介，类似于 [保护包装代码](../../../docs/framework/misc/securing-wrapper-code.md)中所述的托管包装或库代码。 如果基础的非托管代码的功能是完全安全的，则可直接将其公开；否则，首先需要进行合适权限的检查（要求）。  
  
 当代码调入非托管代码，而你不希望要求调用方拥有可访问非托管代码的权限时，则必须声明该权利。 声明会阻止在帧处实施的堆栈审核。 必须非常小心，切勿在这一过程中制造安全漏洞。 通常情况下，这意味着必须要求调用方具有合适权限，然后使用非托管代码仅执行该权限所允许的操作，不能执行其他操作。 在某些情况下（例如，获取一天时间的函数），可将非托管代码直接公开给调用方，无需进行任何安全检查。 在任何情况下，任何断言的代码必须对安全负责。  
  
 由于任何提供代码路径到本机代码的托管代码都是恶意代码的潜在目标，确定哪些非托管代码可以安全使用以及必须如何使用需要特别小心。 通常情况下，绝不应将非托管代码直接公开给部分受信任的调用方。 对于在部分受信任代码可调用的库中使用非托管代码，在评估其安全性时，主要应注意两点：  
  
-   **功能**。 非托管 API 是否提供了不允许调用方执行潜在的危险操作的功能？ 代码访问安全性使用权限强制执行对资源的访问，所以应考虑 API 是否使用文件、用户界面或线程处理，或它是否公开受保护的信息。 如果是，则包装它的托管代码必须要求必要的权限，才能允许其被访问。 此外，未受权限保护时，内存访问必须局限于严格的类型安全。  
  
-   **参数检查**。 常见攻击将意外的参数传递到公开的非托管代码 API 方法，试图使它们超出规范运行。 使用范围外的索引或偏移值的缓冲区溢出是此类型攻击的一个常见示例，如同可能在基础代码中利用 bug 的任何参数一样。 因此，尽管对于部分受信任的调用方而言，非托管代码 API 在功能上是安全的（在作出必要的要求之后），托管代码也必须彻底检查参数有效性，以确保不存在来自使用托管代码包装层的恶意代码的意外调用。  
  
## <a name="using-suppressunmanagedcodesecurityattribute"></a>使用 SuppressUnmanagedCodeSecurityAttribute  
 就声明然后调用非托管代码而言，还存在性能方面的考虑。 对于此类的每个调用，安全系统自动要求非托管代码的权限，这会导致每次都进行堆栈审核。 如果你断言并立即调用非托管的代码，堆栈审核则可能毫无意义：它由断言和非托管代码的调用组成。  
  
 可将名为 <xref:System.Security.SuppressUnmanagedCodeSecurityAttribute> 的自定义特性应用于非托管代码的入口点，从而禁用要求指定了 <xref:System.Security.Permissions.SecurityPermission> 权限的 <xref:System.Security.Permissions.SecurityPermissionFlag.UnmanagedCode> 的常规安全检查。 进行此操作时，须始终保持格外小心，因为此操作会开启一扇无需执行运行时安全检查即可进入非托管代码的大门。 应注意的是，即使应用了 **SuppressUnmanagedCodeSecurityAttribute** ，也存在发生于实时 (JIT) 编译的一次性安全检查，以确保直接调用方有权调用非托管代码。  
  
 如果使用 **SuppressUnmanagedCodeSecurityAttribute**，请检查以下几点：  
  
-   使非托管代码入口点位于内部，或者使其无法在代码外部被访问。  
  
-   任何对非托管代码的调入都是潜在的安全漏洞。 请确保你的代码不是恶意代码间接调入非托管代码及避免安全检查的门户。 合适的话，则请求权限。  
  
-   如以下部分所述，创建指向非托管代码的危险路径时，使用命名约定进行显式标识。  
  
## <a name="naming-convention-for-unmanaged-code-methods"></a>非托管代码方法的命名约定  
 已建立了一个有用且强烈推荐的约定，用以对非托管代码的方法进行命名。 非托管代码的所有方法分为三个类别： **安全**、 **本机**和 **不安全**。 这些关键字可用作其中定义了各种类型的非托管代码入口点的类名。 在源代码中，应将这些关键字添加到类名，例如，像在 `Safe.GetTimeOfDay`、 `Native.Xyz`或 `Unsafe.DangerousAPI`中一样。 如下表所述，每个关键字为使用该类的开发人员提供有用的安全信息。  
  
|关键字|安全注意事项|  
|-------------|-----------------------------|  
|**安全**|对于任何代码（即使是恶意代码）进行调用都是完全无害的。 可像其他托管代码一样使用。 例如，获取一天时间的函数通常是安全的。|  
|**本机**|在安全性方面是非特定的；即需要非托管代码的权限才可进行调用的非托管代码。 检查了安全性，此操作可阻止未经授权的调用方。|  
|**不安全**|取消了安全性的、具有潜在危险的非托管代码入口点。 使用此类非托管代码时，开发人员应加倍小心，要确保其他保护措施到位以避免出现安全漏洞。 开发人员必须负责，因为此关键字覆盖安全系统。|  
  
## <a name="see-also"></a>另请参阅  
 [安全编码准则](../../../docs/standard/security/secure-coding-guidelines.md)

