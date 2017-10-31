---
title: "IWpfHostSupport | Microsoft Docs"
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
  - "IWpfHostSupport 接口"
ms.assetid: cc5a0281-de81-4cc1-87e4-0e46b1a811e9
caps.latest.revision: 8
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 8
---
# IWpfHostSupport
通过 PresentationHost.exe 承载 [!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)] 内容的应用程序实现此接口，以便在宿主与 PresentationHost.exe 之间提供一个集成点。  
  
## 备注  
 诸如 Web 浏览器这样的 [!INCLUDE[TLA#tla_win32](../../../../includes/tlasharptla-win32-md.md)] 应用程序可以承载 [!INCLUDE[TLA#tla_titlewinclient](../../../../includes/tlasharptla-titlewinclient-md.md)] 内容，包括 [!INCLUDE[TLA#tla_xbap#plural](../../../../includes/tlasharptla-xbapsharpplural-md.md)] 和松散 XAML。  为了承载 [!INCLUDE[TLA#tla_titlewinclient](../../../../includes/tlasharptla-titlewinclient-md.md)] 内容，[!INCLUDE[TLA#tla_win32](../../../../includes/tlasharptla-win32-md.md)] 应用程序创建 [WebBrowser control](http://go.microsoft.com/fwlink/?LinkId=97911)（WebBrowser 控件）的一个实例。  为了可被承载，[!INCLUDE[TLA#tla_titlewinclient](../../../../includes/tlasharptla-titlewinclient-md.md)] 创建 PresentationHost.exe 的一个实例，它将承载的 [!INCLUDE[TLA#tla_titlewinclient](../../../../includes/tlasharptla-titlewinclient-md.md)] 内容提供给宿主以显示在 [WebBrowser control](http://go.microsoft.com/fwlink/?LinkId=97911)（WebBrowser 控件）中。  
  
 `IWpfHostSupport` 启用的集成使 PresentationHost.exe 可以：  
  
-   发现宿主应用程序所面向的原始输入设备（智能界面设备）并向它注册。  
  
-   从注册的原始输入设备接收输入消息并将适当的消息转发给宿主应用程序。  
  
-   查询宿主应用程序以获得自定义进度和错误用户界面。  
  
> [!NOTE]
>  此 API 仅专用于本地客户端计算机，并支持在本地客户端计算机上使用  
  
## 成员  
  
|成员|说明|  
|--------|--------|  
|[GetRawInputDevices](../../../../docs/framework/wpf/app-development/getrawinputdevices.md)|使 PresentationHost.exe 可以发现宿主应用程序所面向的原始输入设备（智能界面设备）。|  
|[FilterInputMessage](../../../../docs/framework/wpf/app-development/filterinputmessage.md)|除非返回 E\_NOTIMPL，否则将在收到消息时由 PresentationHost.exe 进行调用。|  
|[GetCustomUI](../../../../docs/framework/wpf/app-development/getcustomui.md)|默认情况下，PresentationHost.exe 提供它自己的部署进度和部署错误用户界面，在部署 WPF 内容后，会显示这些界面。|