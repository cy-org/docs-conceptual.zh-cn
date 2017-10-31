---
title: "支持 .NET 应用程序部署的 Firefox 加载项 | Microsoft Docs"
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
  - ".NET 应用程序部署, 使用 Firefox 加载项部署"
  - ".NET Framework Assistant for Firefox"
  - "用于 .NET 应用程序部署的 Firefox 加载项"
  - "用于 Firefox 的 WPF 插件"
ms.assetid: 2403403b-9b14-48e9-b70d-fa288a3c9081
caps.latest.revision: 22
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 22
---
# 支持 .NET 应用程序部署的 Firefox 加载项
用于 Firefox 的 [!INCLUDE[TLA#tla_wpf](../../../../includes/tlasharptla-wpf-md.md)] 插件和用于 Firefox 的 .NET Framework Assistant 使 [!INCLUDE[TLA#tla_winfxwebapp#plural](../../../../includes/tlasharptla-winfxwebappsharpplural-md.md)]、宽松 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] 以及 ClickOnce 应用程序可以与 Mozilla Firefox 浏览器一起使用。  
  
## 用于 Firefox 的 WPF 插件  
 用于 Firefox 的 WPF 插件使 [!INCLUDE[TLA2#tla_xbap#plural](../../../../includes/tla2sharptla-xbapsharpplural-md.md)] 和宽松 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] 文件可以在 Firefox 浏览器中的顶层或 HTML IFRAME 中进行导航和运行。  [!INCLUDE[TLA2#tla_xbap](../../../../includes/tla2sharptla-xbap-md.md)] 是可发布到 Web 服务器并在支持的浏览器中启动的 [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] 应用程序。  宽松 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] 是可以在支持的浏览器中进行导航和显示的仅使用 XAML 的文件，与 XML 文件非常相似。  
  
 用于 Firefox 的 [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] 插件随 [!INCLUDE[net_v35_short](../../../../includes/net-v35-short-md.md)] 一起安装。  Window 7 包含 [!INCLUDE[net_v35_short](../../../../includes/net-v35-short-md.md)]，但不包含用于 Firefox 的 [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] 插件。不能在 Window 7 上安装用于 Firefox 的 [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] 插件。  
  
 [!INCLUDE[net_v40_short](../../../../includes/net-v40-short-md.md)] 不包含用于 Firefox 的 [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] 插件。不过，如果安装了 [!INCLUDE[net_v35_short](../../../../includes/net-v35-short-md.md)] 和 [!INCLUDE[net_v40_short](../../../../includes/net-v40-short-md.md)]，则用于 Firefox 的 WPF 插件会随 [!INCLUDE[net_v35_short](../../../../includes/net-v35-short-md.md)] 一起安装。  因此，[!INCLUDE[net_v40_short](../../../../includes/net-v40-short-md.md)] 应用程序仍将运行，因为 WPF 主机将加载正确版本的 Framework。  有关更多信息，请参见 [WPF 主机 \(PresentationHost.exe\)](../../../../docs/framework/wpf/app-development/wpf-host-presentationhost-exe.md)。  
  
## 用于 Firefox 的 .NET Framework Assistant  
 用于 Firefox 的 .NET Framework Assistant 使独立 ClickOnce 应用程序可以在 Firefox 浏览器运行。  用于 Firefox 的 .NET Framework Assistant 在 Firefox 浏览器之前和之后安装时的功能是相同的。  Firefox 浏览器启动并且 [!INCLUDE[net_v35SP1_short](../../../../includes/net-v35sp1-short-md.md)] 已安装时，Firefox 会查找并安装用于 Firefox 的 .NET Framework Assistant。  用户可以配置用于 Firefox 的 .NET Framework Assistant 以执行以下任务：  
  
-   在运行 ClickOnce 应用程序前进行提示。  
  
-   报告所有已安装的 .NET Framework 版本或仅报告最新版本。  
  
 用于 Firefox 的 .NET Framework Assistant 随 [!INCLUDE[net_v35SP1_short](../../../../includes/net-v35sp1-short-md.md)] 一起提供。  有关如何移除用于 Firefox 的 .NET Framework Assistant 的信息，请参见 [How to remove the .NET Framework Assistant for Firefox](http://go.microsoft.com/fwlink/?LinkId=177944)（如何移除用于 Firefox 的 .NET Framework Assistant）。  
  
## 请参阅  
 [部署 WPF 应用程序](../../../../docs/framework/wpf/app-development/deploying-a-wpf-application-wpf.md)   
 [WPF XAML 浏览器应用程序概述](../../../../docs/framework/wpf/app-development/wpf-xaml-browser-applications-overview.md)   
 [检测是否已安装 Firefox 的 WPF 插件](../../../../docs/framework/wpf/app-development/how-to-detect-whether-the-wpf-plug-in-for-firefox-is-installed.md)