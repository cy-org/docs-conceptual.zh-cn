---
title: "ClearType 注册表设置 | Microsoft Docs"
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
  - "ClearType, 注册表设置"
  - "版式, ClearType 注册表设置"
ms.assetid: 56f314bb-b30b-4f67-8492-8b8a9fa432ae
caps.latest.revision: 18
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 12
---
# ClearType 注册表设置
本主题概述了 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 应用程序所使用的 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] [!INCLUDE[TLA#tla_ct](../../../../includes/tlasharptla-ct-md.md)] 注册表设置。  
  
   
  
<a name="overview"></a>   
## 技术概述  
 在显示设备上呈现文本的 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 应用程序采用 [!INCLUDE[TLA2#tla_ct](../../../../includes/tla2sharptla-ct-md.md)] 功能来增强您的阅读体验。  [!INCLUDE[TLA2#tla_ct](../../../../includes/tla2sharptla-ct-md.md)] 是由 [!INCLUDE[TLA#tla_ms](../../../../includes/tlasharptla-ms-md.md)] 开发的一种软件技术，可以改善文字在现有 LCD（液晶显示器，如便携式计算机屏幕、Pocket PC 屏幕和平板显示器）上的可读性。  [!INCLUDE[TLA2#tla_ct](../../../../includes/tla2sharptla-ct-md.md)] 通过访问 LCD 屏幕的每个像素中的单个垂直色带元素来工作。  有关 [!INCLUDE[TLA2#tla_ct](../../../../includes/tla2sharptla-ct-md.md)] 的更多信息，请参见 [ClearType 概述](../../../../docs/framework/wpf/advanced/cleartype-overview.md)。  
  
 在不同的显示设备上查看使用 [!INCLUDE[TLA2#tla_ct](../../../../includes/tla2sharptla-ct-md.md)] 呈现的文本时，显示效果会大大不同。  例如，一小部分监视器按照蓝、绿、红的顺序实现色带元素，而不是按照更为常见的红、绿、蓝 \([!INCLUDE[TLA#tla_rgb](../../../../includes/tlasharptla-rgb-md.md)]\) 的顺序实现。  
  
 使用 [!INCLUDE[TLA2#tla_ct](../../../../includes/tla2sharptla-ct-md.md)] 呈现的文本由具有不同级别的颜色敏感度的各个设备进行查看时，显示效果也会大大不同。  某些设备可以更好地检测到细微的颜色差别。  
  
 在上述各种情况下，[!INCLUDE[TLA2#tla_ct](../../../../includes/tla2sharptla-ct-md.md)] 功能需要进行修改以针对各种情况提供最佳阅读体验。  
  
<a name="registry_settings"></a>   
## 注册表设置  
 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 指定了四种用于控制 [!INCLUDE[TLA2#tla_ct](../../../../includes/tla2sharptla-ct-md.md)] 功能的注册表设置：  
  
|设置|说明|  
|--------|--------|  
|[!INCLUDE[TLA2#tla_ct](../../../../includes/tla2sharptla-ct-md.md)] 级别|描述 [!INCLUDE[TLA2#tla_ct](../../../../includes/tla2sharptla-ct-md.md)] 色彩清晰度的级别。|  
|伽马级别|描述显示设备的像素颜色分量的级别。|  
|像素结构|描述显示设备的像素的排列。|  
|文本对比度级别|描述已显示文本的对比度的级别。|  
  
 知道如何引用已标识的 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] [!INCLUDE[TLA2#tla_ct](../../../../includes/tla2sharptla-ct-md.md)] 注册表设置的外部配置实用工具可以访问这些设置。  还可以使用 [!INCLUDE[TLA#tla_mswin](../../../../includes/tlasharptla-mswin-md.md)] 注册表编辑器来直接访问这些值，从而创建或修改这些设置。  
  
 如果未设置 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] [!INCLUDE[TLA2#tla_ct](../../../../includes/tla2sharptla-ct-md.md)] 注册表设置（这是默认状态），则 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 应用程序会查询 [!INCLUDE[TLA#tla_mswin](../../../../includes/tlasharptla-mswin-md.md)] 系统参数信息以获取字体平滑设置。  
  
> [!NOTE]
>  有关枚举显示设备名称的信息，请参见 `SystemParametersInfo` [!INCLUDE[TLA2#tla_win32](../../../../includes/tla2sharptla-win32-md.md)] 函数。  
  
<a name="ClearType_level"></a>   
## ClearType 级别  
 [!INCLUDE[TLA2#tla_ct](../../../../includes/tla2sharptla-ct-md.md)] 级别使您可以根据个人的颜色敏感度和感知力调整文本的呈现效果。对于某些人而言，使用最高级别的 [!INCLUDE[TLA2#tla_ct](../../../../includes/tla2sharptla-ct-md.md)] 呈现文本并不会得到最佳阅读体验。  
  
 [!INCLUDE[TLA2#tla_ct](../../../../includes/tla2sharptla-ct-md.md)] 级别是一个介于 0 到 100 之间的整数值。  默认级别为 100，这意味着 [!INCLUDE[TLA2#tla_ct](../../../../includes/tla2sharptla-ct-md.md)] 使用显示设备色带元素的最大能力。  而 [!INCLUDE[TLA2#tla_ct](../../../../includes/tla2sharptla-ct-md.md)] 级别 0 则将文本呈现为灰度状态。  通过将 [!INCLUDE[TLA2#tla_ct](../../../../includes/tla2sharptla-ct-md.md)] 级别设置为介于 0 和 100 之间的值，可以创建适用于各设备颜色敏感度的中间级别。  
  
### 注册表设置  
 [!INCLUDE[TLA2#tla_ct](../../../../includes/tla2sharptla-ct-md.md)] 级别的注册表设置位置为对应于特定的显示设备名称的单个用户设置：  
  
 `HKEY_CURRENT_USER\SOFTWARE\Microsoft\Avalon.Graphics\<displayName>`  
  
 对于用户的每个显示设备名称，都定义了一个 `ClearTypeLevel` DWORD 值。  下面的屏幕快照演示 [!INCLUDE[TLA2#tla_ct](../../../../includes/tla2sharptla-ct-md.md)] 级别的注册表编辑器设置。  
  
 ![注册表编辑器中的 ClearType 设置](../../../../docs/framework/wpf/advanced/media/cleartyperegistry01.png "ClearTypeRegistry01")  
  
> [!NOTE]
>  [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 应用程序以两种模式（即：使用和不使用 [!INCLUDE[TLA2#tla_ct](../../../../includes/tla2sharptla-ct-md.md)]）中的一种来呈现文本。  不使用 [!INCLUDE[TLA2#tla_ct](../../../../includes/tla2sharptla-ct-md.md)] 呈现文本时，称为灰度呈现。  
  
<a name="gamma_level"></a>   
## 伽马级别  
 伽马级别指像素值和亮度之间的非线性关系。  伽马级别设置应与显示设备的物理特性对应；否则，呈现输出中会出现失真。  例如，测试可能看上去太宽或太窄，或者颜色边缘可能显示在标志符号的垂直主体边缘上。  
  
 伽马级别是一个介于 1000 和 2200 之间的整数值。  默认级别为 1900。  
  
### 注册表设置  
 伽马级别的注册表设置位置为对应于特定的显示设备名称的本地计算机设置：  
  
 `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Avalon.Graphics\<displayName>`  
  
 对于用户的每个显示设备名称，都定义了一个 `GammaLevel` DWORD 值。  下面的屏幕快照演示伽马级别的注册表编辑器设置。  
  
 ![注册表编辑器中的 ClearType 设置](../../../../docs/framework/wpf/advanced/media/cleartyperegistry02.png "ClearTypeRegistry02")  
  
<a name="pixel_structure"></a>   
## 像素结构  
 像素结构描述构成显示设备的像素的类型。  像素结构定义为以下三种类型中的一种：  
  
|类型|值|说明|  
|--------|-------|--------|  
|简单|0|显示设备不存在像素结构。  这意味着每种颜色的光源都均匀分布在像素区域内，这称为灰度呈现。  标准的显示设备就是这样工作的。  [!INCLUDE[TLA2#tla_ct](../../../../includes/tla2sharptla-ct-md.md)] 从不会应用到呈现的文本。|  
|RGB|1|显示设备具有由三条色带按照红、绿、蓝的顺序构成的像素。  [!INCLUDE[TLA2#tla_ct](../../../../includes/tla2sharptla-ct-md.md)] 会应用到呈现的文本。|  
|BGR|2|显示设备具有由三条色带按照蓝、绿、红的顺序构成的像素。  [!INCLUDE[TLA2#tla_ct](../../../../includes/tla2sharptla-ct-md.md)] 会应用到呈现的文本。  请注意，此处的顺序与 RGB 类型的顺序相反。|  
  
 像素结构对应于 0 到 2 之间的整数值。  默认级别为 0，表示平面像素结构。  
  
> [!NOTE]
>  有关枚举显示设备名称的信息，请参见 `EnumDisplayDevices` [!INCLUDE[TLA2#tla_win32](../../../../includes/tla2sharptla-win32-md.md)] 函数。  
  
### 注册表设置  
 像素结构的注册表设置位置为对应于特定的显示设备名称的本地计算机设置：  
  
 `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Avalon.Graphics\<displayName>`  
  
 对于用户的每个显示设备名称，都定义了一个 `PixelStructure` DWORD 值。  下面的屏幕快照演示像素结构的注册表编辑器设置。  
  
 ![注册表编辑器中的 ClearType 设置](../../../../docs/framework/wpf/advanced/media/cleartyperegistry02.png "ClearTypeRegistry02")  
  
<a name="text_contrast_level"></a>   
## 文本对比度级别  
 文本对比度级别使您可以根据标志符号的主体宽度调整文本的呈现效果。  文本对比度级别为介于 0 到 6 之间的整数值，整数值越大，主体越宽。  默认级别为 1。  
  
### 注册表设置  
 文本对比度级别的注册表设置位置为对应于特定的显示设备名称的单个用户设置：  
  
 `HKEY_CURRENT_USER\Software\Microsoft\Avalon.Graphics\<displayName>`  
  
 对于用户的每个显示设备名称，都定义了一个 `TextContrastLevel` DWORD 值。  下面的屏幕快照演示文本对比度级别的注册表编辑器设置。  
  
 ![注册表编辑器中的 ClearType 设置](../../../../docs/framework/wpf/advanced/media/cleartyperegistry01.png "ClearTypeRegistry01")  
  
## 请参阅  
 [ClearType 概述](../../../../docs/framework/wpf/advanced/cleartype-overview.md)   
 [ClearType 抗锯齿](_win32_ClearType_Antialiasing)