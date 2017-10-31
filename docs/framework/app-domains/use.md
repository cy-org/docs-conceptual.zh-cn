---
title: "使用应用程序域"
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
- application domains, about
- common language runtime, application domains
- runtime, application domains
ms.assetid: c6d99815-e022-4d2c-9420-1d7ab5b9d504
caps.latest.revision: 15
author: rpetrusha
ms.author: ronpet
manager: wpickett
ms.translationtype: HT
ms.sourcegitcommit: 306c608dc7f97594ef6f72ae0f5aaba596c936e1
ms.openlocfilehash: b2dac2238ae9117d3678335748c680d594a8b5c6
ms.contentlocale: zh-cn
ms.lasthandoff: 07/28/2017

---
# <a name="using-application-domains"></a>使用应用程序域
应用程序域为公共语言运行时提供隔离单元。 它们在进程中创建和运行。 应用程序域通常由运行时主机创建，运行时主机是一种应用程序，负责向进程加载运行时，并在应用程序域内执行用户代码。 运行时主机创建进程和默认应用程序域，并在其中运行托管代码。 运行时主机包括 ASP.NET、Microsoft Internet Explorer 和 Windows Shell。  
  
 对大多数应用程序而言，你无需创建自己的应用程序域，运行时主机将为你创建任何所需的应用程序域。 但是，如果应用程序需要隔离代码或使用和卸载 DLL，则可以创建和配置额外的应用程序域。  
  
## <a name="in-this-section"></a>本节内容  
 [如何：创建应用程序域](../../../docs/framework/app-domains/how-to-create-an-application-domain.md)  
 说明如何以编程方式创建应用程序域。  
  
 [如何：卸载应用程序域](../../../docs/framework/app-domains/how-to-unload-an-application-domain.md)  
 说明如何以编程方式卸载应用程序域。  
  
 [如何：配置应用程序域](../../../docs/framework/app-domains/how-to-configure-an-application-domain.md)  
 提供关于配置应用程序域的简介。  
  
 [从应用程序域中检索安装信息](../../../docs/framework/app-domains/retrieve-setup-information.md)  
 说明如何从应用程序域检索安装信息。  
  
 [如何：将程序集加载到应用程序域中](../../../docs/framework/app-domains/how-to-load-assemblies-into-an-application-domain.md)  
 说明如何将程序集加载到应用程序域中。  
  
 [如何：从程序集获取类型和成员信息](../../../docs/framework/app-domains/how-to-obtain-type-and-member-information-from-an-assembly.md)  
 说明如何检索关于程序集的信息。  
  
 [卷影复制程序集](../../../docs/framework/app-domains/shadow-copy-assemblies.md)  
 说明卷影复制如何允许对正在使用的程序集进行更新，以及如何配置卷影复制。  
  
 [如何：接收最可能的异常通知](../../../docs/framework/app-domains/how-to-receive-first-chance-exception-notifications.md)  
 说明在公共语言运行时开始搜索异常处理程序之前，可如何接收已引发异常的通知。  
  
 [解析程序集加载](../../../docs/framework/app-domains/resolve-assembly-loads.md)  
 提供有关使用 <xref:System.AppDomain.AssemblyResolve?displayProperty=fullName> 事件处理程序集加载故障的指导。  
  
## <a name="reference"></a>参考  
 <xref:System.AppDomain>  
 表示应用程序域。 提供用于创建和控制应用程序域的方法。  
  
## <a name="related-sections"></a>相关章节  
 [Assemblies in the Common Language Runtime](../../../docs/framework/app-domains/assemblies-in-the-common-language-runtime.md)（公共语言运行时中的程序集）  
 概述程序集执行的功能。  
  
 [使用程序集编程](../../../docs/framework/app-domains/programming-with-assemblies.md)  
 描述如何在程序集上创建、签署和设置特性。  
  
 [发出动态方法和程序集](../../../docs/framework/reflection-and-codedom/emitting-dynamic-methods-and-assemblies.md)  
 描述如何创建动态程序集。  
  
 [应用程序域](../../../docs/framework/app-domains/application-domains.md)  
 提供应用程序域的概念性概述。  
  
 [反射概述](../../../docs/framework/reflection-and-codedom/reflection.md)  
 介绍了如何使用 **Reflection** 类获取程序集的信息。

