---
title: "在 .NET Framework 4.5 安装期间减少系统重新启动"
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
- .NET Framework, reducing system restarts
- installing .NET Framework
- installation [.NET Framework]
ms.assetid: 7aa8cb72-dee9-4716-ac54-b17b9ae8218f
caps.latest.revision: 18
author: mairaw
ms.author: mairaw
manager: wpickett
ms.translationtype: HT
ms.sourcegitcommit: 306c608dc7f97594ef6f72ae0f5aaba596c936e1
ms.openlocfilehash: d3f54e3794d1595ed120685a452478791e0ad37c
ms.contentlocale: zh-cn
ms.lasthandoff: 07/28/2017

---
# <a name="reducing-system-restarts-during-net-framework-45-installations"></a>在 .NET Framework 4.5 安装期间减少系统重新启动
[!INCLUDE[net_v45](../../../includes/net-v45-md.md)] 安装程序使用[重启管理器](http://go.microsoft.com/fwlink/?LinkId=231425)来防止安装期间可能出现的系统重启。 如果应用安装程序安装了 .NET Framework，则此程序可通过使用重启管理器来利用此功能。 有关详细信息，请参阅[如何：获取 .NET Framework 4.5 安装程序的进度](../../../docs/framework/deployment/how-to-get-progress-from-the-dotnet-installer.md)。  
  
## <a name="reasons-for-a-restart"></a>重启的原因  
 如果在安装 [!INCLUDE[net_v45](../../../includes/net-v45-md.md)] 时 .NET Framework 4 应用正在运行，则此安装需要重启系统。 这是因为 [!INCLUDE[net_v45](../../../includes/net-v45-md.md)] 将替代 .NET Framework 4 文件，而在安装期间需要使用这些文件。 在许多情况下，通过提前检测并关闭正在运行的 .NET Framework 4 应用即可避免重启。 但有时某些系统应用不应被关闭。 此时就无法避免重启。  
  
## <a name="end-user-experience"></a>最终用户体验  
 当安装程序检测到 .NET Framework 4 应用正在运行时，执行 [!INCLUDE[net_v45](../../../includes/net-v45-md.md)] 完全安装的最终用户有机会避免系统重启。 系统将显示一条消息，其中列出所有正在运行的 .NET Framework 4 应用并提供在安装前关闭这些应用的选项。 如果用户确认选择，安装程序将关闭这些应用，避免系统重启。 如果用户未在特定时间段内对此消息做出响应，系统将在未关闭这些应用的情况下继续安装。  
  
 如果已关闭了正在运行的应用，但重启管理器仍检测到需要系统重启，则不会显示此消息。  
  
 ![“关闭应用程序”对话框](../../../docs/framework/deployment/media/closeapplicationdialog.png "CloseApplicationDialog")  
关闭正在运行的 .NET Framework 应用的提示  
  
## <a name="using-a-chained-installer"></a>使用链接的安装程序  
 如果想要向应用重新分发 .NET Framework，但希望使用自己的安装程序和 UI，则可将 .NET Framework 安装过程包含在（链接到）自己的安装过程中。 有关链接的安装的详细信息，请参阅[面向开发人员的部署指南](../../../docs/framework/deployment/deployment-guide-for-developers.md)。 为减少链接的安装中的系统重启次数，.NET Framework 安装程序为安装程序提供了需要关闭的应用列表。 安装程序必须通过用户界面（如消息框）向用户提供此信息，获得用户的响应并将响应传递回 .NET Framework 安装程序。 有关链接的安装程序的示例，请参阅文章[如何：获取 .NET Framework 4.5 安装程序的进度](../../../docs/framework/deployment/how-to-get-progress-from-the-dotnet-installer.md)。  
  
 如果使用的是链接的安装程序，但不希望提供自己的消息框用于关闭应用，则链接 .NET Framework 安装过程时可以使用命令行上的 `/showrmui` 和 `/passive` 选项。 一起使用这些选项时，如果可以通过关闭应用避免系统重启，安装程序将显示关闭应用的消息框。 此消息框在被动模式下的行为与在完全用户界面下的行为相同。 请参阅[面向开发人员的部署指南](../../../docs/framework/deployment/deployment-guide-for-developers.md)，了解用于重新分发 .NET Framework 的一组完整命令行选项。  
  
## <a name="see-also"></a>另请参阅  
 [部署](../../../docs/framework/deployment/index.md)   
 [面向开发人员的部署指南](../../../docs/framework/deployment/deployment-guide-for-developers.md)   
 [如何：获取 .NET Framework 4.5 安装程序的进度](../../../docs/framework/deployment/how-to-get-progress-from-the-dotnet-installer.md)

