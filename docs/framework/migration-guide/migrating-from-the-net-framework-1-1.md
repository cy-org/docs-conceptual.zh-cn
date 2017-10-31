---
title: "从 .NET Framework 1.1 迁移"
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
- .NET Framework 4.5, migrating from 1.1
- .NET Framework 1.1, migrating to .NET Framework 4.5
ms.assetid: 7ead0cb3-3b19-414a-8417-a1c1fa198d9e
caps.latest.revision: 12
author: rpetrusha
ms.author: ronpet
manager: wpickett
ms.translationtype: HT
ms.sourcegitcommit: 306c608dc7f97594ef6f72ae0f5aaba596c936e1
ms.openlocfilehash: 5757894a63ed556413147b8ef8c85c2d31ef11a5
ms.contentlocale: zh-cn
ms.lasthandoff: 07/28/2017

---
# <a name="migrating-from-the-net-framework-11"></a>从 .NET Framework 1.1 迁移
[!INCLUDE[win7](../../../includes/win7-md.md)] 及更高版本的 Windows 操作系统不支持 [!INCLUDE[net_v11_long](../../../includes/net-v11-long-md.md)]。 因此，面向 [!INCLUDE[net_v11_short](../../../includes/net-v11-short-md.md)] 的应用程序在未进行修改的情况下将不会在 [!INCLUDE[win7](../../../includes/win7-md.md)] 或更高版本的操作系统上运行。 本主题介绍了在 [!INCLUDE[win7](../../../includes/win7-md.md)] 及更高版本的 Windows 操作系统控制下运行定位 [!INCLUDE[net_v11_short](../../../includes/net-v11-short-md.md)] 的应用程序时需要执行的步骤。 有关 [!INCLUDE[net_v11_long](../../../includes/net-v11-long-md.md)] 和 [!INCLUDE[win8](../../../includes/win8-md.md)] 的详细信息，请参阅[在 Windows 8 及更高版本上运行 .NET Framework 1.1 应用程序](../../../docs/framework/install/run-net-framework-1-1-apps.md)。  
  
## <a name="retargeting-or-recompiling"></a>重定目标或重新编译  
 可通过两种方式让使用 [!INCLUDE[net_v11_short](../../../includes/net-v11-short-md.md)] 编译的应用程序在 [!INCLUDE[win7](../../../includes/win7-md.md)] 或更高版本的 Windows 操作系统上运行：  
  
-   可以将应用程序的目标重定为在 [!INCLUDE[net_v40_long](../../../includes/net-v40-long-md.md)] 下运行。 若要重定目标，必须在应用程序配置文件中添加允许应用程序在 [!INCLUDE[net_v40_short](../../../includes/net-v40-short-md.md)] 控制下运行的 [\<supportedRuntime>](../../../docs/framework/configure-apps/file-schema/startup/supportedruntime-element.md) 元素。 此配置文件采用以下形式：  
  
    ```xml  
    <configuration>   
       <startup>  
          <supportedRuntime version="v4.0"/>  
       </startup>  
    </configuration>  
    ```  
  
-   可以使用面向 [!INCLUDE[net_v40_short](../../../includes/net-v40-short-md.md)]的编译器重新编译应用程序。 如果您最初使用 Visual Studio 2003 开发和编译解决方案，则可在 [!INCLUDE[vs_dev10_long](../../../includes/vs-dev10-long-md.md)] 中打开它，然后使用 **“项目兼容性”** 对话框将该解决方案和项目文件从 Visual Studio 2003 使用的格式转换为 [!INCLUDE[vs_dev10_long](../../../includes/vs-dev10-long-md.md)]使用的 Microsoft Build Engine (MSBuild) 格式。  
  
 无论您是想重新编译应用程序还是重定应用程序的目标，都必须确定应用程序是否会受更高版本的 .NET Framework 中引入的任何更改的影响。 这些更改分为两类：  
  
-   [!INCLUDE[net_v11_short](../../../includes/net-v11-short-md.md)] 和更高版本的 .NET Framework 之间存在的重大更改。  
  
-   [!INCLUDE[net_v11_short](../../../includes/net-v11-short-md.md)] 和更高版本的 .NET Framework 之间的已标记为弃用或过时的类型和类型成员。  
  
 无论您重定应用程序的目标还是重新编译应用程序，都应查看 [!INCLUDE[net_v11_short](../../../includes/net-v11-short-md.md)]之后发布的各个版本的 .NET Framework 的重大更改和已过时类型和成员。  
  
## <a name="breaking-changes"></a>重大更改  
 发生重大更改时，解决方法可能对重定目标的应用程序和重新编译的应用程序都可用，这取决于具体的更改。 在某些情况下，可以在应用程序配置文件的 [\<runtime>](../../../docs/framework/configure-apps/file-schema/startup/supportedruntime-element.md) 元素中添加子元素，从而还原旧行为。 例如，下面的配置文件将还原 [!INCLUDE[net_v11_short](../../../includes/net-v11-short-md.md)] 中使用的字符串排序和比较行为，可以将该文件与重定目标的应用程序或重新编译的应用程序一起使用。  
  
```xml  
<configuration>  
   <runtime>  
      <CompatSortNLSVersion enabled="4096"/>  
   </runtime>  
</configuration>  
```  
  
 但某些情况下，您可能必须修改源代码和重新编译应用程序。  
  
 若要评估重大更改对应用程序产生的影响，您必须查看以下更改列表：  
  
-   [.NET Framework 2.0 中的重大更改](http://go.microsoft.com/fwlink/?LinkId=125263) 记录了 [!INCLUDE[net_v20SP1_short](../../../includes/net-v20sp1-short-md.md)] 中会影响面向 [!INCLUDE[net_v11_short](../../../includes/net-v11-short-md.md)]的应用程序的更改。  
  
-   [.NET Framework 3.5 SP1 中的更改](http://go.microsoft.com/fwlink/?LinkID=186989) 记录了 [!INCLUDE[net_v35_short](../../../includes/net-v35-short-md.md)] 和 [!INCLUDE[net_v35SP1_short](../../../includes/net-v35sp1-short-md.md)]之间的更改。  
  
-   [.NET Framework 4 迁移问题](../../../docs/framework/migration-guide/net-framework-4-migration-issues.md)记录了 [!INCLUDE[net_v35SP1_short](../../../includes/net-v35sp1-short-md.md)] 和 [!INCLUDE[net_v40_short](../../../includes/net-v40-short-md.md)] 之间的更改。  
  
## <a name="obsolete-types-and-members"></a>已过时的类型和成员  
 弃用的类型和成员对重定目标的应用程序和重新编译的应用程序产生的影响略有不同。 使用已过时的类型和成员将不会影响重定目标的应用程序，除非已从其程序集中物理删除这些过时的类型或成员。 重新编译使用过时的类型或成员的应用程序通常会产生编译器警告而不是编译器错误。 但某些情况下会产生编译器错误，且无法成功编译使用过时的类型或成员的代码。 在此情况下，你必须先重新编写调用过时的类型或成员的源代码，然后再重新编译应用程序。 若要详细了解已过时类型和成员，请参阅[类库中过时的内容](../../../docs/framework/whats-new/whats-obsolete.md)。  
  
 若要评估自发布 [!INCLUDE[net_v20SP1_short](../../../includes/net-v20sp1-short-md.md)] 后弃用的类型和成员的影响，请参阅[类库中过时的内容](../../../docs/framework/whats-new/whats-obsolete.md)。 查看 [!INCLUDE[net_v20SP1_short](../../../includes/net-v20sp1-short-md.md)]、[!INCLUDE[net_v35_short](../../../includes/net-v35-short-md.md)] 和 [!INCLUDE[net_v40_short](../../../includes/net-v40-short-md.md)] 的过时类型和成员的列表。

