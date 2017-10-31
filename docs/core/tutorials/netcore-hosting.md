---
title: "托管 .NET Core"
description: "从本机代码托管 .NET Core 运行时"
keywords: ".NET, .NET Core, 托管, 托管 .NET Core"
author: mjrousos
ms.author: mikerou
ms.date: 2/3/2017
ms.topic: article
ms.prod: .net-core
ms.devlang: dotnet
ms.assetid: 13edec8b-614d-47ed-9e95-ed6d3b94ec0c
ms.translationtype: HT
ms.sourcegitcommit: e0271ba3392ce8861dc916714af8c16d4581ce4f
ms.openlocfilehash: 1f0983b909244dda7270d3eff01dc302383639a5
ms.contentlocale: zh-cn
ms.lasthandoff: 08/14/2017

---

# <a name="hosting-net-core"></a>托管 .NET Core

像所有的托管代码一样，.NET Core 应用程序也由主机执行。 主机负责启动运行时（包括 JIT 和垃圾回收器等组件）、创建 AppDomain 并调用托管的入口点。

托管 .NET Core 运行时是高级方案，在大多数情况下，.NET Core 开发人员无需担心托管问题，因为 .NET Core 生成过程会提供默认主机来运行 .NET Core 应用程序。 虽然在某些特殊情况下，它对显式托管 .NET Core 运行时非常有用 - 无论是作为一种在本机进程中调用托管代码的方式还是为了获得对运行时工作原理更好的控制。

本文概述了从本机代码启动 .NET Core 运行时、创建初始应用程序域 (<xref:System.AppDomain>) 以及在域中执行托管代码的必要步骤。

## <a name="prerequisites"></a>先决条件

由于主机是本机应用程序，所以本教程将介绍如何构造 C++ 应用程序以托管 .NET Core。 将需要一个 C++ 开发环境（例如，[Visual Studio](https://www.visualstudio.com/downloads/) 提供的环境）。

还将需要一个简单的 .NET Core 应用程序来测试主机，因此应安装 [.NET Core SDK](https://www.microsoft.com/net/core) 并[构建一个小型的 .NET Core 测试应用](../../core/tutorials/with-visual-studio.md)（例如，“Hello World”应用）。 使用通过新 .NET Core 控制台项目模板创建的“Hello World”应用就足够了。

本教程及其相关示例会构建一个 Windows 主机，请参阅本文结尾处有关在 Unix 上托管的说明。

## <a name="creating-the-host"></a>创建主机

用于演示本文中所述步骤的[示例主机](https://github.com/dotnet/docs/tree/master/samples/core/hosting)可从 dotnet/docs GitHub 存储库获取。 该示例的 host.cpp 文件中的注释清楚地将本教程中已编号的步骤与它们在示例中的执行位置关联。 有关下载说明，请参阅[示例和教程](../../samples-and-tutorials/index.md#viewing-and-downloading-samples)。

请记住，示例主机的用途在于提供学习指导，在纠错方面不甚严谨，其重在可读性而非效率。 更多的真实主机示例可从 [dotnet/coreclr](https://github.com/dotnet/coreclr/tree/master/src/coreclr/hosts) 存储库获取。 尤其是 [CoreRun 主机](https://github.com/dotnet/coreclr/tree/master/src/coreclr/hosts/corerun)，它是学习者了解简单示例后用来深入学习的通用主机。

### <a name="a-note-about-mscoreeh"></a>有关 mscoree.h 的说明
.NET Core 主托管接口 (`ICLRRuntimeHost2`) 在 [MSCOREE.IDL](https://github.com/dotnet/coreclr/blob/master/src/inc/MSCOREE.IDL) 中定义。 主机需要引用的此文件 (mscoree.h) 的标头版本，该版本是在构建 [.NET Core 运行时](https://github.com/dotnet/coreclr/)时通过 MIDL 生成。 如果不想构建 .NET Core 运行时，还可在 dotnet/coreclr 存储库中将 mscoree.h 获取为[预生成的标头](https://github.com/dotnet/coreclr/tree/master/src/pal/prebuilt/inc)。 [有关构建 .NET Core 运行时的说明](https://github.com/dotnet/coreclr#building-the-repository)可在其 GitHub 存储库中找到。 

### <a name="step-1---identify-the-managed-entry-point"></a>步骤 1 - 标识托管的入口点
引用必要的标头后（例如，[mscoree.h](https://github.com/dotnet/coreclr/tree/master/src/pal/prebuilt/inc/mscoree.h) 和 stdio.h），.NET Core 主机必须完成的首要任务之一就是找到要使用的托管入口点。 在示例主机中，通过将主机的第一个命令行参数作为托管的二进制文件（将执行该文件的 `main` 方法）的路径，即可完成此操作。

[!code-cpp[NetCoreHost#1](../../../samples/core/hosting/host.cpp#1)]

### <a name="step-2---find-and-load-coreclrdll"></a>步骤 2 - 查找和加载 CoreCLR.dll
.NET Core 运行时 API 位于 *CoreCLR.dll*（在 Windows 上）中。 若要获取托管接口 (`ICLRRuntimeHost2`)，就必须查找并加载 *CoreCLR.dll*。 由主机定义用于规定 *CoreCLR.dll* 查找方式的约定。 一些主机会预期文件位于一个常用的计算机范围内的位置（如 %programfiles%\dotnet\shared\Microsoft.NETCore.App\1.1.0）。 其他主机会预期 *CoreCLR.dll* 从主机本身或要托管的应用旁的某个位置进行加载。 还有一些主机可能会参考环境变量来查找库。

在 Linux 或 Mac 上，核心运行时库分别是 *libcoreclr.so* 或者 *libcoreclr.dylib*。

示例主机会为 *CoreCLR.dll* 探测几个常用位置。 找到后，必须通过 `LoadLibrary`（在 Linux/Mac 上通过 `dlopen`）进行加载。

[!code-cpp[NetCoreHost#2](../../../samples/core/hosting/host.cpp#2)]

### <a name="step-3---get-an-iclrruntimehost2-instance"></a>步骤 3 - 获取 ICLRRuntimeHost2 实例
通过在 `GetCLRRuntimeHost` 上调用 `GetProcAddress`（或在 Linux/Mac 上调用 `dlsym`），然后再调用该函数来检索 `ICLRRuntimeHost2` 托管接口。 

[!code-cpp[NetCoreHost#3](../../../samples/core/hosting/host.cpp#3)]

### <a name="step-4---setting-startup-flags-and-starting-the-runtime"></a>步骤 4 - 设置启动标志和启动运行时
有了 `ICLRRuntimeHost2`，现在便可指定运行时范围内的启动标志并启动该运行时。 启动标志决定要使用的垃圾回收器 (GC)（并发垃圾回收器或服务器）、是使用单个 AppDomain 还是多个 Appdomain，以及要使用的加载程序优化策略（对于非特定于域的程序集加载）。

[!code-cpp[NetCoreHost#4](../../../samples/core/hosting/host.cpp#4)]

通过调用 `Start` 函数启动运行时。

```C++
hr = runtimeHost->Start();
```

### <a name="step-5---preparing-appdomain-settings"></a>步骤 5 - 准备 AppDomain 设置
启动运行时后，将需要设置 AppDomain。 但创建 .NET AppDomain 时必须指定大量选项，因此必须先准备这些选项。

AppDomain 标志指定与安全性和互操作性相关的 AppDomain 行为。 早期 Silverlight 主机对沙盒用户代码使用这些设置，但大多数现代 .NET Core 主机以完全信任的方式运行用户代码并启用互操作。

[!code-cpp[NetCoreHost#5](../../../samples/core/hosting/host.cpp#5)]

确定要使用的 AppDomain 标志后，必须定义 AppDomain 属性。 该属性是字符串的键/值对。 这些属性中的许多与 AppDomain 程序集的加载方式相关。

常见 AppDomain 属性包括：

* `TRUSTED_PLATFORM_ASSEMBLIES` 这是一个程序集路径的列表（在 Windows 上以“;”分隔，在 Unix 上以“:”分隔），AppDomain 应优先加载它们并对其授予完全信任（甚至在部分受信任域中也一样）。 此列表应包含“框架”程序集和其他受信任的模块，与 .NET Framework 方案中的 GAC 类似。 一些主机会将任何库置于此列表上的 *coreclr.dll* 旁，其他主机具有硬编码的清单，其中列出了用于所需用途的受信任程序集。
* `APP_PATHS` 这是一个用来探测程序集的路径的列表（如果在受信任的平台程序集 (TPA) 列表中找不到程序集）。 这些路径应是可在其中找到用户的程序集的位置。 在沙盒 AppDomain 中，从这些路径加载的程序集仅被授予部分信任。 常见的 APP_PATH 路径包括加载目标应用的路径或其他已知存在用户资产的位置。
*  `APP_NI_PATHS` 此列表与 APP_PATHS 非常相似，不同之处在于其中的路径用于探测本机映像。
*  `NATIVE_DLL_SEARCH_DIRECTORIES` 此属性是一个路径列表，加载程序在查找通过 p/invoke 调用的本机 DLL 时应使用这些路径进行探测。
*  `PLATFORM_RESOURCE_ROOTS` 此列表包含的路径用于探测资源附属程序集（在区域性特定的子目录中）。
*  `AppDomainCompatSwitch` 此字符串指定当不具有显式目标框架名字对象（一种程序集级别的属性，指示程序集应针对哪个框架运行）时应用于程序集的兼容性事项。 通常情况下，应将其设置为 `"UseLatestBehaviorWhenTFMNotSpecified"`，但某些主机可能更想要获取较旧的 Silverlight 或 Windows Phone 兼容性特事项。

在[简单示例主机](https://github.com/dotnet/docs/tree/master/samples/core/hosting)中，这些属性将进行如下设置：

[!code-cpp[NetCoreHost#6](../../../samples/core/hosting/host.cpp#6)]

### <a name="step-6---create-the-appdomain"></a>步骤 6 - 创建 AppDomain
所有 AppDomain 标志和属性都准备都就绪后，可使用 `ICLRRuntimeHost2::CreateAppDomainWithManager` 设置 AppDomain。 此函数选择性地采用完全限定的程序集名称和类型名称作为域的 AppDomain 管理器。 AppDomain 管理器可允许主机控制 AppDomain 行为的某些方面，并且如果主机不打算直接调用用户代码，它可能会提供用于启动托管代码的入口点。   

[!code-cpp[NetCoreHost#7](../../../samples/core/hosting/host.cpp#7)]

### <a name="step-7---run-managed-code"></a>步骤 7 - 运行托管代码！
现在 AppDomain 启动并运行后，主机可以开始执行托管的代码。 执行此操作的最简单方法是使用 `ICLRRuntimeHost2::ExecuteAssembly` 调用托管程序集的入口点方法。 请注意，此函数仅适用于单一域方案。

[!code-cpp[NetCoreHost#8](../../../samples/core/hosting/host.cpp#8)]

如果 `ExecuteAssembly` 不满足主机的需要，那么另一种方法是使用 `CreateDelegate` 创建指向静态托管方法的函数指针。 这要求主机知道要调用的方法的签名（以创建函数指针类型），但允许主机调用代码而不是程序集的入口点。

```C++
void *pfnDelegate = NULL;
hr = runtimeHost->CreateDelegate(
  domainId,
  L"HW, Version=1.0.0.0, Culture=neutral",  // Target managed assembly
  L"ConsoleApplication.Program",            // Target managed type
  L"Main",                                  // Target entry point (static method)
  (INT_PTR*)&pfnDelegate);

((MainMethodFp*)pfnDelegate)(NULL);
```

### <a name="step-8---clean-up"></a>步骤 8 - 清理
最后，主机应随后通过卸载 Appdomain、停止运行时并释放 `ICLRRuntimeHost2` 引用来进行清理。

[!code-cpp[NetCoreHost#9](../../../samples/core/hosting/host.cpp#9)]

## <a name="about-hosting-net-core-on-unix"></a>关于在 Unix 上托管 .NET Core
.NET Core 是一款跨平台产品，可在 Windows、Linux 和 Mac 操作系统上运行。 但作为本机应用程序，用于不同平台的主机之间会有一些差异。 上述使用 `ICLRRuntimeHost2` 启动运行时、创建 AppDomain，然后执行托管代码的过程应适用于任何支持的操作系统。 但是，在 Unix 平台上使用 mscoree.h 中定义的接口可能会很麻烦，因为 mscoree 进行了许多 Win32 假设。

为使在 Unix 平台上进行托管更简单，[coreclrhost.h ](https://github.com/dotnet/coreclr/blob/master/src/coreclr/hosts/inc/coreclrhost.h) 中又提供了一组非特定于平台的托管 API 包装器。

可在 [UnixCoreRun 主机](https://github.com/dotnet/coreclr/tree/master/src/coreclr/hosts)中查看一个使用 coreclrhost.h（而不是直接使用 mscoree.h）的示例。 使用 coreclrhost.h 中的 API 来托管运行时的步骤与使用 mscoree.h 时的步骤类似：

1. 确定要执行的托管代码（例如，从命令行参数）。 
2. 加载 CoreCLR 库。
    1. `dlopen("./libcoreclr.so", RTLD_NOW | RTLD_LOCAL);` 
3. 使用 `dlsym` 获取指向 CoreCLR 的 `coreclr_initialize`、`coreclr_create_delegate`、`coreclr_execute_assembly` 和 `coreclr_shutdown` 函数的函数指针
    1. `coreclr_initialize_ptr coreclr_initialize = (coreclr_initialize_ptr)dlsym(coreclrLib, "coreclr_initialize");`
4. 设置 AppDomain 属性（如 TPA 列表）。 这与上述 mscoree 工作流中的步骤 5 相同。
5. 使用 `coreclr_initialize` 启动运行时并创建 AppDomain。 这还将创建要在将来的托管调用中使用的 `hostHandle` 指针。
    1. 请注意，此函数同时执行上一工作流中步骤 4 和 6 的角色。 
6. 使用 `coreclr_execute_assembly` 或 `coreclr_create_delegate` 执行托管代码。 这些函数类似于上一工作流步骤 7 中 mscoree 的 `ExecuteAssembly` 和 `CreateDelegate` 函数。
7. 使用 `coreclr_shutdown` 卸载 AppDomain 并关闭运行时。 

## <a name="conclusion"></a>结束语
构建主机后，可以通过从命令行运行主机并传递其所需的任何参数（例如，要运行的托管应用）来对其进行测试。 指定主机要运行的 .NET Core 应用时，请务必使用 `dotnet build` 生成的 .dll。 `dotnet publish` 为独立应用程序生成的可执行文件实际上是默认的 .NET Core 主机（以便可直接从主流方案中的命令行启动应用）；用户代码被编译为具有相同名称的 dll。 

如果开始时操作不起作用，请再次检查 *coreclr.dll* 是否在主机预期的位置可用、是否 TPA 列表中包含了所有必需的框架库以及 CoreCLR 的位数（32 位或 64 位）是否匹配主机的构建方式。

托管 .NET Core 运行时是高级方案，许多开发人员并不需要实施这一方案，但对于那些需要从本机进程启动托管代码的人员，或需要更好地控制 .NET Core 运行时的行为的人员而言，它会非常有用。 因为 .NET Core 能够与其自身并行运行，甚至可以创建主机，这些主机能够初始化和启动多个 .NET Core 运行时版本并在同一进程中执行所有这些版本上的应用。 

