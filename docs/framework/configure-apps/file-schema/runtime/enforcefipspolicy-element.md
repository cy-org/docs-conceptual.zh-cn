---
title: "&lt;enforceFIPSPolicy&gt; 元素 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
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
  - "<enforceFIPSPolicy> 元素"
  - "enforceFIPSPolicy 元素"
  - "美国联邦信息处理标准 (FIPS)"
  - "FIPS"
ms.assetid: c35509c4-35cf-43c0-bb47-75e4208aa24e
caps.latest.revision: 7
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 7
---
# &lt;enforceFIPSPolicy&gt; 元素
指定是否启用计算机配置要求的强制执行，使加密算法必须符合美国联邦信息处理标准 \(FIPS\)。  
  
## 语法  
  
```  
<enforceFIPSPolicy enabled="true|false" />  
```  
  
## 特性和元素  
 以下几节描述了特性、子元素和父元素。  
  
### 特性  
  
|特性|说明|  
|--------|--------|  
|enabled|必需的特性。<br /><br /> 指定是否启用计算机配置要求的强制执行，使加密算法必须符合 FIPS。|  
  
## enabled 特性  
  
|值|说明|  
|-------|--------|  
|`true`|如果您的计算机配置为需要与 FIPS 兼容的加密算法，则将强制实施此要求。  如果类实现一种不符合 FIPS 的算法，构造函数或类的 `Create` 方法在计算机运行时会引发异常。  这是默认值。|  
|`false`|无论计算机的配置如何，被应用程序所使用的加密算法无需符合 FIPS。|  
  
### 子元素  
 无。  
  
### 父元素  
  
|元素|说明|  
|--------|--------|  
|`configuration`|公共语言运行时和 .NET Framework 应用程序所使用的每个配置文件中的根元素。|  
|`runtime`|包含有关程序集绑定和垃圾回收的信息。|  
  
## 备注  
 以.NET Framework 2.0开始，实现加密算法的类的创建被受控于计算机的配置。  如果计算机配置为算法需要符合 FIPS，并且类实现了一个与 FIPS 不兼容的算法，则任何创建该类的实例的尝试将引发异常。  构造函数引发 <xref:System.InvalidOperationException> 异常，`Create` 方法引发 <xref:System.Reflection.TargetInvocationException> 异常和内部 <xref:System.InvalidOperationException> 异常。  
  
 如果应用程序运行在其配置需要符合 FIPS 的计算机上，并且应用程序使用与 FIPS 不兼容的算法，则您可使用配置文件中的元素防止公共语言运行时 \(CLR\) 强制实施 FIPS 兼容性。  此元素在 [!INCLUDE[net_v20SP1_long](../../../../../includes/net-v20sp1-long-md.md)] 中引进。  
  
## 示例  
 以下示例显示了如何保护 CLR 免于 FIPS 的强制符合。  
  
```  
<configuration>  
    <runtime>  
        <enforceFIPSPolicy enabled="false"/>  
    </runtime>  
</configuration>  
```  
  
## 请参阅  
 [运行时设置架构](../../../../../docs/framework/configure-apps/file-schema/runtime/index.md)   
 [配置文件架构](../../../../../docs/framework/configure-apps/file-schema/index.md)   
 [加密模型](../../../../../docs/standard/security/cryptography-model.md)