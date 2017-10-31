---
title: "使用程序集编程"
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
ms.assetid: 25918b15-701d-42c7-95fc-c290d08648d6
caps.latest.revision: 18
author: rpetrusha
ms.author: ronpet
manager: wpickett
ms.translationtype: HT
ms.sourcegitcommit: 306c608dc7f97594ef6f72ae0f5aaba596c936e1
ms.openlocfilehash: 368021062a3ad49d2c63f92797c59b8c0f1cddfc
ms.contentlocale: zh-cn
ms.lasthandoff: 07/28/2017

---
# <a name="programming-with-assemblies"></a>使用程序集编程
程序集是 .NET Framework 的构造块；它们构成了部署、版本控制、重复使用、激活范围和安全权限的基本单元。 程序集向公共语言运行时提供了解类型实现所需要的信息。 程序集是为协同工作而生成的类型和资源的集合，这些类型和资源构成了一个逻辑功能单元。 对于运行时，类型不存在于程序集上下文之外。  
  
 本节说明如何创建模块、根据模块创建程序集、创建密钥对并使用强名称为程序集签名，以及如何将程序集安装到全局程序集缓存中。 此外，本节还说明如何使用 [MSIL 反汇编程序 (Ildasm.exe)](../../../docs/framework/tools/ildasm-exe-il-disassembler.md) 查看程序集清单信息。  
  
> [!NOTE]
>  从 .NET Framework 2.0 版开始，对于使用版本号高于当前已加载运行时的 .NET Framework 版本所编译的程序集，运行时将不再加载此类程序集。 这同样适用于主版本号和次版本号的组合。  
  
## <a name="in-this-section"></a>本节内容  
 [创建程序集](../../../docs/framework/app-domains/create-assemblies.md)  
 提供单个文件和多文件程序集的概述。  
  
 [程序集名称](../../../docs/framework/app-domains/assembly-names.md)  
 提供程序集命名的概述。  
  
 [如何：确定程序集的完全限定的名称](../../../docs/framework/app-domains/how-to-determine-assembly-fully-qualified-name.md)  
 介绍如何确定程序集的完全限定的名称。  
  
 [以完全信任的形式运行 Intranet 应用程序](../../../docs/framework/app-domains/running-intranet-applications-in-full-trust.md)  
 介绍如何为 Intranet 共享上的完全信任程序集指定旧安全策略。  
  
 [程序集位置](../../../docs/framework/app-domains/assembly-location.md)  
 提供查找程序集的概述。  
  
 [如何：生成单文件程序集](../../../docs/framework/app-domains/how-to-build-a-single-file-assembly.md)  
 介绍如何创建包含一个文件的程序集。  
  
 [多文件程序集](../../../docs/framework/app-domains/multifile-assemblies.md)  
 描述创建多文件程序集的原因。  
  
 [如何：生成多文件程序集](../../../docs/framework/app-domains/how-to-build-a-multifile-assembly.md)  
 介绍如何创建多文件程序集。  
  
 [设置程序集特性](../../../docs/framework/app-domains/set-assembly-attributes.md)  
 介绍程序集属性及其设置方法。  
  
 [创建和使用具有强名称的程序集](../../../docs/framework/app-domains/create-and-use-strong-named-assemblies.md)  
 说明使用强名称为程序集进行签名的方法和原因，包括操作指南主题。  
  
 [延迟签发程序集](../../../docs/framework/app-domains/delay-sign-assembly.md)  
 介绍如何对程序集执行延迟签名。  
  
 [使用程序集和全局程序集缓存](../../../docs/framework/app-domains/working-with-assemblies-and-the-gac.md)  
 说明将程序集添加到全局程序集缓存的方法和原因，包括操作指南主题。  
  
 [如何：查看程序集内容](../../../docs/framework/app-domains/how-to-view-assembly-contents.md)  
 介绍如何使用 MSIL 反汇编程序 (Ildasm.exe) 查看程序集内容。  
  
 [公共语言运行时中的类型转发](../../../docs/framework/app-domains/type-forwarding-in-the-common-language-runtime.md)  
 介绍如何在不中断现有应用程序的情况下使用类型转发将类型移动到其他程序集。  
  
## <a name="reference"></a>参考  
 <xref:System.Reflection.Assembly>  
 表示程序集的 .NET Framework 类。  
  
## <a name="related-sections"></a>相关章节  
 [如何：从程序集获取类型和成员信息](../../../docs/framework/app-domains/how-to-obtain-type-and-member-information-from-an-assembly.md)  
 介绍如何以编程方式从程序集获得类型和其他信息。  
  
 [Assemblies in the Common Language Runtime](../../../docs/framework/app-domains/assemblies-in-the-common-language-runtime.md)（公共语言运行时中的程序集）  
 提供公共语言运行时程序集的概念性概述。  
  
 [程序集版本控制](../../../docs/framework/app-domains/assembly-versioning.md)  
 提供程序集绑定以及 <xref:System.Reflection.AssemblyVersionAttribute> 和 <xref:System.Reflection.AssemblyInformationalVersionAttribute> 属性的概述。  
  
 [运行时如何定位程序集](../../../docs/framework/deployment/how-the-runtime-locates-assemblies.md)  
 说明运行时如何确定将用于满足绑定请求的程序集。  
  
 [反射](../../../docs/framework/reflection-and-codedom/reflection.md)  
 介绍了如何使用 **Reflection** 类获取程序集的信息。

