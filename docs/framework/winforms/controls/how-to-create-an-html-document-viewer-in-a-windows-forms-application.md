---
title: "如何：在 Windows 窗体应用程序中创建 HTML 文档查看器 | Microsoft Docs"
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
  - "文档查看器"
  - "WebBrowser 控件 [Windows 窗体], 创建 HTML 文档查看器"
  - "Windows 窗体, 创建文档查看器"
ms.assetid: 6a6338fe-f7ee-4f5e-9d8f-0465c57e9039
caps.latest.revision: 12
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 12
---
# 如何：在 Windows 窗体应用程序中创建 HTML 文档查看器
使用 <xref:System.Windows.Forms.WebBrowser> 控件，无需提供 Internet Web 浏览器的完整功能，即可显示和打印 HTML 文档。  如果要利用 HTML 的格式设置功能，但不希望用户加载可能包含不受信任的 Web 控件或可能有恶意的脚本代码的任何网页，这一点十分有用。  例如，可能需要采用这种方式限制 <xref:System.Windows.Forms.WebBrowser> 控件的功能，以便将该控件用作 HTML 电子邮件查看器或在应用程序中提供 HTML 格式的帮助。  
  
### 创建 HTML 文档查看器  
  
1.  将 <xref:System.Windows.Forms.WebBrowser.AllowWebBrowserDrop%2A> 属性设置为 `false` 可防止 <xref:System.Windows.Forms.WebBrowser> 控件打开拖放到其上的文件。  
  
     [!code-csharp[WebBrowserMisc#20](../../../../samples/snippets/csharp/VS_Snippets_Winforms/WebBrowserMisc/CS/WebBrowserMisc.cs#20)]
     [!code-vb[WebBrowserMisc#20](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/WebBrowserMisc/vb/WebBrowserMisc.vb#20)]  
  
2.  将 <xref:System.Windows.Forms.WebBrowser.Url%2A> 属性设置为要显示的初始文件的位置。  
  
     [!code-csharp[WebBrowserMisc#21](../../../../samples/snippets/csharp/VS_Snippets_Winforms/WebBrowserMisc/CS/WebBrowserMisc.cs#21)]
     [!code-vb[WebBrowserMisc#21](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/WebBrowserMisc/vb/WebBrowserMisc.vb#21)]  
  
## 编译代码  
 此示例需要：  
  
-   名为 `webBrowser1` 的 <xref:System.Windows.Forms.WebBrowser> 控件。  
  
-   对 `System` 和 `System.Windows.Forms` 程序集的引用。  
  
## 请参阅  
 <xref:System.Windows.Forms.WebBrowser>   
 <xref:System.Windows.Forms.WebBrowser.AllowWebBrowserDrop%2A>   
 <xref:System.Windows.Forms.WebBrowser.Url%2A>   
 [WebBrowser 控件概述](../../../../docs/framework/winforms/controls/webbrowser-control-overview.md)   
 [WebBrowser 安全](../../../../docs/framework/winforms/controls/webbrowser-security.md)   
 [如何：使用 WebBrowser 控件定位到 URL](../../../../docs/framework/winforms/controls/how-to-navigate-to-a-url-with-the-webbrowser-control.md)   
 [如何：使用 WebBrowser 控件打印](../../../../docs/framework/winforms/controls/how-to-print-with-a-webbrowser-control.md)