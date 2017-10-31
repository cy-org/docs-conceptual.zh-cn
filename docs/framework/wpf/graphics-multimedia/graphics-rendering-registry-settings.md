---
title: "图形呈现注册表设置 | Microsoft Docs"
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
  - "图形 [WPF], 呈现"
  - "呈现图形"
  - "呈现图形, 注册表设置"
  - "呈现图形, 疑难解答"
  - "图形呈现疑难解答"
ms.assetid: f4b41b42-327d-407c-b398-3ed5f505df8b
caps.latest.revision: 18
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 17
---
# 图形呈现注册表设置
此主题概述了影响 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 应用程序的 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 图形呈现注册表设置。  
  
   
  
<a name="overview"></a>   
## 何时使用图形呈现注册表设置  
 这些注册表设置的目的在于疑难解答、调试和提供产品支持。  因为对注册表的更改会影响所有 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 应用程序，所以应用程序不应自动更改这些注册表项或在安装期间更改这些注册表项。  
  
<a name="xpdmandwddm"></a>   
## 什么是 XPDM 和 WDDM？  
 根据视频卡使用的是 XPDM 还是 WDDM 驱动程序，某些图形呈现注册表设置具有不同的默认值。  XPDM 是 [!INCLUDE[TLA#tla_winxp](../../../../includes/tlasharptla-winxp-md.md)] 显示驱动程序模型，而 WDDM 是 Windows 显示驱动程序模型。  WDDM 可在运行 [!INCLUDE[TLA2#tla_winvista](../../../../includes/tla2sharptla-winvista-md.md)] 和 [!INCLUDE[win7](../../../../includes/win7-md.md)] 的计算机上使用。  XPDM 可在运行 [!INCLUDE[TLA2#tla_winvista](../../../../includes/tla2sharptla-winvista-md.md)]、[!INCLUDE[TLA#tla_winxp](../../../../includes/tlasharptla-winxp-md.md)] 和 [!INCLUDE[TLA#tla_winnetsvrfam](../../../../includes/tlasharptla-winnetsvrfam-md.md)] 的计算机上使用。  有关 WDDM 的更多信息，请参见 [Windows Vista Display Driver Model Design Guide](http://go.microsoft.com/fwlink/?LinkId=178394)（Windows Vista 显示驱动程序模型设计指南）。  
  
<a name="registry_settings"></a>   
## 注册表设置  
 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 提供了四个注册表设置来控制 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 呈现：  
  
|设置|说明|  
|--------|--------|  
|**禁用硬件加速选项**|指定是否应启用硬件加速。|  
|**最大多级采样值**|指定消除 [!INCLUDE[TLA2#tla_3d](../../../../includes/tla2sharptla-3d-md.md)] 内容锯齿的多级采样级别。|  
|**必需的视频驱动程序日期设置**|指定系统是否对 2004 年 11 月之前发布的驱动程序禁用硬件加速。|  
|**使用参考光栅器选项**|指定 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 是否应使用参考光栅器。|  
  
 知道如何引用 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 注册表设置的任何外部配置实用工具都可以访问这些设置。  还可以直接使用 [!INCLUDE[TLA#tla_mswin](../../../../includes/tlasharptla-mswin-md.md)] 注册表编辑器来访问这些值，从而创建或修改这些设置。  
  
<a name="disablehardwareacceleration"></a>   
## 禁用硬件加速选项  
  
|注册表项|值类型|  
|----------|---------|  
|`HKEY_CURRENT_USER\SOFTWARE\Microsoft\Avalon.Graphics\DisableHWAcceleration`|DWORD|  
  
 使用**禁用硬件加速选项**，可以出于调试和测试的目的而关闭硬件加速。  在应用程序中看到呈现项目时，尝试关闭硬件加速。  如果项目消失，则视频驱动程序可能有问题。  
  
 **“禁用硬件加速选项”**是一个等于 0 或 1 的 DWORD 值。  如果值为 1，则禁用硬件加速。  假如系统满足硬件加速要求，则值 0 将启用硬件加速；有关更多信息，请参见[图形呈现层](../../../../docs/framework/wpf/advanced/graphics-rendering-tiers.md)。  
  
<a name="maxmultisample"></a>   
## 最大多级采样值  
  
|注册表项|值类型|  
|----------|---------|  
|`HKEY_CURRENT_USER\SOFTWARE\Microsoft\Avalon.Graphics\MaxMultisampleType`|DWORD|  
  
 使用**最大多级采样值**可以调整[!INCLUDE[TLA2#tla_3d](../../../../includes/tla2sharptla-3d-md.md)]内容的最大抗锯齿程度。  使用此级别可在 [!INCLUDE[TLA2#tla_winvista](../../../../includes/tla2sharptla-winvista-md.md)] 中禁用[!INCLUDE[TLA2#tla_3d](../../../../includes/tla2sharptla-3d-md.md)]抗锯齿，或在 [!INCLUDE[TLA#tla_winxp](../../../../includes/tlasharptla-winxp-md.md)] 中启用抗锯齿。  
  
 **“最大多极采样值”**是一个 DWORD 值，其范围为 0 到 16。  值为 0 将指定应禁用三维内容的多极采样抗锯齿，而值为 16 将尝试使用最高为 16 倍速的多极采样抗锯齿（如果视频卡支持）。  请注意，在使用 XPDM 驱动程序的计算机上设置此注册表项值将导致应用程序占用大量额外的视频内存，从而降低 [!INCLUDE[TLA2#tla_3d](../../../../includes/tla2sharptla-3d-md.md)] 呈现的性能，并可能会发生呈现错误和稳定性问题。  
  
 未设置此注册表项时，[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 将默认值设为 0（针对 XPDM 驱动程序）和 4（针对 WDDM 驱动程序）。  
  
<a name="requiredvideodriverdatesetting"></a>   
## 必需的视频驱动程序日期设置  
  
|注册表项|值类型|  
|----------|---------|  
|`HKEY_CURRENT_USER\SOFTWARE\Microsoft\Avalon.Graphics\RequiredVideoDriverDate`|String|  
  
 2004 年 11 月，[!INCLUDE[TLA#tla_ms](../../../../includes/tlasharptla-ms-md.md)] 发布了新版本的驱动程序测试准则；在此日期之后编写的驱动程序可提供更好的稳定性。  默认情况下，[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 将对这些驱动程序使用硬件加速管线，而对在此日期前发布的 XPDM 驱动程序仍使用软件呈现。  
  
 使用**必需的视频驱动程序日期设置**，可以为 XPDM 驱动程序指定一个最早备用日期。  只有在确信视频驱动程序足够稳定，能够支持 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 的情况下，才能指定早于 2004 年 11 月的日期。  
  
 必需的视频驱动程序设置接受以下格式的字符串：  
  
||  
|-|  
|*YYYY* `/` *MM* `/` *DD*|  
  
 其中 *YYYY* 是四位数年份，*MM* 是两位数月份，*DD* 是两位数日期。  如果未设置此值，[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 使用 2004 年 11 月作为其必需的视频驱动程序日期。  
  
<a name="usereferencerasterizeroption"></a>   
## 使用参考光栅器选项  
  
|注册表项|值类型|  
|----------|---------|  
|`HKEY_CURRENT_USER\SOFTWARE\Microsoft\Avalon.Graphics\UseReferenceRasterizer`|DWORD|  
  
 **“使用参考光栅器选项”**使您能够强制 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 进入模拟硬件呈现模式以进行调试：[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 将进入硬件模式，但使用 [!INCLUDE[TLA#tla_d3d](../../../../includes/tlasharptla-d3d-md.md)] 参考软件光栅器 d3dref9.dll，而不是使用实际的硬件设备。  
  
 参考光栅器非常慢，但可以跳过视频驱动程序，避免任何由驱动程序问题导致的呈现问题。  因此，可以使用参考光栅器确定呈现问题是否由视频驱动程序导致。  d3dref9.dll 文件必须位于应用程序可访问的位置，例如在系统路径中的任意位置或在应用程序的本地目录中。  
  
 **使用参考光栅器选项**接受一个 DWORD 值。  值 0 表示不使用参考光栅器。  任何其他非零值则强制 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 使用参考光栅器。  
  
## 请参阅  
 [图形呈现层](../../../../docs/framework/wpf/advanced/graphics-rendering-tiers.md)   
 [WPF 图形呈现疑难解答](../../../../docs/framework/wpf/graphics-multimedia/wpf-graphics-rendering-overview.md)