---
title: "使用托管调试助手诊断错误"
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology:
- dotnet-clr
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- EHMDA
dev_langs:
- VB
- CSharp
- C++
- jsharp
helpviewer_keywords:
- run-time error debugging
- managed code, run-time debugging
- resource debugging
- registry, MDAs
- common language runtime, debugging
- MDAs (managed debugging assistants)
- configuration files [.NET Framework], debugging runtime events
- messages, managed debugging assistants
- application configuration files, managed debugging assistants
- debugging [.NET Framework], managed debugging assistants
- environment variables, MDAs
- access violation debugging [.NET Framework]
- diagnostics, managed debugging assistants
- unmanaged code, run-time debugging
- default debug output stream
- memory, debugging
- app.config files, managed debugging assistants
- managed debugging assistants (MDAs)
- debugging [.NET Framework], run-time errors
- trapping events
- runtime, error debugging
- disabling MDAs
- output, managed debugging assistants
- errors [.NET Framework], managed debugging assistants
ms.assetid: 76994ee6-9fa9-4059-b813-26578d24427c
caps.latest.revision: 63
author: mairaw
ms.author: mairaw
manager: wpickett
ms.translationtype: HT
ms.sourcegitcommit: 306c608dc7f97594ef6f72ae0f5aaba596c936e1
ms.openlocfilehash: 8afc1ec3d5a1dab4412b16826bb32829f9b42263
ms.contentlocale: zh-cn
ms.lasthandoff: 08/21/2017

---
# <a name="diagnosing-errors-with-managed-debugging-assistants"></a>使用托管调试助手诊断错误
托管调试助手 (MDA) 是调试辅助程序，它与公共语言运行时 (CLR) 一起工作以提供关于运行时状态的信息。 这些助手可生成关于你无法通过其他方式捕获的运行时事件的信息性消息。 可以使用 MDA 隔离在托管代码和非托管代码之间转换时发生的、难以发现的应用程序 Bug。 可通过向 Windows 注册表添加注册表项或设置环境变量，启用或禁用所有的 MDA。 可使用应用程序配置设置来启用特定的 MDA。 可以在应用程序的配置文件中为某些单独的 MDA 设置其他配置设置。 由于将在加载运行时后分析这些配置文件，因此必须在托管应用程序启动之前启用 MDA。 不能为已经启动的应用程序启用 MDA。  
  
> [!NOTE]
>  启用 MDA 后，即使不在调试器下执行代码，MDA 也会处于活动状态。 如果在调试器不存在时引发 MDA 事件，尽管这不是未经处理的异常，事件消息也会出现在未经处理的异常对话框中。 若要避免出现该对话框，请在代码未在调试环境中执行时，移除 MDA 启用设置。  
  
> [!NOTE]
>  在 Visual Studio 集成开发环境 (IDE) 中执行代码时，可以避免针对特定 MDA 事件出现的异常对话框。 为此，请在“调试”菜单上，单击“异常”。 （如果“调试”菜单不包含“异常”命令，请单击“工具”菜单上的“自定义”添加该命令。）在“异常”对话框中，展开“托管调试助手”列表，然后清除单个 MDA 的“引发”复选框。 例如，要避免出现 [contextSwitchDeadlock](../../../docs/framework/debug-trace-profile/contextswitchdeadlock-mda.md) 的异常对话框，请在“托管调试助手”列表中清除其名称旁边的“引发”复选框。 也可以使用此对话框启用 MDA 异常对话框的显示。  
  
 下表列出了 .NET Framework 附带的 MDA。  
  
|||  
|-|-|  
|[asynchronousThreadAbort](../../../docs/framework/debug-trace-profile/asynchronousthreadabort-mda.md)|[bindingFailure](../../../docs/framework/debug-trace-profile/bindingfailure-mda.md)|  
|[callbackOnCollectedDelegate](../../../docs/framework/debug-trace-profile/callbackoncollecteddelegate-mda.md)|[contextSwitchDeadlock](../../../docs/framework/debug-trace-profile/contextswitchdeadlock-mda.md)|  
|[dangerousThreadingAPI](../../../docs/framework/debug-trace-profile/dangerousthreadingapi-mda.md)|[dateTimeInvalidLocalFormat](../../../docs/framework/debug-trace-profile/datetimeinvalidlocalformat-mda.md)|  
|[dirtyCastAndCallOnInterface](../../../docs/framework/debug-trace-profile/dirtycastandcalloninterface-mda.md)|[disconnectedContext](../../../docs/framework/debug-trace-profile/disconnectedcontext-mda.md)|  
|[dllMainReturnsFalse](../../../docs/framework/debug-trace-profile/dllmainreturnsfalse-mda.md)|[exceptionSwallowedOnCallFromCom](../../../docs/framework/debug-trace-profile/exceptionswallowedoncallfromcom-mda.md)|  
|[failedQI](../../../docs/framework/debug-trace-profile/failedqi-mda.md)|[fatalExecutionEngineError](../../../docs/framework/debug-trace-profile/fatalexecutionengineerror-mda.md)|  
|[gcManagedToUnmanaged](../../../docs/framework/debug-trace-profile/gcmanagedtounmanaged-mda.md)|[gcUnmanagedToManaged](../../../docs/framework/debug-trace-profile/gcunmanagedtomanaged-mda.md)|  
|[illegalPrepareConstrainedRegion](../../../docs/framework/debug-trace-profile/illegalprepareconstrainedregion-mda.md)|[invalidApartmentStateChange](../../../docs/framework/debug-trace-profile/invalidapartmentstatechange-mda.md)|  
|[invalidCERCall](../../../docs/framework/debug-trace-profile/invalidcercall-mda.md)|[invalidFunctionPointerInDelegate](../../../docs/framework/debug-trace-profile/invalidfunctionpointerindelegate-mda.md)|  
|[invalidGCHandleCookie](../../../docs/framework/debug-trace-profile/invalidgchandlecookie-mda.md)|[invalidIUnknown](../../../docs/framework/debug-trace-profile/invalidiunknown-mda.md)|  
|[invalidMemberDeclaration](../../../docs/framework/debug-trace-profile/invalidmemberdeclaration-mda.md)|[invalidOverlappedToPinvoke](../../../docs/framework/debug-trace-profile/invalidoverlappedtopinvoke-mda.md)|  
|[invalidVariant](../../../docs/framework/debug-trace-profile/invalidvariant-mda.md)|[jitCompilationStart](../../../docs/framework/debug-trace-profile/jitcompilationstart-mda.md)|  
|[loaderLock](../../../docs/framework/debug-trace-profile/loaderlock-mda.md)|[loadFromContext](../../../docs/framework/debug-trace-profile/loadfromcontext-mda.md)|  
|[marshalCleanupError](../../../docs/framework/debug-trace-profile/marshalcleanuperror-mda.md)|[marshaling](../../../docs/framework/debug-trace-profile/marshaling-mda.md)|  
|[memberInfoCacheCreation](../../../docs/framework/debug-trace-profile/memberinfocachecreation-mda.md)|[moduloObjectHashcode](../../../docs/framework/debug-trace-profile/moduloobjecthashcode-mda.md)|  
|[nonComVisibleBaseClass](../../../docs/framework/debug-trace-profile/noncomvisiblebaseclass-mda.md)|[notMarshalable](../../../docs/framework/debug-trace-profile/notmarshalable-mda.md)|  
|[openGenericCERCall](../../../docs/framework/debug-trace-profile/opengenericcercall-mda.md)|[overlappedFreeError](../../../docs/framework/debug-trace-profile/overlappedfreeerror-mda.md)|  
|[pInvokeLog](../../../docs/framework/debug-trace-profile/pinvokelog-mda.md)|[pInvokeStackImbalance](../../../docs/framework/debug-trace-profile/pinvokestackimbalance-mda.md)|  
|[raceOnRCWCleanup](../../../docs/framework/debug-trace-profile/raceonrcwcleanup-mda.md)|[reentrancy](../../../docs/framework/debug-trace-profile/reentrancy-mda.md)|  
|[releaseHandleFailed](../../../docs/framework/debug-trace-profile/releasehandlefailed-mda.md)|[reportAvOnComRelease](../../../docs/framework/debug-trace-profile/reportavoncomrelease-mda.md)|  
|[streamWriterBufferedDataLost](../../../docs/framework/debug-trace-profile/streamwriterbuffereddatalost-mda.md)|[virtualCERCall](../../../docs/framework/debug-trace-profile/virtualcercall-mda.md)|  
  
 默认情况下，.NET Framework 会为所有托管调试器激活 MDA 的子集。 通过单击“调试”菜单上的“异常”并展开“托管调试助手”列表，可以查看 Visual Studio 中的默认集。  
  
## <a name="enabling-and-disabling-mdas"></a>启用和禁用 MDA  
 可使用注册表项、环境变量和应用程序配置设置，启用和禁用 MDA。 若要使用应用程序配置设置，必须启用注册表项或环境变量。  
  
 在 Visual Studio 2005 和更高版本中，启用宿主进程后，不能禁用默认集合中的 MDA 或启用不在默认集合中的 MDA。 默认情况下，宿主进程处于启用状态，因此必须将其显式禁用。  
  
 若要在 Visual Studio 中禁用托管进程，请执行下列操作：  
  
1.  在“解决方案资源管理器”中，选择一个项目。  
  
2.  在“项目”菜单上，单击“属性”。  
  
     此时将显示“项目设计器”窗口。  
  
3.  单击“调试”选项卡。  
  
4.  在“启用调试器”部分中，清除“启用 Visual Studio 托管进程”复选框。  
  
 但是，禁用托管进程会影响性能。 通过阻止 Visual Studio 在每次收到 MDA 通知时显示 MDA 对话框，可以避免需要禁用 MDA。 为此，请单击“调试”菜单上的“异常”，展开“托管调试助手”列表，然后为单个 MDA 选中或清除“引发”复选框。  
  
### <a name="enabling-and-disabling-mdas-by-using-a-registry-key"></a>使用注册表项启用和禁用 MDA  
 可通过在 Windows 注册表中添加 HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\\.NETFramework\MDA 子项（类型为 REG_SZ，值为 1）启用 MDA。 将以下示例复制到名为 MDAEnable.reg 的文本文件中。打开 Windows 注册表编辑器 (RegEdit.exe)，从“文件”菜单选择“导入”。 选择 MDAEnable.reg 文件以在该计算机上启用 MDA。 将子项设置为字符串值 1（不是 DWORD 值 1）能够从 ApplicationName.suffix.mda.config 文件读取 MDA 设置。 （例如，Notepad 的 MDA 配置文件将被命名为 notepad.exe.mda.config）  
  
```  
Windows Registry Editor Version 5.00  
  
[HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\.NETFramework]  
"MDA"="1"  
```  
  
 如果计算机在 64 位操作系统上运行 32 位应用程序，应按下方所示设置 MDA 密钥：  
  
```  
      Windows Registry Editor Version 5.00   
  
[HKEY_LOCAL_MACHINE\SOFTWARE\Wow6432Node\Microsoft\.NETFramework]  
"MDA"="1"  
```  
  
 有关详细信息，请参阅[使用特定于应用程序的配置设置启用和禁用 MDA](#appConfig)。 可以使用 COMPLUS_MDA 环境变量重写注册表设置。 有关详细信息，请参阅[使用环境变量启用和禁用 MDA](#envVariable)。  
  
 若要禁用 MDA，请使用 Windows 注册表编辑器将 MDA 子项设置为 0（零）。  
  
 默认情况下，即使未添加该注册表项，有些 MDA 也会在运行附加到调试器的应用程序时启用。 此类助手的示例包括 [pInvokeStackImbalance](../../../docs/framework/debug-trace-profile/pinvokestackimbalance-mda.md) 和 [invalidApartmentStateChange](../../../docs/framework/debug-trace-profile/invalidapartmentstatechange-mda.md)。 可以按本节前面所述，运行 MDADisable.reg 文件来禁用这些助手。  
  
<a name="envVariable"></a>   
### <a name="enabling-and-disabling-mdas-by-using-an-environment-variable"></a>使用环境变量启用和禁用 MDA  
 还可以通过环境变量 COMPLUS_MDA 控制 MDA 激活，此变量可重写注册表项。 COMPLUS_MDA 字符串是一个区分大小写、以分号分隔的 MDA 名称列表或其他特殊控制字符串。 在托管或非托管调试器下启动将默认启用一组 MDA。 这是通过在环境变量或注册表项的值前面，隐式附加默认在调试器下启用的、以分号分隔的 MDA 的列表来实现的。 特殊控制字符串如下所示：  
  
-   `0` - 停用所有 MDA。  
  
-   `1` - 从 ApplicationName.mda.configg 读取 MDA 设置。  
  
-   `managedDebugger` - 显式激活在调试器下启动托管可执行文件时隐式激活的所有 MDA。  
  
-   `unmanagedDebugger` - 显式激活在调试器下启动非托管可执行文件时隐式激活的所有 MDA。  
  
 如果存在冲突的设置，则最新的设置将重写先前的设置：  
  
-   `COMPLUS_MDA=0` 禁用所有 MDA，包括那些在调试器下隐式启用的 MDA。  
  
-   除了调试器下隐式启用的所有 MDA，`COMPLUS_MDA=gcUnmanagedToManaged` 还启用 `gcUnmanagedToManaged`。  
  
-   `COMPLUS_MDA=0;gcUnmanagedToManaged` 启用 `gcUnmanagedToManaged`，但是禁用将在调试器下隐式启用的 MDA。  
  
<a name="appConfig"></a>   
### <a name="enabling-and-disabling-mdas-by-using-application-specific-configuration-settings"></a>使用特定于应用程序的配置设置启用和禁用 MDA  
 可以在应用程序的 MDA 配置文件中单独地启用、禁用和配置某些助手。 若要使用用于配置 MDA 的应用程序配置文件，必须设置 MDA 注册表项或 COMPLUS_MDA 环境变量。 应用程序配置文件通常与应用程序的可执行文件 (.exe) 位于同一目录中。 文件名采用“ApplicationName.mda.config”形式；例如，notepad.exe.mda.config。在应用程序配置文件中启用的助手可能包含专门设计用于控制该助手的行为的特性或元素。 下面的示例演示如何启用和配置 [marshaling](../../../docs/framework/debug-trace-profile/marshaling-mda.md)。  
  
```xml  
<mdaConfig>  
  <assistants>  
    <marshaling>  
      <methodFilter>  
        <match name="*"/>  
      </methodFilter>  
      <fieldFilter>  
        <match name="*"/>  
      </fieldFilter>  
    </marshaling>  
  </assistants>  
</mdaConfig>  
```  
  
 对于应用程序中每个托管到非托管的转换，`Marshaling` MDA 会发出有关正封送到非托管类型的托管类型信息。 `Marshaling` MDA 还能够分别筛选 `<methodFilter>` 和 `<fieldFilter>` 子元素中提供的方法和结构字段的名称。  
  
 下面的示例演示如何使用其默认设置来启用多个 MDA。  
  
```xml  
<mdaConfig>  
  <assistants>  
    <illegalPrepareConstrainedRegion />  
    <invalidCERCall />  
    <openGenericCERCall />  
    <virtualCERCall />  
  </assistants>  
</mdaConfig>  
```  
  
> [!IMPORTANT]
>  若在配置文件中指定了多个助手，则必须按字母顺序列出这些助手。 例如，若要同时启用 `virtualCERCall` 和 `invalidCERCall` MDA，则必须先添加 `<invalidCERCall />` 项，再添加 `<virtualCERCall />` 项。 如果这些项未按字母顺序排列，将显示未处理的无效配置文件异常消息。  
  
### <a name="mda-output"></a>MDA 输出  
 MDA 输出类似于下面的示例，此示例显示了来自 `pInvokeStackImbalance` MDA 的输出。  
  
 `A call to PInvoke function 'MDATest!MDATest.Program::StdCall' has unbalanced the stack. This is likely because the managed PInvoke signature does not match the unmanaged target signature. Check that the calling convention and parameters of the PInvoke signature match the target unmanaged signature.`  
  
## <a name="see-also"></a>另请参阅  
 [调试、跟踪和分析](../../../docs/framework/debug-trace-profile/index.md)

