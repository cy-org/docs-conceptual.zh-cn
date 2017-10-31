---
title: "如何：在导航历史记录中前进或后退 | Microsoft Docs"
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
  - "历史记录, 导航, 向前导航"
  - "导航, 通过导航历史记录（向前）"
ms.assetid: 5939d574-5f53-469e-85f5-1f2b13607caa
caps.latest.revision: 11
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 11
---
# 如何：在导航历史记录中前进或后退
此示例演示如何定位向前或向后在导航历史记录中的项。  
  
## 示例  
 代码从以下宿主的内容运行可以在导航历史记录，向前定位一项或一次。  
  
-   使用 <xref:System.Windows.Navigation.NavigationService>的<xref:System.Windows.Navigation.NavigationWindow>  
  
-   使用 <xref:System.Windows.Navigation.NavigationService>的<xref:System.Windows.Controls.Frame>  
  
-   [!INCLUDE[TLA#tla_iegeneric](../../../../includes/tlasharptla-iegeneric-md.md)]  
  
 在可以向前定位一项之前，必须先检查在向前导航历史记录中的项通过检查 **CanGoForward** 属性。  向前定位一项，请调用 **GoForward** 方法。  下面的示例对此进行了阐释：  
  
 [!code-csharp[HOWTONavigationSnippets#NavigateForwardCODE](../../../../samples/snippets/csharp/VS_Snippets_Wpf/HOWTONavigationSnippets/CSharp/HomePage.xaml.cs#navigateforwardcode)]
 [!code-vb[HOWTONavigationSnippets#NavigateForwardCODE](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/HOWTONavigationSnippets/visualbasic/homepage.xaml.vb#navigateforwardcode)]  
  
 在可以定位一项之前，必须先检查在向后导航历史记录中的项通过检查 **CanGoBack** 属性。  若要定位一项，请调用 **GoBack** 方法。  下面的示例对此进行了阐释：  
  
 [!code-csharp[HOWTONavigationSnippets#NavigateBackCODE](../../../../samples/snippets/csharp/VS_Snippets_Wpf/HOWTONavigationSnippets/CSharp/HomePage.xaml.cs#navigatebackcode)]
 [!code-vb[HOWTONavigationSnippets#NavigateBackCODE](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/HOWTONavigationSnippets/visualbasic/homepage.xaml.vb#navigatebackcode)]  
  
 **CanGoForward**、 **GoForward**、 **CanGoBack**和 **GoBack** 由 <xref:System.Windows.Navigation.NavigationWindow>、 <xref:System.Windows.Controls.Frame>和 <xref:System.Windows.Navigation.NavigationService>实现。  
  
> [!NOTE]
>  如果调用， **GoForward**，而在向前导航历史记录中没有项，或者，如果调用 **GoBack**，并且，还存在向后导航历史记录中没有项， <xref:System.InvalidOperationException> 将引发。