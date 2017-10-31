---
title: "发出动态方法和程序集"
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
- reflection emit
- dynamic assemblies
- metadata, emit interfaces
- reflection emit, overview
- assemblies [.NET Framework], emitting dynamic assemblies
ms.assetid: 8e8e2631-62fd-40e7-a8ee-0039b06749bc
caps.latest.revision: 18
author: rpetrusha
ms.author: ronpet
manager: wpickett
ms.translationtype: HT
ms.sourcegitcommit: 306c608dc7f97594ef6f72ae0f5aaba596c936e1
ms.openlocfilehash: c28a5b71a93ea5159adc73316771d490dbe0db87
ms.contentlocale: zh-cn
ms.lasthandoff: 07/28/2017

---
# <a name="emitting-dynamic-methods-and-assemblies"></a>发出动态方法和程序集
本节介绍 <xref:System.Reflection.Emit> 命名空间中的一组托管类型，它们允许编译器或工具在运行时发出元数据和 Microsoft 中间语言 (MSIL)，并在磁盘上生成可移植可执行 (PE) 文件（可选）。 脚本引擎和编译器是此命名空间的主要使用者。 在本节中，<xref:System.Reflection.Emit> 命名空间提供的功能被称为反射发出。  
  
 反射发出具有以下功能：  
  
-   在运行时定义轻量全局方法（使用 <xref:System.Reflection.Emit.DynamicMethod> 类）并通过委托执行这些方法。  
  
-   在运行时定义程序集，然后运行程序集以及/或者将程序集保存到磁盘。  
  
-   在运行时定义程序集，运行程序集，然后卸载程序集并允许垃圾回收回收其资源。  
  
-   在运行时在新的程序集中定义模块，然后运行模块以及/或者将模块保存到磁盘。  
  
-   在运行时在模块中定义类型，创建这些类型的实例并调用其方法。  
  
-   为已定义模块定义可供工具（如调试器和代码探查器）使用的符号化信息。  
  
 除了 <xref:System.Reflection.Emit> 命名空间中的托管类型，还有非托管元数据接口，非托管元数据接口在[元数据接口](../../../docs/framework/unmanaged-api/metadata/metadata-interfaces.md)参考文档中介绍。 托管的反射发出提供比非托管元数据接口更强的语义错误检查和更高级别的元数据抽象。  
  
 元数据和 MSIL 的另一个有用资源是《公共语言基础结构 (CLI)》文档，尤其是“第二部分：元数据定义和语义”和“第三部分: CIL 指令集”。 该文档可在 [MSDN](http://go.microsoft.com/fwlink/?LinkID=65555) 和 [Ecma 网站](http://go.microsoft.com/fwlink/?LinkId=116487)上联机获取。  
  
## <a name="in-this-section"></a>本节内容  
 [反射发出中的安全问题](../../../docs/framework/reflection-and-codedom/security-issues-in-reflection-emit.md)  
 介绍与使用反射发出创建动态程序集相关的安全问题。  
  
## <a name="reference"></a>参考  
 <xref:System.Reflection.Emit.OpCodes>  
 编录可用于生成方法体的 MSIL 指令代码。  
  
 <xref:System.Reflection.Emit>  
 包含用于发出动态方法、程序集和类型的托管类。  
  
 <xref:System.Type>  
 介绍 <xref:System.Type> 类，该类代表托管反射和反射发出中的类型，它是使用这些技术的关键。  
  
 <xref:System.Reflection>  
 包含用于浏览元数据和托管代码的托管类。  
  
## <a name="related-sections"></a>相关章节  
 [反射](../../../docs/framework/reflection-and-codedom/reflection.md)  
 说明如何浏览元数据和托管代码。  
  
 [Assemblies in the Common Language Runtime](../../../docs/framework/app-domains/assemblies-in-the-common-language-runtime.md)（公共语言运行时中的程序集）  
 概述 .NET Framework 中的程序集。

