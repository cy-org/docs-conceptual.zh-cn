---
title: "WPF 部分信任安全 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-wpf"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "调试部分信任应用程序"
  - "检测权限"
  - "功能安全要求"
  - "管理权限"
  - "部分信任应用程序, 调试"
  - "部分信任安全"
  - "权限, 检测"
  - "权限, 管理"
  - "Internet Explorer 的安全设置"
ms.assetid: ef2c0810-1dbf-4511-babd-1fab95b523b5
caps.latest.revision: 40
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 36
---
# WPF 部分信任安全
<a name="introduction"></a> 通常，应该限制 Internet 应用程序直接访问关键系统资源，防止恶意损坏。  默认情况下，[!INCLUDE[TLA#tla_html](../../../includes/tlasharptla-html-md.md)] 和客户端脚本语言无法访问关键系统资源。  因为以 [!INCLUDE[TLA#tla_wpf](../../../includes/tlasharptla-wpf-md.md)] 浏览器为宿主的应用程序可以从该浏览器中启动，所以它们应该符合一组类似的限制。  为了实施这些限制，[!INCLUDE[TLA2#tla_wpf](../../../includes/tla2sharptla-wpf-md.md)] 同时依赖于 [!INCLUDE[TLA#tla_cas](../../../includes/tlasharptla-cas-md.md)] 和 [!INCLUDE[TLA#tla_clickonce](../../../includes/tlasharptla-clickonce-md.md)]（请参见 [WPF 安全策略 — 平台安全性](../../../docs/framework/wpf/wpf-security-strategy-platform-security.md)）。  默认情况下，以浏览器为宿主的应用程序请求 Internet 区域 [!INCLUDE[TLA2#tla_cas](../../../includes/tla2sharptla-cas-md.md)] 权限集，而无论它们是从 Internet、本地 Intranet 还是本地计算机中启动的。  如果应用程序的运行权限小于完全权限集，那么就说该应用程序正在部分信任环境下运行。  
  
 [!INCLUDE[TLA2#tla_wpf](../../../includes/tla2sharptla-wpf-md.md)] 提供了各种各样的支持，确保可以在部分信任环境中安全地使用尽可能多的功能；还与 [!INCLUDE[TLA2#tla_cas](../../../includes/tla2sharptla-cas-md.md)] 一起为部分信任编程提供了附加支持。  
  
 本主题包含以下各节：  
  
-   [WPF 功能部分信任支持](#WPF_Feature_Partial_Trust_Support)  
  
-   [部分信任编程](#Partial_Trust_Programming)  
  
-   [管理权限](#Managing_Permissions)  
  
<a name="WPF_Feature_Partial_Trust_Support"></a>   
## WPF 功能部分信任支持  
 下表列出了可以在 Internet 区域权限集限制范围内安全使用的 [!INCLUDE[TLA#tla_wpf](../../../includes/tlasharptla-wpf-md.md)] 高级功能。  
  
 表 1：在部分信任环境中安全的 WPF 功能  
  
|功能区域|功能|  
|----------|--------|  
|常规|浏览器窗口<br /><br /> 源站点访问<br /><br /> IsolatedStorage（512KB 限制）<br /><br /> UIAutomation 提供程序<br /><br /> 命令<br /><br /> 输入法编辑器 \(IME\)<br /><br /> 触笔和墨迹<br /><br /> 使用 Mouse Capture 和 Move 事件模拟的拖放<br /><br /> OpenFileDialog<br /><br /> XAML 反序列化（通过 XamlReader.Load）|  
|Web 集成|“浏览器下载”对话框<br /><br /> 顶级用户启动的导航<br /><br /> mailto:links<br /><br /> 统一资源标识符参数<br /><br /> HTTPWebRequest<br /><br /> IFRAME 中承载的 WPF 内容<br /><br /> 使用框架承载同一站点 HTML 页<br /><br /> 使用 WebBrowser 承载同一站点 HTML 页<br /><br /> Web Services \(ASMX\)<br /><br /> Web Services（使用 Windows Communication Foundation）<br /><br /> 脚本<br /><br /> 文档对象模型|  
|视觉效果|二维和三维<br /><br /> 动画<br /><br /> 媒体（源站点和跨域）<br /><br /> 图像处理\/音频\/视频|  
|阅读|FlowDocuments<br /><br /> XPS 文档<br /><br /> 嵌入式字体与系统字体<br /><br /> CFF 字体与 TrueType 字体|  
|编辑|拼写检查<br /><br /> RichTextBox<br /><br /> 纯文本和墨迹剪贴板支持<br /><br /> 用户启动的粘贴<br /><br /> 复制选定内容|  
|控件|常规控件|  
  
 此表包括了高级 [!INCLUDE[TLA2#tla_wpf](../../../includes/tla2sharptla-wpf-md.md)] 功能。  有关更多详细信息，请参见 [!INCLUDE[TLA#tla_lhsdk](../../../includes/tlasharptla-lhsdk-md.md)] 文档，其中介绍了 [!INCLUDE[TLA2#tla_wpf](../../../includes/tla2sharptla-wpf-md.md)] 中的每个成员所需的权限。  此外，以下功能含有关于部分信任执行的详细信息，其中包括特殊注意事项。  
  
-   [!INCLUDE[TLA2#tla_xaml](../../../includes/tla2sharptla-xaml-md.md)]（请参见 [XAML 概述 \(WPF\)](../../../docs/framework/wpf/advanced/xaml-overview-wpf.md)）。  
  
-   弹出（请参见 <xref:System.Windows.Controls.Primitives.Popup?displayProperty=fullName>）。  
  
-   拖放（请参见[拖放概述](../../../docs/framework/wpf/advanced/drag-and-drop-overview.md)）。  
  
-   剪贴板（请参见 <xref:System.Windows.Clipboard?displayProperty=fullName>）。  
  
-   图像处理（请参见 <xref:System.Windows.Controls.Image?displayProperty=fullName>）。  
  
-   序列化（请参见 <xref:System.Windows.Markup.XamlReader.Load%2A?displayProperty=fullName> 和 <xref:System.Windows.Markup.XamlWriter.Save%2A?displayProperty=fullName>）。  
  
-   “打开文件”对话框（请参见 <xref:Microsoft.Win32.OpenFileDialog?displayProperty=fullName>）。  
  
 下表概括了不能在 Internet 区域权限集限制范围内安全运行的 [!INCLUDE[TLA2#tla_wpf](../../../includes/tla2sharptla-wpf-md.md)] 功能。  
  
 表 2：在部分信任环境中不安全的 WPF 功能  
  
|功能区域|功能|  
|----------|--------|  
|常规|窗口（应用程序定义的窗口和对话框）<br /><br /> SaveFileDialog<br /><br /> 文件系统<br /><br /> 注册表访问<br /><br /> 拖放<br /><br /> XAML 序列化（通过 XamlWriter.Save）<br /><br /> UIAutomation 客户端<br /><br /> 源窗口访问 \(HwndHost\)<br /><br /> 完全语音支持<br /><br /> Windows 窗体互操作性|  
|视觉效果|位图效果<br /><br /> 图像编码|  
|编辑|RTF 格式剪贴板<br /><br /> 完全 XAML 支持|  
  
<a name="Partial_Trust_Programming"></a>   
## 部分信任编程  
 对于 [!INCLUDE[TLA2#tla_xbap](../../../includes/tla2sharptla-xbap-md.md)] 应用程序，超出默认权限集的代码将有不同的行为，具体情况视安全区域而定。  在某些情况下，用户将在尝试安装它时收到警告。  用户可以选择继续或取消安装。  下表描述每个安全区域的应用程序的行为，以及您为了使应用程序接收完全信任而必须执行的操作。  
  
|安全区域|行为|获取完全信任|  
|----------|--------|------------|  
|本地计算机|自动完全信任|无需执行任何操作。|  
|Intranet 和可信站点|提示完全信任|使用证书对 XBAP 进行签名，以便用户在提示中看到源。|  
|Internet|失败，并显示“未授予信任”|使用证书对 XBAP 进行签名。|  
  
> [!NOTE]
>  上表中描述的行为针对的是不遵循 ClickOnce 受信任部署模型的完全信任的 XBAP。  
  
 通常，超出允许权限的代码可能是在独立应用程序和以浏览器为宿主的应用程序之间共享的公用代码。  [!INCLUDE[TLA2#tla_cas](../../../includes/tla2sharptla-cas-md.md)] 和 [!INCLUDE[TLA2#tla_wpf](../../../includes/tla2sharptla-wpf-md.md)] 提供了几个用于管理此方案的技巧。  
  
<a name="Detecting_Permissions_using_CAS"></a>   
### 使用 CAS 检测权限  
 在一些情况下，独立应用程序和 [!INCLUDE[TLA2#tla_xbap#plural](../../../includes/tla2sharptla-xbapsharpplural-md.md)] 可能同时使用库程序集中的共享代码。  这时，代码执行的功能所需要的权限可能超出应用程序的授权权限集允许的权限。  通过使用 [!INCLUDE[TLA#tla_winfx](../../../includes/tlasharptla-winfx-md.md)] 安全性，应用程序可以检测它是否具有某个权限。  具体来说，它可以通过在所需权限的实例上调用 <xref:System.Security.CodeAccessPermission.Demand%2A> 方法来测试它是否具有特定权限。  以下示例对此进行了演示，该示例中的代码查询它是否能够将文件保存到本地磁盘：  
  
 [!code-csharp[PartialTrustSecurityOverviewSnippets#DetectPermsCODE1](../../../samples/snippets/csharp/VS_Snippets_Wpf/PartialTrustSecurityOverviewSnippets/CSharp/FileHandling.cs#detectpermscode1)]
 [!code-vb[PartialTrustSecurityOverviewSnippets#DetectPermsCODE1](../../../samples/snippets/visualbasic/VS_Snippets_Wpf/PartialTrustSecurityOverviewSnippets/VisualBasic/FileHandling.vb#detectpermscode1)]  
[!code-csharp[PartialTrustSecurityOverviewSnippets#DetectPermsCODE2](../../../samples/snippets/csharp/VS_Snippets_Wpf/PartialTrustSecurityOverviewSnippets/CSharp/FileHandling.cs#detectpermscode2)]
[!code-vb[PartialTrustSecurityOverviewSnippets#DetectPermsCODE2](../../../samples/snippets/visualbasic/VS_Snippets_Wpf/PartialTrustSecurityOverviewSnippets/VisualBasic/FileHandling.vb#detectpermscode2)]  
  
 如果应用程序不具有所需的权限，则对 <xref:System.Security.CodeAccessPermission.Demand%2A> 的调用将引发安全异常。  如果没有引发异常，则表示已授予该权限。  `IsPermissionGranted` 封装了这一行为，并且根据情况返回 `true` 或 `false`。  
  
<a name="Graceful_Degradation_of_Functionality"></a>   
### 功能下降  
 对于可以从不同区域执行的代码而言，能够检测代码是否具有完成所需操作的权限是很有意义的。  能够检测区域固然不错，但如果能够为用户提供替代方法，则要好得多。  例如，完全信任应用程序通常使用户能够在他们希望的任何地方创建文件，而部分信任应用程序只能在独立存储中创建文件。  如果用于创建文件的代码存在于由完全信任（独立）应用程序和部分信任（以浏览器为宿主）应用程序共享的程序集中，并且这两个应用程序都希望用户能够创建文件，则共享代码应该首先检测它是在部分信任环境还是完全信任环境中运行，然后才能在适当的位置创建文件。  下面的代码对这两种情况进行了演示。  
  
 [!code-csharp[PartialTrustSecurityOverviewSnippets#DetectPermsGracefulCODE1](../../../samples/snippets/csharp/VS_Snippets_Wpf/PartialTrustSecurityOverviewSnippets/CSharp/FileHandlingGraceful.cs#detectpermsgracefulcode1)]
 [!code-vb[PartialTrustSecurityOverviewSnippets#DetectPermsGracefulCODE1](../../../samples/snippets/visualbasic/VS_Snippets_Wpf/PartialTrustSecurityOverviewSnippets/VisualBasic/FileHandlingGraceful.vb#detectpermsgracefulcode1)]  
[!code-csharp[PartialTrustSecurityOverviewSnippets#DetectPermsGracefulCODE2](../../../samples/snippets/csharp/VS_Snippets_Wpf/PartialTrustSecurityOverviewSnippets/CSharp/FileHandlingGraceful.cs#detectpermsgracefulcode2)]
[!code-vb[PartialTrustSecurityOverviewSnippets#DetectPermsGracefulCODE2](../../../samples/snippets/visualbasic/VS_Snippets_Wpf/PartialTrustSecurityOverviewSnippets/VisualBasic/FileHandlingGraceful.vb#detectpermsgracefulcode2)]  
  
 在很多情况下，应该能够找到部分信任替代方法。  
  
 在受控环境（例如 Intranet）中，可以将自定义托管框架安装到整个客户端群的 [!INCLUDE[TLA#tla_gac](../../../includes/tlasharptla-gac-md.md)] 中。  这些库可以执行需要完全信任的代码，并且可以通过使用 <xref:System.Security.AllowPartiallyTrustedCallersAttribute> 从只被授予部分信任的应用程序中引用（有关更多信息，请参见 [安全性](../../../docs/framework/wpf/security-wpf.md)和 [WPF 安全策略 — 平台安全性](../../../docs/framework/wpf/wpf-security-strategy-platform-security.md)）。  
  
<a name="Browser_Host_Detection"></a>   
### 浏览器宿主检测  
 在需要按权限进行检查时，使用 [!INCLUDE[TLA2#tla_cas](../../../includes/tla2sharptla-cas-md.md)] 检查是否具有权限是一种恰当的方法。  然而，这一技巧依赖于在正常处理过程中捕获异常（通常不鼓励这样做），并且可能导致性能问题。  如果 [!INCLUDE[TLA#tla_xbap](../../../includes/tlasharptla-xbap-md.md)] 只在 Internet 区域沙盒内运行，则可以改为使用 <xref:System.Windows.Interop.BrowserInteropHelper.IsBrowserHosted%2A?displayProperty=fullName> 属性（它为 [!INCLUDE[TLA#tla_xbap#plural](../../../includes/tlasharptla-xbapsharpplural-md.md)] 返回 true）。  
  
> [!NOTE]
>  <xref:System.Windows.Interop.BrowserInteropHelper.IsBrowserHosted%2A> 只区分应用程序是否在浏览器中运行，而不区分应用程序正在通过哪个权限集运行。  
  
<a name="Managing_Permissions"></a>   
## 管理权限  
 默认情况下，[!INCLUDE[TLA2#tla_xbap#plural](../../../includes/tla2sharptla-xbapsharpplural-md.md)] 在部分信任环境（默认 Internet 区域权限集）下运行。  但是，根据应用程序的要求，可以更改默认的权限集。  例如，如果 [!INCLUDE[TLA2#tla_xbap#plural](../../../includes/tla2sharptla-xbapsharpplural-md.md)] 是从本地 Intranet 启动的，则可以利用增强的权限集，如下表所示。  
  
 表 3：LocalIntranet 和 Internet 权限  
  
|权限|特性|LocalIntranet|Internet|  
|--------|--------|-------------------|--------------|  
|DNS|访问 DNS 服务器|是|否|  
|环境变量|Read|是|否|  
|文件对话框|打开|是|是|  
|文件对话框|无限制|是|否|  
|独立存储|按用户隔离程序集|是|否|  
|独立存储|未知隔离|是|是|  
|独立存储|无限制用户配额|是|否|  
|媒体|安全音频、视频和图像|是|是|  
|打印|默认打印|是|否|  
|打印|安全打印|是|是|  
|反射|发出|是|否|  
|安全性|托管代码执行|是|是|  
|安全性|声明授予的权限|是|否|  
|用户界面|无限制|是|否|  
|用户界面|安全顶级窗口|是|是|  
|用户界面|自己的剪贴板|是|是|  
|Web 浏览器|HTML 中的安全框架导航|是|是|  
  
> [!NOTE]
>  如果由用户启动，则剪切和粘贴只允许以部分信任方式执行。  
  
 如果需要增加权限，则需要更改项目设置和 ClickOnce 应用程序清单。  有关更多信息，请参见 [WPF XAML 浏览器应用程序概述](../../../docs/framework/wpf/app-development/wpf-xaml-browser-applications-overview.md)。  以下各个文档可能也会有帮助。  
  
-   [Mage.exe（清单生成和编辑工具）](../../../docs/framework/tools/mage-exe-manifest-generation-and-editing-tool.md).  
  
-   [MageUI.exe（图形化客户端中的清单生成和编辑工具）](../../../docs/framework/tools/mageui-exe-manifest-generation-and-editing-tool-graphical-client.md).  
  
-   [保护 ClickOnce 应用程序](../Topic/Securing%20ClickOnce%20Applications.md).  
  
 如果 [!INCLUDE[TLA2#tla_xbap](../../../includes/tla2sharptla-xbap-md.md)] 需要完全信任，则可以使用相同的工具来增加请求的权限，  但只有从本地计算机、Intranet 或从浏览器的受信任或允许网站中列出的 URL 安装和启动 [!INCLUDE[TLA2#tla_xbap](../../../includes/tla2sharptla-xbap-md.md)] 时，它才会得到完全信任。  如果从 Intranet 或受信任网站安装应用程序，则用户将收到标准 ClickOnce 提示，通知用户提升了权限。  用户可以选择继续或取消安装。  
  
 或者，可以使用 ClickOnce 受信任部署模型从任何安全区域中进行完全信任部署。  有关更多信息，请参见[受信任的应用程序部署概述](../Topic/Trusted%20Application%20Deployment%20Overview.md)和 [安全性](../../../docs/framework/wpf/security-wpf.md)。  
  
## 请参阅  
 [安全性](../../../docs/framework/wpf/security-wpf.md)   
 [WPF 安全策略 — 平台安全性](../../../docs/framework/wpf/wpf-security-strategy-platform-security.md)   
 [WPF 安全策略 — 安全工程](../../../docs/framework/wpf/wpf-security-strategy-security-engineering.md)