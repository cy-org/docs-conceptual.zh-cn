---
title: ".NET Framework 4.7、4.6 和 4.5 的迁移指南 "
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
- .NET Framework, migrating applications to
- migration, .NET Framework
ms.assetid: 02d55147-9b3a-4557-a45f-fa936fadae3b
caps.latest.revision: 56
author: rpetrusha
ms.author: ronpet
manager: wpickett
ms.translationtype: HT
ms.sourcegitcommit: 306c608dc7f97594ef6f72ae0f5aaba596c936e1
ms.openlocfilehash: 820d1966172a93c06c6451c51bc7f360496f46b8
ms.contentlocale: zh-cn
ms.lasthandoff: 07/28/2017

---
# <a name="migration-guide-to-the-net-framework-47-46-and-45"></a>.NET Framework 4.7、4.6 和 4.5 的迁移指南 
如果已使用早期版本的 .NET Framework 构建应用，通常可以将其轻松升级到 .NET Framework 4.5 及其点版本（4.5.1 和 4.5.2）、.NET Framework 4.6 及其点版本（4.6.1 和 4.6.2），或 .NET Framework 4.7。 在 Visual Studio 中打开项目。 如果已在早期版本中创建项目，“项目兼容性”对话框将自动打开。 有关在 Visual Studio 中升级项目的详细信息，请参阅[移植、迁移和升级 Visual Studio 项目](/visualstudio/porting/port-migrate-and-upgrade-visual-studio-projects)和 [Visual Studio 2017 平台目标以及兼容性](https://www.visualstudio.com/en-us/productinfo/vs2017-compatibility-vs)。  
  
 但是，.NET Framework 中的某些更改需要更改你的代码。 你可能还希望利用 .NET Framework 4.5 及其点版本、.NET Framework 4.6 及其点版本或 .NET Framework 4.7 中的新增功能。 通常，针对新版本的 .NET Framework 来对应用进行这些类型的更改的过程称作“迁移”。 如果不必迁移应用，那么你可以在 .NET Framework 4.5 或更高版本中运行它，而无需编译它。  
  
## <a name="migration-resources"></a>迁移资源  
 在将应用从 .NET Framework 的早期版本迁移到版本 4.5、4.5.1、4.5.2、4.6、4.6.1、4.6.2 或 4.7 之前，请查看以下文档：  
  
-   请参阅[版本和依赖关系](../../../docs/framework/migration-guide/versions-and-dependencies.md)以了解作为每个 .NET Framework 版本基础的 CLR 版本，并查看成功设定应用目标的指南。  
  
-   查看[应用程序兼容性](../../../docs/framework/migration-guide/application-compatibility.md)以了解可能影响应用的运行时和重定目标更改以及如何处理这些更改。  
  
-   查看[类库中过时的内容](../../../docs/framework/whats-new/whats-obsolete.md)以确定代码中已过时的任何类型或成员以及建议的备选项。  
  
-   查看[新增功能](../../../docs/framework/whats-new/index.md)以了解可能需要向应用添加的新功能的说明。  
  
## <a name="see-also"></a>另请参阅  
 [应用程序兼容性](../../../docs/framework/migration-guide/application-compatibility.md)   
 [从 .NET Framework 1.1 迁移](../../../docs/framework/migration-guide/migrating-from-the-net-framework-1-1.md)   
 [版本兼容性](../../../docs/framework/migration-guide/version-compatibility.md)   
 [版本和依赖关系](../../../docs/framework/migration-guide/versions-and-dependencies.md)   
 [如何：配置应用以支持 .NET Framework 4 或 4.5](../../../docs/framework/migration-guide/how-to-configure-an-app-to-support-net-framework-4-or-4-5.md)   
 [新增功能](../../../docs/framework/whats-new/index.md)   
 [类库中过时的内容](../../../docs/framework/whats-new/whats-obsolete.md)   
 [.NET Framework 版本和程序集信息](http://go.microsoft.com/fwlink/?LinkId=201701)   
 [Microsoft .NET Framework 支持生命周期策略](http://go.microsoft.com/fwlink/?LinkId=196607) [.NET Framework 4 迁移问题](net-framework-4-migration-issues.md)

