---
title: ".NET Framework 版本和依赖关系"
ms.custom: 
ms.date: 05/02/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology:
- dotnet-clr
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- versions, .NET Framework
ms.assetid: f75a72de-e2f2-4a7a-9574-3f278684ea90
caps.latest.revision: 122
author: rpetrusha
ms.author: ronpet
manager: wpickett
ms.translationtype: HT
ms.sourcegitcommit: 306c608dc7f97594ef6f72ae0f5aaba596c936e1
ms.openlocfilehash: a2e3e87f94dec62f6a55e5ef87ee8028f24a5f0e
ms.contentlocale: zh-cn
ms.lasthandoff: 07/28/2017

---
# <a name="net-framework-versions-and-dependencies"></a>.NET Framework 版本和依赖关系
每个版本的 .NET framework 都包含公共语言运行时 (CLR)、基类库和其他托管库。 本主题按版本介绍了 .NET Framework 的关键功能，提供了有关基础 CLR 版本和相关开发环境的信息，并标识了 Windows 操作系统所安装的版本。  
  
> [!NOTE]
>  若要了解如何下载和安装 .NET Framework，请参阅[安装面向开发人员的 .NET Framework](../../../docs/framework/install/guide-for-developers.md)。  
  
 下表总结了 .NET Framework 版本历史，并将每个版本与 Visual Studio、Windows 和 Windows Server 相关联。 请注意，Visual Studio 提供了多目标功能，因此你将不会限于仅使用列出的 .NET Framework 版本。  
  
 每个新版本的 .NET Framework 都会保留早期版本中的功能并会添加新功能。 CLR 由其自己的版本号标识。 虽然 CLR 版本并不总是递增的，但 .NET Framework 版本号在每次发布时都会递增。 例如，.NET Framework 4、4.5 和更高版本包含 CLR 4，而 .NET Framework 2.0、3.0 和 3.5 包含 CLR 2.0。 （没有版本 3 的 CLR。）  
  
 有关受支持操作系统的完整列表，请参阅[系统要求](../../../docs/framework/get-started/system-requirements.md)。 有关下载，请参阅[安装面向开发人员的 .NET Framework](../../../docs/framework/install/guide-for-developers.md)。 有关确定计算机上已安装的 .NET Framework 的版本信息，请参阅[如何：确定安装了哪些 .NET Framework 版本](../../../docs/framework/migration-guide/how-to-determine-which-versions-are-installed.md)。  
  
 在表中，带有标记 ✓ 的操作系统版本上安装的 .NET Framework 版本必须在[控制面板](../../../docs/framework/install/dotnet-35-windows-10.md)中启用（适用于 Windows）或通过服务器管理器启用（适用于 Windows Server），该标记显示在“包含在/可安装在 Windows 中”和“包含在/可安装在 Windows Server 中”列。  
  
|.NET Framework 版本|CLR 版本|功能|包含在 Visual Studio 版本中|✓ 包括在内<br />+ 可在其上安装<br />Windows|✓ 包括在内<br />+ 可在其上安装<br />Windows Server|确定已安装的 .NET 版本|  
|----------------------------|-----------------|--------------|---------------------------------------|----------------------------------------------------|-----------------------------------------------------------|-----------------------------------------| 
|4.7|4|- 支持由操作系统提供的 TLS 支持级别。<br/> - 能够为 TLS1.1 或 TLS1.2 配置默认的消息安全设置。 <br /> - 提高了 <xref:System.Runtime.Serialization.Json.DataContractJsonSerializer> 的可靠性。 <br /> - 提高了 WCF 应用程序序列化和反序列化的可靠性。 <br /> - 能够扩展 ASP.NET 对象缓存。 <br /> - 支持基于 `WM_POINTER` Windows 消息（而不是 WPF 应用程序的 Windows Ink 服务平台 (WISP)）的触控/触笔堆叠。 <br /> - 使用窗口的打印文档包 API 在 WPF 应用程序中进行打印。<br /> - 增强了对 Windows 窗体应用程序（在 Windows 10 创意者更新上运行）的高 DPI 和多监视器支持。 | | ✓  10 创意者更新 <br/> <br/> + 10 周年更新 <br/> + 8.1 <br/> +7| + 2016 <br/> + 2012 R2 <br/> + 2012 <br/> + 2008 R2 SP1 |使用 `Release` DWORD：<br/><br/> - 460798（Windows 10 创意者更新） <br/> - 460805（所有其他操作系统版本） <br/><br/> （请参阅[说明](../../../docs/framework/migration-guide/how-to-determine-which-versions-are-installed.md)） |  
|4.6.2|4|-   加密增强功能，包括对包含 FIS 186-3 DSA 的 X509 证书的支持、对持久化密钥对称加密的支持、对 SHA-2 哈希的 <xref:System.Security.Cryptography.Xml.SignedXml> 支持，提高了 ECDiffieHellman 密钥派生例程输入的清晰度。<br />-  对于 Windows Presentation Foundation (WPF) 应用，支持屏幕键盘和按监视器 DPI 感知。<br />-   对 TLS 1.1 和 TLS 1.2 协议的 ClickOnce 支持。<br />-   支持将 Windows 窗体和 WPF 应用转换为 UWP 应用。||✓  10 周年更新<br /><br /> + 8.1<br />+ 7|✓  2016<br /><br /> + 2012 R2<br />+ 2012<br />+ 2008 R2 SP1|使用 `Release` DWORD：<br /><br /> -   394802（Windows 10 周年更新）<br />-   394806（所有其他操作系统版本）<br /><br /> （请参阅[说明](../../../docs/framework/migration-guide/how-to-determine-which-versions-are-installed.md)）|  
|4.6.1|4|-   对包含 ECDSA 的 X509 证书的支持<br />-   对 ADO.NET 中的硬件保护密钥的始终加密支持<br />-   WPF 中的拼写检查改进<br />-   [更多...](../../../docs/framework/whats-new/index.md)||✓  10 November Update<br /><br /> + 10<br />+ 8.1<br />+ 8<br />+ 7|+ 2012 R2<br />+ 2012<br />+ 2008 R2 SP1|使用 `Release` DWORD：<br /><br /> -   394254（Windows 10 十一月更新）<br />-   394271（所有其他操作系统版本）<br /><br /> （请参阅[说明](../../../docs/framework/migration-guide/how-to-determine-which-versions-are-installed.md)）|  
|4.6|4|-   使用 .NET Native 编译<br />-   ASP.NET Core 5<br />-   事件跟踪改进<br />-   对页面编码的支持<br />-   [更多...](../../../docs/framework/whats-new/index.md)|2015，尽管部分 .NET 库可在 [NuGet](https://www.nuget.org/) 上获取。 有关详细信息，请参阅 [.NET Framework 和带外版本](../../../docs/framework/get-started/the-net-framework-and-out-of-band-releases.md)。|✓ 10<br />+ 8.1<br />+ 8<br />+ 7<br />+ Vista|+ 2012 R2<br />+ 2012<br />+ 2008 R2 SP1<br />+ 2008 SP2|使用 `Release` DWORD：<br /><br /> -   393295 (Windows 10)<br />-   393297（所有其他操作系统版本）<br /><br /> （请参阅[说明](../../../docs/framework/migration-guide/how-to-determine-which-versions-are-installed.md)）|  
|4.5.2|4|-   用于事务系统和 ASP.NET 的新 API<br />-   Windows 窗体控件中的系统 DPI 调整大小功能<br />-   分析改进<br />-   ETW 和压力日志记录改进<br />-   [更多...](../../../docs/framework/whats-new/index.md)|-|+ 8.1<br />+ 8<br />+ 7<br />+ Vista|+ 2012 R2<br />+ 2012<br />+ 2008 R2 SP1<br />+ 2008 SP2|使用 `Release` DWORD：379893<br />（请参阅[说明](../../../docs/framework/migration-guide/how-to-determine-which-versions-are-installed.md)）|  
|4.5.1|4|-   对 Windows Phone 应用商店应用的支持<br />-   自动绑定重定向<br />-   性能和调试改进<br />-   [更多...](../../../docs/framework/whats-new/index.md)|2013|✓ 8.1<br />+ 8<br />+ 7<br />+ Vista|✓ 2012 R2<br />+ 2012<br />+ 2008 R2 SP1<br />+ 2008 SP2|使用 `Release` DWORD：<br /><br /> -   378675 (Windows 8.1)<br />-   378758（所有其他）<br /><br /> （请参阅[说明](../../../docs/framework/migration-guide/how-to-determine-which-versions-are-installed.md)）|  
|4.5|4|-   对 Windows 应用商店应用的支持<br />-   WPF、WCF、WF、ASP.NET 更新<br />-   [更多...](../../../docs/framework/whats-new/index.md)|2012|✓ 8<br />+ 7<br />+ Vista|✓ 2012<br />+ 2008 R2 SP1<br />+ 2008 SP2|使用 `Release` DWORD：378389<br />（请参阅[说明](../../../docs/framework/migration-guide/how-to-determine-which-versions-are-installed.md)）|  
|4|4|-   扩展的基类库<br />-   使用可移植类库的跨平台开发<br />-   MEF、DLR、代码协定<br />-   [更多...](http://msdn.microsoft.com/library/ms171868\(v=vs.100\).aspx)|2010|+ 7<br />+ Vista|+ 2008 R2 SP1<br />+ 2008 SP2<br />+ 2003|请参阅[说明](../../../docs/framework/migration-guide/how-to-determine-which-versions-are-installed.md)|  
|3.5|2.0|-   启用 AJAX 的网站<br />-   LINQ<br />-   动态数据<br />-   [更多...](http://msdn.microsoft.com/library/ms171868\(v=vs.90\).aspx)|2008|✓ 10✓ 8.1*<br />✓ 8\*<br />✓ 7<br />+ Vista|✓2008 R2 SP1*<br />+ 2012 R2<br />+ 2012<br />+ 2008 SP2<br />+ 2003|请参阅[说明](../../../docs/framework/migration-guide/how-to-determine-which-versions-are-installed.md)|  
|3.0|2.0|-   WPF、WCF、WF、CardSpace|-|✓ Vista|✓ 2008 R2 SP1*<br />✓ 2008 SP2\*<br />+ 2003|请参阅[说明](../../../docs/framework/migration-guide/how-to-determine-which-versions-are-installed.md)|  
|2.0|2.0|-   泛型<br />-   ASP.NET 添加项<br />-   [更多...](http://msdn.microsoft.com/library/t357fb32\(v=vs.80\).aspx)|2005|-|✓ 2008 R2 SP1<br />✓ 2008 SP2<br />✓ 2003|请参阅[说明](../../../docs/framework/migration-guide/how-to-determine-which-versions-are-installed.md)|  
|1.1|1.1|-   ASP.NET 和 ADO.NET 更新<br />-   并行执行<br />-   [更多...](http://msdn.microsoft.com/library/9wtde3k4\(v=vs.80\).aspx)|2003|-|✓ 2003|请参阅[说明](../../../docs/framework/migration-guide/how-to-determine-which-versions-are-installed.md)|  
|1.0|1.0|.NET Framework 的第一个版本。|Visual Studio .NET|-|-|请参阅[说明](../../../docs/framework/migration-guide/how-to-determine-which-versions-are-installed.md)|  
  
 通常，你不应卸载计算机上安装的 .NET Framework 的任何版本，因为你使用的应用程序可能依赖于特定版本，如果你移除该版本，则应用程序可能会中断。 你可以在一台计算机上同时加载 .NET Framework 的多个版本。 这意味着，你可以安装 .NET Framework 而无需卸载早期版本。 有关详细信息，请参阅[入门](../../../docs/framework/get-started/index.md)。  
  
## <a name="targeting-and-running-net-framework-apps-for-version-45-and-later"></a>面向并运行 .NET Framework 版本 4.5 和更高版本的应用  
 [!INCLUDE[net_v45](../../../includes/net-v45-md.md)] 是替代计算机上的 [!INCLUDE[net_v40_short](../../../includes/net-v40-short-md.md)] 的就地更新，同样，[!INCLUDE[net_v451](../../../includes/net-v451-md.md)] 4.5.2、4.6、4.6.1、4.6.2 和 4.7 是对 [!INCLUDE[net_v45](../../../includes/net-v45-md.md)] 的就地更新，这意味着它们将使用相同的运行时版本，但是程序集版本会更新并包括新类型和成员。 在安装其中某个更新后，你的 [!INCLUDE[net_v40_short](../../../includes/net-v40-short-md.md)][!INCLUDE[net_v45](../../../includes/net-v45-md.md)] 或 [!INCLUDE[net_v46](../../../includes/net-v46-md.md)] 应用应继续运行，而无需重新编译。 但是，反过来则不行。 建议不要在较早版本的 .NET Framework 上运行面向更高版本的 .NET Framework 的应用。 例如，我们建议你不要在 [!INCLUDE[net_v45](../../../includes/net-v45-md.md)] 上运行面向 [!INCLUDE[net_v46](../../../includes/net-v46-md.md)] 的应用。 以下准则将适用：  
  
-   在 Visual Studio 中，可以选择 [!INCLUDE[net_v45](../../../includes/net-v45-md.md)] 作为项目的目标框架（这将设置 <xref:Microsoft.Build.Tasks.GetReferenceAssemblyPaths.TargetFrameworkMoniker%2A?displayProperty=fullName> 属性）以将项目编译为 [!INCLUDE[net_v45](../../../includes/net-v45-md.md)] 程序集或可执行文件。 此程序集或可执行文件随后可用于安装了 [!INCLUDE[net_v45](../../../includes/net-v45-md.md)]、4.5.1、4.5.2、4.6、4.6.1、4.6.2 或 4.7 的任何计算机。  
  
-   在 Visual Studio 中，可以选择 [!INCLUDE[net_v451](../../../includes/net-v451-md.md)] 作为项目的目标框架（这将设置 <xref:Microsoft.Build.Tasks.GetReferenceAssemblyPaths.TargetFrameworkMoniker%2A?displayProperty=fullName> 属性）以将项目编译为 [!INCLUDE[net_v451](../../../includes/net-v451-md.md)] 程序集或可执行文件。 此程序集或可执行文件应只在安装了 [!INCLUDE[net_v451](../../../includes/net-v451-md.md)] 或 .NET Framework 更高版本的计算机上运行。 将阻止面向 [!INCLUDE[net_v451](../../../includes/net-v451-md.md)] 的可执行文件在仅安装了 .NET Framework 的早期版本（例如 [!INCLUDE[net_v45](../../../includes/net-v45-md.md)]）的计算机上运行，并且系统会提示用户安装 [!INCLUDE[net_v451](../../../includes/net-v451-md.md)]。 此外，不应从面向 .NET Framework 的早期版本（例如 [!INCLUDE[net_v45](../../../includes/net-v45-md.md)]）的应用中调用 [!INCLUDE[net_v451](../../../includes/net-v451-md.md)] 程序集。  
  
     此处使用的 [!INCLUDE[net_v451](../../../includes/net-v451-md.md)] 和 [!INCLUDE[net_v45](../../../includes/net-v45-md.md)] 仅作为示例。 此原则适用于任意满足以下条件的应用：应用所面向的 .NET framework 版本高于运行该应用的系统上的 .NET framework 版本。  
  
 .NET Framework 中的某些更改可能需要更改应用代码；请先参阅[应用程序兼容性](../../../docs/framework/migration-guide/application-compatibility.md)，然后再使用 [!INCLUDE[net_v45](../../../includes/net-v45-md.md)] 或更高版本运行现有应用。 若要了解如何安装当前版本，请参阅[安装面向开发人员的 .NET Framework](../../../docs/framework/install/guide-for-developers.md)。 有关对 .NET Framework 的支持的信息，请参阅 Microsoft 支持网站上的 [Microsoft .NET Framework 支持生命周期策略](http://go.microsoft.com/fwlink/?LinkId=196607)。  
  
## <a name="targeting-and-running-apps-for-older-versions"></a>以针对早期版本的应用程序为目标并运行这些应用程序  
 .NET Framework 版本 2.0、3.0 和 3.5 是使用同一 CLR 版本 (CLR 2.0) 生成的。 这些版本表示单个安装的连续层。 每个版本将基于早期版本以增量方式生成。 无法在计算机上并行运行版本 2.0、3.0 和 3.5。 在安装 3.5 版时，你将自动获得 2.0 和 3.0 层，并且为版本 2.0、3.0 和 3.5 生成的应用程序均可在 3.5 版上运行。 但是，.NET Framework 4 会结束此分层方法。 从 .NET Framework 4 开始，可使用进程内并行承载在单个进程中运行 CLR 的多个版本。 有关详细信息，请参阅[程序集和并行执行](../../../docs/framework/app-domains/assemblies-and-side-by-side-execution.md)。  
  
 此外，如果你的应用程序面向 2.0、3.0 或 3.5 版，你的用户可能需要先在 [!INCLUDE[win8](../../../includes/win8-md.md)] 或 [!INCLUDE[win81](../../../includes/win81-md.md)]计算机上启用 .NET Framework 3.5，然后才能运行应用程序。 有关详细信息，请参阅[在 Windows 10、Windows 8.1 和 Windows 8 上安装 .NET Framework 3.5](../../../docs/framework/install/dotnet-35-windows-10.md)。  
  
## <a name="next-steps"></a>后续步骤  
  
-   如果不熟悉 .NET Framework，请参阅[概述](../../../docs/framework/get-started/overview.md)以大致了解关键概念和功能。  
  
-   有关 [!INCLUDE[net_v45](../../../includes/net-v45-md.md)] 及其单点版本中的新功能和改进，请参阅 [.NET Framework 中的新增功能](../../../docs/framework/whats-new/index.md)。  
  
-   有关将应用从 .NET Framework 4 迁移到 [!INCLUDE[net_v45](../../../includes/net-v45-md.md)] 及其单点版本的信息，请参阅[迁移指南](../../../docs/framework/migration-guide/index.md)。  
  
-   有关确定计算机上安装了哪些版本或更新的信息，请参阅[如何：确定安装了哪些 .NET Framework 版本](../../../docs/framework/migration-guide/how-to-determine-which-versions-are-installed.md)和[如何：确定安装了哪些 .NET Framework 更新](../../../docs/framework/migration-guide/how-to-determine-which-net-framework-updates-are-installed.md)。  
  
## <a name="see-also"></a>请参阅

[版本兼容性](../../../docs/framework/migration-guide/version-compatibility.md)   
[Microsoft .NET Framework 支持生命周期策略](http://go.microsoft.com/fwlink/?LinkId=196607)   
[安装和卸载 .NET Framework 受阻疑难解答](../../../docs/framework/install/troubleshoot-blocked-installations-and-uninstallations.md)

