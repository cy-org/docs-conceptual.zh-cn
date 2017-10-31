---
title: "&lt;ThrowUnobservedTaskExceptions&gt; 元素 | Microsoft Docs"
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
  - "<ThrowUnobservedTaskExceptions> 元素"
  - "ThrowUnobservedTaskExceptions 元素"
ms.assetid: cea7e588-8b8d-48d2-9ad5-8feaf3642c18
caps.latest.revision: 6
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 6
---
# &lt;ThrowUnobservedTaskExceptions&gt; 元素
指定未经处理的任务异常是否应停止正在运行的进程。  
  
## 语法  
  
```vb  
<ThrowUnobservedTaskExceptions  
   enabled="true|false"/>  
```  
  
## 特性和元素  
 下列各节描述了特性、子元素和父元素。  
  
### 特性  
  
|特性|说明|  
|--------|--------|  
|`enabled`|必需的特性。<br /><br /> 指定未经处理的任务异常是否应停止正在运行的进程。|  
  
## enabled 特性  
  
|值|说明|  
|-------|--------|  
|`false`|不会终止一个未经处理的任务异常的进程的运行。  这是默认设置。|  
|`true`|终止一个正在运行的未经处理任务异常的进程。|  
  
### 子元素  
 无。  
  
### 父元素  
  
|元素|说明|  
|--------|--------|  
|`configuration`|公共语言运行时和 .NET Framework 应用程序所使用的每个配置文件中的根元素。|  
|`runtime`|包含关于运行时初始化选项的信息。|  
|||  
  
## 备注  
 如果与 <xref:System.Threading.Tasks.Task> 相关的异常未观察，没有 <xref:System.Threading.Tasks.Task.Wait%2A> 操作，父未附加，并且，则 <xref:System.Threading.Tasks.Task.Exception%2A?displayProperty=fullName> 属性未读取任务异常视为未观察到的。  
  
 在 [!INCLUDE[net_v40_long](../../../../../includes/net-v40-long-md.md)]中，默认情况下，如果有未观察到的异常的<xref:System.Threading.Tasks.Task>是回收的垃圾，终结器引发异常并终止进程。  进程终止依赖垃圾回收和终止计时。  
  
 若要使开发人员可以轻松地基于任务编写异步代码，[!INCLUDE[net_v45](../../../../../includes/net-v45-md.md)]更改未观察异常的默认行为。  未观察到的异常将导致引发 <xref:System.Threading.Tasks.TaskScheduler.UnobservedTaskException> 事件，但是，默认情况下，进程不终止。  相反，无论事件处理程序是否观察异常，在引发事件后异常被忽略。  
  
 在 [!INCLUDE[net_v45](../../../../../includes/net-v45-md.md)]中，在应用程序配置文件可以使用 [\<ThrowUnobservedTaskExceptions\> 元素](../../../../../docs/framework/configure-apps/file-schema/runtime/throwunobservedtaskexceptions-element.md) 启用 [!INCLUDE[net_v40_short](../../../../../includes/net-v40-short-md.md)] 引发异常的行为。  
  
 可以采用以下方式之一中指定异常行为：  
  
-   通过设置 `COMPlus_ThrowUnobservedTaskExceptions` \(`set COMPlus_ThrowUnobservedTaskExceptions=1`环境变量。  
  
-   在HKEY\_LOCAL\_MACHINE\\SOFTWARE\\Microsoft\\.NETFramework 键中，通过设置注册表 ThrowUnobservedTaskExceptions DWORD 值 \= 1。  
  
## 示例  
 下面的示例演示如何使用应用程序配置文件来启用任务中引发的异常。。  
  
```  
<configuration>   
    <runtime>   
        <ThrowUnobservedTaskExceptions enabled="true"/>   
    </runtime>   
</configuration>  
  
```  
  
## 示例  
 下面的示例演示一个未观察到的异常如何从任务引发。  代码必须作为一个发布的程序来运行来工作正常。  
  
 [!code-csharp[ThrowUnobservedTaskExceptions#1](../../../../../samples/snippets/csharp/VS_Snippets_CLR/throwunobservedtaskexceptions/cs/program.cs#1)]
 [!code-vb[ThrowUnobservedTaskExceptions#1](../../../../../samples/snippets/visualbasic/VS_Snippets_CLR/throwunobservedtaskexceptions/vb/program.vb#1)]  
  
## 请参阅  
 [运行时设置架构](../../../../../docs/framework/configure-apps/file-schema/runtime/index.md)   
 [配置文件架构](../../../../../docs/framework/configure-apps/file-schema/index.md)