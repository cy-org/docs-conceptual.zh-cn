---
title: "&lt;PreferComInsteadOfManagedRemoting&gt; 元素 | Microsoft Docs"
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
  - "<PreferComInsteadOfManagedRemoting> 元素"
  - "PreferComInsteadOfManagedRemoting 元素"
ms.assetid: a279a42a-c415-4e79-88cf-64244ebda613
caps.latest.revision: 17
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 17
---
# &lt;PreferComInsteadOfManagedRemoting&gt; 元素
指定运行时是否将为跨应用程序域边界的所有调用使用 COM 互操作而不是远程处理。  
  
## 语法  
  
```  
<PreferComInsteadOfManagedRemoting enabled="true|false"/>  
```  
  
## 特性和元素  
 下列各节描述了特性、子元素和父元素。  
  
### 特性  
  
|特性|说明|  
|--------|--------|  
|`enabled`|必需的特性。<br /><br /> 指示运行时是否将跨应用程序域边界使用 COM 互操作而不是远程处理。|  
  
## enabled 特性  
  
|值|说明|  
|-------|--------|  
|`false`|运行时将跨应用程序域边界使用远程处理。  这是默认设置。|  
|`true`|运行时将跨应用程序域边界使用 COM 互操作。|  
  
### 子元素  
 无。  
  
### 父元素  
  
|元素|说明|  
|--------|--------|  
|`configuration`|公共语言运行时和 .NET Framework 应用程序所使用的每个配置文件中的根元素。|  
|`runtime`|包含有关程序集绑定和垃圾回收的信息。|  
  
## 备注  
 在将 `enabled` 特性设置为 `true` 时，运行时的行为如下所示：  
  
-   当[IUnknown](http://go.microsoft.com/fwlink/?LinkId=148003)接口通过 COM接口进入域时，运行时不会为[IManagedObject](../../../../../ocs/framework/unmanaged-api/hosting/imanagedobject-interface.md)接口调用[IUnknown::QueryInterface](http://go.microsoft.com/fwlink/?LinkID=144867)。  相反，运行时会围绕对象构建一个[运行时可调用包装](../../../../../docs/framework/interop/runtime-callable-wrapper.md) \(RCW\)。  
  
-   当运行时收到针对此域中已创建的任何 [COM 可调用包装](../../../../../docs/framework/interop/com-callable-wrapper.md) \(CCW\) 的 [IManagedObject](../../../../../ocs/framework/unmanaged-api/hosting/imanagedobject-interface.md) 接口的 `QueryInterface` 调用时，它会返回 E\_NOINTERFACE。  
  
 这两种行为可确保，针对跨应用程序域边界的托管对象之间的 COM 接口的所有调用都使用 COM 和 COM 互操作，而不是远程处理。  
  
## 示例  
 下面的示例演示如何指定运行时应跨隔离边界使用 COM 互操作：  
  
```  
<configuration>  
  <runtime>  
    <PreferComInsteadOfManagedRemoting enabled="true"/>  
  </runtime>  
</configuration>  
```  
  
## 请参阅  
 [运行时设置架构](../../../../../docs/framework/configure-apps/file-schema/runtime/index.md)   
 [配置文件架构](../../../../../docs/framework/configure-apps/file-schema/index.md)