---
title: "WPF 和 Windows 窗体互操作 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-wpf"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "混合控件 [WPF 互操作性]"
  - "互操作性 [WPF], Windows 窗体"
  - "nester 互操作 [WPF]"
  - "Windows 窗体 [WPF], 互操作性"
  - "Windows 窗体, WPF 互操作"
ms.assetid: 9e8aa6b6-112c-4579-98d1-c974917df499
caps.latest.revision: 23
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 22
---
# WPF 和 Windows 窗体互操作
[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 和 [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)]提供两种用于创建应用程序接口的不同体系结构。  <xref:System.Windows.Forms.Integration?displayProperty=fullName> 命名空间提供实现常见互操作方案的类。  实现互操作功能的两个关键类是 <xref:System.Windows.Forms.Integration.WindowsFormsHost> 和 <xref:System.Windows.Forms.Integration.ElementHost>。  本主题介绍支持哪些互操作方案以及不支持哪些互操作方案。  
  
> [!NOTE]
>  关于混合控件方案，需要考虑一些特殊因素。  混合控件将一种技术中的控件嵌套于另一种技术中的控件。  这也称为“嵌套互操作”。  多级混合控件具有多个级别的混合控件嵌套。  多级嵌套互操作的一个示例是包含 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 控件的 [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)]控件，前者又包含另一个 [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)]控件。  不支持多级混合控件。  
  
   
  
<a name="Windows_Presentation_Foundation_Application_Hosting"></a>   
## 在 WPF 中承载 Windows 窗体控件  
 当 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 控件承载一个 [!INCLUDE[TLA2#tla_winforms](../../../../includes/tla2sharptla-winforms-md.md)]控件时，支持下列互操作方案：  
  
-   [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 控件可以使用 XAML 承载一个或多个 [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)]控件。  
  
-   它可以使用代码承载一个或多个 [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)]控件。  
  
-   它可以承载包含其他 [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)]控件的 [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)]容器控件。  
  
-   它可以承载具有 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 母版和 [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)]详细信息的母版\/详细信息窗体。  
  
-   它可以承载具有 [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)]母版和 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 详细信息的母版\/详细信息窗体。  
  
-   它可以承载一个或多个 [!INCLUDE[TLA2#tla_actx](../../../../includes/tla2sharptla-actx-md.md)] 控件。  
  
-   它可以承载一个或多个复合控件。  
  
-   它可以使用[!INCLUDE[TLA#tla_xaml](../../../../includes/tlasharptla-xaml-md.md)] 承载混合控件。  
  
-   它可以使用代码承载混合控件。  
  
### 布局支持  
 下面所列内容描述了当 <xref:System.Windows.Forms.Integration.WindowsFormsHost> 元素尝试将其承载的 [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)]控件集成到 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 布局系统中时的已知限制。  
  
-   某些情况下，[!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)]控件无法调整大小，或者大小只能调整为特定的尺寸。  例如，[!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)] <xref:System.Windows.Forms.ComboBox> 控件仅支持由控件的字号定义的单一高度。  在元素可以垂直拉伸的 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 动态布局中，承载的 <xref:System.Windows.Forms.ComboBox> 控件不会如预期那样拉伸。  
  
-   [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)]控件不能旋转或扭曲。  例如，当您将用户界面旋转 90 度时，所承载的 [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)]控件将保持其垂直位置。  
  
-   某些情况下，[!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)]控件不支持按比例缩放。  尽管该控件的整体尺寸将会缩放，但其子控件和组件元素可能不会如预期那样调整大小。  此限制取决于每个 [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)]控件支持缩放的程度。  
  
-   在 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 用户界面中，您可以更改元素的 z 顺序以控制重叠行为。  由于承载的 [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)]控件是在单独的 HWND 中绘制的，所以它始终绘制在 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 元素的顶部。  
  
-   [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)]控件支持基于字号的自动缩放。  在 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 用户界面中，更改字号不会改变整个布局的大小，不过个别元素可能会动态调整大小。  
  
### 环境属性  
 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 控件的一些环境属性具有 [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)]等效项。  这些环境属性传播到所承载的 [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)]控件，并作为 <xref:System.Windows.Forms.Integration.WindowsFormsHost> 控件的公共属性公开。  <xref:System.Windows.Forms.Integration.WindowsFormsHost> 控件将每个 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 环境属性转换为它的 [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)]等效项。  
  
 有关更多信息，请参见[Windows 窗体和 WPF 属性映射](../../../../docs/framework/wpf/advanced/windows-forms-and-wpf-property-mapping.md)。  
  
### 行为  
 下表介绍互操作行为。  
  
|行为|是否支持|不支持|  
|--------|----------|---------|  
|透明度|[!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)]控件呈现支持透明度。  父 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 控件的背景可以成为所承载的 [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)]控件的背景。|某些 [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)]控件不支持透明度。  例如，<xref:System.Windows.Forms.TextBox> 和 <xref:System.Windows.Forms.ComboBox> 控件在由 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 承载时将不会是透明的。|  
|Tab 键|所承载的 [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)]控件的 Tab 键顺序与这些控件承载于基于 [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)]的应用程序中时是一样的。<br /><br /> 使用 Tab 键和 Shift\+Tab 键从 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 控件切换到 [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)]控件将按常规方式工作。<br /><br /> 当用户按 Tab 键依次通过多个控件时，具有值为 `false` 的 <xref:System.Windows.Forms.Control.TabStop%2A> 属性的 [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)]控件不会获得焦点。<br /><br /> -   每个 <xref:System.Windows.Forms.Integration.WindowsFormsHost> 控件都有一个 <xref:System.Windows.Forms.Integration.WindowsFormsHost.TabIndex%2A> 值，这决定了该 <xref:System.Windows.Forms.Integration.WindowsFormsHost> 控件获得焦点的时间。<br />-   包含在 <xref:System.Windows.Forms.Integration.WindowsFormsHost> 容器内部的 [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)]控件遵循 <xref:System.Windows.Forms.Control.TabIndex%2A> 属性指定的顺序。  从最后一个 Tab 键索引使用 Tab 键会将焦点置于下一个 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 控件上（如果存在的话）。  如果没有其他可设定焦点的 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 控件存在，按 Tab 键将返回到 Tab 键顺序中的第一个 [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)]控件。<br />-   <xref:System.Windows.Forms.Integration.WindowsFormsHost> 内部控件的 <xref:System.Windows.Forms.Integration.WindowsFormsHost.TabIndex%2A> 值是相对于 <xref:System.Windows.Forms.Integration.WindowsFormsHost> 控件中包含的同级 [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)]控件而言的。<br />-   Tab 键会遵循特定控件的行为。  例如，在具有值为 `true` 的 <xref:System.Windows.Forms.TextBoxBase.AcceptsTab%2A> 属性的 <xref:System.Windows.Forms.TextBox> 控件中按 Tab 键会在文本框中输入一个制表符，而不是移动焦点。|不适用。|  
|使用箭头键进行导航|-   在 <xref:System.Windows.Forms.Integration.WindowsFormsHost> 控件中使用箭头键进行导航与在普通的 [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)]容器控件中相同：上箭头键和左箭头键选择上一个控件，下箭头键和右箭头键选择下一个控件。<br />-   从 <xref:System.Windows.Forms.Integration.WindowsFormsHost> 控件中包含的第一个控件按上箭头键和左箭头键与 Shift\+Tab 键盘快捷方式所执行的操作相同。  如果存在可设定焦点的 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 控件，则焦点将移到 <xref:System.Windows.Forms.Integration.WindowsFormsHost> 控件的外部。  此行为与标准 <xref:System.Windows.Forms.ContainerControl> 行为的不同之处在于，不回到最后一个控件。  如果没有其他可设定焦点的 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 控件存在，焦点将返回到 Tab 键顺序中的最后一个 [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)]控件。<br />-   从 <xref:System.Windows.Forms.Integration.WindowsFormsHost> 控件中包含的最后一个控件按下箭头键和右箭头键将执行与 Tab 键相同的操作。  如果存在可设定焦点的 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 控件，则焦点将移到 <xref:System.Windows.Forms.Integration.WindowsFormsHost> 控件的外部。  此行为与标准 <xref:System.Windows.Forms.ContainerControl> 行为的不同之处在于，不回到第一个控件。  如果没有其他可设定焦点的 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 控件存在，焦点将返回到 Tab 键顺序中的第一个 [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)]控件。|不适用。|  
|快捷键|快捷键按常规方式工作，但在“不支持”列中指出的情况除外。|不同技术中的重复快捷键不会像普通的重复快捷键那样工作。  当在不同技术之间重复快捷键，并且至少一个在 [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)]控件上，另一个在 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 控件上时，[!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)]控件将总是接收该快捷键。  当按重复快捷键时，焦点不会在控件之间切换。|  
|快捷键|快捷键按常规方式工作，但在“不支持”列中指出的情况除外。|-   在预处理阶段处理的 [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)]快捷键总是优先于 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 快捷键。  例如，如果您有一个定义了 Ctrl\+S 快捷键的 <xref:System.Windows.Forms.ToolStrip> 控件，并且存在绑定于 Ctrl\+S 的 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 命令，则 <xref:System.Windows.Forms.ToolStrip> 控件处理程序将总是首先调用，而不管焦点具体在哪个控件上。<br />-   由 <xref:System.Windows.Forms.Control.KeyDown> 事件处理的 [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)]快捷键在 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 中最后处理。  您可以通过重写 [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)]控件的 <xref:System.Windows.Forms.Control.IsInputKey%2A> 方法或处理 <xref:System.Windows.Forms.Control.PreviewKeyDown> 事件来防止此行为。  从 <xref:System.Windows.Forms.Control.IsInputKey%2A> 方法返回 `true`，或者在 <xref:System.Windows.Forms.Control.PreviewKeyDown> 事件处理程序中将 <xref:System.Windows.Forms.PreviewKeyDownEventArgs.IsInputKey%2A?displayProperty=fullName> 属性的值设置为 `true`。|  
|AcceptsReturn、AcceptsTab 以及其他特定于控件的行为|更改默认键盘行为的属性按常规方式工作，前提是 [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)]控件重写 <xref:System.Windows.Forms.Control.IsInputKey%2A> 方法以返回 `true`。|通过处理 <xref:System.Windows.Forms.Control.KeyDown> 事件来更改默认键盘行为的 [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)]控件在 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 宿主控件中最后一个处理。  因为这些控件在最后处理，所以可能产生意外的行为。|  
|Enter 和 Leave 事件|如果焦点未转到 <xref:System.Windows.Forms.Integration.ElementHost> 包含控件，那么当焦点在一个 <xref:System.Windows.Forms.Integration.WindowsFormsHost> 控件中更改时，将会像通常那样引发 Enter 和 Leave 事件。|当发生以下焦点更改时，不会引发 Enter 和 Leave 事件：<br /><br /> -   从 <xref:System.Windows.Forms.Integration.WindowsFormsHost> 控件内部到外部。<br />-   从 <xref:System.Windows.Forms.Integration.WindowsFormsHost> 控件外部到内部。<br />-   在 <xref:System.Windows.Forms.Integration.WindowsFormsHost> 控件外部。<br />-   从 <xref:System.Windows.Forms.Integration.WindowsFormsHost> 控件中承载的 [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)]控件到同一 <xref:System.Windows.Forms.Integration.WindowsFormsHost> 内部承载的 <xref:System.Windows.Forms.Integration.ElementHost> 控件。|  
|多线程处理|支持所有类型的多线程。|[!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)]和 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 技术均采用单线程并发模型。  调试期间，从其他线程调用框架对象会引发一个异常，从而强制满足此要求。|  
|安全性|所有互操作方案都需要完全信任。|在部分信任下不允许任何互操作方案。|  
|辅助功能|支持所有辅助功能方案。  当辅助技术产品用于同时包含 [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)]和 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 控件的混合应用程序时，可正常工作。|不适用。|  
|Clipboard|所有剪贴板操作都按常规方式工作。  这包括 [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)]与 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 控件之间的剪切和粘贴。|不适用。|  
|拖放功能|所有拖放操作都按常规方式工作。  这包括 [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)]与 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 控件之间的操作。|不适用。|  
  
<a name="Windows_Forms_Application_Hosting_Windows"></a>   
## 在 Windows 窗体中承载 WPF 控件  
 当 [!INCLUDE[TLA2#tla_winforms](../../../../includes/tla2sharptla-winforms-md.md)]控件承载一个 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 控件时，支持下列互操作方案：  
  
-   使用代码承载一个或多个 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 控件。  
  
-   将属性表与一个或多个承载的 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 控件关联。  
  
-   在一个窗体中承载一个或多个 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 页。  
  
-   启动 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 窗口。  
  
-   承载具有 [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)]母版和 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 详细信息的母版\/详细信息窗体。  
  
-   承载具有 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 母版和 [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)]详细信息的母版\/详细信息窗体。  
  
-   承载自定义 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 控件。  
  
-   承载混合控件。  
  
### 环境属性  
 [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)]控件的一些环境属性具有 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 等效项。  这些环境属性传播到所承载的 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 控件，并作为 <xref:System.Windows.Forms.Integration.ElementHost> 控件的公共属性公开。  <xref:System.Windows.Forms.Integration.ElementHost> 控件将每个 [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)]环境属性转换为它的 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 等效项。  
  
 有关更多信息，请参见[Windows 窗体和 WPF 属性映射](../../../../docs/framework/wpf/advanced/windows-forms-and-wpf-property-mapping.md)。  
  
### 行为  
 下表介绍互操作行为。  
  
|行为|是否支持|不支持|  
|--------|----------|---------|  
|透明度|[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]控件呈现支持透明度。  父 [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)]控件的背景可以成为所承载的 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 控件的背景。|不适用。|  
|多线程处理|支持所有类型的多线程。|[!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)]和 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 技术均采用单线程并发模型。  调试期间，从其他线程调用框架对象会引发一个异常，从而强制满足此要求。|  
|安全性|所有互操作方案都需要完全信任。|在部分信任下不允许任何互操作方案。|  
|辅助功能|支持所有辅助功能方案。  当辅助技术产品用于同时包含 [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)]和 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 控件的混合应用程序时，可正常工作。|不适用。|  
|Clipboard|所有剪贴板操作都按常规方式工作。  这包括 [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)]与 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 控件之间的剪切和粘贴。|不适用。|  
|拖放功能|所有拖放操作都按常规方式工作。  这包括 [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)]与 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 控件之间的操作。|不适用。|  
  
## 请参阅  
 <xref:System.Windows.Forms.Integration.ElementHost>   
 <xref:System.Windows.Forms.Integration.WindowsFormsHost>   
 [演练：在 WPF 中承载 Windows 窗体控件](../../../../docs/framework/wpf/advanced/walkthrough-hosting-a-windows-forms-control-in-wpf.md)   
 [演练：在 WPF 中承载 Windows 窗体复合控件](../../../../docs/framework/wpf/advanced/walkthrough-hosting-a-windows-forms-composite-control-in-wpf.md)   
 [演练：在 Windows 窗体中承载 WPF 复合控件](../../../../docs/framework/wpf/advanced/walkthrough-hosting-a-wpf-composite-control-in-windows-forms.md)   
 [Windows 窗体和 WPF 属性映射](../../../../docs/framework/wpf/advanced/windows-forms-and-wpf-property-mapping.md)