---
title: "部署 WPF 应用程序 (WPF) | Microsoft Docs"
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
  - "部署 [WPF], 应用程序"
  - "WPF 应用程序, 部署"
ms.assetid: 12cadca0-b32c-4064-9a56-e6a306dcc76d
caps.latest.revision: 27
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 26
---
# 部署 WPF 应用程序 (WPF)
生成 [!INCLUDE[TLA#tla_wpf](../../../../includes/tlasharptla-wpf-md.md)] 应用程序后，需要对它们进行部署。  [!INCLUDE[TLA#tla_mswin](../../../../includes/tlasharptla-mswin-md.md)] 和 [!INCLUDE[TLA2#tla_winfx](../../../../includes/tla2sharptla-winfx-md.md)] 包含一些部署技术。  用于部署 [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] 应用程序的部署技术取决于应用程序类型。  本主题简要概述了每个部署技术，以及它们如何用于满足每个 [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] 应用程序类型的部署要求。  
  
   
  
<a name="Deployment_Technologies"></a>   
## 部署技术  
 [!INCLUDE[TLA#tla_mswin](../../../../includes/tlasharptla-mswin-md.md)] 和 [!INCLUDE[TLA2#tla_winfx](../../../../includes/tla2sharptla-winfx-md.md)] 包含一些部署技术，其中包括：  
  
-   XCopy 部署。  
  
-   [!INCLUDE[TLA2#tla_wininstall](../../../../includes/tla2sharptla-wininstall-md.md)] 部署。  
  
-   [!INCLUDE[TLA#tla_clickonce](../../../../includes/tlasharptla-clickonce-md.md)] 部署。  
  
<a name="XCopy_Deployment"></a>   
### XCopy 部署  
 XCopy 部署指使用 XCopy 命令行程序将文件从一个位置复制到另一个位置。  在下列情况下，适合使用 XCopy 部署：  
  
-   应用程序是独立的。  它不需要更新客户端来运行。  
  
-   应用程序文件必须从一个位置移动到另一个位置，例如从生成位置（本地磁盘、[!INCLUDE[TLA2#tla_unc](../../../../includes/tla2sharptla-unc-md.md)] 文件共享等）移动到发布位置（网站、[!INCLUDE[TLA2#tla_unc](../../../../includes/tla2sharptla-unc-md.md)] 文件共享等）。  
  
-   应用程序不需要 shell 集成（“开始”菜单快捷方式、桌面图标等）。  
  
 XCopy 适用于简单的部署情况，当要求更复杂的部署功能时它就无法满足要求了。  特别是，使用 XCopy 通常会增加为了以可靠方式管理部署而创建、执行和维护脚本方面的系统开销。  而且，XCopy 不支持版本管理、卸载或回滚。  
  
<a name="Windows_Installer"></a>   
### Windows Installer  
 [!INCLUDE[TLA2#tla_wininstall](../../../../includes/tla2sharptla-wininstall-md.md)] 允许应用程序打包为独立的可执行程序，它们可以容易地分发到客户端并运行。  而且，[!INCLUDE[TLA2#tla_wininstall](../../../../includes/tla2sharptla-wininstall-md.md)] 随 [!INCLUDE[TLA#tla_mswin](../../../../includes/tlasharptla-mswin-md.md)] 安装，从而能与桌面、“开始”菜单和“程序”控制面板集成。  
  
 [!INCLUDE[TLA2#tla_wininstall](../../../../includes/tla2sharptla-wininstall-md.md)] 简化了应用程序的安装和卸载，但是从版本管理的角度看，它无法提供功能来确保安装的应用程序是最新的。  
  
 有关 [!INCLUDE[TLA2#tla_wininstall](../../../../includes/tla2sharptla-wininstall-md.md)]的更多信息，请参见[Windows Installer Deployment](http://msdn.microsoft.com/zh-cn/121be21b-b916-43e2-8f10-8b080516d2a0)。  
  
<a name="ClickOnce_Deployment"></a>   
### ClickOnce 部署  
 [!INCLUDE[TLA2#tla_clickonce](../../../../includes/tla2sharptla-clickonce-md.md)] 为非 Web 应用程序实现 Web 风格的应用程序部署。应用程序将发布到 Web 服务器或文件服务器，并从中部署。  虽然 [!INCLUDE[TLA2#tla_clickonce](../../../../includes/tla2sharptla-clickonce-md.md)] 不完全支持 [!INCLUDE[TLA2#tla_wininstall](../../../../includes/tla2sharptla-wininstall-md.md)] 安装的应用程序所支持的全部客户端功能，但它支持其中一部分功能，包括以下各项：  
  
-   与“开始”菜单和“程序”控制面板的集成。  
  
-   版本控制、回滚和卸载。  
  
-   联机安装模式，该模式始终从部属位置启动应用程序。  
  
-   在新版本发布后自动更新。  
  
-   文件扩展名注册。  
  
 有关 [!INCLUDE[TLA2#tla_clickonce](../../../../includes/tla2sharptla-clickonce-md.md)]的更多信息，请参见[ClickOnce 安全和部署](../Topic/ClickOnce%20Security%20and%20Deployment.md)。  
  
<a name="Deploying_WPF_Applications"></a>   
## 部署 WPF 应用程序  
 [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] 应用程序的部署选项取决于应用程序的类型。  从部署角度来看，[!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] 有三种重要的应用程序类型：  
  
-   独立应用程序。  
  
-   仅标记 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] 应用程序。  
  
-   [!INCLUDE[TLA#tla_xbap#plural](../../../../includes/tlasharptla-xbapsharpplural-md.md)].  
  
<a name="Deploying_Standalone_Applications"></a>   
### 部署独立应用程序  
 独立应用程序是使用 [!INCLUDE[TLA#tla_clickonce](../../../../includes/tlasharptla-clickonce-md.md)] 或 [!INCLUDE[TLA2#tla_wininstall](../../../../includes/tla2sharptla-wininstall-md.md)] 部署的。  不论是用哪种方式，独立应用程序都需要以完全信任的方式运行。  完全信任会自动授予给使用 [!INCLUDE[TLA2#tla_wininstall](../../../../includes/tla2sharptla-wininstall-md.md)] 部署的独立应用程序。  完全信任不会自动授予给使用 [!INCLUDE[TLA2#tla_clickonce](../../../../includes/tla2sharptla-clickonce-md.md)] 部署的独立应用程序。  [!INCLUDE[TLA2#tla_clickonce](../../../../includes/tla2sharptla-clickonce-md.md)] 会显示一个安全警告对话框，用户必须接受才能安装独立应用程序。  如果用户接受，则独立应用程序会安装，并被授予完全信任。  如果用户不接受，则不会安装独立应用程序。  
  
<a name="Deploying_Markup_Only_XAML_Applications"></a>   
### 部署仅标记 XAML 应用程序  
 仅标记 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] 页通常发布到 Web 服务器，并且类似于 [!INCLUDE[TLA2#tla_html](../../../../includes/tla2sharptla-html-md.md)] 页，可以使用 [!INCLUDE[TLA2#tla_iegeneric](../../../../includes/tla2sharptla-iegeneric-md.md)] 查看。  仅标记 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] 页使用 Internet 区域权限集定义的限制在部分信任安全沙盒中运行。  这提供了与基于 [!INCLUDE[TLA2#tla_html](../../../../includes/tla2sharptla-html-md.md)] Web 应用程序等效的安全沙盒。  
  
 有关 [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] 应用程序的安全性的更多信息，请参见 [安全性](../../../../docs/framework/wpf/security-wpf.md)。  
  
 可以使用 XCopy 或 [!INCLUDE[TLA2#tla_wininstall](../../../../includes/tla2sharptla-wininstall-md.md)] 将仅标记 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] 页安装到本地文件系统。  可以使用 [!INCLUDE[TLA2#tla_iegeneric](../../../../includes/tla2sharptla-iegeneric-md.md)] 或 [!INCLUDE[TLA2#tla_mswin](../../../../includes/tla2sharptla-mswin-md.md)] 资源管理器来查看这些页。  
  
 有关 XAML 的更多信息，请参见 [XAML 概述 \(WPF\)](../../../../docs/framework/wpf/advanced/xaml-overview-wpf.md)。  
  
<a name="Deploying_XAML_Browser_Applications"></a>   
### 部署 XAML 浏览器应用程序  
 [!INCLUDE[TLA2#tla_xbap#plural](../../../../includes/tla2sharptla-xbapsharpplural-md.md)] 是已编译的应用程序，需要部署下列三个文件：  
  
-   *应用程序名称*.exe：可执行程序集应用程序文件。  
  
-   *应用程序名称*.xbap：部署清单。  
  
-   *应用程序名称*.exe.manifest：应用程序清单。  
  
> [!NOTE]
>  有关部署和应用程序清单的更多信息，请参见[生成 WPF 应用程序](../../../../docs/framework/wpf/app-development/building-a-wpf-application-wpf.md)。  
  
 这些文件是在生成 [!INCLUDE[TLA2#tla_xbap](../../../../includes/tla2sharptla-xbap-md.md)] 时生成的。  有关更多信息，请参见[如何：创建新的 WPF 浏览器应用程序项目](http://msdn.microsoft.com/zh-cn/72ef4d90-e163-42a1-8df0-ea7ccfd1901f)。  与仅标记 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] 页类似，[!INCLUDE[TLA2#tla_xbap#plural](../../../../includes/tla2sharptla-xbapsharpplural-md.md)] 通常发布到 Web 服务器，可使用 [!INCLUDE[TLA2#tla_iegeneric](../../../../includes/tla2sharptla-iegeneric-md.md)] 查看。  
  
 可以使用任何部署技术将 [!INCLUDE[TLA2#tla_xbap#plural](../../../../includes/tla2sharptla-xbapsharpplural-md.md)] 部署到客户端。  但是，建议使用 [!INCLUDE[TLA#tla_clickonce](../../../../includes/tlasharptla-clickonce-md.md)]，因为它提供了以下功能：  
  
1.  当新版本发布时自动更新。  
  
2.  为以完全信任方式运行的 [!INCLUDE[TLA2#tla_xbap](../../../../includes/tla2sharptla-xbap-md.md)] 提升权限。  
  
 默认情况下，ClickOnce 用 .deploy 扩展名发布应用程序文件。  这可能会出现问题，但可以禁用。  有关更多信息，请参见 [ClickOnce 部署中的服务器和客户端配置问题](../Topic/Server%20and%20Client%20Configuration%20Issues%20in%20ClickOnce%20Deployments.md)。  
  
 有关部署 [!INCLUDE[TLA#tla_xbap#plural](../../../../includes/tlasharptla-xbapsharpplural-md.md)] 的更多信息，请参见 [WPF XAML 浏览器应用程序概述](../../../../docs/framework/wpf/app-development/wpf-xaml-browser-applications-overview.md)。  
  
<a name="Installing__NET_Framework_3_0"></a>   
## 安装 .NET Framework  
 必须在客户端上安装 [!INCLUDE[TLA#tla_winfx](../../../../includes/tlasharptla-winfx-md.md)] 才能运行 [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] 应用程序。  当查看 [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] 浏览器承载的应用程序时，[!INCLUDE[TLA2#tla_ie](../../../../includes/tla2sharptla-ie-md.md)] 会自动检测客户端是否安装了 [!INCLUDE[TLA2#tla_winfx](../../../../includes/tla2sharptla-winfx-md.md)]。  如果未安装 [!INCLUDE[TLA2#tla_winfx](../../../../includes/tla2sharptla-winfx-md.md)]，[!INCLUDE[TLA2#tla_ie](../../../../includes/tla2sharptla-ie-md.md)] 将提示用户进行安装。  
  
 为了检测是否安装了 [!INCLUDE[TLA2#tla_winfx](../../../../includes/tla2sharptla-winfx-md.md)]，[!INCLUDE[TLA2#tla_ie](../../../../includes/tla2sharptla-ie-md.md)] 包含一个引导应用程序，它注册为内容文件的回退[!INCLUDE[TLA#tla_mime](../../../../includes/tlasharptla-mime-md.md)] 处理程序，具有以下扩展名：.xaml、.xps、.xbap 和 .application。  如果导航到这些文件类型，并且客户端上未安装 [!INCLUDE[TLA2#tla_winfx](../../../../includes/tla2sharptla-winfx-md.md)]，则引导应用程序会请求安装它的权限。  如果没有提供权限，就不会安装 [!INCLUDE[TLA2#tla_winfx](../../../../includes/tla2sharptla-winfx-md.md)] 或应用程序。  
  
 如果授予了权限，[!INCLUDE[TLA2#tla_ie](../../../../includes/tla2sharptla-ie-md.md)] 会使用 [!INCLUDE[TLA#tla_bits](../../../../includes/tlasharptla-bits-md.md)] 下载并安装 [!INCLUDE[TLA2#tla_winfx](../../../../includes/tla2sharptla-winfx-md.md)]。  成功安装 [!INCLUDE[TLA2#tla_winfx](../../../../includes/tla2sharptla-winfx-md.md)] 后，会在新浏览器窗口中打开原始请求的文件。  
  
 在已安装 [!INCLUDE[TLA2#tla_ie7](../../../../includes/tla2sharptla-ie7-md.md)] 或更高版本的 [!INCLUDE[TLA#tla_longhorn](../../../../includes/tlasharptla-longhorn-md.md)]、[!INCLUDE[TLA#tla_winxpsp2](../../../../includes/tlasharptla-winxpsp2-md.md)] 和 [!INCLUDE[TLA#tla_winnetsvrfamsp1](../../../../includes/tlasharptla-winnetsvrfamsp1-md.md)] 客户端上提供了 [!INCLUDE[TLA2#tla_winfx](../../../../includes/tla2sharptla-winfx-md.md)] 自动检测。  
  
 有关更多信息，请参见[部署 .NET Framework 和应用程序](../../../../docs/framework/deployment/net-framework-and-applications.md)。  
  
## 请参阅  
 [生成 WPF 应用程序](../../../../docs/framework/wpf/app-development/building-a-wpf-application-wpf.md)   
 [安全性](../../../../docs/framework/wpf/security-wpf.md)