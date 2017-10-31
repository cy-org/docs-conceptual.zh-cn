---
title: "向 Windows 运行时传递 URI | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-standard"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "VB"
  - "CSharp"
  - "C++"
  - "jsharp"
helpviewer_keywords: 
  - "Windows 运行时, .NET Framework 支持"
  - "Windows 运行时, 将 URI 传递给"
ms.assetid: 3eb5ce6f-f304-4f87-8e81-0f25092f5ad4
caps.latest.revision: 10
author: "mairaw"
ms.author: "mairaw"
manager: "wpickett"
caps.handback.revision: 10
---
# 向 Windows 运行时传递 URI
Windows 运行时方法只接受绝对 URI。 如果将一个相对 URI 传递给 [!INCLUDE[wrt](../../../includes/wrt-md.md)] 方法，则将会引发 <xref:System.ArgumentException> 异常。 原因如下：在 .NET Framework 代码中使用 [!INCLUDE[wrt](../../../includes/wrt-md.md)] 时，[Windows.Foundation.Uri](http://go.microsoft.com/fwlink/p/?LinkId=238376) 类显示为 Intellisense 中的 <xref:System.Uri?displayProperty=fullName>。<xref:System.Uri?displayProperty=fullName> 类允许相对 URI，但 [Windows.Foundation.Uri](http://go.microsoft.com/fwlink/p/?LinkId=238376) 类不允许。 这也适用于 [!INCLUDE[wrt](../../../includes/wrt-md.md)] 组件中公开的方法。 如果组件公开接收 URI 的方法，则代码中的签名包含 <xref:System.Uri?displayProperty=fullName>。 但是，对于组件的用户，签名包含 [Windows.Foundation.Uri](http://go.microsoft.com/fwlink/p/?LinkId=238376)。 传递给组件的 URI 必须是绝对 URI。  
  
 本主题演示了如何检测绝对 URI 以及如何在引用应用包中的资源时创建一个。  
  
## 检测和使用绝对 URI  
 使用 <xref:System.Uri.IsAbsoluteUri%2A?displayProperty=fullName> 属性确保在将 URI 传递给 [!INCLUDE[wrt](../../../includes/wrt-md.md)] 之前，该 URI 是绝对的。 使用此属性比捕获和处理 <xref:System.ArgumentException> 异常更为有效。  
  
## 将绝对 URI 用于应用包中的资源  
 如果想要为应用包包含的资源指定 URI，可以使用 `ms-appx` 或 `ms-appx-web` 方案来创建绝对 URI。  
  
 下面的示例演示如何使用 XAML 和代码，将 [WebView](http://msdn.microsoft.com/library/windows/apps/xaml/windows.ui.xaml.controls.webview.aspx) 控件的 [Source](http://msdn.microsoft.com/library/windows/apps/xaml/windows.ui.xaml.controls.webview.source.aspx) 属性和 [Image](http://msdn.microsoft.com/library/windows/apps/br242752.aspx) 控件的 [Source](http://msdn.microsoft.com/library/windows/apps/windows.ui.xaml.controls.image.source.aspx) 属性设置为包含在名为“Pages”的文件夹中的资源。  
  
 [!code-xml[System.URIToWindowsURI#1](../../../samples/snippets/csharp/VS_Snippets_CLR_System/system.uritowindowsuri/cs/mainpage.xaml#1)]  
[!code-csharp[System.URIToWindowsURI#2](../../../samples/snippets/csharp/VS_Snippets_CLR_System/system.uritowindowsuri/cs/mainpage.xaml.cs#2)]
[!code-vb[System.URIToWindowsURI#2](../../../samples/snippets/visualbasic/VS_Snippets_CLR_System/system.uritowindowsuri/vb/mainpage.xaml.vb#2)]  
  
 有关这些方案的详细信息，请参阅 Windows 开发人员中心中的 [URI 方案](http://msdn.microsoft.com/library/windows/apps/jj655406.aspx)。  
  
## 请参阅  
 [.NET Framework 对 Windows 应用商店应用程序和 Windows 运行时的支持情况](../../../docs/standard/cross-platform/support-for-windows-store-apps-and-windows-runtime.md)