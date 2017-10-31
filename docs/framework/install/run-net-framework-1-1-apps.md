---
title: "在 Windows 8、Windows 8.1 或 Windows 10 上运行 .NET Framework 1.1 应用"
ms.custom: 
ms.date: 05/26/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology:
- dotnet-clr
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Windows 8, running .NET Framework 1.1 apps
- .NET Framework 1.1, running on Windows 8
ms.assetid: fb14e195-fea5-4561-b9a8-60a67283edb9
caps.latest.revision: 9
author: mairaw
ms.author: mairaw
manager: wpickett
ms.translationtype: HT
ms.sourcegitcommit: 21c6a1485f3d0c38bde065d6ecc7b07d5e424c1d
ms.openlocfilehash: c7b53a842dc4f9b6bfc04e058411e4a6d11a7bd1
ms.contentlocale: zh-cn
ms.lasthandoff: 08/05/2017

---

# <a name="run-net-framework-11-apps-on-windows-8-windows-81-or-windows-10"></a>在 Windows 8、Windows 8.1 或 Windows 10 上运行 .NET Framework 1.1 应用

[!INCLUDE[win8](../../../includes/win8-md.md)]、[!INCLUDE[win81](../../../includes/win81-md.md)]、[!INCLUDE[winserver8](../../../includes/winserver8-md.md)]、[!INCLUDE[winblue_server_2](../../../includes/winblue-server-2-md.md)] 或 Windows 10 操作系统上不支持 .NET Framework 1.1。 在某些情况下，.NET Framework 1.1 专门标识为是运行应用所必需的。 在这些情况下，应联系独立软件供应商 (ISV) 以升级该应用，使其可在 [!INCLUDE[net_v35SP1_short](../../../includes/net-v35sp1-short-md.md)] 或更高版本上运行。 有关其他信息，请参阅[从 .NET Framework 1.1 迁移](../../../docs/framework/migration-guide/migrating-from-the-net-framework-1-1.md)。

## <a name="install-the-net-framework-11-from-a-cd-or-download-center"></a>从 CD 或下载中心安装 .NET Framework 1.1

在 [!INCLUDE[win8](../../../includes/win8-md.md)]、[!INCLUDE[win81](../../../includes/win81-md.md)]、[!INCLUDE[winserver8](../../../includes/winserver8-md.md)]、[!INCLUDE[winblue_server_2](../../../includes/winblue-server-2-md.md)] 或 Windows 10 上无法手动安装 .NET Framework 1.1。 它不再受支持。 如果尝试安装此包，将显示以下错误消息：“安装程序无法继续，因为该版本的 .NET Framework 与之前安装的版本不兼容”。 若要解决此问题，请安装 [.NET Framework 3.5 SP1](http://www.microsoft.com/download/details.aspx?id=22)。 此版本包括 .NET Framework 2.0（.NET Framework 1.1 之后的版本），[!INCLUDE[win8](../../../includes/win8-md.md)]、[!INCLUDE[win81](../../../includes/win81-md.md)] 和 Windows 10 上支持 .NET Framework 2.0。 首先，应始终尝试安装该应用，确定其是否会自动更新到 .NET Framework 的更高版本。 如果不会，请联系 ISV 获取应用更新。

## <a name="see-also"></a>请参阅

[从 .NET Framework 1.1 迁移](../../../docs/framework/migration-guide/migrating-from-the-net-framework-1-1.md)
[在 Windows 10、Windows 8.1 和 Windows 8 上安装 .NET Framework 3.5](../../../docs/framework/install/dotnet-35-windows-10.md)

