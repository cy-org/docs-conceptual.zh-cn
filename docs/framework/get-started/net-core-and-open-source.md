---
title: ".NET 核心和开放源代码"
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology:
- dotnet-clr
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: e6bd4655-ce37-4003-8462-468a6fe2c40f
caps.latest.revision: 8
author: mairaw
ms.author: mairaw
manager: wpickett
ms.translationtype: HT
ms.sourcegitcommit: 3155295489e1188640dae5aa5bf9fdceb7480ed6
ms.openlocfilehash: db4689ee58b48fad2e3696e5e64aa187710f4868
ms.contentlocale: zh-cn
ms.lasthandoff: 08/05/2017

---
# <a name="net-core-and-open-source"></a>.NET 核心和开放源代码
本主题提供有关 .NET 核心概念的简要概述并展示如何查找更多信息。 若要查找有关 .NET Core 的完整主题列表，请访问 [.NET Core 指南](../../core/index.md)。
  
<a name="BKMK_WhatisNETCore"></a>   
## <a name="what-is-net-core"></a>.NET 核心是什么？  
 .NET Core 是 .NET 标准的常规用途、模块化、跨平台和开放源代码实现。 它包含 .NET Framework 这样的许多相同 API（但 .NET Core 是较小的集）并包括支持不同操作系统和芯片目标的运行时、框架、编译器和工具组件。 .NET Core 实现主要由 ASP.NET 核心工作负载驱动，但同时也由拥有一个更现代的实现这一需求和愿望驱动。 它可以用于设备、云和嵌入式/IoT 方案。  
  
 若要开始使用 .NET 核心，请访问 [.NET 核心主页](https://www.microsoft.com/net/core)。  
  
 下面列出了 .NET 核心的主要特征：  
  
-   **跨平台：**.NET 核心提供了实现所需应用功能的关键功能，并且可以重用代码而不考虑平台目标。 它当前支持三种主要的操作系统 (OS)：Windows、 Linux 和 macOS。 可以编写无需修改即可跨受支持操作系统运行的应用和库。 若要查看受支持操作系统的列表，请访问 [.NET Core 路线图](https://github.com/dotnet/core/blob/master/roadmap.md)。
  
-   **开放源代码：**.NET 核心是 [.NET Foundation](http://www.dotnetfoundation.org/) 管理下的很多项目中的一个，并在 [GitHub](https://github.com/) 上提供。  将 .NET 核心作为开放源代码项目促使开发过程更加透明并能提升社区的活跃度及参与度。  
  
-   **灵活部署：**部署应用有两种主要方法：依赖框架的部署或独立部署。 使用依赖框架的部署时，仅安装应用和第三方依赖关系，而应用依赖于存在系统范围版本的 .NET 核心。  使用独立部署时，用于构建应用程序的 .NET 核心版本随应用和第三方依赖关系一同部署，并可与其他版本并行运行。    有关详细信息，请参阅 [.NET 核心应用程序部署](../../core/deploying/index.md)。

-   模块化：.NET Core 为模块化，因为它通过 NuGet 以较小的程序集包发布。 与包含了大部分核心功能的大型程序集不同，.NET 核心作为以功能为中心的小型数据包提供。 这为我们提供了更加灵活的开发模型，允许优化应用使其仅包含所需的 NuGet 程序包。 较小的应用图面区域的优势包括：提升安全性、减少维护、提高性能并采用按使用情况付费的模式降低成本。  
  
## <a name="the-net-core-platform"></a>.NET 核心平台  
 .NET 核心平台由一些组件构成，其中包括托管的编译器、运行时、基类库和大量应用程序模型，如 ASP.NET 核心。 可以通过访问以下 [GitHub](https://github.com/) 存储库来了解更多关于不同组件的信息并参与进来：  
  
-   [.NET Core](https://github.com/dotnet/core)  
  
-   [CoreFX - .NET Core foundational libraries](https://github.com/dotnet/corefx)  
  
-   [CoreCLR - .NET Core runtime](https://github.com/dotnet/coreclr)  
  
-   [CLI - .NET Core command-line tools](https://github.com/dotnet/cli)  
  
-   [Roslyn - .NET Compiler Platform](https://github.com/dotnet/roslyn)  
  
-   [ASP.NET Core](https://github.com/aspnet/home)  
  
## <a name="see-also"></a>另请参阅  
 [.NET 核心主页](https://www.microsoft.com/net/core)   
 [.NET Core 指南](../../core/index.md)   
 [ASP.NET 核心文档](/aspnet/core/)

