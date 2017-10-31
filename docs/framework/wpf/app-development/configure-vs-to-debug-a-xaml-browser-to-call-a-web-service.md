---
title: "如何：配置 Visual Studio 以调试 XAML 浏览器应用程序来调用 Web 服务 | Microsoft Docs"
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
  - "配置 Visual Studio 以调试 XAML 浏览器应用程序 [WPF]"
  - "配置 Visual Studio 以调试 XBAP [WPF]"
  - "调试 XBAP 的安全异常 [WPF]"
  - "调试调用 Web 服务的 XBAP [WPF]"
  - "XBAP 的安全异常 [WPF], 调试"
ms.assetid: fd1db082-a7bb-4c4b-9331-6ad74a0682d0
caps.latest.revision: 9
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 9
---
# 如何：配置 Visual Studio 以调试 XAML 浏览器应用程序来调用 Web 服务
[!INCLUDE[TLA#tla_xbap#plural](../../../../includes/tlasharptla-xbapsharpplural-md.md)] 在一个限于 Internet 区域权限集的部分信任的安全沙盒中运行。  此权限集将 Web 服务调用限于仅位于 [!INCLUDE[TLA2#tla_xbap](../../../../includes/tla2sharptla-xbap-md.md)] 应用程序源站点的 Web 服务。  但是，当在 [!INCLUDE[TLA#tla_visualstu2005](../../../../includes/tlasharptla-visualstu2005-md.md)] 中调试 [!INCLUDE[TLA2#tla_xbap](../../../../includes/tla2sharptla-xbap-md.md)] 时，并不将其视为具有与其引用的 Web 服务相同的源站点。  当 [!INCLUDE[TLA2#tla_xbap](../../../../includes/tla2sharptla-xbap-md.md)] 尝试调用 Web 服务时，这将导致引发安全异常。  但是，可以配置 [!INCLUDE[TLA#tla_visualstu2005](../../../../includes/tlasharptla-visualstu2005-md.md)] [!INCLUDE[TLA#tla_wpfbrowserappproj](../../../../includes/tlasharptla-wpfbrowserappproj-md.md)] 项目以在调试时模拟与其调用的 Web 服务具有相同的站点。  这允许 [!INCLUDE[TLA2#tla_xbap](../../../../includes/tla2sharptla-xbap-md.md)] 安全地调用 Web 服务，而不导致安全异常。  
  
## 配置 Visual Studio  
 若要配置 [!INCLUDE[TLA#tla_visualstu2005](../../../../includes/tlasharptla-visualstu2005-md.md)] 以对调用 Web 服务的 [!INCLUDE[TLA2#tla_xbap](../../../../includes/tla2sharptla-xbap-md.md)] 进行调试，请执行以下操作：  
  
1.  在**“解决方案资源管理器”**中选定一个项目，然后在**“项目”**菜单中单击**“属性”**。  
  
2.  在**“项目设计器”**中，单击**“调试”**选项卡。  
  
3.  在**“启动操作”**部分中选择**“启动外部程序”**，然后输入以下内容：  
  
     `C:\WINDOWS\System32\PresentationHost.exe`  
  
4.  在**“启动选项”**部分的**“命令行参数”**文本框中输入以下内容：  
  
     `-debug`  *filename*  
  
     **\-debug** 参数的 *filename* 值是 .xbap 文件名，例如：  
  
     `-debug c:\example.xbap`  
  
> [!NOTE]
>  这是使用 [!INCLUDE[TLA2#tla_visualstu2005](../../../../includes/tla2sharptla-visualstu2005-md.md)] [!INCLUDE[TLA#tla_wpfbrowserappproj](../../../../includes/tlasharptla-wpfbrowserappproj-md.md)] 项目模板创建的解决方案的默认配置。  
  
1.  在**“解决方案资源管理器”**中选定一个项目，然后在**“项目”**菜单中单击**“属性”**。  
  
2.  在**“项目设计器”**中，单击**“调试”**选项卡。  
  
3.  在**“启动选项”**部分，请将以下命令行参数添加到**“命令行参数”**文本框：  
  
     `-debugSecurityZoneURL`  *URL*  
  
     **\-debugSecurityZoneURL** 参数的 *URL* 值是需要模拟为应用程序源站点位置的 [!INCLUDE[TLA#tla_url](../../../../includes/tlasharptla-url-md.md)]。  
  
 例如，请考虑使用具有以下 [!INCLUDE[TLA2#tla_url](../../../../includes/tla2sharptla-url-md.md)] 的 Web 服务的 [!INCLUDE[TLA#tla_xbap](../../../../includes/tlasharptla-xbap-md.md)]：  
  
 `http://services.msdn.microsoft.com/ContentServices/ContentService.asmx`  
  
 此 Web 服务的源站点 [!INCLUDE[TLA2#tla_url](../../../../includes/tla2sharptla-url-md.md)] 为：  
  
 `http://services.msdn.microsoft.com`  
  
 因此，完整的 **\-debugSecurityZoneURL** 命令行参数和值为：  
  
 `-debugSecurityZoneURL http://services.msdn.microsoft.com`  
  
## 请参阅  
 [WPF 主机 \(PresentationHost.exe\)](../../../../docs/framework/wpf/app-development/wpf-host-presentationhost-exe.md)