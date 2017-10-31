---
title: "指定程序集的位置 | Microsoft Docs"
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
  - "应用程序配置 [.NET Framework]"
  - "程序集 [.NET Framework], 指定位置"
  - "配置 [.NET Framework], 应用程序"
ms.assetid: 1cb92bd7-6bab-44cf-8fd3-36303ce84fea
caps.latest.revision: 8
author: "mcleblanc"
ms.author: "markl"
manager: "markl"
caps.handback.revision: 8
---
# 指定程序集的位置
有两种方法用来指定程序集的位置：  
  
-   使用 [\<codeBase\>](../../../docs/framework/configure-apps/file-schema/runtime/codebase-element.md) 元素  
  
-   使用 [\<probing\>](../../../docs/framework/configure-apps/file-schema/runtime/probing-element.md)元素  
  
 还可以使用 [.NET Framework 配置工具 \(Mscorcfg.msc\)](http://msdn.microsoft.com/zh-cn/a7106c52-68da-490e-b129-971b2c743764) 来指定程序集位置或者为公共语言运行时指定要探测程序集的位置。  
  
## 使用 \<codeBase\> 元素  
 只有在计算机配置文件或重定向程序集版本的发行者策略文件中，才可以使用**\<codeBase\>**元素。  在运行时确定要使用哪一程序集版本时，它应用确定版本的文件中的基本代码设置。  如果未指出基本代码，那么运行时就以通常的方法探测程序集。  有关详细信息，请参见[运行时如何定位程序集](../../../docs/framework/deployment/how-the-runtime-locates-assemblies.md)。  
  
 下面的示例说明如何指定程序集的位置。  
  
```  
<configuration>  
   <runtime>  
      <assemblyBinding xmlns="urn:schemas-microsoft-com:asm.v1">  
       <dependentAssembly>  
         <assemblyIdentity name="myAssembly"  
                           publicKeyToken="32ab4ba45e0a69a1"  
                           culture="en-us" />  
         <codeBase version="2.0.0.0"  
                   href="http://www.litwareinc.com/myAssembly.dll"/>  
       </dependentAssembly>  
      </assemblyBinding>  
   </runtime>  
</configuration>  
```  
  
 对于所有具有强名称的程序集，要求 **version** 特性，但对于不具有强名称的程序集应省略。  **\<codeBase\>** 元素要求**href**特性。  在**\<codeBase\>**元素中不能指定版本范围。  
  
> [!NOTE]
>  如果为不具有强名称的程序集提供基本代码提示，那么该提示必须指向应用程序基或该应用程序基目录的子目录。  
  
## 使用\<probing\>元素  
 运行时通过探测的方法来查找没有基本代码的程序集。  有关探测的更多信息，请参见[运行时如何定位程序集](../../../docs/framework/deployment/how-the-runtime-locates-assemblies.md)。  
  
 可以在应用程序配置文件中使用[\<probing\>](../../../docs/framework/configure-apps/file-schema/runtime/probing-element.md)元素，来指定在查找程序集时运行时应搜索的子目录。  下面的示例说明如何指定运行时应搜索的目录。  
  
```  
<configuration>  
   <runtime>  
      <assemblyBinding xmlns="urn:schemas-microsoft-com:asm.v1">  
         <probing privatePath="bin;bin2\subbin;bin3"/>  
      </assemblyBinding>  
   </runtime>  
</configuration>  
```  
  
 **privatePath** 特性包含运行时应在其中搜索程序集的目录。  如果应用程序位于 C:\\Program Files\\MyApp，那么运行时将在 C:\\Program Files\\MyApp\\Bin、C:\\Program Files\\MyApp\\Bin2\\Subbin 和 C:\\Program Files\\MyApp\\Bin3 中查找未指定基本代码的程序集。  **privatePath** 中指定的目录必须是应用程序基目录的子目录。  
  
## 请参阅  
 [公共语言运行时中的程序集](../../../docs/framework/app-domains/assemblies-in-the-common-language-runtime.md)   
 [使用程序集编程](../../../docs/framework/app-domains/programming-with-assemblies.md)   
 [运行时如何定位程序集](../../../docs/framework/deployment/how-the-runtime-locates-assemblies.md)   
 [Configuring .NET Framework Apps](http://msdn.microsoft.com/zh-cn/d789b592-fcb5-4e3d-8ac9-e0299adaaa42)