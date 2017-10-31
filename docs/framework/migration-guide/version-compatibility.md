---
title: ".NET Framework 的版本兼容性"
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
- .NET Framework, version compatibility
- .NET Framework 4.5, compatibility with earlier versions
- .NET Framework versions, compatibility
ms.assetid: 2f25e522-456a-48c3-8a53-e5f39275649f
caps.latest.revision: 35
author: rpetrusha
ms.author: ronpet
manager: wpickett
ms.translationtype: HT
ms.sourcegitcommit: 306c608dc7f97594ef6f72ae0f5aaba596c936e1
ms.openlocfilehash: 741c2d1c49f44a6a7b299845cdc37cc8425c326b
ms.contentlocale: zh-cn
ms.lasthandoff: 07/28/2017

---
# <a name="version-compatibility-in-the-net-framework"></a>.NET Framework 的版本兼容性
向后兼容性表示为某个平台的特定版本开发的应用程序将在该平台的更高版本上运行。 .NET Framework 尝试最大程度地支持向后兼容性：为某个版本的 .NET Framework 编写的源代码应在更高版本的 .NET Framework 上编译，而在某个版本的 .NET Framework 上运行的二进制文件的行为方式应与其在更高版本的 .NET Framework 上的行为方式相同。  
  
<a name="Apps"></a>   
## <a name="version-compatibility-for-apps"></a>应用程序的版本兼容性  
 默认情况下，应用将在其目标 .NET Framework 版本上运行。 如果该版本不存在且应用程序配置文件未定义支持的版本，则可能出现 .NET Framework 初始化错误。 在此情况下，尝试运行应用程序将失败。  
  
 若要定义运行应用的特定版本，请将一个或多个 [\<supportedRuntime>](../../../docs/framework/configure-apps/file-schema/startup/supportedruntime-element.md) 元素添加到应用的配置文件中。 每个 `<supportedRuntime>` 元素都列出了支持的运行时版本，第一个元素指定了优先级最高的版本，最后一个元素指定了优先级最低的版本。  
  
```xml  
<configuration>  
   <startup>  
      <supportedRuntime version="v2.0.50727" />  
      <supportedRuntime version="v4.0" />  
   </startup>  
</configuration>  
```  
  
 有关详细信息，请参阅[如何：配置应用以支持 .NET Framework 4 或 4.x](../../../docs/framework/migration-guide/how-to-configure-an-app-to-support-net-framework-4-or-4-5.md)。  
  
## <a name="version-compatibility-for-components"></a>组件的版本兼容性  
 应用程序可控制运行它的 .NET Framework 版本，但组件不能。 由于组件和类库在特定应用的上下文中加载，因此它们会自动在运行应用的 .NET Framework 版本上运行。  
  
 由于存在此限制，因此兼容性保证对组件特别重要。 从 .NET Framework 4 开始，你可以通过将 <xref:System.Runtime.Versioning.ComponentGuaranteesAttribute?displayProperty=fullName> 特性应用于某个组件，来指定希望该组件与多个版本的兼容程度。 工具可使用此特性来检测组件的将来版本中的兼容性保证的潜在冲突。  
  
## <a name="backward-compatibility-and-the-net-framework-45"></a>向后兼容性和 .NET Framework 4.5  
 .NET Framework 4.5 及其单点版本（4.5.1、4.5.2、4.6、4.6.1、4.6.2 和 4.7）与使用早期版本的 .NET Framework 生成的应用向后兼容。 换句话说，使用早期版本的 .NET Framework 生成的应用程序和组件将运行，而无需在 .NET Framework 4.5 上进行修改。 但在默认情况下，应用程序在其进行开发的公共语言运行时版本上运行，因此你必须提供配置文件，使应用程序能在 .NET Framework 4.5 上运行。 有关详细信息，请参阅本文前面的[应用的版本兼容性](#Apps)一节。  
  
 实际上，.NET Framework 中看似无关紧要的更改和编程技术上的更改会损坏此兼容性。 例如，.NET Framework 4.5 中的性能改进会公开早期版本中未出现的争用条件。 同样，使用 .NET Framework 程序集的硬编码路径，执行与特定版本的 .NET Framework 的相等比较，以及使用反射获取私有字段的值都不是向后兼容的做法。 此外，每个版本的 .NET Framework 都包含 Bug 修复和可能影响某些应用程序和组件的兼容性的安全相关更改。  
  
 如果应用和组件在 .NET Framework 4.5（包括其单点版本，即 [!INCLUDE[net_v451](../../../includes/net-v451-md.md)]、4.5.2、4.6、4.6.1、4.6.2 或 4.7）上未按预期运行，请使用以下清单：  
  
-   检查这些主题以了解可能影响应用程序的任何更改并采用描述的解决方法：  
  
    -   [.NET Framework 4 迁移问题](../../../docs/framework/migration-guide/net-framework-4-migration-issues.md)  
  
    -   [4.5 中的应用程序兼容性](../../../docs/framework/migration-guide/application-compatibility-in-the-net-framework-4-5.md)  
  
    -   [4.5.1 中的应用程序兼容性](../../../docs/framework/migration-guide/application-compatibility-in-the-net-framework-4-5-1.md)  
  
    -   [4.5.2 中的应用程序兼容性](../../../docs/framework/migration-guide/application-compatibility-in-the-net-framework-4-5-2.md)  
  
    -   [4.6 中的应用程序兼容性](../../../docs/framework/migration-guide/application-compatibility-in-the-net-framework-4-6.md)  
  
    -   [4.6.1 中的应用程序兼容性](../../../docs/framework/migration-guide/application-compatibility-in-the-net-framework-4-6-1.md)  
  
    -   [4.6.2 中的应用程序兼容性](../../../docs/framework/migration-guide/application-compatibility-in-the-net-framework-4-6-2.md)  

    - [4.7 中的应用程序兼容性](../../../docs/framework/migration-guide/application-compatibility-in-the-net-framework-4-6-2.md)
       
-   如果拥有 .NET Framework 1.1 应用程序，也请查看这些主题：  
  
    -   [.NET Framework 2.0 中的更改](http://go.microsoft.com/fwlink/?LinkID=125263)  
  
    -   [.NET Framework 3.5 SP1 中的更改](http://go.microsoft.com/fwlink/?LinkId=186989)  
  
-   如果要重新编译现有源代码以在 .NET Framework 4.5 或其单点版本上运行，或者要从现有源代码库开发面向 [!INCLUDE[net_v45](../../../includes/net-v45-md.md)] 的新版本的应用或组件，请查看[类库中过时的内容](../../../docs/framework/whats-new/whats-obsolete.md)以了解过时的类型和成员，并采用描述的解决方法。 （以前编译的代码将继续针对已标记为过时的类型和成员运行。）  
  
-   如果确定 [!INCLUDE[net_v45](../../../includes/net-v45-md.md)] 中的更改损坏了应用，请检查[运行时设置架构](../../../docs/framework/configure-apps/file-schema/runtime/index.md)，确定是否能在应用的配置文件中使用运行时设置来还原以前的行为。  
  
-   如果遇到未记录的问题，请记录 [Microsoft Connect](http://go.microsoft.com/fwlink/?LinkID=154815) Bug，然后以电子邮件的形式将 Bug 号发送到 [netfxcf@microsoft.com](mailto:netfxcf@microsoft.com)。  
  
## <a name="compatibility-and-side-by-side-execution"></a>兼容性和并行执行  
 如果找不到解决问题的适当方法，请记住，.NET Framework 4.5（或其中一个单点版本）是与版本 1.1、2.0 和 3.5 并行运行的，并且是取代版本 4 的就地更新。 对于以版本 1.1、2.0 和 3.5 为目标的应用程序，你可以在目标计算机上安装适当的 .NET Framework 版本以在其最佳环境中运行该应用程序。 有关并行执行的详细信息，请参阅[并行执行](../../../docs/framework/deployment/side-by-side-execution.md)。  
  
## <a name="see-also"></a>另请参阅  
 [新增功能](../../../docs/framework/whats-new/index.md)   
 [类库中过时的内容](../../../docs/framework/whats-new/whats-obsolete.md)   
 [应用程序兼容性](../../../docs/framework/migration-guide/application-compatibility.md)   
 [Microsoft .NET Framework 支持生命周期策略](http://go.microsoft.com/fwlink/p/?LinkId=248212)   
 [.NET Framework 4 迁移问题](../../../docs/framework/migration-guide/net-framework-4-migration-issues.md)

