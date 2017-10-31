---
title: "使用应用程序域和程序集编程"
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
- assemblies [.NET Framework], programming
- programming assemblies
- application domains, programming
- programming application domains
ms.assetid: 96d3b8e3-bef8-4da0-9a81-9841e23a94e9
caps.latest.revision: 11
author: rpetrusha
ms.author: ronpet
manager: wpickett
ms.translationtype: HT
ms.sourcegitcommit: 306c608dc7f97594ef6f72ae0f5aaba596c936e1
ms.openlocfilehash: 6dcf8e4c9bf2401309b1d80d2306bd619b96460d
ms.contentlocale: zh-cn
ms.lasthandoff: 09/05/2017

---
# <a name="programming-with-application-domains-and-assemblies"></a>使用应用程序域和程序集编程
Microsoft Internet Explorer、ASP.NET 和 Windows Shell 等主机将公共语言运行时加载到进程中，在相应进程中创建[应用程序域](../../../docs/framework/app-domains/application-domains.md)，然后在 .NET Framework 应用程序运行时加载并执行相应应用程序域中的用户代码。 在大多数情况下，不必担心创建应用程序域和将程序集加载到这些域中，因为运行时主机会执行这些任务。  
  
 不过，如果要创建将托管公共语言运行时的应用程序、要创建以编程方式卸载的工具/代码或要创建可以动态卸载和重载的可插入组件，需要创建自己的应用程序域。 即使不要创建运行时主机，也可以参阅本部分，其中介绍了有关如何使用应用程序域和这些应用程序域中加载的程序集的重要信息。  
  
## <a name="in-this-section"></a>本节内容  
 [应用程序域和程序集用法主题](../../../docs/framework/app-domains/application-domains-and-assemblies-how-to-topics.md)  
 收录了使用应用程序域和程序集进行编程的相关概念性文档中的所有用法主题链接。  
  
 [使用应用程序域](../../../docs/framework/app-domains/use.md)  
 举例说明了如何创建、配置和使用应用程序域。  
  
 [使用程序集编程](../../../docs/framework/app-domains/programming-with-assemblies.md)  
 描述如何在程序集上创建、签署和设置特性。  
  
## <a name="related-sections"></a>相关章节  
 [发出动态方法和程序集](../../../docs/framework/reflection-and-codedom/emitting-dynamic-methods-and-assemblies.md)  
 描述如何创建动态程序集。  
  
 [Assemblies in the Common Language Runtime](../../../docs/framework/app-domains/assemblies-in-the-common-language-runtime.md)（公共语言运行时中的程序集）  
 提供程序集的概念性概述。  
  
 [应用程序域](../../../docs/framework/app-domains/application-domains.md)  
 提供应用程序域的概念性概述。  
  
 [反射概述](../../../docs/framework/reflection-and-codedom/reflection.md)  
 介绍了如何使用 **Reflection** 类获取程序集的信息。

