---
title: "将玻璃框扩展到 WPF 应用程序 | Microsoft Docs"
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
  - "应用程序, 将玻璃框扩展到"
  - "将玻璃框扩展到应用程序中"
  - "玻璃框, 扩展到应用程序中"
  - "图形, 将玻璃框扩展到应用程序中"
ms.assetid: 74388a3a-4b69-4a9d-ba1f-e107636bd660
caps.latest.revision: 12
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 9
---
# 将玻璃框扩展到 WPF 应用程序
本主题演示如何将 [!INCLUDE[TLA#tla_winvista](../../../../includes/tlasharptla-winvista-md.md)] 玻璃框扩展至 [!INCLUDE[TLA#tla_wpf](../../../../includes/tlasharptla-wpf-md.md)] 应用程序的工作区。  
  
> [!NOTE]
>  此示例仅在运行已启用玻璃效果的桌面窗口管理器 \(DWM\) 的 [!INCLUDE[TLA2#tla_winvista](../../../../includes/tla2sharptla-winvista-md.md)] 计算机上才会起作用。  [!INCLUDE[TLA2#tla_winvista](../../../../includes/tla2sharptla-winvista-md.md)] Home Basic 版本不支持透明玻璃效果。  通常利用透明玻璃效果呈现的区域在其他版本的 [!INCLUDE[TLA2#tla_winvista](../../../../includes/tla2sharptla-winvista-md.md)] 上呈现为不透明。  
  
## 示例  
 下面的示例演示一个已扩展到 Internet Explorer 7 地址栏的玻璃框。  
  
 **Internet Explorer，扩展的玻璃框位于地址栏后。**  
  
 ![具有扩展到地址栏后的玻璃框的 IE7。](../../../../docs/framework/wpf/graphics-multimedia/media/ie7glasstopbar.PNG "IE7glasstopbar")  
  
 若要在 [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] 应用程序上扩展玻璃框，需要访问非托管的 [!INCLUDE[TLA#tla_api](../../../../includes/tlasharptla-api-md.md)]。  下面的代码示例为扩展玻璃框工作区所需的两个 [!INCLUDE[TLA2#tla_api](../../../../includes/tla2sharptla-api-md.md)] 执行平台调用 \(pinvoke\)。  每个 [!INCLUDE[TLA2#tla_api](../../../../includes/tla2sharptla-api-md.md)] 都是在名为 **NonClientRegionAPI** 的类中声明的。  
  
<!-- TODO: review snippet reference  [!CODE [AvalonClientGlass#DWMExtendFramePInvokeAPI](AvalonClientGlass#DWMExtendFramePInvokeAPI)]  -->  
  
 [DwmExtendFrameIntoClientArea](_udwm_dwmextendframeintoclientarea) [](_udwm_dwmextendframeintoclientarea) 是用于将框扩展到工作区中的 DWM 函数。  它有两个参数，一个窗口句柄，一个 [MARGINS](inet_MARGINS) 结构。  [MARGINS](inet_MARGINS) 用于告知 DWM 框扩展到工作区中时延伸的程度。  
  
## 示例  
 若要使用 [DwmExtendFrameIntoClientArea](_udwm_dwmextendframeintoclientarea) 函数，必须获取一个窗口句柄。  在 [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] 中，可以通过 <xref:System.Windows.Interop.HwndSource> 的 <xref:System.Windows.Interop.HwndSource.Handle%2A> 属性获取窗口句柄。  在下面的示例中，框扩展至窗口的 <xref:System.Windows.FrameworkElement.Loaded> 事件的工作区。  
  
<!-- TODO: review snippet reference  [!CODE [AvalonClientGlass#AvalonGlassOnLoadedCSharp](AvalonClientGlass#AvalonGlassOnLoadedCSharp)]  -->  
  
## 示例  
 下面的示例演示一个简单的窗口，在此窗口中框扩展至工作区。  此框扩展到上边框的后面，上边框包含两个 <xref:System.Windows.Controls.TextBox> 对象。  
  
<!-- TODO: review snippet reference  [!CODE [AvalonClientGlass#AvalonGlassFullWindowXAML](AvalonClientGlass#AvalonGlassFullWindowXAML)]  -->  
  
 下图说明扩展至 [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] 应用程序的玻璃框。  
  
 **扩展到**  [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)]  **应用程序中的玻璃框。**  
  
 ![扩展到 WPF 应用程序中的玻璃框。](../../../../docs/framework/wpf/graphics-multimedia/media/wpfextendedglassintoclient.png "WPFextendedGlassIntoClient")  
  
## 请参阅  
 [桌面窗口管理器概述](_udwm_overview)   
 [桌面窗口管理器模糊概述](_udwm_blur_ovw)   
 [DwmExtendFrameIntoClientArea](_udwm_dwmextendframeintoclientarea)