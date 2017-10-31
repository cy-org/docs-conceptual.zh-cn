---
title: "&lt;requiredRuntime&gt; 元素 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "http://schemas.microsoft.com/.NetConfiguration/v2.0#requiredRuntime"
  - "http://schemas.microsoft.com/.NetConfiguration/v2.0#configuration/startup/requiredRuntime"
dev_langs: 
  - "VB"
  - "CSharp"
  - "C++"
  - "jsharp"
helpviewer_keywords: 
  - "<requiredRuntime> 元素"
  - "容器标记, <requiredRuntime> 元素"
  - "requiredRuntime 元素"
ms.assetid: 9fa1639e-beb8-43be-b7a4-12f7b229c34b
caps.latest.revision: 11
author: "mcleblanc"
ms.author: "markl"
manager: "markl"
caps.handback.revision: 11
---
# &lt;requiredRuntime&gt; 元素
指定应用程序仅支持公共语言运行时 1.0 版。  
  
## 语法  
  
```  
  
   <requiredRuntime    
version="runtime version"  
safemode="true|false"/>  
```  
  
## 特性和元素  
 以下几节描述了特性、子元素和父元素。  
  
### 特性  
  
|特性|说明|  
|--------|--------|  
|`version`|可选特性。<br /><br /> 一个字符串值，它指定此应用程序支持的 .NET Framework 版本。  字符串值必须与位于 .NET Framework 安装根目录下的目录名称匹配。  不分析字符串值的内容。|  
|`safemode`|可选特性。<br /><br /> 指定运行时启动代码是否搜索注册表以确定运行时版本。|  
  
## 安全模式特性  
  
|值|说明|  
|-------|--------|  
|`false`|运行时启动代码在注册表中搜索。  这是默认值。|  
|`true`|运行时启动代码不在注册表中搜索。|  
  
### 子元素  
 无。  
  
### 父元素  
  
|元素|说明|  
|--------|--------|  
|`configuration`|公共语言运行时和 .NET Framework 应用程序所使用的每个配置文件中的根元素。|  
|`startup`|包含 `<requiredRuntime>` 元素。|  
  
## 备注  
 仅为支持运行时 1.0 版而生成的应用程序必须使用 `<requiredRuntime>` 元素。  使用运行时的版本 1.1 或更高版本生成的应用程序必须使用 `<supportedRuntime>` 元素。  
  
> [!NOTE]
>  如果使用 [CorBindToRuntimeByCfg](../../../../../ocs/framework/unmanaged-api/hosting/corbindtoruntimebycfg-function.md) 函数来指定配置文件，则必须使用适用于运行时的所有版本的 `<requiredRuntime>` 元素。  当您使用 [CorBindToRuntimeByCfg](../../../../../ocs/framework/unmanaged-api/hosting/corbindtoruntimebycfg-function.md) 时，`<supportedRuntime>` 元素将被忽略。  
  
 `version` 特性字符串必须与指定的 .NET Framework 版本的安装文件夹名称匹配。  不解释此字符串。  如果运行时启动代码找不到匹配的文件夹，则不加载运行时；启动代码显示错误信息并退出。  
  
> [!NOTE]
>  Microsoft Internet Explorer 中承载的应用程序的启动代码忽略 `<requiredRuntime>` 元素。  
  
## 示例  
 下面的示例说明如何在配置文件中指定运行时版本。  
  
```  
<configuration>  
   <startup>  
      <requiredRuntime version="v1.0.3705" safemode="true"/>  
   </startup>  
</configuration>  
```  
  
## 请参阅  
 [启动设置架构](../../../../../docs/framework/configure-apps/file-schema/startup/index.md)   
 [配置文件架构](../../../../../docs/framework/configure-apps/file-schema/index.md)   
 [\<PaveOver\> Specifying Which Runtime Version to Use](http://msdn.microsoft.com/zh-cn/c376208d-980d-42b4-865b-fbe0d9cc97c2)