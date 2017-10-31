---
title: "WebBrowser 安全 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-winforms"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "jsharp"
helpviewer_keywords: 
  - "安全性 [Windows 窗体], WebBrowser 控件"
  - "WebBrowser 控件 [Windows 窗体], 安全性"
ms.assetid: 0968846e-48ee-485a-9797-65b5b9a622f8
caps.latest.revision: 13
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 13
---
# WebBrowser 安全
<xref:System.Windows.Forms.WebBrowser> 控件仅用于在完全信任模式下工作。  该控件中显示的 HTML 内容可以来自外部 Web 服务器，并且可能包含脚本或 Web 控件形式的非托管代码。  在这种情况下，使用 <xref:System.Windows.Forms.WebBrowser> 控件的安全性不比使用 Internet Explorer 低，但是托管的 <xref:System.Windows.Forms.WebBrowser> 控件不会阻止此类非托管代码运行。  
  
 有关与基础 ActiveX `WebBrowser` 控件相关的安全问题的更多信息，请参见[WebBrowser Control](http://go.microsoft.com/fwlink/?LinkId=198812)（WebBrowser 控件）。  
  
## 请参阅  
 <xref:System.Windows.Forms.WebBrowser>   
 [WebBrowser 控件概述](../../../../docs/framework/winforms/controls/webbrowser-control-overview.md)   
 [WebBrowser Control](http://go.microsoft.com/fwlink/?LinkId=198812)