---
title: "如何：检测是否已安装 Firefox 的 WPF 插件 | Microsoft Docs"
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
  - "检查 Firefox 插件 [WPF]"
  - "检测 Firefox 安装 [WPF]"
  - "检测是否安装了 Firefox 的 WPF 插件 [WPF]"
  - "Firefox [WPF], 检测安装"
  - "Firefox 的插件 [WPF]"
ms.assetid: 5f839373-e3fb-44f1-88ad-4a0761f02189
caps.latest.revision: 9
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 9
---
# 如何：检测是否已安装 Firefox 的 WPF 插件
Firefox 的 [!INCLUDE[TLA#tla_wpf](../../../../includes/tlasharptla-wpf-md.md)] 插件使 [!INCLUDE[TLA#tla_xbap#plural](../../../../includes/tlasharptla-xbapsharpplural-md.md)] 和松散 XAML 文件能够在 Mozilla Firefox 浏览器中运行。  本主题提供一个以 HTML 和 JavaScript 编写的脚本，管理员可以使用该脚本确定是否安装了 Firefox 的 WPF 插件。  
  
> [!NOTE]
>  有关安装、部署和检测 [!INCLUDE[dnprdnshort](../../../../includes/dnprdnshort-md.md)] 的更多信息，请参见[安装 .NET Framework](../../../../docs/framework/install/guide-for-developers.md)。  
  
## 示例  
 在安装 [!INCLUDE[net_v35_short](../../../../includes/net-v35-short-md.md)] 时，客户端计算机将配置为带有 Firefox 的 WPF 插件。  下面的示例脚本将检查是否有 Firefox 的 WPF 插件，然后显示相应的状态消息。  
  
```  
<HTML>  
  
  <HEAD>  
    <TITLE>Test for the WPF plug-in for Firefox</TITLE>  
    <META HTTP-EQUIV="Content-Type" CONTENT="text/html; charset=utf-8" />  
    <SCRIPT type="text/javascript">  
    <!--  
    function OnLoad()  
    {  
  
       // Check for the WPF plug-in for Firefox and report  
       var msg = "The WPF plug-in for Firefox is ";  
       var wpfPlugin = navigator.plugins["Windows Presentation Foundation"];  
       if( wpfPlugin != null ) {  
          document.writeln(msg + " installed.");  
       }  
       else {  
          document.writeln(msg + " not installed. Please install or reinstall the .NET Framework 3.5.");  
       }  
    }  
    -->  
    </SCRIPT>  
  </HEAD>  
  
  <BODY onload="OnLoad()" />  
  
</HTML>  
```  
  
 如果检查 Firefox 的 WPF 插件的操作成功，则会显示以下状态消息：  
  
 `The WPF plug-in for Firefox is installed.`  
  
 否则，将显示以下状态消息：  
  
 `The WPF plug-in for Firefox is not installed.  Please install or reinstall the .NET Framework 3.5.`  
  
## 请参阅  
 [检测是否安装了 .NET Framework 3.0](../../../../docs/framework/wpf/app-development/how-to-detect-whether-the-net-framework-3-0-is-installed.md)   
 [检测是否安装了 .NET Framework 3.5](../../../../docs/framework/wpf/app-development/how-to-detect-whether-the-net-framework-3-5-is-installed.md)   
 [WPF XAML 浏览器应用程序概述](../../../../docs/framework/wpf/app-development/wpf-xaml-browser-applications-overview.md)