---
title: "独立存储 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-standard"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "代码, 独立存储"
  - "使用独立存储的数据存储"
  - "使用独立存储的数据存储, 选项"
  - "使用独立存储的数据存储, 何时不使用"
  - "独立存储"
  - "独立存储, 选项"
  - "独立存储, 何时不使用"
  - "隔离"
  - "文件系统中独立存储的位置"
  - "标准化存储系统"
  - "存储"
  - "使用独立存储来存储数据"
  - "使用独立存储来存储数据, 选项"
  - "使用独立存储来存储数据, 何时不使用"
ms.assetid: aff939d7-9e49-46f2-a8cd-938d3020e94e
caps.latest.revision: 32
author: "mairaw"
ms.author: "mairaw"
manager: "wpickett"
caps.handback.revision: 31
---
# 独立存储
<a name="top"></a> 对于[!INCLUDE[desktop_appname](../../../includes/desktop-appname-md.md)]应用，独立存储是一种数据存储机制，它在代码与保存的数据之间定义了标准化的关联方式，从而提供隔离性和安全性。 同时，标准化也提供了其他好处。 管理员可以使用旨在操作独立存储的工具来配置文件存储空间、设置安全策略及删除未使用的数据。 通过独立存储，代码不再需要使用唯一的路径来指定文件系统中的安全位置，同时可以保护数据免遭只具有独立存储访问权限的其他应用程序的损坏。 不再需要指示应用程序的存储区域位置的硬编码信息。  
  
> [!IMPORTANT]
>  独立存储不适用于 [!INCLUDE[win8_appname_long](../../../includes/win8-appname-long-md.md)]应用。 相反，使用 `Windows.Storage` API 中包含的 [!INCLUDE[wrt](../../../includes/wrt-md.md)] 命名空间中的应用程序数据类来存储本地数据和文件。 有关详细信息，请参阅 Windows 开发人员中心的[应用程序数据](http://go.microsoft.com/fwlink/?LinkId=229175)。  
  
 本主题包含以下各节：  
  
-   [数据隔离舱和存储区](#data_compartments_and_stores)  
  
-   [独立存储的配额](#quotas)  
  
-   [安全访问](#secure_access)  
  
-   [允许的用法和安全风险](#allowed_usage)  
  
-   [独立存储位置](#isolated_storage_locations)  
  
-   [创建、枚举和删除独立存储](#isolated_storage_tasks)  
  
-   [独立存储的情况](#scenarios_for_isolated_storage)  
  
-   [相关主题](#related_topics)  
  
-   [参考](#reference)  
  
<a name="data_compartments_and_stores"></a>   
## 数据隔离舱和存储区  
 当应用程序在文件中存储数据时，必须仔细选择文件名和存储位置，最大程度地减小其他应用程序知道该存储位置的可能性，从而使数据不易受到损坏。 如果没有标准系统来管理这些问题，想开发出最大程度地减少存储冲突的特别技术可能并非易事，而且开发出来的技术也不见得可靠。  
  
 通过使用独立存储，数据将始终按用户和程序集进行隔离。 程序集的源或强名称等凭据确定程序集的身份。 通过使用类似的凭据，数据还可以按应用程序域进行隔离。  
  
 当使用独立存储时，应用程序将数据保存到与代码标识的某些方面（例如，其发行者或签名）关联的独特数据隔离舱。 数据隔离舱是一个抽象的存储位置，而不是具体的存储位置，它由一个或多个独立的存储文件（叫做存储区）组成，这些独立的存储文件包含存储数据的实际目录位置。 例如，应用程序可能有一个与其关联的数据隔离舱，文件系统中的某个目录将实现实际保留应用程序数据的存储区。 保存在存储区中的数据可以是任意类型的数据，无论是用户首选项信息还是应用程序状态都可以。 对于开发人员来说，数据隔离舱的位置是透明的。 应用商店通常位于客户端，但是，服务器应用程序可以使用独立存储通过模拟该服务的用户存储信息。 独立存储还可以将信息和用户漫游配置文件一起存储在服务器上，这样，漫游用户就可以随时使用该信息。  
  
 [返回页首](#top)  
  
<a name="quotas"></a>   
## 独立存储的配额  
 配额是对可使用的独立存储数量的限制。 配额包括文件空间的字节及与存储区中目录和其他信息关联的系统开销。 独立存储使用权限配额，这些配额是使用 <xref:System.Security.Permissions.IsolatedStoragePermission> 对象设置的存储限制。 如果尝试写入的数据超出配额，则会引发 <xref:System.IO.IsolatedStorage.IsolatedStorageException> 异常。  安全策略确定向代码授予的权限，它可以使用 .NET Framework 配置工具 \(Mscorcfg.msc\) 来修改。 已授予 <xref:System.Security.Permissions.IsolatedStoragePermission> 的代码所使用的存储范围不能超过 <xref:System.Security.Permissions.IsolatedStoragePermission.UserQuota%2A> 属性的限制。 但是，由于代码可以通过表示不同的用户标识绕过权限配额，所以权限配额用作指导代码如何工作的指南，而不是对代码行为的硬性限制。  
  
 不对漫游存储区强制执行配额。 因此，对使用它们的代码要求稍高级别的权限。 枚举值 <xref:System.Security.Permissions.IsolatedStorageContainment> 和 <xref:System.Security.Permissions.IsolatedStorageContainment> 为漫游用户指定使用独立存储的权限。  
  
 [返回页首](#top)  
  
<a name="secure_access"></a>   
## 安全访问  
 通过使用独立存储，可以使部分受信任的应用程序以由计算机安全策略控制的方式存储数据。 对于用户需慎重运行的下载的组件来说，这尤为有用。 在使用标准 I\/O 机制访问文件系统时，安全策略很少向这种代码授予权限。 但是默认情况下，会对在本地计算机、本地网络或 Internet 中运行的代码授予使用独立存储的权限。  
  
 管理员可以根据适当的信任级别限制应用程序或用户可以使用多少独立存储。 另外，管理员可以完全移除用户的持久性数据。 若要创建或访问独立存储，则必须授予代码相应的 <xref:System.Security.Permissions.IsolatedStorageFilePermission> 权限。  
  
 要访问独立存储，代码必须具有所有必要的本机平台操作系统权限。 必须满足用来控制哪些用户有权使用文件系统的访问控制列表 \(ACL\)。 除非执行（特定于平台的）模拟，否则 .NET Framework 应用程序已经具有访问独立存储的操作系统权限。 在这种情况下，应用程序负责确保被模拟的用户标识具有访问独立存储的适当操作系统权限。 对于在 Web 上运行或从 Web 下载的代码而言，这种访问为之提供了一种对与特定用户相关的存储区域进行读写操作的简便方法。  
  
 为了控制对独立存储的访问，公共语言运行时使用 <xref:System.Security.Permissions.IsolatedStorageFilePermission> 对象。 每个对象都具有指定以下值的属性：  
  
-   允许的用法，这指出了所允许的访问类型。 这些值是 <xref:System.Security.Permissions.IsolatedStorageContainment> 枚举的成员。 有关这些值的更多信息，请参见下一节中的表。  
  
-   存储配额（如上一节所述）。  
  
 当代码第一次尝试打开存储时，运行时要求 <xref:System.Security.Permissions.IsolatedStorageFilePermission> 权限。 它根据代码的受信程度决定是否授予此权限。 如果授予此权限，则允许的用法和存储配额值由安全策略和代码对 <xref:System.Security.Permissions.IsolatedStorageFilePermission> 的请求决定。 安全策略使用 .NET Framework 配置工具 \(Mscorcfg.msc\) 来进行设置。 检查调用堆栈中的所有调用方以确保每个调用方至少具有适当的允许的用法。 运行时还检查强加于代码的配额，该代码打开或创建将在其中保存文件的存储区。 如果满足这些条件，就授予权限。 每次文件写入存储区时，都将再次检查配额。  
  
 因为公共语言运行时将根据安全策略授予任何适当的 <xref:System.Security.Permissions.IsolatedStorageFilePermission>，所以请求权限不需要应用程序代码。 然而，有很好的理由来请求应用程序需要的特定权限，包括 <xref:System.Security.Permissions.IsolatedStorageFilePermission>。  
  
 [返回页首](#top)  
  
<a name="allowed_usage"></a>   
## 允许的用法和安全风险  
 <xref:System.Security.Permissions.IsolatedStorageFilePermission> 指定的允许的用法确定允许代码创建和使用独立存储的程度。 下表显示了权限中指定的允许的用法如何与隔离的类型对应，并总结了与每种允许的用法关联的安全风险。  
  
|允许的用法|隔离类型|安全影响|  
|-----------|----------|----------|  
|<xref:System.Security.Permissions.IsolatedStorageContainment>|不允许使用任何独立存储。|没有安全影响。|  
|<xref:System.Security.Permissions.IsolatedStorageContainment>|按用户、域和程序集隔离。 每个程序集在域中都有单独的子存储区。 使用此权限的存储也由计算机隐式隔离。|此权限级别无法阻止他人未经授权滥用资源，尽管强制的配额对此做法增添了一些难度。 这叫做拒绝服务攻击。|  
|<xref:System.Security.Permissions.IsolatedStorageContainment>|与 `DomainIsolationByUser` 相同，但如果启用漫游用户配置文件且不强制配额，则存储将保存到将漫游的位置。|因为必须禁用配额，所以存储资源更易受到拒绝服务攻击。|  
|<xref:System.Security.Permissions.IsolatedStorageContainment>|按用户和程序集隔离。 使用此权限的存储也由计算机隐式隔离。|在此级别强制实施配额以帮助防止拒绝服务攻击。 由于另一个域中相同的程序集可以访问该存储区，这就使信息可能在应用程序间泄露。|  
|<xref:System.Security.Permissions.IsolatedStorageContainment>|与 `AssemblyIsolationByUser` 相同，但如果启用漫游用户配置文件且不强制配额，则存储将保存到将漫游的位置。|与 `AssemblyIsolationByUser` 中相同，但没有配额，增加了拒绝服务攻击的风险。|  
|<xref:System.Security.Permissions.IsolatedStorageContainment>|按用户隔离。 通常，只有管理或调试工具才使用此级别的权限。|使用该权限访问允许代码查看或删除任何的用户独立存储文件或目录（而不论程序集是否隔离）。 存在的风险包括（但不限于）泄露信息和数据丢失。|  
|<xref:System.Security.Permissions.IsolatedStorageContainment>|按所有用户、域和程序集隔离。 通常，只有管理或调试工具才使用此级别的权限。|此权限有可能会整个危害所有用户的所有独立存储区。|  
  
 [返回页首](#top)  
  
<a name="isolated_storage_locations"></a>   
## 独立存储位置  
 有时候，使用操作系统的文件系统来验证对独立存储进行的更改会非常有帮助。 你可能还需要了解独立存储文件的位置。 该位置随操作系统的不同而不同。 下表显示了在几个常见操作系统上创建独立存储的根位置。 在此根位置下查找 Microsoft\\IsolatedStorage 目录。 您必须更改文件夹设置以显示隐藏文件和文件夹，才能查看到文件系统中的独立存储。  
  
|操作系统|在文件系统中的位置|  
|----------|---------------|  
|Windows 2000、Windows XP、Windows Server 2003（从 Windows NT 4.0 升级）|支持漫游的存储区 \=<br /><br /> \<SYSTEMROOT\>\\Profiles\\\<用户\>\\Application Data<br /><br /> 非漫游存储区 \=<br /><br /> \<SYSTEMROOT\>\\Profiles\\\<用户\>\\Local Settings\\Application Data|  
|Windows 2000 \- 全新安装（和从 Windows 98 及 Windows NT 3.51 升级）|支持漫游的存储区 \=<br /><br /> \<SYSTEMDRIVE\>\\Documents and Settings\\\<用户\>\\Application Data<br /><br /> 非漫游存储区 \=<br /><br /> \<SYSTEMDRIVE\>\\Documents and Settings\\\<用户\>\\Local Settings\\Application Data|  
|Windows XP、Windows Server 2003 \- 全新安装（和从 Windows 2000 及 Windows 98 升级）|支持漫游的存储区 \=<br /><br /> \<SYSTEMDRIVE\>\\Documents and Settings\\\<用户\>\\Application Data<br /><br /> 非漫游存储区 \=<br /><br /> \<SYSTEMDRIVE\>\\Documents and Settings\\\<用户\>\\Local Settings\\Application Data|  
|[!INCLUDE[win8](../../../includes/win8-md.md)]、Windows 7、Windows Server 2008、Windows Vista|支持漫游的存储区 \=<br /><br /> \<SYSTEMDRIVE\>\\Users\\\<用户\>\\AppData\\Roaming<br /><br /> 非漫游存储区 \=<br /><br /> \<SYSTEMDRIVE\>\\Users\\\<用户\>\\AppData\\Local|  
  
 [返回页首](#top)  
  
<a name="isolated_storage_tasks"></a>   
## 创建、枚举和删除独立存储  
 .NET Framework 在 <xref:System.IO.IsolatedStorage> 命名空间中提供了三个类来帮助你执行涉及独立存储的任务：  
  
-   <xref:System.IO.IsolatedStorage.IsolatedStorageFile> 派生自 <xref:System.IO.IsolatedStorage.IsolatedStorage?displayProperty=fullName>，它提供对存储的程序集和应用程序文件的基本管理。<xref:System.IO.IsolatedStorage.IsolatedStorageFile> 类的实例表示位于文件系统中的单个存储区。  
  
-   <xref:System.IO.IsolatedStorage.IsolatedStorageFileStream> 派生自 <xref:System.IO.FileStream?displayProperty=fullName>，它提供对存储中的文件的访问。  
  
-   <xref:System.IO.IsolatedStorage.IsolatedStorageScope> 是一个枚举，使您可以创建并选择具有适当隔离类型的存储区。  
  
 独立存储类使您可以创建、枚举并删除独立存储。 通过 <xref:System.IO.IsolatedStorage.IsolatedStorageFile> 对象可以使用执行这些任务的方法。 某些操作要求你具有 <xref:System.Security.Permissions.IsolatedStorageFilePermission> 权限（表示管理独立存储的权限）；你可能还需要具有访问文件或目录的操作系统权限。  
  
 有关演示常见的独立存储任务的一系列示例，请参见[相关主题](#related_topics)中列出的帮助主题。  
  
 [返回页首](#top)  
  
<a name="scenarios_for_isolated_storage"></a>   
## 独立存储的情况  
 在许多情况下，独立存储非常有用，包括这四种场景：  
  
-   下载的控件。 不允许从 Internet 下载的托管代码控件通过正常的 I\/O 类写入硬盘，但它们可以使用独立存储来持久保存用户设置和应用程序状态。  
  
-   共享组件存储。 应用程序间共享的组件可以使用独立存储来提供对数据存储区的有控制的访问。  
  
-   服务器存储。 服务器应用程序可以使用独立存储为请求应用程序的大量用户提供单独的存储区。 因为独立存储始终按用户进行隔离，所以服务器必须模拟发出请求的用户。 在这种情况下，根据主体的标识隔离数据，该标识与应用程序用来区分其用户的标识是同一个标识。  
  
-   漫游。 应用程序还可以将独立存储和漫游用户配置文件一起使用。 这允许用户的独立存储区和配置文件一起漫游。  
  
 不应该在以下情况下使用独立存储：  
  
-   用来存储重要机密，例如不加密的密钥或密码，因为独立存储对高度受信任的代码、非托管代码或计算机的受信任用户不设防。  
  
-   用来存储代码。  
  
-   用来存储管理员控制的配置和部署设置。 （因为管理员不控制用户首选项，所以用户首选项不被认为是配置设置。）  
  
 许多应用程序都使用数据库来存储和隔离数据，在这种情况下，数据库中的一个或多个行可能代表某个特定用户的存储。 当用户数较少时、当使用数据库的系统开销非常大时或当不存在数据库功能时，您可以选择使用独立存储而不使用数据库。 另外，当应用程序要求比数据库的行所提供的存储更加灵活和复杂的存储时，独立存储也可以提供一个可行的替代方案。  
  
 [返回页首](#top)  
  
<a name="related_topics"></a>   
## 相关主题  
  
|标题|描述|  
|--------|--------|  
|[隔离的类型](../../../docs/standard/io/types-of-isolation.md)|描述不同类型的隔离。|  
|[如何：获取独立存储的存储区](../../../docs/standard/io/how-to-obtain-stores-for-isolated-storage.md)|提供使用 <xref:System.IO.IsolatedStorage.IsolatedStorageFile> 类获取按用户和程序集隔离的存储区的示例。|  
|[如何：枚举独立存储的存储区](../../../docs/standard/io/how-to-enumerate-stores-for-isolated-storage.md)|演示如何使用 <xref:System.IO.IsolatedStorage.IsolatedStorageFile.GetEnumerator%2A?displayProperty=fullName> 方法计算用户的所有独立存储的大小。|  
|[如何：删除独立存储中的存储区](../../../docs/standard/io/how-to-delete-stores-in-isolated-storage.md)|演示如何使用 <xref:System.IO.IsolatedStorage.IsolatedStorageFile.Remove%2A?displayProperty=fullName> 方法以两种不同方式删除独立存储区。|  
|[如何：预见独立存储中的空间不足条件](../../../docs/standard/io/how-to-anticipate-out-of-space-conditions-with-isolated-storage.md)|说明如何测量独立存储区中剩余的空间。|  
|[如何：在独立存储中创建文件和目录](../../../docs/standard/io/how-to-create-files-and-directories-in-isolated-storage.md)|提供一些在独立存储区中创建文件和目录的示例。|  
|[如何：在独立存储中查找现有文件和目录](../../../docs/standard/io/how-to-find-existing-files-and-directories-in-isolated-storage.md)|演示如何读取独立存储区中的目录结构和文件。|  
|[如何：在独立存储中读取和写入文件](../../../docs/standard/io/how-to-read-and-write-to-files-in-isolated-storage.md)|提供一个向独立存储文件写入字符串并将其读取回的示例。|  
|[如何：在独立存储中删除文件和目录](../../../docs/standard/io/how-to-delete-files-and-directories-in-isolated-storage.md)|演示如何删除独立存储文件和目录。|  
|[文件和流 I\/O](../../../docs/standard/io/index.md)|解释如何执行同步和异步文件和数据流访问。|  
  
<a name="reference"></a>   
## 参考  
 <xref:System.IO.IsolatedStorage.IsolatedStorage?displayProperty=fullName>  
  
 <xref:System.IO.IsolatedStorage.IsolatedStorageFile?displayProperty=fullName>  
  
 <xref:System.IO.IsolatedStorage.IsolatedStorageFileStream?displayProperty=fullName>  
  
 <xref:System.IO.IsolatedStorage.IsolatedStorageScope?displayProperty=fullName>