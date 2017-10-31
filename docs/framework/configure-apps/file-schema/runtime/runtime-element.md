---
title: "&lt;runtime&gt; 元素 | Microsoft Docs"
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
  - "http://schemas.microsoft.com/.NetConfiguration/v2.0#runtime"
  - "http://schemas.microsoft.com/.NetConfiguration/v2.0#configuration/runtime"
dev_langs: 
  - "VB"
  - "CSharp"
  - "C++"
  - "jsharp"
helpviewer_keywords: 
  - "<runtime> 元素"
  - "容器标记, <runtime> 元素"
  - "runtime 元素"
ms.assetid: 1eb2fae3-de4b-45b6-852f-517c39b751bd
caps.latest.revision: 70
author: "mcleblanc"
ms.author: "markl"
manager: "markl"
caps.handback.revision: 62
---
# &lt;runtime&gt; 元素
包含有关程序集绑定和垃圾回收的信息。  
  
## 语法  
  
```  
<runtime>  
</runtime>  
```  
  
## 特性和元素  
 下列各节描述了特性、子元素和父元素。  
  
### 特性  
 无。  
  
### 子元素  
  
|元素|说明|  
|--------|--------|  
|[\<alwaysFlowImpersonationPolicy\>](../../../../../docs/framework/configure-apps/file-schema/runtime/alwaysflowimpersonationpolicy-element.md)|指定无论模拟是如何执行的，Windows 标识始终流经异步点。|  
|[\<appDomainManagerAssembly\>](../../../../../docs/framework/configure-apps/file-schema/runtime/appdomainmanagerassembly-element.md)|指定用于为进程内的默认应用程序域提供应用程序域管理器的程序集。|  
|[\<appDomainManagerType\>](../../../../../docs/framework/configure-apps/file-schema/runtime/appdomainmanagertype-element.md)|指定用作默认应用程序域的应用程序域管理器的类型。|  
|[\<appDomainResourceMonitoring\>](../../../../../docs/framework/configure-apps/file-schema/runtime/appdomainresourcemonitoring-element.md)|指示运行时在进程的生存期内收集有关进程中所有应用程序域的统计信息。|  
|[\<assemblyBinding\>](../../../../../docs/framework/configure-apps/file-schema/runtime/assemblybinding-element-for-runtime.md)|包含有关程序集版本重定向和程序集位置的信息。|  
|[\<bypassTrustedAppStrongNames\>](../../../../../docs/framework/configure-apps/file-schema/runtime/bypasstrustedappstrongnames-element.md)|指定是否应跳过对受信任程序集的强名称验证。|  
|[\<CompatSortNLSVersion\>](../../../../../docs/framework/configure-apps/file-schema/runtime/compatsortnlsversion-element.md)|指定在执行字符串比较时，运行时应使用旧式的排序行为。|  
|[\<developmentMode\>](../../../../../docs/framework/configure-apps/file-schema/runtime/developmentmode-element.md)|指定运行时是否在 DEVPATH 环境变量指定的目录中搜索程序集。|  
|[\<disableCachingBindingFailures\>](../../../../../docs/framework/configure-apps/file-schema/runtime/disablecachingbindingfailures-element.md)|指定是否禁用对绑定故障进行缓存，这是 .NET Framework 2.0 版中的默认行为。|  
|[\<disableCommitThreadStack\>](../../../../../docs/framework/configure-apps/file-schema/runtime/disablecommitthreadstack-element.md)|指定在线程启动时是否提交完整的线程堆栈。|  
|[\<disableFusionUpdatesFromADManager\>](../../../../../docs/framework/configure-apps/file-schema/runtime/disablefusionupdatesfromadmanager-element.md)|指定是否禁用默认行为，此行为允许运行时主机重写应用程序域的配置设置。|  
|[\<enforceFIPSPolicy\>](../../../../../docs/framework/configure-apps/file-schema/runtime/enforcefipspolicy-element.md)|指定是否启用计算机配置要求的强制执行，使加密算法必须符合美国联邦信息处理标准 \(FIPS\)。|  
|[\<etwEnable\>](../../../../../docs/framework/configure-apps/file-schema/runtime/etwenable-element.md)|指定是否为公共语言运行时事件启用 Windows 事件跟踪 \(ETW\)。|  
|[\<forcePerformanceCounterUniqueSharedMemoryReads\>](../../../../../docs/framework/configure-apps/file-schema/runtime/forceperformancecounteruniquesharedmemoryreads-element.md)|指定 PerfCounter.dll 是否在 .NET Framework 1.1 版本的应用程序中使用 CategoryOptions 注册表设置，以决定是否从特定于类别的共享内存或全局内存中加载性能计数器数据。|  
|[\<gcAllowVeryLargeObjects\>](../../../../../docs/framework/configure-apps/file-schema/runtime/gcallowverylargeobjects-element.md)|在64位平台上，可以允许总共大于2千兆字节的数组。|  
|[\<gcConcurrent\>](../../../../../docs/framework/configure-apps/file-schema/runtime/gcconcurrent-element.md)|指定公共语言运行时是否同时运行垃圾回收。|  
|[\<GCCpuGroup\>](../../../../../docs/framework/configure-apps/file-schema/runtime/gccpugroup-element.md)|指定垃圾回收是否支持多个 CPU 组。|  
|[\<gcServer\>](../../../../../docs/framework/configure-apps/file-schema/runtime/gcserver-element.md)|指定公共语言运行时是否运行服务器垃圾回收。|  
|[\<generatePublisherEvidence\>](../../../../../docs/framework/configure-apps/file-schema/runtime/generatepublisherevidence-element.md)|指定运行时是否使用代码访问安全性 \(CAS\) 发行者策略。|  
|[\<legacyCorruptedStateExceptionsPolicy\>](../../../../../docs/framework/configure-apps/file-schema/runtime/legacycorruptedstateexceptionspolicy-element.md)|指定运行时是否允许托管代码捕获访问冲突和其他损坏状态异常。|  
|[\<legacyImpersonationPolicy\>](../../../../../docs/framework/configure-apps/file-schema/runtime/legacyimpersonationpolicy-element.md)|指定无论当前线程上的执行上下文的流设置如何，Windows 标识都不流经异步点。|  
|[\<loadfromRemoteSources\>](../../../../../docs/framework/configure-apps/file-schema/runtime/loadfromremotesources-element.md)|指定是否将来自远程源的程序集作为完全信任的程序集进行加载。|  
|[\<NetFx40\_LegacySecurityPolicy\>](../../../../../docs/framework/configure-apps/file-schema/runtime/netfx40-legacysecuritypolicy-element.md)|指定运行时是否使用旧版代码访问安全性 \(CAS\) 策略。|  
|[\<NetFx40\_PInvokeStackResilience\>](../../../../../docs/framework/configure-apps/file-schema/runtime/netfx40-pinvokestackresilience-element.md)|指定运行时是否以降低托管和未托管代码之间的转换速度为代价，自动修复运行时上不正确的平台调用声明。|  
|[\<NetFx45\_CultureAwareComparerGetHashCode\_LongStrings\>](../../../../../docs/framework/configure-apps/file-schema/runtime/netfx45-cultureawarecomparergethashcode-longstrings-element.md)|Specifies whether the runtime uses a fixed amount of memory to calculate hash codes for the <xref:System.StringComparer.GetHashCode%2A?displayProperty=fullName> method.|  
|[\<PreferComInsteadOfRemoting\>](../../../../../docs/framework/configure-apps/file-schema/runtime/prefercominsteadofmanagedremoting-element.md)|指定运行时将跨应用程序域边界使用 COM 互操作而不是远程处理。|  
|[\<relativeBindForResources\>](../../../../../docs/framework/configure-apps/file-schema/runtime/relativebindforresources-element.md)|Optimizes the probe for satellite assemblies.|  
|[\<shadowCopyVerifyByTimeStamp\>](../../../../../docs/framework/configure-apps/file-schema/runtime/shadowcopyverifybytimestamp-element.md)|指定是否影像复制在 [!INCLUDE[net_v40_long](../../../../../includes/net-v40-long-md.md)] 中用引入的默认启动行为，或恢复为 .NET Framework 早期版本的启动行为。|  
|[\<supportPortability\>](../../../../../docs/framework/configure-apps/file-schema/runtime/supportportability-element.md)|指定应用程序可以在 .NET Framework 的两个不同实现中引用同一个程序集，方法为禁用默认行为，该默认行为因应用程序优先级目的将程序集处理为等同物。|  
|[\<system.runtime.caching\>](../../../../../docs/framework/configure-apps/file-schema/runtime/system-runtime-caching-element-cache-settings.md)|为默认内存中对象缓存提供配置信息。|  
|[\<Thread\_UseAllCpuGroups\>](../../../../../docs/framework/configure-apps/file-schema/runtime/thread-useallcpugroups-element.md)|指定运行时是否在所有的 CPU 组中分布托管的线程。|  
|[\<ThrowUnobservedTaskExceptions\>](../../../../../docs/framework/configure-apps/file-schema/runtime/throwunobservedtaskexceptions-element.md)|指定未经处理的任务异常是否应停止正在运行的进程。|  
|[\<TimeSpan\_LegacyFormatMode\>](../../../../../docs/framework/configure-apps/file-schema/runtime/runtime-element.md)|指定运行时是否对 <xref:System.TimeSpan> 值使用旧格式设置。|  
|[\<UseRandomizedStringHashAlgorithm\>](../../../../../docs/framework/configure-apps/file-schema/runtime/userandomizedstringhashalgorithm-element.md)|指定运行时是否在每个应用程序域基础上计算字符串的哈希代码。|  
|[\<UseSmallInternalThreadStacks\>](../../../../../docs/framework/configure-apps/file-schema/runtime/usesmallinternalthreadstacks-element.md)|请求运行时在创建其内部使用的某些线程时使用显式的堆栈大小，而非使用默认的堆栈大小。|  
  
### 父元素  
  
|元素|说明|  
|--------|--------|  
|`configuration`|公共语言运行时和 .NET Framework 应用程序所使用的每个配置文件中的根元素。|  
  
## 备注  
 在 .NET Framework 2.0 版中，模拟标识流经应用程序域中的异步点。  在 .NET Framework 2.0 版中，您可以启用或禁用模拟流经异步点，方法是在 machine.config 文件或应用程序配置文件中正确配置运行时元素。  For ASP.NET, the impersonation flow can be configured in the aspnet.config file found in the \<Windows Folder\>\\Microsoft.NET\\Framework\\vx.x.xxxx directory.  
  
 默认情况下，ASP.NET 使用以下配置设置在 aspnet.config 文件中禁用模拟流：  
  
```  
configuration>  
   <runtime>  
      <legacyImpersonationPolicy enabled="true"/>  
      <alwaysFlowImpersonationPolicy enabled="false"/>  
   </runtime>  
</configuration>  
```  
  
 在 ASP.NET 中，如果您要允许模拟流，您就必须显式使用以下配置设置：  
  
```  
<configuration>  
   <runtime>  
      <legacyImpersonationPolicy enabled="false"/>  
      <alwaysFlowImpersonationPolicy enabled="true"/>  
   </runtime>  
</configuration>  
```  
  
 有关更多信息，请参见[\<legacyImpersonationPolicy\> 元素](../../../../../docs/framework/configure-apps/file-schema/runtime/legacyimpersonationpolicy-element.md)和[\<alwaysFlowImpersonationPolicy\> 元素](../../../../../docs/framework/configure-apps/file-schema/runtime/alwaysflowimpersonationpolicy-element.md)。  
  
## 示例  
 下面的示例说明如何将一个程序集版本重定向到另一个版本。  
  
```  
<configuration>  
   <runtime>  
      <assemblyBinding xmlns="urn:schemas-microsoft-com:asm.v1">  
         <dependentAssembly>  
            <assemblyIdentity name="myAssembly"  
                              publicKeyToken="32ab4ba45e0a69a1"  
                              culture="neutral" />  
             <bindingRedirect oldVersion="1.0.0.0"  
                              newVersion="2.0.0.0"/>  
         </dependentAssembly>  
      </assemblyBinding>  
   </runtime>  
</configuration>  
```  
  
## 请参阅  
 [运行时设置架构](../../../../../docs/framework/configure-apps/file-schema/runtime/index.md)   
 [配置文件架构](../../../../../docs/framework/configure-apps/file-schema/index.md)   
 [重定向程序集版本](../../../../../docs/framework/configure-apps/redirect-assembly-versions.md)   
 [How to: Disable Concurrent Garbage Collection](http://msdn.microsoft.com/zh-cn/ba2c6c67-5778-497c-9fac-5f793b5500c7)