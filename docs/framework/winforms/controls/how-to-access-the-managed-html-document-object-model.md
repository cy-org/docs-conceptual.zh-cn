---
title: "如何：访问托管 HTML 文档对象模型 | Microsoft Docs"
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
  - "HTML DOM 访问"
  - "托管 HTML DOM 访问"
ms.assetid: 40fa5cd5-1ed8-42f6-a93f-9ac01608bbeb
caps.latest.revision: 12
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 12
---
# 如何：访问托管 HTML 文档对象模型
可以从两种类型的应用程序访问托管 HTML 文档对象模型 (DOM)：  
  
-   承载了托管的 Windows 窗体应用程序 (.exe) <xref:System.Windows.Forms.WebBrowser>控件。 这两种技术互相补充，使用<xref:System.Windows.Forms.WebBrowser>向用户和 HTML DOM 表示文档的逻辑结构显示页面的控件。  
  
-   Windows 窗体<xref:System.Windows.Forms.UserControl> Internet Explorer 内托管。 您可以访问 HTML DOM 表示的页面您<xref:System.Windows.Forms.UserControl>托管以更改文档的结构或打开模式对话框，还有许多其他功能。  
  
### <a name="to-access-dom-from-a-windows-forms-application"></a>从 Windows 窗体应用程序访问 DOM  
  
1.  主机<xref:System.Windows.Forms.WebBrowser>控件在 Windows 窗体应用程序，并监视<xref:System.Windows.Forms.WebBrowser.DocumentCompleted>事件。 有关托管控件和事件监视的详细信息，请参阅[事件](../../../../docs/standard/events/index.md)。  
  
2.  检索<xref:System.Windows.Forms.HtmlDocument>通过访问当前页<xref:System.Windows.Forms.WebBrowser.Document%2A>属性<xref:System.Windows.Forms.WebBrowser>控件。  
  
<!-- TODO: review snippet reference  [!CODE [AccessHTMLDOMApp#1](AccessHTMLDOMApp#1)]  -->  
  
### <a name="to-access-dom-from-a-usercontrol-hosted-in-internet-explorer"></a>从在 Internet Explorer 中托管的 UserControl 访问 DOM  
  
1.  创建你自己的自定义的派生的类<xref:System.Windows.Forms.UserControl>类。 有关详细信息，请参阅[如何︰ 创作复合控件](../../../../docs/framework/winforms/controls/how-to-author-composite-controls.md)。  
  
2.  下面将代码放置在 Load 事件处理程序您<xref:System.Windows.Forms.UserControl>:  
  
 [!code-csharp[AccessHTMLDOMControl#1](../../../../samples/snippets/csharp/VS_Snippets_Winforms/AccessHTMLDOMControl/cs/UserControl1.cs#1)]
 [!code-vb[AccessHTMLDOMControl#1](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/AccessHTMLDOMControl/vb/UserControl1.vb#1)]  
  
## <a name="robust-programming"></a>可靠编程  
  
1.  使用通过 DOM 时<xref:System.Windows.Forms.WebBrowser>控件，您应始终将一直等到<xref:System.Windows.Forms.WebBrowser.DocumentCompleted>事件发生前尝试访问<xref:System.Windows.Forms.WebBrowser.Document%2A>属性<xref:System.Windows.Forms.WebBrowser>控件。 <xref:System.Windows.Forms.WebBrowser.DocumentCompleted>加载整个文档之后引发事件; 如果你之前用过 DOM，则可能导致应用程序中的运行时异常。  
  
## <a name="net-framework-security"></a>.NET Framework 安全性  
  
1.  您的应用程序或<xref:System.Windows.Forms.UserControl>将需要完全信任才能访问托管的 HTML dom。 如果您正在部署 Windows 窗体应用程序使用[!INCLUDE[ndptecclick](../../../../includes/ndptecclick-md.md)]，您可以请求完全信任权限提升或受信任的应用程序部署使用; 请参阅[保护 ClickOnce 应用程序](../Topic/Securing%20ClickOnce%20Applications.md)有关的详细信息。  
  
## <a name="see-also"></a>另请参阅  
 [使用托管的 HTML 文档对象模型](../../../../docs/framework/winforms/controls/using-the-managed-html-document-object-model.md)