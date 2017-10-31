---
title: "方法 ETW 事件"
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
- ETW, method events (CLR)
- method events [.NET Framework]
ms.assetid: 167a4459-bb6e-476c-9046-7920880f2bb5
caps.latest.revision: 9
author: mairaw
ms.author: mairaw
manager: wpickett
ms.translationtype: HT
ms.sourcegitcommit: 306c608dc7f97594ef6f72ae0f5aaba596c936e1
ms.openlocfilehash: 353ae034381ab29787aba1c1c362f4c6fc57da7e
ms.contentlocale: zh-cn
ms.lasthandoff: 08/21/2017

---
# <a name="method-etw-events"></a>方法 ETW 事件
<a name="top"></a> 这些事件收集特定于方法的信息。 符号解析需要这些事件的负载。 此外，这些事件还提供如调用方法的次数等有用信息。  
  
 所有方法事件都具有“信息性 (4)”级别。 所有方法的详细事件都具有“详细级别 (5)”级别。  
  
 所有方法事件都是由运行时提供程序下的 `JITKeyword` (0x10) 关键字或 `NGenKeyword` (0x20) 关键字引发的，或是由断开提供程序下的 `JitRundownKeyword` (0x10) 或 `NGENRundownKeyword` (0x20) 引发的。  
  
 CLR 方法事件进一步细分为以下几类：  
  
-   [CLR 方法事件](#clr_method_events)  
  
-   [CLR 方法标记事件](#clr_method_marker_events)  
  
-   [CLR 方法详细事件](#clr_method_verbose_events)  
  
-   [MethodJittingStarted 事件](#methodjittingstarted_event)  
  
<a name="clr_method_events"></a>   
## <a name="clr-method-events"></a>CLR 方法事件  
 下表显示了关键字和级别。 （有关详细信息，请参阅 [CLR ETW Keywords and Levels](../../../docs/framework/performance/clr-etw-keywords-and-levels.md)。）  
  
|引发事件的关键字|级别|  
|-----------------------------------|-----------|  
|`JITKeyword` (0x10) 运行时提供程序|信息性 (4)|  
|`NGenKeyword` (0x20) 运行时提供程序|信息性 (4)|  
|`JitRundownKeyword` (0x10) 断开提供程序|信息性 (4)|  
|`NGENRundownKeyword` (0x20) 断开提供程序|信息性 (4)|  
  
 下表显示了事件信息。  
  
|Event|事件 ID|描述|  
|-----------|--------------|-----------------|  
|`MethodLoad_V1`|136|在实时加载（JIT 加载）方法或者加载 NGEN 映像时引发。 动态和泛型方法不使用此版本进行方法加载。 JIT 帮助器从不使用此版本。|  
|`MethodUnLoad_V1`|137|在卸载模块或销毁应用程序域时引发。 动态方法从不使用此版本进行方法卸载。|  
|`MethodDCStart_V1`|137|启动断开期间的枚举方法。|  
|`MethodDCEnd_V1`|138|结束断开期间的枚举方法。|  
  
 下表显示了事件数据。  
  
|字段名|数据类型|描述|  
|----------------|---------------|-----------------|  
|MethodID|win:UInt64|方法的唯一标识符。 对于 JIT 帮助器方法，将设置为该方法的起始地址。|  
|ModuleID|win:UInt64|此方法所属的模块标识符（0 表示 JIT 帮助器）。|  
|MethodStartAddress|win:UInt64|方法的起始地址。|  
|MethodSize|win:UInt32|方法的大小。|  
|MethodToken|win:UInt32|0 代表动态方法和 JIT 帮助器。|  
|MethodFlags|win:UInt32|0x1：动态方法。<br /><br /> 0x2：泛型方法。<br /><br /> 0x4：JIT 编译的代码方法（否则为 NGEN 本机映像代码）。<br /><br /> 0x8：帮助器方法。|  
|ClrInstanceID|win:UInt16|CLR 或 CoreCLR 的实例的唯一 ID。|  
  
 [返回页首](#top)  
  
<a name="clr_method_marker_events"></a>   
## <a name="clr-method-marker-events"></a>CLR 方法标记事件  
 仅在断开提供程序中会引发这些事件。 它们表示在启动或结束断开期间方法枚举的结束。 （即，启用 `NGENRundownKeyword`、 `JitRundownKeyword`、 `LoaderRundownKeyword`或 `AppDomainResourceManagementRundownKeyword` 关键字时引发。）  
  
 下表显示了关键字和级别。  
  
|引发事件的关键字|级别|  
|-----------------------------------|-----------|  
|`AppDomainResourceManagementRundownKeyword` (0x800) 断开提供程序|信息性 (4)|  
|`JitRundownKeyword` (0x10) 断开提供程序|信息性 (4)|  
|`NGENRundownKeyword` (0x20) 断开提供程序|信息性 (4)|  
  
 下表显示了事件信息。  
  
|Event|事件 ID|说明|  
|-----------|--------------|----------------|  
|`DCStartInit_V1`|147|启动断开期间枚举开始之前发送。|  
|`DCStartComplete_V1`|145|启动断开期间枚举结束时发送。|  
|`DCEndInit_V1`|148|结束断开期间枚举开始之前发送。|  
|`DCEndComplete_V1`|146|结束断开期间枚举结束时发送。|  
  
 下表显示了事件数据。  
  
|字段名|数据类型|描述|  
|----------------|---------------|-----------------|  
|ClrInstanceID|win:UInt16|CLR 或 CoreCLR 的实例的唯一 ID。|  
  
 [返回页首](#top)  
  
<a name="clr_method_verbose_events"></a>   
## <a name="clr-method-verbose-events"></a>CLR 方法详细事件  
 下表显示了关键字和级别。  
  
|引发事件的关键字|级别|  
|-----------------------------------|-----------|  
|`JITKeyword` (0x10) 运行时提供程序|详细级别 (5)|  
|`NGenKeyword` (0x20) 运行时提供程序|详细级别 (5)|  
|`JitRundownKeyword` (0x10) 断开提供程序|详细级别 (5)|  
|`NGENRundownKeyword` (0x20) 断开提供程序|详细级别 (5)|  
  
 下表显示了事件信息。  
  
|Event|事件 ID|描述|  
|-----------|--------------|-----------------|  
|`MethodLoadVerbose_V1`|143|当方法为 JIT 加载的或加载 NGEN 映像时引发。 动态和泛型方法始终使用此版本进行方法加载。 JIT 帮助器始终使用此版本。|  
|`MethodUnLoadVerbose_V1`|144|在销毁动态方法、卸载模块或销毁应用程序域时引发。 动态方法始终使用此版本进行方法卸载。|  
|`MethodDCStartVerbose_V1`|141|启动断开期间的枚举方法。|  
|`MethodDCEndVerbose_V1`|142|结束断开期间的枚举方法。|  
  
 下表显示了事件数据。  
  
|字段名|数据类型|描述|  
|----------------|---------------|-----------------|  
|MethodID|win:UInt64|方法的唯一标识符。 对于 JIT 帮助器方法，将设置为该方法的起始地址。|  
|ModuleID|win:UInt64|此方法所属的模块标识符（0 表示 JIT 帮助器）。|  
|MethodStartAddress|win:UInt64|起始地址。|  
|MethodSize|win:UInt32|方法长度。|  
|MethodToken|win:UInt32|0 代表动态方法和 JIT 帮助器。|  
|MethodFlags|win:UInt32|0x1：动态方法。<br /><br /> 0x2：泛型方法。<br /><br /> 0x4：JIT 编译的方法（否则由 NGen.exe 生成）<br /><br /> 0x8：帮助器方法。|  
|MethodNameSpace|win:UnicodeString|与该方法关联的完整命名空间名称。|  
|MethodName|win:UnicodeString|与该方法关联的完整类名称。|  
|MethodSignature|win:UnicodeString|方法的签名（以逗号分隔的类型名称列表）。|  
|ClrInstanceID|win:UInt16|CLR 或 CoreCLR 的实例的唯一 ID。|  
  
 [返回页首](#top)  
  
<a name="methodjittingstarted_event"></a>   
## <a name="methodjittingstarted-event"></a>MethodJittingStarted 事件  
 下表显示了关键字和级别。  
  
|引发事件的关键字|级别|  
|-----------------------------------|-----------|  
|`JITKeyword` (0x10) 运行时提供程序|详细级别 (5)|  
|`NGenKeyword` (0x20) 运行时提供程序|详细级别 (5)|  
|`JitRundownKeyword` (0x10) 断开提供程序|详细级别 (5)|  
|`NGENRundownKeyword` (0x20) 断开提供程序|详细级别 (5)|  
  
 下表显示了事件信息。  
  
|Event|事件 ID|描述|  
|-----------|--------------|-----------------|  
|`MethodJittingStarted`|145|在方法由 JIT 编译时引发。|  
  
 下表显示了事件数据。  
  
|字段名|数据类型|描述|  
|----------------|---------------|-----------------|  
|MethodID|win:UInt64|方法的唯一标识符。|  
|ModuleID|win:UInt64|此方法所属的模块标识符。|  
|MethodToken|win:UInt32|0 代表动态方法和 JIT 帮助器。|  
|MethodILSize|win:UInt32|JIT 编译的方法的 Microsoft 中间语言 (MSIL) 的大小。|  
|MethodNameSpace|win:UnicodeString|与该方法关联的完整类名称。|  
|MethodName|win:UnicodeString|方法的名称。|  
|MethodSignature|win:UnicodeString|方法的签名（以逗号分隔的类型名称列表）。|  
|ClrInstanceID|win:UInt16|CLR 或 CoreCLR 的实例的唯一 ID。|  
  
## <a name="see-also"></a>另请参阅  
 [CLR ETW 事件](../../../docs/framework/performance/clr-etw-events.md)

