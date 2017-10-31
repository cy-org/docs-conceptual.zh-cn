---
title: "WPF 主机 (PresentationHost.exe) | Microsoft Docs"
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
  - "PresentationHost.exe"
  - "WPF 宿主应用程序"
ms.assetid: 3215bfa1-722c-4ac8-a7c5-bdd02d30afbd
caps.latest.revision: 14
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 12
---
# WPF 主机 (PresentationHost.exe)
[!INCLUDE[TLA#tla_wpf](../../../../includes/tlasharptla-wpf-md.md)] 宿主 \(PresentationHost.exe\) 是一个应用程序，它使 [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] 应用程序可承载于兼容的浏览器（包括 [!INCLUDE[TLA#tla_ie6](../../../../includes/tlasharptla-ie6-md.md)] 及更高版本）中。  在默认情况下，[!INCLUDE[TLA#tla_wpf](../../../../includes/tlasharptla-wpf-md.md)] 主机注册为浏览器承载的 [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] 内容的 shell 和 [!INCLUDE[TLA2#tla_mime](../../../../includes/tla2sharptla-mime-md.md)] 处理程序，包括：  
  
-   松散（未编译）[!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] 文件 \(.xaml\)。  
  
-   [!INCLUDE[TLA#tla_xbap](../../../../includes/tlasharptla-xbap-md.md)] \(.xbap\)。  
  
 对于这些文件类型，[!INCLUDE[TLA#tla_wpf](../../../../includes/tlasharptla-wpf-md.md)] 主机：  
  
-   启动注册的 [!INCLUDE[TLA2#tla_html](../../../../includes/tla2sharptla-html-md.md)] 处理程序来承载 [!INCLUDE[TLA#tla_wpf](../../../../includes/tlasharptla-wpf-md.md)] 内容。  
  
-   加载所需[!INCLUDE[TLA#tla_clr](../../../../includes/tlasharptla-clr-md.md)] 和 [!INCLUDE[TLA#tla_wpf](../../../../includes/tlasharptla-wpf-md.md)] 程序集的正确版本。  
  
-   确保部署所在区域具有适当的权限级别。  
  
 本主题介绍了可以与 PresentationHost.exe 一起使用的命令行参数。  
  
## 用法  
 `PresentationHost.exe [parameters] uri|filename`  
  
## 参数  
  
|Parameter|说明|  
|---------------|--------|  
|filename|要激活的文件的路径，  也可以为 [!INCLUDE[TLA2#tla_uri](../../../../includes/tla2sharptla-uri-md.md)]。|  
|\-debug|当激活应用程序时，请勿从存储区中提交或运行它。  此限制仅在激活本地文件时起作用。|  
|\-debugSecurityZoneURL \<url\>|与 [!INCLUDE[TLA2#tla_url](../../../../includes/tla2sharptla-url-md.md)] 值一起用来向 PresentationHost.exe 表明：由于将应用程序视为是从指定的 [!INCLUDE[TLA2#tla_url](../../../../includes/tla2sharptla-url-md.md)] 部署的，因此应该调试该应用程序。  这将确定部署区域和原始站点。|  
|\-embedding|OLE 需要该参数。  如果指定了 `-event` 或 `-debug` 参数，则不必指定 `-embedding` 参数，因为该参数已在内部设置。|  
|\-event \<事件名\>|打开具有此名称的事件，并在 PresentationHost.exe 初始化并准备承载 [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] 内容时向该事件发出信号。  如果打开事件时发生错误（如该事件还未创建），则 PresentationHost.exe 将终止。|  
|\-launchApplication \<url\>|从指定 URL 启动独立的 [!INCLUDE[ndptecclick](../../../../includes/ndptecclick-md.md)] 应用程序。  将应用与 .NET 应用程序相关的 [!INCLUDE[TLA2#tla_iegeneric](../../../../includes/tla2sharptla-iegeneric-md.md)] 和 WinINet 安全策略。|  
  
## 方案  
  
### shell 处理程序  
 `PresentationHost.exe example.xbap`  
  
### MIME 处理程序  
 `PresentationHost.exe -embedding example.xbap`  
  
### Visual Studio 调试  
 `PresentationHost.exe -debug example.xbap`  
  
### 在区域中进行 Visual Studio 调试  
 `PresentationHost.exe -debug -debugSecurityZoneURL http://www.example.com c:\folderpath\example.xbap`  
  
## 请参阅  
 [安全性](../../../../docs/framework/wpf/security-wpf.md)