---
title: "隔离的类型 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-standard"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "使用独立存储来存储数据，访问独立存储"
  - "使用独立存储来存储数据，隔离类型"
  - "身份验证 [.NET Framework]，独立存储"
  - "程序集 [.NET Framework]，标识"
  - "独立存储，访问"
  - "使用独立存储的数据存储，隔离类型"
  - "使用独立存储的数据存储，访问独立存储"
  - "域标识"
  - "独立存储，类型"
  - "用户身份验证，独立存储"
ms.assetid: 14812988-473f-44ae-b75f-fd5c2f21fb7b
caps.latest.revision: 16
author: "mairaw"
ms.author: "mairaw"
manager: "wpickett"
caps.handback.revision: 16
---
# 隔离的类型
对独立存储的访问总是限制在创建该存储的用户。  要实现这种类型的隔离，公共语言运行时使用的用户标识注记与操作系统识别的注记相同，该用户标识注记是与存储区打开时代码在其中运行的进程相关联的标识。  虽然该标识是已验证身份的用户标识，但是模拟可以导致当前用户的标识动态地改变。  
  
 访问独立存储根据与应用程序的域和程序集相关的（或仅与程序集相关的）标识被限制。  运行时以下面几种方式获得这些标识：  
  
-   代表应用程序的证据的域标识，在 Web 应用程序情况下，该域标识可能是完整 URL。  对于寄宿于 shell 的代码，该域标识可能基于应用程序目录路径。  例如，如果可执行文件在路径 C:\\Office\\MyApp.exe 中运行，域标识可能为 C:\\Office\\MyApp.exe。  
  
-   程序集标识是程序集的证据。  程序集标识可能来自于加密的数字签名，它可以是程序集的[强名称](../../../docs/framework/app-domains/strong-named-assemblies.md)、程序集的发行者或其 URL 标识。  如果程序集同时具有强名称和发行者标识，则使用发行者标识。  如果程序集来自 Internet 并且未签名，则使用 URL 标识。  有关程序集和强名称的更多信息，请参见[使用程序集编程](../../../docs/framework/app-domains/programming-with-assemblies.md)。  
  
-   漫游存储区和具有漫游用户配置文件的用户一起移动。  文件被写入网络目录并被下载到用户登录的任何一台计算机上。  有关漫游用户配置文件的更多信息，请参见 <xref:System.IO.IsolatedStorage.IsolatedStorageScope?displayProperty=fullName>。  
  
 将用户、域和程序集标识的概念结合起来，独立存储可以按下面几种方式隔离数据，每种方式都有其自己的使用情况：  
  
-   [按用户和程序集隔离](#UserAssembly)  
  
-   [按用户、域和程序集隔离。](#UserDomainAssembly)  
  
 这两种隔离的每一种都可以和漫游用户配置文件结合。  有关更多信息，请参见 [独立存储和漫游](#Roaming)节。  
  
 下面的插图说明了如何将存储区隔离在不同的范围。  
  
 ![按用户和程序集隔离](../../../docs/standard/io/media/typesofisolation.gif "typesofisolation")  
独立存储的类型  
  
 请注意，除了漫游存储区之外，独立存储始终被计算机隐式隔离，这是因为独立存储使用给定计算机本地的存储功能。  
  
> [!IMPORTANT]
>  独立存储不适用于 [!INCLUDE[win8_appname_long](../../../includes/win8-appname-long-md.md)]应用。  相反，用[!INCLUDE[wrt](../../../includes/wrt-md.md)]API中包含的`Windows.Storage`命名空间中的应用程序数据类来保存数据和文件。  有关更多信息，请参见Windows开发者中心中的[Application data](http://go.microsoft.com/fwlink/?LinkId=229175)  
  
<a name="UserAssembly"></a>   
## 按用户和程序集隔离  
 当需要从任何应用程序域都可以访问使用数据存储区程序集时，按用户和程序集隔离比较合适。  通常，在这种情况下，独立存储用于存储跨多个应用程序应用的数据（例如用户的名称或许可证信息），这些数据不依赖于任何特定的应用程序。  要访问按用户和程序集隔离的存储，代码必须受信以在应用程序之间传输信息。  通常，允许在 Intranet 上使用按用户和程序集隔离，但不允许在 Internet 上使用。  调用静态的<xref:System.IO.IsolatedStorage.IsolatedStorageFile.GetStore%2A?displayProperty=fullName> 方法并传入用户和程序集<xref:System.IO.IsolatedStorage.IsolatedStorageScope>将返回具有这种隔离的存储。  
  
 下面的代码示例检索按用户和程序集隔离的漫游存储区。  可通过 `isoFile` 对象访问该存储区。  
  
 [!code-cpp[Conceptual.IsolatedStorage#17](../../../samples/snippets/cpp/VS_Snippets_CLR/conceptual.isolatedstorage/cpp/source11.cpp#17)]
 [!code-csharp[Conceptual.IsolatedStorage#17](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.isolatedstorage/cs/source11.cs#17)]
 [!code-vb[Conceptual.IsolatedStorage#17](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.isolatedstorage/vb/source11.vb#17)]  
  
 有关使用证据参数的示例，请参见 <xref:System.IO.IsolatedStorage.IsolatedStorageFile.GetStore%28System.IO.IsolatedStorage.IsolatedStorageScope%2CSystem.Security.Policy.Evidence%2CSystem.Type%2CSystem.Security.Policy.Evidence%2CSystem.Type%29>。  
  
 <xref:System.IO.IsolatedStorage.IsolatedStorageFile.GetUserStoreForAssembly%2A> 方法可作为快捷方式，如下面的代码示例中所示。  此快捷方式无法用于打开能够漫游的存储区，在这种情况下，请使用 <xref:System.IO.IsolatedStorage.IsolatedStorageFile.GetStore%2A>。  
  
 [!code-cpp[Conceptual.IsolatedStorage#18](../../../samples/snippets/cpp/VS_Snippets_CLR/conceptual.isolatedstorage/cpp/source11.cpp#18)]
 [!code-csharp[Conceptual.IsolatedStorage#18](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.isolatedstorage/cs/source11.cs#18)]
 [!code-vb[Conceptual.IsolatedStorage#18](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.isolatedstorage/vb/source11.vb#18)]  
  
<a name="UserDomainAssembly"></a>   
## 按用户、域和程序集隔离  
 如果应用程序使用需要私有数据存储区的第三方程序集，可隔离存储来存储私有数据。  按用户、域和程序集隔离确保只有当在程序集创建存储区时运行的应用程序使用该程序集时，并且只有当为其创建存储区的用户运行该应用程序时，只有给定程序集中的代码才可以访问数据。  按用户、域和程序集隔离使第三方程序集不能向其他应用程序泄露数据。  如果您知道要使用隔离存储但不确定要使用哪种类型的隔离，这种隔离类型应该是您的默认选择。  调用 <xref:System.IO.IsolatedStorage.IsolatedStorageFile> 的静态 <xref:System.IO.IsolatedStorage.IsolatedStorageFile.GetStore%2A> 方法并传入用户、域和程序集，<xref:System.IO.IsolatedStorage.IsolatedStorageScope> 将返回具有这种隔离的存储。  
  
 下面的代码示例检索按用户、域和程序集隔离的存储区。  可通过 `isoFile` 对象访问该存储区。  
  
 [!code-cpp[Conceptual.IsolatedStorage#14](../../../samples/snippets/cpp/VS_Snippets_CLR/conceptual.isolatedstorage/cpp/source10.cpp#14)]
 [!code-csharp[Conceptual.IsolatedStorage#14](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.isolatedstorage/cs/source10.cs#14)]
 [!code-vb[Conceptual.IsolatedStorage#14](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.isolatedstorage/vb/source10.vb#14)]  
  
 另一个方法可作为快捷方式，如下面的代码示例中所示。  此快捷方式无法用于打开能够漫游的存储区，在这种情况下，请使用 <xref:System.IO.IsolatedStorage.IsolatedStorageFile.GetStore%2A>。  
  
 [!code-cpp[Conceptual.IsolatedStorage#15](../../../samples/snippets/cpp/VS_Snippets_CLR/conceptual.isolatedstorage/cpp/source10.cpp#15)]
 [!code-csharp[Conceptual.IsolatedStorage#15](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.isolatedstorage/cs/source10.cs#15)]
 [!code-vb[Conceptual.IsolatedStorage#15](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.isolatedstorage/vb/source10.vb#15)]  
  
<a name="Roaming"></a>   
## 独立存储和漫游  
 漫游用户配置文件是用户可以在网络上设置一标识和使用该标识登录任何系统您的计算机上 Windows 功能，使任何个性化设置转入。  使用独立存储的程序集可以指定用户的独立存储和漫游用户配置文件一起移动。  漫游可以和按用户和程序集隔离或按用户、域和程序集隔离一起使用。  如果未使用漫游范围，即使使用了漫游用户配置文件，存储区也不漫游。  
  
 下面的代码示例检索按用户和程序集隔离的漫游存储区。  可通过 `isoFile` 对象访问该存储区。  
  
 [!code-cpp[Conceptual.IsolatedStorage#11](../../../samples/snippets/cpp/VS_Snippets_CLR/conceptual.isolatedstorage/cpp/source9.cpp#11)]
 [!code-csharp[Conceptual.IsolatedStorage#11](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.isolatedstorage/cs/source9.cs#11)]
 [!code-vb[Conceptual.IsolatedStorage#11](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.isolatedstorage/vb/source9.vb#11)]  
  
 可以添加域范围来创建按用户、域和应用程序隔离的漫游存储区。  下面的代码示例对此进行了演示。  
  
 [!code-cpp[Conceptual.IsolatedStorage#12](../../../samples/snippets/cpp/VS_Snippets_CLR/conceptual.isolatedstorage/cpp/source9.cpp#12)]
 [!code-csharp[Conceptual.IsolatedStorage#12](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.isolatedstorage/cs/source9.cs#12)]
 [!code-vb[Conceptual.IsolatedStorage#12](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.isolatedstorage/vb/source9.vb#12)]  
  
## 请参阅  
 <xref:System.IO.IsolatedStorage.IsolatedStorageScope>   
 [独立存储](../../../docs/standard/io/isolated-storage.md)