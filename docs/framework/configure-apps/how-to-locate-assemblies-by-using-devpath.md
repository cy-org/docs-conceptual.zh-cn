---
title: "如何：使用 DEVPATH 查找程序集 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "VB"
  - "CSharp"
  - "C++"
  - "jsharp"
helpviewer_keywords: 
  - ".NET Framework 应用程序配置, 程序集"
  - "app.config 文件, 程序集位置"
  - "应用程序配置文件, 指定程序集的位置"
  - "程序集 [.NET Framework], 位置"
  - "DEVPATH"
  - "查找程序集"
ms.assetid: 44d2eadf-7eec-443c-a2ac-d601fd919e17
caps.latest.revision: 8
author: "mcleblanc"
ms.author: "markl"
manager: "markl"
caps.handback.revision: 8
---
# 如何：使用 DEVPATH 查找程序集
开发人员可能想确保他们正在生成的共享程序集能与多个应用程序一起正常使用。  在开发周期内开发人员不用频繁地将程序集放在全局程序集缓存中，他们可以创建 DEVPATH 环境变量，让该变量指向程序集的生成输出目录。  
  
 例如，假设您正在生成名为 MySharedAssembly 的共享程序集，且输出目录是 C:\\MySharedAssembly\\Debug。  可以将 C:\\MySharedAssembly\\Debug 置于 DEVPATH 变量中。  必须在机器配置文件中指定 [\<developmentMode\>](../../../docs/framework/configure-apps/file-schema/runtime/developmentmode-element.md)元素。  该元素告诉公共语言运行时使用 DEVPATH 来查找程序集。  
  
 共享程序集必须能够由运行时发现。若要指定用于解析程序集引用的私有目录，请在配置文件中使用 [\<codeBase\> 元素](../../../docs/framework/configure-apps/file-schema/runtime/codebase-element.md) 或 [\<probing\> 元素](../../../docs/framework/configure-apps/file-schema/runtime/probing-element.md)，如 [指定程序集的位置](../../../docs/framework/configure-apps/specify-assembly-location.md) 中所述。还可以将程序集放在应用程序目录的子目录中。  有关详细信息，请参阅[运行时如何定位程序集](../../../docs/framework/deployment/how-the-runtime-locates-assemblies.md)。  
  
> [!NOTE]
>  这是一项高级功能，只应用于开发。  
  
 下面的示例说明如何使运行时在由 DEVPATH 环境变量所指定的目录中搜索程序集。  
  
## 示例  
  
```  
<configuration>  
  <runtime>  
    <developmentMode developerInstallation="true"/>  
  </runtime>  
</configuration>  
```  
  
 该设置默认为假。  
  
> [!NOTE]
>  仅在开发时使用此设置。  运行时不检查在 DEVPATH 中找到的具有强名称的程序集的版本。  它只是使用所找到的第一个程序集。  
  
## 请参阅  
 [Configuring .NET Framework Apps](http://msdn.microsoft.com/zh-cn/d789b592-fcb5-4e3d-8ac9-e0299adaaa42)