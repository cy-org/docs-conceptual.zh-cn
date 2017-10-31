---
title: "如何：创建发行者策略 | Microsoft Docs"
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
  - "GAC（全局程序集缓存）, 发行者策略程序集"
  - "全局程序集缓存, 发行者策略程序集"
  - "发行者策略程序集"
  - "发行者策略文件"
ms.assetid: 8046bc5d-2fa9-4277-8a5e-6dcc96c281d9
caps.latest.revision: 15
author: "mcleblanc"
ms.author: "markl"
manager: "markl"
caps.handback.revision: 15
---
# 如何：创建发行者策略
程序集的供应商会通过将发行者策略文件与升级的程序集包括在一起，声明应用程序应使用较新版本的程序集。  发行者策略文件指定程序集重定向和基本代码设置，并使用与应用程序配置文件相同的格式。  发行者策略文件被编译到某个程序集中，并放置在全局程序集缓存中。  
  
 创建发行者策略涉及以下三个步骤：  
  
1.  创建发行者策略文件。  
  
2.  创建发行者策略程序集。  
  
3.  将发行者策略程序集添加到全局程序集缓存中。  
  
 在[重定向程序集版本](../../../docs/framework/configure-apps/redirect-assembly-versions.md)中对发行者策略的架构进行了描述。  下面的示例说明了一个发行者策略文件，该文件将 `myAssembly` 的一个版本重定向到另一个版本。  
  
```  
<configuration>  
   <runtime>  
      <assemblyBinding xmlns="urn:schemas-microsoft-com:asm.v1">  
       <dependentAssembly>  
         <assemblyIdentity name="myAssembly"  
                           publicKeyToken="32ab4ba45e0a69a1"  
                           culture="en-us" />  
         <!-- Redirecting to version 2.0.0.0 of the assembly. -->  
         <bindingRedirect oldVersion="1.0.0.0"  
                          newVersion="2.0.0.0"/>  
       </dependentAssembly>  
      </assemblyBinding>  
   </runtime>  
</configuration>  
```  
  
 若要了解如何指定基本代码，请参见[指定程序集的位置](../../../docs/framework/configure-apps/specify-assembly-location.md)。  
  
## 创建发行者策略程序集  
 使用[程序集链接器 \(Al.exe\)](../../../docs/framework/tools/al-exe-assembly-linker.md) 创建发行者策略程序集。  
  
#### 创建发行者策略程序集  
  
1.  在命令提示处键入以下命令：  
  
     **al \/link:** *publisherPolicyFile* **\/out:** *publisherPolicyAssemblyFile* **\/keyfile:** *keyPairFile* **\/platform:** *processorArchitecture*  
  
     在此命令中：  
  
    -   *publisherPolicyFile* 参数是发行者策略文件的名称。  
  
    -   *publisherPolicyAssemblyFile* 参数是该命令所生成的发行者策略程序集的名称。  程序集文件名必须遵循以下格式：  
  
         **policy.** *majorNumber* **.** *minorNumber* **.** *mainAssemblyName* **.dll**  
  
    -   *keyPairFile* 参数是包含密钥对的文件的名称。  必须用同一密钥对对程序集和发行者策略程序集进行签名。  
  
    -   *processorArchitecture* 参数标识特定于处理器的程序集的目标平台。  
  
        > [!NOTE]
        >  以特定处理器结构为目标的功能是 .NET Framework version 2.0 中的新增功能。  
  
     下面的命令从名为 `pub.config` 的发行者策略文件创建名为 `policy.1.0.myAssembly` 的发行者策略程序集，用 `sgKey.snk` 文件中的密钥对为该程序集分配一个强名称，并指定该程序集以 x86 处理器结构为目标。  
  
    ```  
    al /link:pub.config /out:policy.1.0.myAssembly.dll /keyfile:sgKey.snk /platform:x86  
    ```  
  
     发行者策略程序集必须与其所适用的程序集的处理器结构相匹配。  因此，如果程序集具有 <xref:System.Reflection.ProcessorArchitecture> 的 <xref:System.Reflection.AssemblyName.ProcessorArchitecture%2A> 值，则必须使用 `/platform:anycpu` 创建针对该程序集的发行者策略程序集。  必须为每个特定于处理器的程序集提供一个单独的发行者策略程序集。  
  
     该规则所产生的一个结果是，为了更改程序集的处理器结构，必须更改主版本号或次版本号部分，以便可以提供具有正确处理器结构的新发行者策略程序集。  如果程序集具有不同的处理器结构，旧的发行者策略程序集则无法处理该程序集。  
  
     另一个结果是，2.0 版链接器无法用于创建使用较早版本的 .NET Framework 编译的程序集的发行者策略程序集，因为它始终指定处理器结构。  
  
## 将发行者策略程序集添加到全局程序集缓存中  
 使用[全局程序集缓存工具 \(Gacutil.exe\)](../../../docs/framework/tools/gacutil-exe-gac-tool.md) 将发行者策略程序集添加到全局程序集缓存中。  
  
#### 将发行者策略程序集添加到全局程序集缓存中  
  
1.  在命令提示处键入以下命令：  
  
     **gacutil \/i**  *publisherPolicyAssemblyFile*  
  
     下面的命令将 `policy.1.0.myAssembly.dll` 添加到全局程序集缓存中。  
  
    ```  
    gacutil /i policy.1.0.myAssembly.dll  
    ```  
  
    > [!IMPORTANT]
    >  仅当原始发行者策略文件与程序集位于同一目录中时，才能将发行者策略程序集添加到全局程序集缓存中。  
  
## 请参阅  
 [使用程序集编程](../../../docs/framework/app-domains/programming-with-assemblies.md)   
 [运行时如何定位程序集](../../../docs/framework/deployment/how-the-runtime-locates-assemblies.md)   
 [配置应用](../../../docs/framework/configure-apps/index.md)   
 [Configuring .NET Framework Apps](http://msdn.microsoft.com/zh-cn/d789b592-fcb5-4e3d-8ac9-e0299adaaa42)   
 [运行时设置架构](../../../docs/framework/configure-apps/file-schema/runtime/index.md)   
 [配置文件架构](../../../docs/framework/configure-apps/file-schema/index.md)   
 [重定向程序集版本](../../../docs/framework/configure-apps/redirect-assembly-versions.md)