---
title: "安装面向开发人员的 .NET Framework"
ms.custom: 
ms.date: 05/26/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology:
- dotnet-clr
ms.tgt_pltfrm: 
ms.topic: get-started-article
helpviewer_keywords:
- .NET Framework redistributable package, downloading
- .NET Framework, installing
- installing .NET Framework
- installation [.NET Framework]
ms.assetid: daf9d9d5-84ac-4bd9-a864-27665ffd0f5c
caps.latest.revision: 165
author: rpetrusha
ms.author: ronpet
manager: wpickett
ms.translationtype: HT
ms.sourcegitcommit: 21c6a1485f3d0c38bde065d6ecc7b07d5e424c1d
ms.openlocfilehash: 844b3e40b816d324ca4ba22d6884be5a7e3a2ec1
ms.contentlocale: zh-cn
ms.lasthandoff: 08/05/2017

---

# <a name="install-the-net-framework-for-developers"></a>安装面向开发人员的 .NET Framework

.NET 是在 Windows 上运行的多个应用不可缺少的一部分，并且对这些应用运行发挥着同样的功能。 对开发人员而言，.NET Framework 为生成具有视觉冲击力的用户体验和无缝安全通信的应用提供了一个全面且一致的编程模型。  

本文所附链接指向如何在计算机上安装 .NET Framework 4.5 及其次要版本（4.5.1、4.5.2）、[!INCLUDE[net_v46](../../../includes/net-v46-md.md)] 及其次要版本（4.6.1、4.6.2）和 .NET Framework 4.7。 如果你是开发人员，你也可以使用这些链接来下载 .NET Framework 并将其与你的应用程序一起重新分发。

请注意，安装 .NET Framework 的新版本并非总会替换之前的版本。 有关 .NET Framework 版本以及如何确定计算机上安装了哪些版本的详细信息，请参阅[版本和依赖关系](~/docs/framework/migration-guide/versions-and-dependencies.md)以及[如何：确定安装了哪些 .NET Framework 版本](../../../docs/framework/migration-guide/how-to-determine-which-versions-are-installed.md)。 下表中列出的所有 .NET Framework 版本都是对 .NET Framework 4 的就地更新。 也就是说，如果你要安装一个更高的版本，如 .NET Framework 4.6，则你无需首先安装之前的版本，如 .NET Framework 4.5、4.5.1 或 4.5.2。 同样，如果你要安装一个更高的版本，如 .NET Framework 4.6，则你无需首先安装之前的版本，如 .NET Framework 4.5、4.5.1 或 4.5.2。 

事实上，更高版本的 .NET Framework 4.x 是对早期版本的就地更新，这意味着如果已安装更高版本，将*无法*安装表格中列出的早期版本。 例如，由于 .NET Framework 4.6.1 已预安装在 Windows 10 十一月更新系统上，因此无法在该系统上安装 .NET Framework 4.6。    

> [!NOTE]
> 有关 .NET Framework 3.5 的信息，请参阅[在 Windows 10、Windows 8.1 和 Windows 8 上安装 .NET Framework 3.5](~/docs/framework/install/dotnet-35-windows-10.md)。  
  
使用下表获取快速链接或进一步阅读以获取详细信息。 若要在安装前查看 .NET Framework 的系统要求，请参阅[系统要求](~/docs/framework/get-started/system-requirements.md)。 有关疑难解答的帮助，请参阅[疑难解答](~/docs/framework/install/troubleshoot-blocked-installations-and-uninstallations.md)。  
  
|.NET Framework 版本|开发人员安装|可再发行组件安装|平台支持|  
|----------------------------|----------------------------|----------------------------------|----------------------|  
|**4.7**|[NET Framework 4.7 开发者工具包](http://go.microsoft.com/fwlink/?LinkId=825319)|[4.7 Web 安装程序下载页](http://go.microsoft.com/fwlink/?LinkId=825299)<br /><br /> [4.7 脱机安装程序下载页](http://go.microsoft.com/fwlink/?LinkId=825303)|包含于： <br/>Windows 10 创意者更新<br /><br /> 可以安装于：<br /> Windows 10 周年更新<br /> Windows 8.1 和更早版本<br /> Windows Server 2012 R2 和更早版本<br /> （有关完整列表，请参阅[系统要求](~/docs/framework/get-started/system-requirements.md)）||
|**4.6.2**|[NET Framework 4.6.2 开发人员工具包](http://go.microsoft.com/fwlink/?LinkId=780617)|[4.6.2 Web 安装程序下载页](http://go.microsoft.com/fwlink/?LinkId=780597)<br /><br /> [4.6.2 脱机安装程序下载页](http://go.microsoft.com/fwlink/?LinkId=780601)|包含于： <br /> Windows 10 周年纪念版<br /><br /> 可以安装于：<br /> Windows 10 <br /> Windows 8.1 和更早版本<br /> Windows Server 2012 R2 和更早版本<br /> （有关完整列表，请参阅[系统要求](~/docs/framework/get-started/system-requirements.md)）|
|**4.6.1**|[NET Framework 4.6.1 开发人员工具包](http://go.microsoft.com/fwlink/?LinkId=690706)|[4.6.1 Web 安装程序下载页](http://go.microsoft.com/fwlink/?LinkId=671729)<br /><br /> [4.6.1 脱机安装程序下载页](http://go.microsoft.com/fwlink/?LinkId=671744)|可以安装于：<br /> Windows 10 <br /> Windows 8.1 和更早版本<br /> Windows Server 2012 R2 和更早版本<br /> （有关完整列表，请参阅[系统要求](~/docs/framework/get-started/system-requirements.md)）|
|**4.6**|包含于 [!INCLUDE[vs_dev14](../../../includes/vs-dev14-md.md)]。 有关详细信息，请参阅[欢迎使用 Visual Studio 2015](http://msdn.microsoft.com/library/dd831853\(v=vs.140\).aspx)。<br /><br /> [Microsoft .NET Framework 4.6 目标包](http://go.microsoft.com/fwlink/?LinkId=528261)|[4.6 Web 安装程序下载页](http://go.microsoft.com/fwlink/?LinkId=528259)<br /><br /> [4.6 脱机安装程序下载页](http://go.microsoft.com/fwlink/?LinkId=528233)|包含于： <br /> Windows 10 <br />[!INCLUDE[vs_dev14](../../../includes/vs-dev14-md.md)]<br /><br /> 还可以安装于：<br /> Windows 8.1 和更早版本<br /> Windows Server 2012 R2 和更早版本<br /> （有关完整列表，请参阅[系统要求](~/docs/framework/get-started/system-requirements.md)）|  
|**4.5.2**|[Microsoft .NET Framework 4.5.2 开发人员工具包](http://go.microsoft.com/fwlink/?LinkId=397702)<br /><br /> 适用于 [Visual Studio 2013](http://go.microsoft.com/fwlink/?LinkID=325532)、Visual Studio 2012 或其他 IDE|[4.5.2 Web 安装程序下载页](http://go.microsoft.com/fwlink/p/?LinkId=397703)<br /><br /> [4.5.2 脱机安装程序下载页](http://go.microsoft.com/fwlink/p/?LinkId=397706)|可以安装于：<br /> Windows 8.1 和更早版本<br /> Windows Server 2012 R2 和更早版本<br /> （有关完整列表，请参阅[系统要求](~/docs/framework/get-started/system-requirements.md)）|  
|**4.5.1**|[Microsoft .NET Framework 4.5.1 开发人员工具包](http://go.microsoft.com/fwlink/?LinkId=324213)<br /><br /> 适用于 Visual Studio 2012 或其他 IDE|[4.5.1 Web 安装程序下载页](http://go.microsoft.com/fwlink/p/?LinkId=310158)<br /><br /> [4.5.1 脱机安装程序下载页](http://go.microsoft.com/fwlink/p/?LinkId=310159)|包含于：<br /> [!INCLUDE[win81](../../../includes/win81-md.md)]<br /> Windows Server 2012 R2<br /> [Visual Studio 2013](http://go.microsoft.com/fwlink/?LinkID=325532)<br /><br /> 还可以安装于：<br /> [!INCLUDE[win8](../../../includes/win8-md.md)] 和更早版本<br /> [!INCLUDE[winserver8](../../../includes/winserver8-md.md)] 和更早版本<br />（有关完整列表，请参阅[系统要求](~/docs/framework/get-started/system-requirements.md)）|  
|**4.5**|包含于 Visual Studio 2012 中<br /><br /> 也可作为 [Windows 8 SDK](http://msdn.microsoft.com/windows/hardware/hh852363) 的一部分提供|[4.5 Web 安装程序下载页](http://go.microsoft.com/fwlink/p/?LinkId=245484)|包含于： <br /> [!INCLUDE[win8](../../../includes/win8-md.md)]<br /> [!INCLUDE[winserver8](../../../includes/winserver8-md.md)]<br /> Visual Studio 2012<br /><br /> 还可以安装于：<br /> Windows 7 和更早版本<br /> Windows Server 2008 SP2 和更早版本<br />（有关完整列表，请参阅[系统要求](~/docs/framework/get-started/system-requirements.md)）|  

可以在所有支持的平台上针对特定版本的 .NET Framework（如果有）安装**开发人员工具包**。  
  
可以在以下系统上安装 **Web 或脱机安装程序**：  
  
- Windows 8.1 和更早版本  
  
- Windows Server 2012 R2 和更早版本  
  
有关完整列表，请参阅[系统要求](~/docs/framework/get-started/system-requirements.md)。  

有关适用于用户和开发人员的 .NET Framework 的常规说明，请参阅[入门](../get-started/index.md)。 有关使用应用部署 .NET Framework 的信息，请参阅[部署指南](~/docs/framework/deployment/deployment-guide-for-developers.md)。 若要了解 .NET Framework 的体系结构和主要功能，请参阅[概述](~/docs/framework/get-started/overview.md)。  

<a name="choices"></a>
## <a name="installation-choices"></a>安装选项

安装开发人员目标包以在 Visual Studio 或其他开发环境中针对最新版本的 .NET Framework 进行开发，或下载 .NET Framework 可再发行组件以与你的应用或控件一起分发。  
  
## <a name="to-install-the-net-framework-developer-or-targeting-pack"></a>安装 .NET Framework 开发人员包或目标包

.NET Framework 4.5.1 或 4.5.2 开发人员工具包、[!INCLUDE[net_v46](../../../includes/net-v46-md.md)] 目标包以及 [!INCLUDE[net_v461](../../../includes/net-v461-md.md)]、4.6.2 或 4.7 开发人员工具包提供 .NET Framework 4.5.1、4.5.2、[!INCLUDE[net_v46](../../../includes/net-v46-md.md)]、4.6.1、4.6.2 或 .NET Framework 4.7 引用程序集、语言包和 IntelliSense 文件，以供在集成开发环境（如 Visual Studio）中使用。  如果你使用的是 Visual Studio，则在你创建新项目时，开发人员包或目标包也将向目标选择添加 .NET Framework 的已安装版本。  在这些开发人员包或目标包中选择其中之一：  

- [Microsoft .NET Framework 4.7 开发者工具包](http://go.microsoft.com/fwlink/?LinkId=825319)

- [Microsoft .NET Framework 4.6.2 开发人员工具包](http://go.microsoft.com/fwlink/?LinkId=780617)  
  
- [Microsoft .NET Framework 4.6.2 开发人员工具包](http://go.microsoft.com/fwlink/?LinkId=780617)  
  
- [Microsoft .NET Framework 4.6.1 开发人员工具包](http://go.microsoft.com/fwlink/?LinkId=690706)  
  
- [Microsoft .NET Framework 4.6 目标包](http://go.microsoft.com/fwlink/?LinkId=528261)  
  
- [.NET Framework 4.5.2 开发人员工具包](http://go.microsoft.com/fwlink/?LinkId=397702)，用于在 Windows 8.1 或更早版本、Visual Studio 2013、Visual Studio 2012 或其他 IDE 上安装版本 4.5.2。  
  
- [.NET Framework 4.5.1 开发人员工具包](http://go.microsoft.com/fwlink/?LinkId=324213)，用于在 Visual Studio 2012 或其他 IDE 上安装版本 4.5.1。  
  
从开发人员工具包下载页中，选择“下载”。 随后选择“运行”或“保存”，并在出现提示时按照说明操作。  
  
## <a name="to-install-or-download-the-net-framework-redistributable"></a>安装或下载 .NET Framework 可再发行组件

这些安装程序为面向这些版本的 .NET Framework 的应用程序或控件下载 .NET Framework 组件。 这些组件必须安装在运行应用程序或控件的每台计算机上。 由于两个安装程序都是可再发行的，因此你可将其包含在你的应用程序的安装程序中。  
  
下载页以多种语言提供，但大多数下载仅以英语提供。 若要获得其他语言支持，你必须安装语言包。  
  
提供了两种类型的可再发行组件安装：  
  
- **Web 安装程序**（Web 引导程序）用于从 Web 下载匹配安装计算机的操作系统的所需组件和语言包。 此程序包远远小于脱机安装程序，但需要一致的 Internet 连接。 可以下载[独立的语言包](#standalone_language_packs)来安装其他语言支持。  
  
- **脱机安装程序**（独立的可再发行组件）包含安装 .NET Framework 所需的所有组件，但不包含语言包。 此下载大于 Web 安装程序。 脱机安装程序不需要 Internet 连接。 运行脱机安装程序后，可以下载[独立的语言包](#standalone_language_packs)来安装语言支持。 如果你无法拥有一致的 Internet 连接，请使用脱机安装程序。  
  
Web 和脱机安装程序均针对基于 x86 和 x64 的计算机而设计（请参阅[系统要求](~/docs/framework/get-started/system-requirements.md)），但不支持基于 Itanium 的计算机。  
  
1.  打开要安装的 .NET Framework 版本的下载页：  

    - .NET Framework 4.7（[Web 安装程序](http://go.microsoft.com/fwlink/?LinkId=825299)或[脱机安装程序](http://go.microsoft.com/fwlink/p/?LinkId=825303)）

    - .NET Framework 4.6.2（[Web 安装程序](http://go.microsoft.com/fwlink/?LinkId=780597)或[脱机安装程序](http://go.microsoft.com/fwlink/p/?LinkId=780601)）  
    
    - .NET Framework 4.6.1（[Web 安装程序](http://go.microsoft.com/fwlink/?LinkId=671729)或[脱机安装程序](http://go.microsoft.com/fwlink/p/?LinkId=671744)）  
  
    - .NET Framework 4.6（[Web 安装程序](http://go.microsoft.com/fwlink/?LinkId=528259)或[脱机安装程序](http://go.microsoft.com/fwlink/p/?LinkId=528233)）  
  
    - .NET Framework 4.5.2（[Web 安装程序](http://go.microsoft.com/fwlink/p/?LinkId=397703)或[脱机安装程序](http://go.microsoft.com/fwlink/p/?LinkId=397706)）  
  
    - .NET Framework 4.5.1（[Web 安装程序](http://go.microsoft.com/fwlink/p/?LinkId=310158)或[脱机安装程序](http://go.microsoft.com/fwlink/p/?LinkId=310159)）  
  
    - [.NET Framework 4.5](http://go.microsoft.com/fwlink/p/?LinkId=245484)  
  
1. 选择下载页的语言。 此选项不会下载 .NET Framework 的本地化资源；它只影响下载页上显示的文本。  
  
1. 选择“下载”。  
  
1. 出现提示时，请选择与系统体系结构相匹配的下载，然后选择“下一步”。  
  
1. 显示下载提示时，执行下列操作之一：
  
   - 如果要在计算机上安装 .NET Framework，请选择“运行”，然后按照屏幕上的提示操作。   
  
   - 如果要下载 .NET Framework 以供重新分发，请选择“保存”，然后按照屏幕上的提示操作。  
  
1. 若要下载其他语言的资源，请按照下一节中的说明进行操作来安装一个或多个语言包。  
  
> [!NOTE]
> 如果在安装期间遇到任何问题，请参阅[疑难解答](~/docs/framework/install/troubleshoot-blocked-installations-and-uninstallations.md)。  
  
 **安装说明：**  
  
- [!INCLUDE[net_v451](../../../includes/net-v451-md.md)] 和 4.5.2 以及 [!INCLUDE[net_v46](../../../includes/net-v46-md.md)]、4.6.1、4.6.2 和 4.7 是对 [!INCLUDE[net_v45](../../../includes/net-v45-md.md)] 的就地更新。  
  
- [!INCLUDE[net_v45](../../../includes/net-v45-md.md)] 及其次要版本、[!INCLUDE[net_v46](../../../includes/net-v46-md.md)] 及其次要版本和 .NET Framework 4.7 替换 [!INCLUDE[net_v40_long](../../../includes/net-v40-long-md.md)]。 在安装了 [!INCLUDE[net_v40_short](../../../includes/net-v40-short-md.md)] 的系统上安装这些版本时，将会替换这些程序集。
  
- 卸载 [!INCLUDE[net_v45](../../../includes/net-v45-md.md)] 及其次要版本、[!INCLUDE[net_v46](../../../includes/net-v46-md.md)] 及其次要版本或 .NET Framework 4.7 也会删除既有的 [!INCLUDE[net_v40_short](../../../includes/net-v40-short-md.md)] 文件。 若要返回到 [!INCLUDE[net_v40_short](../../../includes/net-v40-short-md.md)]，你必须重新安装它以及它的任何更新。 （请参阅[安装 .NET Framework 4](http://go.microsoft.com/fwlink/p/?LinkId=230665)。）  
  
- 必须拥有管理员凭据，才能安装 [!INCLUDE[net_v45](../../../includes/net-v45-md.md)] 及其次要版本、.NET Framework 4.6 及其次要版本和 .NET Framework 4.7。
  
- .NET Framework 4.5 可再发行组件于 2012 年 10 月 9 日进行了更新，纠正了一个与数字证书中的错误时间戳相关的问题，此问题会导致 Microsoft 生成并签名的文件中的数字签名提前过期。 如果之前安装了日期为 2012 年 8 月 16 日的 .NET Framework 4.5 可再发行组件包，建议使用 [Microsoft 下载中心](http://go.microsoft.com/fwlink/p/?LinkId=245484)内的最新可再发行组件来更新副本。 有关此问题的详细信息，请参阅 [Microsoft 安全公告 2749655](http://technet.microsoft.com/security/advisory/2749655) 和[知识库文章 2770445](http://support.microsoft.com/kb/2770445)。  
  
<a name="standalone_language_packs"></a>   
## <a name="to-install-language-packs"></a>安装语言包

 语言包是包含受支持语言的本地化资源（例如，翻译后的错误消息和 UI 文本）的可执行文件。 如果你不安装语言包，则会用英语显示 .NET Framework 错误消息和其他文本。  请注意，Web 安装程序会自动安装与你的操作系统相匹配的语言包，但是你可以将其他语言包下载到你的计算机。 脱机安装程序不包含任何语言包。 
  
> [!IMPORTANT]
> 语言包不包含运行应用程序所需的 .NET Framework 组件，因此，你必须在安装语言包之前运行 Web 安装程序或脱机安装程序。 如果已安装语言包，请将其卸载，安装 .NET Framework，然后重新安装语言包。  
  
1.  打开已安装的 .NET Framework 版本的语言包下载页：  
  
    - [.NET Framework 4.7 语言包](http://go.microsoft.com/fwlink/?LinkID=825306) 

    - [.NET Framework 4.6.2 语言包](http://go.microsoft.com/fwlink/?LinkID=780604)  
  
    - [.NET Framework 4.6.1 语言包](http://go.microsoft.com/fwlink/?LinkID=671747)  
  
    - [.NET Framework 4.6 语言包](http://go.microsoft.com/fwlink/?LinkID=528314)  
  
    - [.NET Framework 4.5.2 语言包](http://go.microsoft.com/fwlink/?LinkId=397701)  
  
    - [.NET Framework 4.5.1 语言包](http://go.microsoft.com/fwlink/?LinkId=322101)  
  
    - [.NET Framework 4.5 语言包](http://go.microsoft.com/fwlink/p/?LinkId=245451)  
  
2.  在语言列表中，选择要下载的语言，并等待几秒钟，以便使用该语言重新加载页面。  
  
3.  选择“下载”。  
  
下表列出了支持的语言。  
  
| 语言              | 区域性 |
| --------------------- | :-----: |
| 阿拉伯语                | ar      |
| 捷克语                 | cs      |
| 丹麦语                | da      |
| 荷兰语                 | nl      |
| 芬兰语               | fi      |
| 法语                | fr      |
| 德语                | de      |
| 希腊语                 | el      |
| 希伯来语                | he      |
| 匈牙利语             | hu      |
| 意大利语               | it      |
| 日语              | ja      |
| 朝鲜语                | ko      |
| 挪威语             | no      |
| 波兰语                | pl      |
| 葡萄牙语(巴西)   | pt-BR   |
| 葡萄牙语（葡萄牙） | pt-PT   |
| 俄语               | ru      |
| 简体中文    | zh-CHS  |
| 西班牙语               | es      |
| 瑞典语               | sv      |
| 繁体中文   | zh-CHT  |
| 土耳其语               | tr      |
| 英语（美国）            | zh-CN   |
  
## <a name="next-steps"></a>后续步骤  
  
- 如果不熟悉 .NET Framework，请参阅[概述](~/docs/framework/get-started/overview.md)以大致了解关键概念和组件。  
  
- 有关 .NET Framework 4.7、[!INCLUDE[net_v462](../../../includes/net-v462-md.md)]、[!INCLUDE[net_v461](../../../includes/net-v461-md.md)]、[!INCLUDE[net_v46](../../../includes/net-v46-md.md)]、4.5.2、4.5.1 和 4.5 中的新功能和改进，请参阅[新增功能](../../../docs/framework/whats-new/index.md)。  
  
- 有关使用应用部署 .NET Framework 的详细信息，请参阅[面向开发人员的部署指南](~/docs/framework/deployment/deployment-guide-for-developers.md)。  
  
- 有关影响通过应用部署 .NET Framework 的过程的更改，请参阅[在 .NET Framework 4.5 安装期间减少系统重新启动](~/docs/framework/deployment/reducing-system-restarts.md)。  
  
- 有关将应用从 .NET Framework 4 迁移到 [!INCLUDE[net_v45](../../../includes/net-v45-md.md)] 或其单点版本之一的信息，请参阅[迁移指南](~/docs/framework/migration-guide/index.md)。 

- 请参阅 [.NET Framework 引用源](http://referencesource.microsoft.com/)以联机浏览 .NET Framework 源代码。 还可以在 [Github](https://github.com/Microsoft/referencesource) 上获取引用源。 可[下载引用源](http://referencesource.microsoft.com/download.html)以供脱机查看和在调试期间逐步执行源（包括修补程序和更新）。 有关详细信息，请参阅日志 [.NET 引用源的全新外观](http://blogs.msdn.com/b/dotnet/archive/2014/02/24/a-new-look-for-net-reference-source.aspx)。  
  
## <a name="see-also"></a>另请参阅

[面向开发人员的部署指南](~/docs/framework/deployment/deployment-guide-for-developers.md)   
[面向管理员的部署指南](~/docs/framework/deployment/guide-for-administrators.md)   
[在 Windows 10、Windows 8.1 和 Windows 8 上安装 .NET Framework 3.5](~/docs/framework/install/dotnet-35-windows-10.md)   
[安装和卸载 .NET Framework 受阻疑难解答](~/docs/framework/install/troubleshoot-blocked-installations-and-uninstallations.md)

