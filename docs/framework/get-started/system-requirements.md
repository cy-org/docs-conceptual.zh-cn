---
title: ".NET Framework 系统要求"
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology:
- dotnet-clr
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- software requirements
- .NET Framework, system requirements
- system requirements
- operating systems supported
- hardware requirements
ms.assetid: 298275e2-da1d-4618-9f74-6a3567832350
caps.latest.revision: 95
author: rpetrusha
ms.author: ronpet
manager: wpickett
ms.translationtype: HT
ms.sourcegitcommit: 21c6a1485f3d0c38bde065d6ecc7b07d5e424c1d
ms.openlocfilehash: 18875105836ee4be0a3d3fb61a83ef6cd29b8c58
ms.contentlocale: zh-cn
ms.lasthandoff: 08/05/2017

---

# <a name="net-framework-system-requirements"></a>.NET Framework 系统要求

本主题中的表格提供 .NET Framework 4.5 及其单点版本（4.5.1 和 4.5.2）、[!INCLUDE[net_v46](../../../includes/net-v46-md.md)] 及其单点版本（4.6.1 和 4.6.2）和 .NET Framework 4.7 的硬件、操作系统及软件要求。 允许你开发 .NET Framework 的应用的开发环境具有单独的一套需求。

有关下载信息和链接，请参阅[安装面向开发者的 .NET Framework](../../../docs/framework/install/guide-for-developers.md)。

有关 .NET Framework 版本的支持生命周期的信息，请参阅 [Microsoft 支持生命周期](https://support.microsoft.com/en-us/lifecycle/search?sort=PN&alpha=Microsoft%20.NET%20Framework&Filter=FilterNO)。

## <a name="hardware-requirements"></a>硬件要求

|                          |        |
| ------------------------ | ------ |
| **处理器**            | 1 GHz  |
| **RAM**                  | 512 MB |
| **磁盘空间（最小值）** |        |
| 32 位                   | 4.5 GB |
| 64 位                   | 4.5 GB |

## <a name="installation-requirements"></a>安装要求

需要具有管理员权限才能安装 .NET Framework。 如果在要安装 .NET Framework 的计算机上不具有管理员权限，请联系网络管理员。

## <a name="supported-client-operating-systems"></a>支持的客户端操作系统

| 操作系统 | 支持的版本 | 随 OS 预安装 | 可安装单独 |
| ---------------- | ------------------ | ------------------------ | ---------------------- |
| Windows 10 创意者更新 | 32 位和 64 位 | .NET Framework 4.7 | | 
| Windows 10 周年更新 | 32 位和 64 位 | [!INCLUDE[net_v462](../../../includes/net-v462-md.md)]|.NET Framework 4.7 |
| Windows 10 November Update | 32 位和 64 位 | [!INCLUDE[net_v461](../../../includes/net-v461-md.md)] | |
| Windows 10 | 32 位和 64 位 | [!INCLUDE[net_v46](../../../includes/net-v46-md.md)] | [!INCLUDE[net_v461](../../../includes/net-v461-md.md)] |
| [!INCLUDE[win81](../../../includes/win81-md.md)] | 32 位、64 位和 ARM | [!INCLUDE[net_v451](../../../includes/net-v451-md.md)] | [!INCLUDE[net_v452](../../../includes/net-v452-md.md)]<br /><br /> [!INCLUDE[net_v46](../../../includes/net-v46-md.md)]<br /><br /> [!INCLUDE[net_v461](../../../includes/net-v461-md.md)]<br /><br /> [!INCLUDE[net_v462](../../../includes/net-v462-md.md)]<br /><br />.NET Framework 4.7 |
| [!INCLUDE[win8](../../../includes/win8-md.md)] | 32 位、64 位和 ARM | [!INCLUDE[net_v45](../../../includes/net-v45-md.md)] | [!INCLUDE[net_v451](../../../includes/net-v451-md.md)]<br /><br /> [!INCLUDE[net_v452](../../../includes/net-v452-md.md)]<br /><br /> [!INCLUDE[net_v46](../../../includes/net-v46-md.md)]<br /><br /> [!INCLUDE[net_v461](../../../includes/net-v461-md.md)] |
| Windows 7 SP1|32 位和 64 位 | -- | .NET Framework 4<br /><br /> [!INCLUDE[net_v45](../../../includes/net-v45-md.md)]<br /><br /> [!INCLUDE[net_v451](../../../includes/net-v451-md.md)]<br /><br /> [!INCLUDE[net_v452](../../../includes/net-v452-md.md)]<br /><br /> [!INCLUDE[net_v46](../../../includes/net-v46-md.md)]<br /><br /> [!INCLUDE[net_v461](../../../includes/net-v461-md.md)]<br /><br /> [!INCLUDE[net_v462](../../../includes/net-v462-md.md)]<br /><br />.NET Framework 4.7 |
| Windows Vista SP2|32 位和 64 位 | -- | .NET Framework 4<br /><br /> [!INCLUDE[net_v45](../../../includes/net-v45-md.md)]<br /><br /> [!INCLUDE[net_v451](../../../includes/net-v451-md.md)]<br /><br /> [!INCLUDE[net_v452](../../../includes/net-v452-md.md)]<br /><br /> [!INCLUDE[net_v46](../../../includes/net-v46-md.md)] |
| Windows XP |32 位和 64 位 | -- | .NET Framework 4 |

 **注意：**

- 在 Windows 7 系统上，.NET Framework 要求安装 Windows 7 SP1。 如果使用的是 Windows 7 系统，但尚未安装 Service Pack 1，则需要先安装 SP1，然后才能安装 .NET Framework。

- Windows Preinstallation Environment (Windows PE) 上支持 [!INCLUDE[net_v45](../../../includes/net-v45-md.md)]。 Windows PE 上并非支持所有功能。

- .NET Framework 4 还支持 IA64 平台。

- 对于所有平台，我们都建议升级到最新的 Windows Service Pack 并安装 [Windows Update 网站](http://go.microsoft.com/fwlink/?LinkId=168461)上提供的关键更新，从而确保实现最佳兼容性和安全性。

- 在 64 位操作系统上，.NET Framework 支持 WOW64（在 64 位计算机上进行 32 位处理）和本机 64 位处理。

## <a name="supported-server-operating-systems"></a>支持的服务器操作系统

| 操作系统 | 支持的版本 | 随 OS 预安装 | 可安装单独 |
| ---------------- | ------------------ | ------------------------ | ---------------------- |
| Windows 2016 Server | 64 位 | [!INCLUDE[net_v462](../../../includes/net-v462-md.md)] | .NET Framework 4.7 |
| [!INCLUDE[winblue_server_2](../../../includes/winblue-server-2-md.md)] | 64 位 | [!INCLUDE[net_v451](../../../includes/net-v451-md.md)] | [!INCLUDE[net_v452](../../../includes/net-v452-md.md)]<br /><br /> [!INCLUDE[net_v46](../../../includes/net-v46-md.md)]<br /><br /> [!INCLUDE[net_v461](../../../includes/net-v461-md.md)]<br /><br /> [!INCLUDE[net_v462](../../../includes/net-v462-md.md)]<br /><br />.NET Framework 4.7 |
| [!INCLUDE[winserver8](../../../includes/winserver8-md.md)]（64 位版本） | 64 位| [!INCLUDE[net_v45](../../../includes/net-v45-md.md)] | [!INCLUDE[net_v451](../../../includes/net-v451-md.md)]<br /><br /> [!INCLUDE[net_v452](../../../includes/net-v452-md.md)]<br /><br /> [!INCLUDE[net_v46](../../../includes/net-v46-md.md)]<br /><br /> [!INCLUDE[net_v461](../../../includes/net-v461-md.md)]<br /><br /> [!INCLUDE[net_v462](../../../includes/net-v462-md.md)]<br /><br />.NET Framework 4.7 |
| Windows Server 2008 R2 SP1|64 位 | -- | .NET Framework 4<br /><br /> [!INCLUDE[net_v45](../../../includes/net-v45-md.md)]<br /><br /> [!INCLUDE[net_v451](../../../includes/net-v451-md.md)]<br /><br /> [!INCLUDE[net_v452](../../../includes/net-v452-md.md)]<br /><br /> [!INCLUDE[net_v46](../../../includes/net-v46-md.md)]<br /><br /> [!INCLUDE[net_v461](../../../includes/net-v461-md.md)]<br /><br /> [!INCLUDE[net_v462](../../../includes/net-v462-md.md)]<br /><br />.NET Framework 4.7 |
| Windows Server 2008 SP2|32 位和 64 位 | -- | .NET Framework 4<br /><br /> [!INCLUDE[net_v45](../../../includes/net-v45-md.md)]<br /><br /> [!INCLUDE[net_v451](../../../includes/net-v451-md.md)]<br /><br /> [!INCLUDE[net_v452](../../../includes/net-v452-md.md)]<br /><br /> [!INCLUDE[net_v46](../../../includes/net-v46-md.md)] |

 **注意：**

- [!INCLUDE[winserver8](../../../includes/winserver8-md.md)] 包括 [!INCLUDE[net_v45](../../../includes/net-v45-md.md)]，因此，你不必单独安装它。 同样，[!INCLUDE[winblue_server_2](../../../includes/winblue-server-2-md.md)]包含 [!INCLUDE[net_v451](../../../includes/net-v451-md.md)]。

- 在 Windows Server 2008 R2 SP1 或更高版本上，.NET Framework 在服务器核心角色中受支持，但在基于 Itanium 的系统的 Windows Server 2008 R2 上不受支持。

- 在 Windows Server 2008 SP2 上，.NET Framework 在服务器核心角色中不受支持。

- 对于所有平台，我们都建议升级到最新的 Windows Service Pack 并安装 [Windows Update 网站](http://go.microsoft.com/fwlink/?LinkId=168461)上提供的关键更新，从而确保实现最佳兼容性和安全性。 某些操作系统上可能需要安装最新的 Windows Service Pack。

- 在 64 位操作系统上，.NET Framework 支持 WOW64（在 64 位计算机上进行 32 位处理）和本机 64 位处理。

## <a name="see-also"></a>请参阅

[安装指南](../../../docs/framework/install/index.md)   
[入门](../../../docs/framework/get-started/index.md)   
[安装和卸载 .NET Framework 受阻疑难解答](../../../docs/framework/install/troubleshoot-blocked-installations-and-uninstallations.md)

