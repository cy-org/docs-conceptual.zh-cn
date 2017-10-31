---
title: "ColorConvertedBitmap 标记扩展 | Microsoft Docs"
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
  - "ColorConvertedBitmap 标记扩展"
  - "XAML, ColorConvertedBitmap 标记扩展"
ms.assetid: 18321c18-c898-4470-93fa-a702b47770c1
caps.latest.revision: 8
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 8
---
# ColorConvertedBitmap 标记扩展
提供一种方法来指定没有嵌入式配置文件的位图源。  颜色上下文\/配置文件由 [!INCLUDE[TLA2#tla_uri](../../../../includes/tla2sharptla-uri-md.md)] 指定，此 URI 与图像源 [!INCLUDE[TLA2#tla_uri](../../../../includes/tla2sharptla-uri-md.md)] 是一致的。  
  
## XAML 属性用法  
  
```  
<object property="{ColorConvertedBitmap imageSource sourceIIC destinationIIC}" .../>  
```  
  
## XAML 值  
  
|||  
|-|-|  
|`imageSource`|未配置的位图的 [!INCLUDE[TLA2#tla_uri](../../../../includes/tla2sharptla-uri-md.md)]。|  
|`sourceIIC`|源配置文件配置的 [!INCLUDE[TLA2#tla_uri](../../../../includes/tla2sharptla-uri-md.md)]。|  
|`destinationIIC`|目标配置文件配置的 [!INCLUDE[TLA2#tla_uri](../../../../includes/tla2sharptla-uri-md.md)]。|  
  
## 备注  
 此标记扩展旨在填充图像\-源的一组相关属性值，如 <xref:System.Windows.Media.Imaging.BitmapImage.UriSource%2A>。  
  
 特性语法是最常用于此标记扩展的语法。  `ColorConvertedBitmap`（或 `ColorConvertedBitmapExtension`）不能用于属性元素语法中，因为这些值只能设置为初始构造函数（扩展标识符后面的字符串）上的值。  
  
 `ColorConvertedBitmap` 是标记扩展。  当要求转义属性 \(Attribute\) 值应为非文本值或非处理程序名称时，通常会实现标记扩展，相对于只在某些类型或属性 \(Property\) 上放置类型转换器而言，此要求更具有全局性。  [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] 中的所有标记扩展在其特性语法中都使用 { 和 } 字符，[!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] 处理器通过这一约定确认标记扩展必须处理该特性。  有关更多信息，请参见 [标记扩展和 WPF XAML](../../../../docs/framework/wpf/advanced/markup-extensions-and-wpf-xaml.md)。  
  
## 请参阅  
 <xref:System.Windows.Media.Imaging.BitmapImage.UriSource%2A>   
 [标记扩展和 WPF XAML](../../../../docs/framework/wpf/advanced/markup-extensions-and-wpf-xaml.md)   
 [图像处理概述](../../../../docs/framework/wpf/graphics-multimedia/imaging-overview.md)