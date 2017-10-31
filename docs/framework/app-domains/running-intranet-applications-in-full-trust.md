---
title: "在完全信任环境中运行 Intranet 应用程序"
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology:
- dotnet-bcl
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- full trust, running intranet applications in
- intranet applications, running in full trust
- running intranet applications in full trust
ms.assetid: ee13c0a8-ab02-49f7-b8fb-9eab16c6c4f0
caps.latest.revision: 20
author: rpetrusha
ms.author: ronpet
manager: wpickett
ms.translationtype: HT
ms.sourcegitcommit: 306c608dc7f97594ef6f72ae0f5aaba596c936e1
ms.openlocfilehash: 58eeda82c66ecda6ffd714e808b006634ccba804
ms.contentlocale: zh-cn
ms.lasthandoff: 07/28/2017

---
# <a name="running-intranet-applications-in-full-trust"></a>在完全信任环境中运行 Intranet 应用程序
从 .NET Framework 3.5 版 Service Pack 1 (SP1) 开始，应用程序及其库程序集可在网络共享中作为完全信任的程序集运行。 <xref:System.Security.SecurityZone.MyComputer> 区域证据自动添加到从 Intranet 上的共享加载的程序集。 此证据为这些程序集提供与计算机上程序集所具有的相同授予集（通常为完全信任）。 此功能不适用于 ClickOnce 应用程序或用于在主机上运行的应用程序。  
  
## <a name="rules-for-library-assemblies"></a>库程序集的规则  
 以下规则适用于可执行文件在网络共享上加载的程序集：  
  
-   库程序集必须与可执行程序集位于同一文件夹。 不能为位于子文件夹或通过不同路径引用的程序集提供完全信任的授予集。  
  
-   如果可执行文件延迟加载程序集，则它必须使用启动可执行文件所用的路径。 例如，如果共享 \\\\network-computer\\share 映射到某个驱动器号，并且可执行文件是从该路径运行的，那么由该可执行文件使用网络路径加载的程序集将不会被授予完全信任。 若要在 <xref:System.Security.SecurityZone.MyComputer> 区域延迟加载程序集，则可执行文件必须使用驱动器号路径。  
  
## <a name="restoring-the-former-intranet-policy"></a>还原以前的 Intranet 策略  
 在早期版本的 .NET framework 中，可为 <xref:System.Security.SecurityZone.Intranet> 区域证据授予共享程序集。 必须指定代码访问安全策略才能为共享上的程序集授予完全信任。  
  
 这一新行为现在是 Intranet 程序集的默认行为。 通过设置适用于计算机上所有应用程序的注册表项，可以还原到早期提供 <xref:System.Security.SecurityZone.Intranet> 证据的行为。 此过程在 32 位和 64 位计算机上有所不同：  
  
-   对于 32 位计算机，在系统注册表中的 HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\\.NETFramework 项下创建子项。 使用项名称 LegacyMyComputerZone，DWORD 值为 1。  
  
-   对于 64 位计算机，在系统注册表中的 HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\\.NETFramework 项下创建子项。 使用项名称 LegacyMyComputerZone，DWORD 值为 1。 在 HKEY_LOCAL_MACHINE\SOFTWARE\Wow6432Node\Microsoft\\.NETFramework 项下创建相同的子项。  
  
## <a name="see-also"></a>另请参阅  
 [使用程序集编程](../../../docs/framework/app-domains/programming-with-assemblies.md)

