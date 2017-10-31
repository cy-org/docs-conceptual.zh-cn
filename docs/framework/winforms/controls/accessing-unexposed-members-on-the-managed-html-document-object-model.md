---
title: "在托管 HTML 文档对象模型中访问未公开成员 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-winforms"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "jsharp"
helpviewer_keywords: 
  - "托管 HTML DOM, 访问未公开成员"
  - "未公开成员"
ms.assetid: 762295bd-2355-4aa7-b43c-5bff997a33e6
caps.latest.revision: 10
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 10
---
# 在托管 HTML 文档对象模型中访问未公开成员
托管 HTML 文档对象模型 \(DOM\) 包含一个名为 <xref:System.Windows.Forms.HtmlElement> 的类，该类公开所有 HTML 元素所共同拥有的属性、方法和事件。  不过在某些情况下，您需要访问托管接口不直接公开的成员。  本主题将分析两种访问未公开成员的方法，包括在网页内部定义的 [!INCLUDE[jsprjscript](../../../../includes/jsprjscript-md.md)] 和 VBScript 函数。  
  
## 通过托管接口访问未公开的成员  
 <xref:System.Windows.Forms.HtmlDocument> 和 <xref:System.Windows.Forms.HtmlElement> 提供了四种可以访问未公开成员的方式。  下表显示了各种类型及其相应的方法。  
  
|成员类型|方法|  
|----------|--------|  
|属性 \(<xref:System.Windows.Forms.HtmlElement>\)|<xref:System.Windows.Forms.HtmlElement.GetAttribute%2A><br /><br /> <xref:System.Windows.Forms.HtmlElement.SetAttribute%2A>|  
|方法|<xref:System.Windows.Forms.HtmlElement.InvokeMember%2A>|  
|事件 \(<xref:System.Windows.Forms.HtmlDocument>\)|<xref:System.Windows.Forms.HtmlDocument.AttachEventHandler%2A><br /><br /> <xref:System.Windows.Forms.HtmlDocument.DetachEventHandler%2A>|  
|事件 \(<xref:System.Windows.Forms.HtmlElement>\)|<xref:System.Windows.Forms.HtmlElement.AttachEventHandler%2A><br /><br /> <xref:System.Windows.Forms.HtmlElement.DetachEventHandler%2A>|  
|事件 \(<xref:System.Windows.Forms.HtmlWindow>\)|<xref:System.Windows.Forms.HtmlWindow.AttachEventHandler%2A><br /><br /> <xref:System.Windows.Forms.HtmlWindow.DetachEventHandler%2A>|  
  
 使用这些方法时，假设您有一个具有基础类型恰好合适的元素。  假设您要侦听 HTML 页上的 `FORM` 元素的 `Submit` 事件，以便可以在用户向服务器提交 `FORM` 的值之前先对这些值进行某些预处理。  理想情况下，如果可以控制 HTML，则可以将 `FORM` 定义为拥有唯一的 `ID` 特性。  
  
```  
<HTML>  
  
    <HEAD>  
        <TITLE>Form Page</TITLE>  
    </HEAD>  
  
    <BODY>  
        <FORM ID="form1">  
             ... form fields defined here ...  
        </FORM>  
    </BODY>  
  
</HTML>  
```  
  
 将此页加载到 <xref:System.Windows.Forms.WebBrowser> 控件后，可以将 `form1` 作为参数使用 <xref:System.Windows.Forms.HtmlDocument.GetElementById%2A> 方法在运行时检索 `FORM`。  
  
 [!code-csharp[System.Windows.Forms.HtmlElement#10](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.HtmlElement/CS/Form1.cs#10)]
 [!code-vb[System.Windows.Forms.HtmlElement#10](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.HtmlElement/VB/Form1.vb#10)]  
  
## 访问非托管接口  
 您还可以使用由每个 DOM 类公开的非托管组件对象模型 \(COM\) 接口来访问托管 HTML DOM 上的未公开成员。  如果必须多次调用未公开成员，或者未公开成员返回不是由托管 HTML DOM 包装的其他非托管接口，建议使用此方式。  
  
 下表显示了通过托管 HTML DOM 公开的所有非托管接口。  单击每个链接可以获取其用法及代码示例的解释。  
  
|类型|非托管接口|  
|--------|-----------|  
|<xref:System.Windows.Forms.HtmlDocument>|<xref:System.Windows.Forms.HtmlDocument.DomDocument%2A>|  
|<xref:System.Windows.Forms.HtmlElement>|<xref:System.Windows.Forms.HtmlElement.DomElement%2A>|  
|<xref:System.Windows.Forms.HtmlWindow>|<xref:System.Windows.Forms.HtmlWindow.DomWindow%2A>|  
|<xref:System.Windows.Forms.HtmlHistory>|<xref:System.Windows.Forms.HtmlHistory.DomHistory%2A>|  
  
 使用 COM 接口的最简便方法将添加对非托管 HTML DOM 库 \(mshtml.dll\) 从应用程序，不过，这是不受支持。  有关更多信息，请参见 [知识库第 934368](http://support.microsoft.com/kb/934368)。  
  
## 访问 Script 函数  
 通过使用脚本语言（如 [!INCLUDE[jsprjscript](../../../../includes/jsprjscript-md.md)] 或 VBScript），HTML 页可以定义一个或多个函数。  这些函数均放置在此页中的 `SCRIPT` 页内，并且可以按需运行或响应 DOM 中的事件。  
  
 您可以使用 <xref:System.Windows.Forms.HtmlDocument.InvokeScript%2A> 方法调用在 HTML 页中定义的任何脚本函数。  如果此脚本方法返回一个 HTML 元素，则可以使用强制转换将此结果转换为 <xref:System.Windows.Forms.HtmlElement>。  有关详细信息及代码示例，请参见 <xref:System.Windows.Forms.HtmlDocument.InvokeScript%2A>。  
  
## 请参阅  
 [使用托管 HTML 文档对象模型](../../../../docs/framework/winforms/controls/using-the-managed-html-document-object-model.md)