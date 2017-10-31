---
title: "目标框架"
description: "了解用于 .NET Core 应用和库的目标框架。"
keywords: ".NET, .NET Core, 框架, TFM"
author: richlander
ms.author: mairaw
ms.date: 08/25/2017
ms.topic: article
ms.prod: .net
ms.technology: dotnet-standard
ms.devlang: dotnet
ms.assetid: 6ef56a2e-593d-497b-925a-1e25bb6df2e6
ms.translationtype: HT
ms.sourcegitcommit: 18b2f7a1c0857abb5f7e09a39ca120b521ba4ddc
ms.openlocfilehash: 7f25cdd52cf5249d3b201978eacb98aaa4a74fa9
ms.contentlocale: zh-cn
ms.lasthandoff: 08/25/2017

---

# <a name="target-frameworks"></a>目标框架

以应用或库中的框架为目标时，需要指定想要向应用或库提供的 API 集。 使用目标框架名字对象 (TFM) 在项目文件中指定目标框架。

应用或库可以使用 [.NET Standard](~/docs/standard/net-standard.md) 版本作为目标。 .NET Standard 版本表示所有 .NET 实现中的标准化 API 集。 例如，库可以使用 .NET Standard 1.6 作为目标，并获得对可使用相同基本代码跨 .NET Core 和 .NET Framework 工作的 API 的访问权限。

应用或库还能以一个特定 .NET 实现为目标，获得特定于实现的 API 的访问权限。 例如，面向 Xamarin.iOS 的应用（如 `Xamarin.iOS10`）有权访问 Xamarin 提供的适用于 iOS 10 的 iOS API 包装器；面向通用 Windows 平台 (UWP) 的应用（如 `uap10.0`）有权访问为运行 Windows 10 的设备编译的 API。

对于某些目标框架（例如 .NET Framework），API 由框架在系统上安装的程序集定义，并且可能包括应用程序框架 API（例如 ASP.NET）。

对于基于包的目标框架（例如 .NET Standard 和 .NET Core），API 由包含在应用或库中的包定义。 元包是一个 NuGet 包，NuGet 包本身不包含任何内容，只是一个依赖项列表（其他包）。 基于 NuGet 包的目标框架隐式指定一个元包，该元包引用一起构成框架的所有包。

## <a name="latest-target-framework-versions"></a>最新目标框架版本

下表定义了最常见的目标框架、如何引用这些框架，以及它们实现的 [.NET Standard](~/docs/standard/net-standard.md) 版本。 这些目标框架版本是最新的稳定版本。 预览版不会显示。 目标框架名字对象 (TFM) 是一个标准化令牌格式，用于指定 .NET 应用或库的目标框架。 

| 目标 Framework      | 最新版本 | 目标框架名字对象 (TFM) | .NET Standard 版本 | 元包 |
| :-------------------: | :------------: | :----------------------------: | :-------------------: | :---------: |
| .NET Standard         | 2.0.0          | netstandard2.0                 | 不可用                   | [NETStandard.Library](https://www.nuget.org/packages/NETStandard.Library) |
| .NET Core 应用程序 | 2.0.0          | netcoreapp2.0                  | 2.0                   | [Microsoft.NETCore.App](https://www.nuget.org/packages/Microsoft.NETCore.App) |
| .NET Framework        | 4.7            | net47                          | 1.5                   | 不可用 |

## <a name="supported-target-framework-versions"></a>支持的目标框架版本

目标框架通常由 TFM 引用。 下表显示 .NET Core SDK 和 NuGet 客户端支持的目标框架。 等效项显示在括号内。 例如，`win81` 对于 `netcore451` 来说等效于 TFM。

| 目标 Framework           | TFM |
| -------------------------- | --- |
| .NET Standard              | netstandard1.0<br>netstandard1.1<br>netstandard1.2<br>netstandard1.3<br>netstandard1.4<br>netstandard1.5<br>netstandard1.6<br>netstandard2.0 |
| .NET 核心                  | netcoreapp1.0<br>netcoreapp1.1<br>netcoreapp2.0 |
| .NET Framework             | net11<br>net20<br>net35<br>net40<br>net403<br>net45<br>net451<br>net452<br>net46<br>net461<br>net462<br>net47 |
| Windows 应用商店              | netcore [netcore45]<br>netcore45 [win] [win8]<br>netcore451 [win81] |
| .NET Micro Framework       | netmf |
| Silverlight                | sl4<br>sl5 |
| Windows Phone              | wp [wp7]<br>wp7<br>wp75<br>wp8<br>wp81<br>wpa81 |
| 通用 Windows 平台 | uap [uap10.0]<br>uap10.0 [win10] [netcore50] |

## <a name="how-to-specify-target-frameworks"></a>如何指定目标框架

在项目文件中指定目标框架。 指定单个目标框架时，使用 TargetFramework 元素。 以下控制台应用项目文件演示了如何以 .NET Core 2.0 为目标：

```xml
<Project Sdk="Microsoft.NET.Sdk">

  <PropertyGroup>
    <OutputType>Exe</OutputType>
    <TargetFramework>netcoreapp2.0</TargetFramework>
  </PropertyGroup>

</Project>
```

指定多个目标框架时，可有条件地为每个目标框架引用程序集。 在代码中，可使用具有 -if-then-else 逻辑的预处理器符号，有条件地针对这些程序集进行编译。

以下库项目文件以 .NET Standard (`netstandard1.4`) 的 API 和 .NET Framework（`net40` 和 `net45`）的 API 作为目标。 将复数形式的 TargetFrameworks 元素与多个目标框架一起使用。 请注意为两个 .NET Framework TFM 编译库时，`Condition` 属性包括特定于实现的包的方法：

```xml
<Project Sdk="Microsoft.NET.Sdk">

  <PropertyGroup>
    <TargetFrameworks>netstandard1.4;net40;net45</TargetFrameworks>
  </PropertyGroup>

  <!-- Conditionally obtain references for the .NET Framework 4.0 target -->
  <ItemGroup Condition=" '$(TargetFramework)' == 'net40' ">
    <Reference Include="System.Net" />
  </ItemGroup>

  <!-- Conditionally obtain references for the .NET Framework 4.5 target -->
  <ItemGroup Condition=" '$(TargetFramework)' == 'net45' ">
    <Reference Include="System.Net.Http" />
    <Reference Include="System.Threading.Tasks" />
  </ItemGroup>

</Project>
```

在库或应用中，编写条件代码以为每个目标框架编译：

```csharp
public class MyClass
{
    static void Main()
    {
#if NET40
        Console.WriteLine("Target framework: .NET Framework 4.0");
#elif NET45  
        Console.WriteLine("Target framework: .NET Framework 4.5");
#else
        Console.WriteLine("Target framework: .NET Standard 1.4");
#endif
    }
}
```

生成系统可识别预处理器符号，这些符号表示[支持的目标框架版本](#supported-target-framework-versions)表中所示的目标框架。 使用表示 .NET Standard 或 .NET Core TFM 的符号时，用下划线替代句点，并将小写字母转换为大写字母（例如，`netstandard1.4` 的符号是 `NETSTANDARD1_4`）。

完整的 .NET Core 目标框架的预处理器符号列表：

[!INCLUDE [Preprocessor symbols](~/includes/preprocessor-symbols.md)]

## <a name="deprecated-target-frameworks"></a>已弃用的目标框架

以下目标框架已弃用。 以这些目标框架为目标的包应迁移到指明的替代框架。

| 已弃用的 TFM                                                                             | Replacement |
| ------------------------------------------------------------------------------------------ | ----------- |
| aspnet50<br>aspnetcore50<br>dnxcore50<br>dnx<br>dnx45<br>dnx451<br>dnx452                  | netcoreapp  |
| dotnet<br>dotnet50<br>dotnet51<br>dotnet52<br>dotnet53<br>dotnet54<br>dotnet55<br>dotnet56 | netstandard |
| netcore50                                                                                  | uap10.0     |
| win                                                                                        | netcore45   |
| win8                                                                                       | netcore45   |
| win81                                                                                      | netcore451  |
| win10                                                                                      | uap10.0     |
| winrt                                                                                      | netcore45   |

## <a name="see-also"></a>请参阅

[包、元包和框架](~/docs/core/packages.md)  
[使用跨平台工具开发库](~/docs/core/tutorials/libraries.md)  
[.NET Standard](~/docs/standard/net-standard.md)  
[.NET Core 版本控制](~/docs/core/versions/index.md)  
[dotnet/standard GitHub 存储库](https://github.com/dotnet/standard)  
[NuGet 工具 GitHub 存储库](https://github.com/joelverhagen/NuGetTools)  
[.NET 中的框架配置文件](http://blog.stephencleary.com/2012/05/framework-profiles-in-net.html)

