---
title: "&lt;configuration&gt; 的 &lt;assemblyBinding&gt; 元素 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "http://schemas.microsoft.com/.NetConfiguration/v2.0#configuration/assemblyBinding"
dev_langs: 
  - "VB"
  - "CSharp"
  - "C++"
  - "jsharp"
helpviewer_keywords: 
  - "<assemblyBinding> 元素"
  - "assemblyBinding 元素"
ms.assetid: 6cc55983-b894-449b-8e26-b258e53939cd
caps.latest.revision: 6
author: "mcleblanc"
ms.author: "markl"
manager: "markl"
caps.handback.revision: 6
---
# &lt;configuration&gt; 的 &lt;assemblyBinding&gt; 元素
指定配置级的程序集绑定策略。  
  
## 语法  
  
```  
<assemblyBinding    
   xmlns="urn:schemas-microsoft-com:asm.v1">  
</assemblyBinding>  
```  
  
## 特性和元素  
 以下几节描述了特性、子元素和父元素。  
  
### 特性  
  
|特性|说明|  
|--------|--------|  
|`xmlns`|必需的特性。<br /><br /> 指定程序集绑定所需的 XML 命名空间。  使用字符串“urn:schemas\-microsoft\-com:asm.v1”作为值。|  
  
### 子元素  
  
|元素|说明|  
|--------|--------|  
|[\<linkedConfiguration\> 元素](../../../../docs/framework/configure-apps/file-schema/linkedconfiguration-element.md)|指定要包含的配置文件。|  
  
### 父元素  
  
|元素|说明|  
|--------|--------|  
|[\<configuration\> 元素](../../../../docs/framework/configure-apps/file-schema/configuration-element.md)|公共语言运行时和 .NET Framework 应用程序所使用的每个配置文件中的根元素。|  
  
## 备注  
 [\<linkedConfiguration\> 元素](../../../../docs/framework/configure-apps/file-schema/linkedconfiguration-element.md) 允许应用程序配置文件包含已知位置的程序集配置文件，而不是复制程序集配置设置，从而简化了组件程序集的管理。  
  
> [!NOTE]
>  具有 Windows 并行清单的应用程序不支持 `<linkedConfiguration>` 元素。  
  
## 示例  
 下面的代码示例演示如何包含本地硬盘上的配置文件。  
  
```  
<configuration>  
   <assemblyBinding xmlns="urn:schemas-microsoft-com:asm.v1">  
      <linkedConfiguration href="file://c:\Program Files\Contoso\sharedConfig.xml"/>  
   </assemblyBinding>  
</configuration>  
```  
  
## 请参阅  
 [配置文件架构](../../../../docs/framework/configure-apps/file-schema/index.md)