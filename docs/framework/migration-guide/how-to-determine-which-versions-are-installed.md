---
title: "如何：确定安装了哪些 .NET Framework 版本"
ms.date: 08/09/2017
ms.prod: .net-framework
ms.technology:
- dotnet-clr
ms.topic: article
helpviewer_keywords:
- versions, determining for .NET Framework
- .NET Framework, determining version
ms.assetid: 40a67826-e4df-4f59-a651-d9eb0fdc755d
caps.latest.revision: 62
author: rpetrusha
ms.author: ronpet
manager: wpickett
ms.translationtype: HT
ms.sourcegitcommit: 775e4512a5ff31c7059961f6332c6bdc0dc5247a
ms.openlocfilehash: afb01fd47ed2ce3b9c5838f3a8f61c8d34147378
ms.contentlocale: zh-cn
ms.lasthandoff: 08/11/2017

---
# <a name="how-to-determine-which-net-framework-versions-are-installed"></a>如何：确定安装了哪些 .NET Framework 版本
用户可在他们的计算机上安装和运行 .NET Framework 的多个版本。 当你开发或部署应用时，你可能需要知道用户的计算机上安装了哪些 .NET Framework 版本。 请注意，.NET Framework 由两个采用不同版本的主要组件构成：  
  
-   一组程序集，它们是为应用提供功能的类型与资源的集合。 .NET Framework 和程序集使用相同的版本号。  
  
-   公共语言运行时 (CLR)，可管理并执行应用的代码。 CLR 由其自己的版本号标识（请参阅[版本和依赖关系](~/docs/framework/migration-guide/versions-and-dependencies.md)）。  
  
 若要获取计算机上安装的 .NET Framework 版本的准确列表，你可以在代码中查看注册表或查询注册表：  
  
 [查看注册表（版本 1-4）](#net_a)  
 [查看注册表（版本 4.5 和更高版本）](#net_b)  
 [使用代码查询注册表（版本 1-4）](#net_c)  
 [使用代码查询注册表（版本 4.5 和更高版本）](#net_d)  
 [使用 PowerShell 查询注册表（版本 4.5 及更高版本）](#ps_a)  
  
 若要查找 CLR 版本，你可以使用工具或代码：  
  
 [使用 Clrver 工具](#clr_a)  
 [使用代码查询 System.Environment 类](#clr_b)  
  
 有关检测每个版本 .NET Framework 所安装更新的信息，请参阅[如何：确定安装了哪些 .NET Framework 更新](~/docs/framework/migration-guide/how-to-determine-which-net-framework-updates-are-installed.md)。 若要了解如何安装 .NET Framework，请参阅[安装面向开发人员的 .NET Framework](../../../docs/framework/install/guide-for-developers.md)。  
  
<a name="net_a"></a>   
#### <a name="to-find-net-framework-versions-by-viewing-the-registry-net-framework-1-4"></a>通过查看注册表来查找 .NET Framework 版本 (.NET Framework 1-4)  
  
1.  在“开始”菜单上，选择“运行”。  
  
2.  在“打开”框中，输入“regedit.exe”。  
  
     你必须具有管理凭据才能运行 regedit.exe。  
  
3.  在注册表编辑器中，打开以下子项：  
  
     `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\NET Framework Setup\NDP`  
  
     安装的版本将在 NDP 子项的下方列出。 版本号存储在“版本”项中。 对于 [!INCLUDE[net_v40_long](../../../includes/net-v40-long-md.md)]，“版本”项位于客户端或完整子项下（在 NDP 下），或在这两个子项下。  
  

    > [!NOTE]
    > 注册表中的“NET Framework Setup”文件夹不会以句点开头。

<a name="net_b"></a> 
#### <a name="to-find-net-framework-versions-by-viewing-the-registry-net-framework-45-and-later"></a>通过查看注册表来查找 .NET Framework 版本（.NET Framework 4.5 和更高版本）

1. 在“开始”菜单上，选择“运行”。

2. 在“打开”框中，输入“regedit.exe”。

     你必须具有管理凭据才能运行 regedit.exe。

3. 在注册表编辑器中，打开以下子项：

     `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\NET Framework Setup\NDP\v4\Full`

     请注意，`Full` 子项的路径包括 `Net Framework` 子项，而不包括 `.NET Framework`。

    > [!NOTE]
    > 如果 `Full` 子项不存在，则表示你尚未安装 .NET Framework 4.5 或更高版本。

     检查名为 `Release` 的 DWORD 值。 存在 `Release` DWORD 表明该计算机上已安装 [!INCLUDE[net_v45](../../../includes/net-v45-md.md)] 或更新版本。

     ![.NET Framework 4.5 的注册表项。](../../../docs/framework/migration-guide/media/clr-installdir.png "CLR_InstallDir")

     `Release` DWORD 的值指示将安装的 .NET Framework 版本。

    |Release DWORD 的值|版本|
    |--------------------------------|-------------|
    |378389|.NET Framework 4.5|
    |378675|使用 Windows 8.1 或 Windows Server 2012 R2 安装的 .NET Framework 4.5.1|
    |378758|安装在 Windows 8、Windows 7 SP1 或 Windows Vista SP2 上的 .NET Framework 4.5.1|
    |379893|.NET Framework 4.5.2|
    |在 Windows 10 系统上：393295<br /><br /> 在所有其他操作系统版本上：393297|[!INCLUDE[net_v46](../../../includes/net-v46-md.md)]|
    |在 Windows 10 November Update 系统上：394254<br /><br /> 在所有其他操作系统版本上：394271|[!INCLUDE[net_v461](../../../includes/net-v461-md.md)]|
    |在 Windows 10 Anniversary Update 上：394802<br /><br /> 在所有其他操作系统版本上：394806|[!INCLUDE[net_v462](../../../includes/net-v462-md.md)]| 
    |在 Windows 10 创意者更新上：460798<br/><br/> 在所有其他操作系统版本上： 460805 | .NET Framework 4.7 |

<a name="net_c"></a> 
#### <a name="to-find-net-framework-versions-by-querying-the-registry-in-code-net-framework-1-4"></a>通过在代码中查询注册表来查找 .NET Framework 版本 (.NET Framework 1-4)

- 使用 <xref:Microsoft.Win32.RegistryKey?displayProperty=fullName> 类访问 Windows 注册表中 HKEY_LOCAL_MACHINE 下的 Software\Microsoft\NET Framework Setup\NDP\ 子项。

     下面的代码显示此查询的示例。

    > [!NOTE]
    > 此代码不演示如何检测 [!INCLUDE[net_v45](../../../includes/net-v45-md.md)] 或更高版本。 检查 `Release` DWORD 以检测这些版本，如上一节所述。 有关检测 [!INCLUDE[net_v45](../../../includes/net-v45-md.md)] 或更高版本的代码，请参阅本文的下一节。

     [!code-csharp[ListVersions](../../../samples/snippets/csharp/framework/migration-guide/versions-installed1.cs)]    [!code-vb[ListVersions](../../../samples/snippets/visualbasic/framework/migration-guide/versions-installed1.vb)]

     该示例生成类似下面内容的输出：

    ```
    v2.0.50727  2.0.50727.4016  SP2
    v3.0  3.0.30729.4037  SP2
    v3.5  3.5.30729.01  SP1
    v4
      Client  4.0.30319
      Full  4.0.30319
    ```

<a name="net_d"></a> 
#### <a name="to-find-net-framework-versions-by-querying-the-registry-in-code-net-framework-45-and-later"></a>通过在代码中查询注册表来查找 .NET Framework 版本（.NET Framework 4.5 和更高版本）

1. `Release` DWORD 的存在表明该计算机上已安装 .NET Framework 4.5 或更高版本。 关键字的值表示已安装的版本。 要检查此关键字，请使用 <xref:Microsoft.Win32.RegistryKey?displayProperty=fullName> 类的 <xref:Microsoft.Win32.RegistryKey.OpenBaseKey%2A> 和 <xref:Microsoft.Win32.RegistryKey.OpenSubKey%2A> 方法访问 Windows 注册表中 HKEY_LOCAL_MACHINE 下的 Software\Microsoft\NET Framework Setup\NDP\v4\Full 子项。

2. 检查 `Release` 关键字的值以确定安装的版本。 为了向前兼容，你可以检查是否有一个值大于或等于表中所列的值。 此处是 .NET Framework 版本及相关联的 `Release` 关键字。

    |版本|Release DWORD 的值|
    |-------------|--------------------------------|
    |.NET Framework 4.5|378389|
    |使用 Windows 8.1 安装的 .NET Framework 4.5.1|378675|
    |安装在 Windows 8、Windows 7 SP1 或 Windows Vista SP2 上的 .NET Framework 4.5.1|378758|
    |.NET Framework 4.5.2|379893|
    |随 Windows 10 一起安装的 [!INCLUDE[net_v46](../../../includes/net-v46-md.md)]|393295|
    |在所有其他 Windows 操作系统版本上安装的 [!INCLUDE[net_v46](../../../includes/net-v46-md.md)]|393297|
    |Windows 10 上安装的 [!INCLUDE[net_v461](../../../includes/net-v461-md.md)]|394254|
    |在所有其他 Windows 操作系统版本上安装的 [!INCLUDE[net_v461](../../../includes/net-v461-md.md)]|394271|
    |在 Windows 10 周年更新上安装的 [!INCLUDE[net_v462](../../../includes/net-v462-md.md)]|394802|
    |在所有其他 Windows 操作系统版本上安装的 [!INCLUDE[net_v462](../../../includes/net-v462-md.md)]|394806|
    |在 Windows 10 创意者更新上安装的 .NET Framework 4.7|460798|
    |在所有其他 Windows 操作系统版本上安装的 .NET Framework 4.7|460805|

     以下示例检查注册表中的 `Release` 值来确定是否已安装 [!INCLUDE[net_v45](../../../includes/net-v45-md.md)] 或更高版本的 .NET Framework。

     [!code-csharp[ListVersions#5](../../../samples/snippets/csharp/framework/migration-guide/versions-installed3.cs)]   [!code-vb[ListVersions#5](../../../samples/snippets/visualbasic/framework/migration-guide/versions-installed3.vb)]

     此示例遵循版本检查的建议做法：

    - 检查 `Release` 项的值是否*大于等于*已知版本键的值。

    - 按从最新版本到最早版本的顺序检查。

<a name="ps_a"></a> 
#### <a name="to-check-for-a-minimum-required-net-framework-version-by-querying-the-registry-in-powershell-net-framework-45-and-later"></a>使用 PowerShell 查询注册表（NET Framework 4.5 及更高版本）以检查所需的 .NET Framework 最低版本的具体步骤

- 下面的示例检查 `Release` 关键字的值，以确定是否已安装 .NET Framework 4.6.2 或更高版本，无论 Windows OS 版本如何（如果已安装，返回 `True`；否则，返回 `False`）。

    ```PowerShell
    Get-ChildItem "hklm:SOFTWARE\Microsoft\NET Framework Setup\NDP\v4\Full\" | Get-ItemPropertyValue -Name Release | % { $_ -ge 394802 } 
    ```

    可以将上一示例中的 `394802` 替换为下表中的另一值，以检查另一个所需的 .NET Framework 最低版本。
  
    |版本|Release DWORD 的最小值|
    |-------------|--------------------------------|
    |.NET Framework 4.5|378389|
    |.NET Framework 4.5.1|378675|
    |.NET Framework 4.5.2|379893|
    |[!INCLUDE[net_v46](../../../includes/net-v46-md.md)]|393295|
    |[!INCLUDE[net_v461](../../../includes/net-v461-md.md)]|394254|
    |[!INCLUDE[net_v462](../../../includes/net-v462-md.md)]|394802|
    |.NET Framework 4.7|460798|

<a name="clr_a"></a> 
#### <a name="to-find-the-current-runtime-version-by-using-the-clrver-tool"></a>使用 Clrver 工具查找当前运行时版本

- 使用 CLR 版本工具 (Clrver.exe) 决定已安装在计算机上的公共语言运行时的版本。

     从 Visual Studio 命令提示符处，输入 `clrver`。 该命令生成类似下面的输出：

    ```
    Versions installed on the machine:
    v2.0.50727
    v4.0.30319
    ```

     有关使用此工具的详细信息，请参阅 [Clrver.exe（CLR 版本工具）](~/docs/framework/tools/clrver-exe-clr-version-tool.md)。

<a name="clr_b"></a> 
#### <a name="to-find-the-current-runtime-version-by-querying-the-environment-class-in-code"></a>通过在代码中查询 Environment 类来查找当前运行时版本

- 查询 <xref:System.Environment.Version%2A?displayProperty=fullName> 属性，以检索标识当前正在执行代码的运行时版本的 <xref:System.Version> 对象。 你可以使用 <xref:System.Version.Major%2A?displayProperty=fullName> 属性获取主版本标识符（例如，4.0 版的“4”），使用 <xref:System.Version.Minor%2A?displayProperty=fullName> 属性获取次版本标识符（例如，4.0 版的“0”），或使用 <xref:System.Object.ToString%2A?displayProperty=fullName> 方法获取完整版本字符串（例如“4.0.30319.18010”，如下面的代码中所示）。 此属性返回一个值，该值反映当前正在执行代码的运行时的版本；它不返回程序集版本或可能已在计算机上安装的运行时的其他版本。

     对于 .NET Framework 版本 4、4.5、4.5.1 和 4.5.2，<xref:System.Environment.Version%2A?displayProperty=fullName> 属性返回字符串表现形式具有窗体 `4.0.30319.xxxxx` 的 <xref:System.Version> 对象。 对于 .NET Framework 4.6 及更高版本，形式为 `4.0.30319.42000`。

    > [!IMPORTANT]
    > 对于 [!INCLUDE[net_v45](../../../includes/net-v45-md.md)] 和更高版本，不建议使用 <xref:System.Environment.Version%2A?displayProperty=fullName> 属性来检测运行时的版本。 相反，我们建议查询注册表，如本文前面[通过用代码查询注册表来查找 .NET Framework 版本（.NET Framework 4.5 及更高版本）](#net_d)一节所述。

     以下是在 <xref:System.Environment.Version%2A?displayProperty=fullName> 属性中查询运行时版本信息的示例：

     [!code-csharp[ListVersions](../../../samples/snippets/csharp/framework/migration-guide/versions-installed2.cs)]    [!code-vb[ListVersions](../../../samples/snippets/visualbasic/framework/migration-guide/versions-installed2.vb)]

     该示例生成类似下面内容的输出：

    ```
    Version: 4.0.30319.18010
    ```

## <a name="see-also"></a>另请参阅
 [如何：确定安装了哪些 .NET Framework 更新](~/docs/framework/migration-guide/how-to-determine-which-net-framework-updates-are-installed.md)   
 [安装面向开发人员的 .NET Framework](../../../docs/framework/install/guide-for-developers.md)   
 [版本和依赖关系](~/docs/framework/migration-guide/versions-and-dependencies.md)

