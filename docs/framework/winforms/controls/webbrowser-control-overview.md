---
title: "WebBrowser 控件概述 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-winforms"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "WebBrowser"
dev_langs: 
  - "jsharp"
helpviewer_keywords: 
  - "网页, 在应用程序中显示"
  - "WebBrowser 控件 [Windows 窗体], 关于"
ms.assetid: 6e3e1cc2-9c48-4136-9659-e99e4e60b7e9
caps.latest.revision: 15
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 15
---
# WebBrowser 控件概述
<xref:System.Windows.Forms.WebBrowser> 控件为 WebBrowser ActiveX 控件提供了托管包装。  托管包装使您可以在 Windows 窗体客户端应用程序中显示网页。  使用 <xref:System.Windows.Forms.WebBrowser> 控件，可以复制应用程序中的 Internet Explorer Web 浏览功能，还可以禁用默认的 Internet Explorer 功能，并将该控件用作简单的 HTML 文档查看器。  此外，可以使用该控件将基于 DHTML 的用户界面元素添加到窗体中，还可以隐瞒这些元素在 <xref:System.Windows.Forms.WebBrowser> 控件中承载的事实。  通过这种方法，可以将 Web 控件和 Windows 窗体控件无缝地整合到一个应用程序中。  
  
## 常用的属性、方法和事件  
 <xref:System.Windows.Forms.WebBrowser> 控件包含多种可以用来实现 Internet Explorer 中的控件的属性、方法和事件。  例如，可以使用 `Navigate` 方法实现地址栏，使用 `GoBack`、`GoForward`、`Stop` 和 `Refresh` 方法实现工具栏中的导航按钮。  可以处理 `Navigated` 事件，以便使用 `Url` 属性的值更新地址栏，使用 `DocumentTitle` 属性的值更新标题栏。  
  
 如果想要在应用程序中生成自己的页面内容，可以设置 `DocumentText` 属性。  如果熟悉 HTML 文档对象模型 \(DOM\)，还可以通过 `Document` 属性操作当前网页的内容。  通过此属性，您可以将文档存储在内存中来修改文档，而不用在文件间进行导航。  
  
 此外，使用 `Document` 属性，可以从客户端应用程序代码调用网页脚本代码中实现的方法。  若要从脚本代码访问客户端应用程序代码，请设置 `ObjectForScripting` 属性。  脚本代码可以将指定的对象作为 `window.external` 对象访问。  
  
|名称|说明|  
|--------|--------|  
|<xref:System.Windows.Forms.WebBrowser.Document%2A> 属性|获取一个对象，用于提供对当前网页的 HTML 文档对象模型 \(DOM\) 的托管访问。|  
|<xref:System.Windows.Forms.WebBrowser.DocumentCompleted> 事件|网页完成加载时发生。|  
|<xref:System.Windows.Forms.WebBrowser.DocumentText%2A> 属性|获取或设置当前网页的 HTML 内容。|  
|<xref:System.Windows.Forms.WebBrowser.DocumentTitle%2A> 属性|获取当前网页的标题。|  
|<xref:System.Windows.Forms.WebBrowser.GoBack%2A> 方法|定位到历史记录中的上一页。|  
|<xref:System.Windows.Forms.WebBrowser.GoForward%2A> 方法|定位到历史记录中的下一页。|  
|<xref:System.Windows.Forms.WebBrowser.Navigate%2A> 方法|定位到指定的 URL。|  
|<xref:System.Windows.Forms.WebBrowser.Navigating> 事件|导航开始之前发生，使操作可以被取消。|  
|<xref:System.Windows.Forms.WebBrowser.ObjectForScripting%2A> 属性|获取或设置网页脚本代码可以用来与应用程序进行通信的对象。|  
|<xref:System.Windows.Forms.WebBrowser.Print%2A> 方法|打印当前的网页。|  
|<xref:System.Windows.Forms.WebBrowser.Refresh%2A> 方法|重新加载当前的网页。|  
|<xref:System.Windows.Forms.WebBrowser.Stop%2A> 方法|暂停当前的导航，停止动态页元素，如声音和动画。|  
|<xref:System.Windows.Forms.WebBrowser.Url%2A> 属性|获取或设置当前网页的 URL。  设置该属性时，会将该控件定位到新的 URL。|  
  
## 请参阅  
 <xref:System.Windows.Forms.WebBrowser>   
 <xref:System.Windows.Forms.WebBrowserDocumentCompletedEventArgs>   
 <xref:System.Windows.Forms.WebBrowserDocumentCompletedEventHandler>   
 <xref:System.Windows.Forms.WebBrowserEncryptionLevel>   
 <xref:System.Windows.Forms.WebBrowserNavigatedEventArgs>   
 <xref:System.Windows.Forms.WebBrowserNavigatedEventHandler>   
 <xref:System.Windows.Forms.WebBrowserNavigatingEventArgs>   
 <xref:System.Windows.Forms.WebBrowserNavigatingEventHandler>   
 <xref:System.Windows.Forms.WebBrowserProgressChangedEventArgs>   
 <xref:System.Windows.Forms.WebBrowserReadyState>   
 <xref:System.Windows.Forms.WebBrowserRefreshOption>   
 [如何：使用 WebBrowser 控件定位到 URL](../../../../docs/framework/winforms/controls/how-to-navigate-to-a-url-with-the-webbrowser-control.md)   
 [如何：使用 WebBrowser 控件打印](../../../../docs/framework/winforms/controls/how-to-print-with-a-webbrowser-control.md)   
 [如何：将 Web 浏览器功能添加到 Windows 窗体应用程序](../../../../docs/framework/winforms/controls/how-to-add-web-browser-capabilities-to-a-windows-forms-application.md)   
 [如何：在 Windows 窗体应用程序中创建 HTML 文档查看器](../../../../docs/framework/winforms/controls/how-to-create-an-html-document-viewer-in-a-windows-forms-application.md)   
 [如何：在 DHTML 代码和客户端应用程序代码之间实现双向通信](../../../../docs/framework/winforms/controls/implement-two-way-com-between-dhtml-and-client.md)   
 [WebBrowser 安全](../../../../docs/framework/winforms/controls/webbrowser-security.md)