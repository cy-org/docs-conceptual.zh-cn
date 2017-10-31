---
title: "WindowsFormsHost 元素的布局注意事项 | Microsoft Docs"
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
  - "与设备无关的像素"
  - "动态布局 [WPF 互操作性]"
  - "互操作性 [WPF], Windows 窗体"
  - "Windows 窗体 [WPF], 互操作性"
  - "Windows 窗体, WPF 互操作"
  - "WindowsFormsHost 元素布局注意事项"
ms.assetid: 3c574597-bbde-440f-95cc-01371f1a5d9d
caps.latest.revision: 20
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 20
---
# WindowsFormsHost 元素的布局注意事项
本主题描述 <xref:System.Windows.Forms.Integration.WindowsFormsHost> 元素如何与 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 布局系统交互。  
  
 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 和 [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)]支持不同但类似的逻辑，用于对窗体或页面上的元素进行大小调整和定位。  如果创建一个用于承载 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 中的 [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)]控件的混合用户界面 \(UI\)，<xref:System.Windows.Forms.Integration.WindowsFormsHost> 元素会集成这两种布局方案。  
  
## WPF 和 Windows 窗体的布局差异  
 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 使用与分辨率无关的布局。  所有 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 布局维度是使用与设备无关的像素指定的。  与设备无关的像素的大小为九十六之一英寸，且与分辨率无关，因此不论您是在 72 dpi 监视器还是在 19,200 dpi 打印机上呈现，均可以获得相似的结果。  
  
 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 还基于动态布局。  这表示 UI 元素会根据其内容、其父布局容器和可用的屏幕大小在窗体或页面上排列自身。  当 UI 元素包含的字符串改变长度时，动态布局会通过自动调整大小和位置来协助进行本地化。  
  
 [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)]中的布局是与设备相关的，很可能是静态的。  通常，使用以硬件像素为单位指定的维度，在窗体上以绝对方式来定位 [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)]控件。  不过，[!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)]不支持某些动态布局功能，如下表汇总所示。  
  
|布局功能|描述|  
|----------|--------|  
|自动调整大小|某些 [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)]控件可以调整自身大小，以便恰当地显示内容。  有关更多信息，请参见 [AutoSize 属性概述](../../../../docs/framework/winforms/controls/autosize-property-overview.md)。|  
|锚定和停靠|[!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)]控件支持基于父容器进行定位和大小调整。  有关更多信息，请参见<xref:System.Windows.Forms.Control.Anchor%2A?displayProperty=fullName>和<xref:System.Windows.Forms.Control.Dock%2A?displayProperty=fullName>。|  
|自动缩放|容器控件基于输出设备的分辨率或默认容器的字号（单位为像素）来调整自身及其子控件的大小。  有关更多信息，请参见[Windows 窗体中的自动缩放](../../../../docs/framework/winforms/automatic-scaling-in-windows-forms.md)。|  
|布局容器|<xref:System.Windows.Forms.FlowLayoutPanel> 和 <xref:System.Windows.Forms.TableLayoutPanel> 控件根据其内容来排列子控件以及设定自身大小。|  
  
## 布局限制  
 通常，无法将 [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)]控件缩放及转换到 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 中可能的范围。  下面所列内容描述了当 <xref:System.Windows.Forms.Integration.WindowsFormsHost> 元素尝试将其承载的 [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)]控件集成到 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 布局系统中时的已知限制。  
  
-   某些情况下，[!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)]控件无法调整大小，或者大小只能调整为特定的尺寸。  例如，[!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)] <xref:System.Windows.Forms.ComboBox> 控件仅支持由控件的字号定义的单一高度。  在元素可以垂直拉伸的 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 动态布局中，承载的 <xref:System.Windows.Forms.ComboBox> 控件不会如预期那样拉伸。  
  
-   [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)]控件不能旋转或扭曲。  如果应用扭曲或旋转变换，<xref:System.Windows.Forms.Integration.WindowsFormsHost> 元素会引发 <xref:System.Windows.Forms.Integration.WindowsFormsHost.LayoutError> 事件。  如果未处理 <xref:System.Windows.Forms.Integration.WindowsFormsHost.LayoutError> 事件，会引发 <xref:System.InvalidOperationException>。  
  
-   某些情况下，[!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)]控件不支持按比例缩放。  尽管该控件的整体尺寸将会缩放，但其子控件和组件元素可能不会如预期那样调整大小。  此限制取决于每个 [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)]控件支持缩放的程度。  此外，您不能将 [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)]控件缩小至 0 像素大小。  
  
-   [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)]控件支持自动缩放，其中的窗体会基于字号自动调整自身及其控件的大小。  在 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 用户界面中，更改字号不会改变整个布局的大小，不过个别元素可能会动态调整大小。  
  
### Z 顺序  
 在 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 用户界面中，您可以更改元素的 z 顺序以控制重叠行为。  由于承载的 [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)]控件是在单独的 HWND 中绘制的，所以它始终绘制在 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 元素的顶部。  
  
 承载的 [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)]控件还是在任意 <xref:System.Windows.Documents.Adorner> 元素的顶部绘制的。  
  
## 布局行为  
 以下各节介绍当在 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 中承载 [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)]控件时布局行为的特定方面。  
  
### 缩放、单位换算和设备无关性  
 不论何时 <xref:System.Windows.Forms.Integration.WindowsFormsHost> 元素执行涉及 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 和 [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)]维度的操作，会牵涉到两个坐标系：用于 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 的与设备无关的像素、用于 [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)]的硬件像素。  因此，必须应用适当的单位和缩放转换，以实现一致的布局。  
  
 坐标系之间的转换取决于当前设备分辨率和应用于 <xref:System.Windows.Forms.Integration.WindowsFormsHost> 元素或其上级的任意布局或呈现转换。  
  
 如果输出设备为 96 dpi，并且没有向 <xref:System.Windows.Forms.Integration.WindowsFormsHost> 元素应用任何缩放，则一个与设备无关的像素等于一个硬件像素。  
  
 其他所有情况均需要坐标系缩放。  承载的控件不会调整大小，  而是由 <xref:System.Windows.Forms.Integration.WindowsFormsHost> 元素尝试缩放承载的控件及其所有子控件。  由于 [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)]不完全支持缩放，所以 <xref:System.Windows.Forms.Integration.WindowsFormsHost> 元素只能缩放到特定控件支持的程度。  
  
 重写 <xref:System.Windows.Forms.Integration.WindowsFormsHost.ScaleChild%2A> 方法以便为承载的 [!INCLUDE[TLA2#tla_winforms](../../../../includes/tla2sharptla-winforms-md.md)]控件提供自定义缩放行为。  
  
 除缩放外，<xref:System.Windows.Forms.Integration.WindowsFormsHost> 元素还会处理舍入和溢出情况，如下表所示。  
  
|转换问题|描述|  
|----------|--------|  
|舍入|[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 与设备无关的像素尺寸以 `double` 格式指定，[!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)] 硬件像素尺寸以 `int` 格式指定。  如果基于 `double` 的维度转换为基于 `int` 的维度，<xref:System.Windows.Forms.Integration.WindowsFormsHost> 元素将使用标准舍入，这样小于 0.5 的小数值向下舍入为 0。|  
|溢出|当 <xref:System.Windows.Forms.Integration.WindowsFormsHost> 元素从 `double` 值转换为 `int` 值时，可能会发生溢出。  大于 <xref:System.Int32.MaxValue> 的值均设置为 <xref:System.Int32.MaxValue>。|  
  
### 与布局相关的属性  
 用于控制 [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)]控件和 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 元素中布局行为的属性是通过 <xref:System.Windows.Forms.Integration.WindowsFormsHost> 元素进行相应映射的。  有关更多信息，请参见[Windows 窗体和 WPF 属性映射](../../../../docs/framework/wpf/advanced/windows-forms-and-wpf-property-mapping.md)。  
  
### 承载的控件中的布局更改  
 承载的 [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)]控件中的布局更改会传播到 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 以触发布局更新。  <xref:System.Windows.Forms.Integration.WindowsFormsHost> 上的 <xref:System.Windows.UIElement.InvalidateMeasure%2A> 方法可以确保承载的控件中的布局更改会导致 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 布局引擎运行。  
  
### 连续调整 Windows 窗体控件的大小  
 支持连续缩放的 [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)]控件与 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 布局系统是完全交互的。  <xref:System.Windows.Forms.Integration.WindowsFormsHost> 元素通常使用 <xref:System.Windows.FrameworkElement.MeasureOverride%2A> 和 <xref:System.Windows.FrameworkElement.ArrangeOverride%2A> 方法来调整和排列承载的 [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)]控件。  
  
### 大小调整算法  
 <xref:System.Windows.Forms.Integration.WindowsFormsHost> 元素使用下面的过程来调整承载的控件的大小：  
  
1.  <xref:System.Windows.Forms.Integration.WindowsFormsHost> 元素重写 <xref:System.Windows.FrameworkElement.MeasureOverride%2A> 和 <xref:System.Windows.FrameworkElement.ArrangeOverride%2A> 方法。  
  
2.  若要确定承载的控件的大小，<xref:System.Windows.FrameworkElement.MeasureOverride%2A> 方法会利用从传递到 <xref:System.Windows.FrameworkElement.MeasureOverride%2A> 方法的约束转换而来的约束，来调用承载的控件的 <xref:System.Windows.Forms.Control.GetPreferredSize%2A> 方法。  
  
3.  <xref:System.Windows.FrameworkElement.ArrangeOverride%2A> 方法会尝试将承载的控件设置为给定大小约束。  
  
4.  如果承载的控件的 <xref:System.Windows.Forms.Control.Size%2A> 属性与指定的约束匹配，那么承载的控件的大小会调整到约束大小。  
  
 如果 <xref:System.Windows.Forms.Control.Size%2A> 属性与指定的约束不匹配，那么该承载的控件不支持连续调整大小。  例如，<xref:System.Windows.Forms.MonthCalendar> 控件仅允许不连续的大小。  此控件的允许大小由整数（代表月数）组成，用于表示高度和宽度。  这种情况下，<xref:System.Windows.Forms.Integration.WindowsFormsHost> 元素具有如下行为：  
  
-   如果 <xref:System.Windows.Forms.Control.Size%2A> 属性返回一个大于指定约束的大小，<xref:System.Windows.Forms.Integration.WindowsFormsHost> 元素会剪裁承载的控件。  因为高度和宽度是分别进行处理的，所以在这两个方向上都可能会剪裁承载的控件。  
  
-   如果 <xref:System.Windows.Forms.Control.Size%2A> 属性返回一个小于指定约束的大小，<xref:System.Windows.Forms.Integration.WindowsFormsHost> 会接受此大小值，并向 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 布局系统返回该值。  
  
## 请参阅  
 <xref:System.Windows.Forms.Integration.ElementHost>   
 <xref:System.Windows.Forms.Integration.WindowsFormsHost>   
 [演练：在 WPF 中排列 Windows 窗体控件](../../../../docs/framework/wpf/advanced/walkthrough-arranging-windows-forms-controls-in-wpf.md)   
 [在WPF中排列Windows窗体控件示例](http://go.microsoft.com/fwlink/?LinkID=159971)   
 [Windows 窗体和 WPF 属性映射](../../../../docs/framework/wpf/advanced/windows-forms-and-wpf-property-mapping.md)   
 [迁移和互操作性](../../../../docs/framework/wpf/advanced/migration-and-interoperability.md)