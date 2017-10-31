---
title: "Popup 概述 | Microsoft Docs"
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
  - "控件, Popup"
  - "Popup 控件 [WPF], 关于 Popup 控件"
ms.assetid: 774f53ca-bff8-470e-9ce9-3928b4cf3d4c
caps.latest.revision: 34
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 33
---
# Popup 概述
<xref:System.Windows.Controls.Primitives.Popup> 控件提供一种在单独窗口中显示内容的方法，该窗口相对于指定元素或屏幕坐标浮动于当前应用程序窗口之上。  本主题介绍 <xref:System.Windows.Controls.Primitives.Popup> 控件，并提供有关其用法的信息。  
  
   
  
<a name="What_Is_a_Popup_"></a>   
## 什么是 Popup？  
 <xref:System.Windows.Controls.Primitives.Popup> 控件可在单独窗口中相对于屏幕上的元素或点显示内容。  当 <xref:System.Windows.Controls.Primitives.Popup> 可见时，<xref:System.Windows.Controls.Primitives.Popup.IsOpen%2A> 属性设置为 `true`。  
  
> [!NOTE]
>  当鼠标指针移动到其父对象之上时，<xref:System.Windows.Controls.Primitives.Popup> 不会自动打开。  如果希望 <xref:System.Windows.Controls.Primitives.Popup> 自动打开，请使用 <xref:System.Windows.Controls.ToolTip> 或 <xref:System.Windows.Controls.ToolTipService> 类。  有关更多信息，请参见[ToolTip 概述](../../../../docs/framework/wpf/controls/tooltip-overview.md)。  
  
<a name="APopupExample"></a>   
## 创建 Popup  
 下面的示例演示如何定义 <xref:System.Windows.Controls.Primitives.Popup> 控件，该控件是 <xref:System.Windows.Controls.Button> 控件的子元素。  由于 <xref:System.Windows.Controls.Button> 只能有一个子元素，因此此示例将 <xref:System.Windows.Controls.Button> 和 <xref:System.Windows.Controls.Primitives.Popup> 控件的文本放入 <xref:System.Windows.Controls.StackPanel> 中。   <xref:System.Windows.Controls.Primitives.Popup> 的内容将显示在 <xref:System.Windows.Controls.TextBlock> 控件中，这样就会将其文本显示在单独的窗口中，该窗口浮动在应用程序窗口之上并且靠近相关 <xref:System.Windows.Controls.Button> 控件。  
  
 [!code-xml[PopupSimple#1](../../../../samples/snippets/csharp/VS_Snippets_Wpf/PopupSimple/CSharp/Window1.xaml#1)]  
  
 [!code-xml[PopupSimple#CreatePopupCodeXAML](../../../../samples/snippets/csharp/VS_Snippets_Wpf/PopupSimple/CSharp/Window1.xaml#createpopupcodexaml)]  
  
<a name="PopupUses"></a>   
## 实现 Popup 的控件  
 您可以将 <xref:System.Windows.Controls.Primitives.Popup> 控件生成到其他控件中。  以下控件针对特定的用途实现 <xref:System.Windows.Controls.Primitives.Popup> 控件：  
  
-   <xref:System.Windows.Controls.ToolTip>.  如果需要为某个元素创建工具提示，请使用 <xref:System.Windows.Controls.ToolTip> 和 <xref:System.Windows.Controls.ToolTipService> 类。  有关更多信息，请参见[ToolTip 概述](../../../../docs/framework/wpf/controls/tooltip-overview.md)。  
  
-   <xref:System.Windows.Controls.ContextMenu>.  如果需要为某个元素创建上下文菜单，请使用 <xref:System.Windows.Controls.ContextMenu> 控件。  有关更多信息，请参见 [ContextMenu 概述](../../../../docs/framework/wpf/controls/contextmenu-overview.md)。  
  
-   <xref:System.Windows.Controls.ComboBox>.  如果需要创建一个具有可以显示或隐藏的下拉列表框的选择控件，请使用 <xref:System.Windows.Controls.ComboBox> 控件。  
  
-   <xref:System.Windows.Controls.Expander>.  如果需要创建一个可显示标题（该标题同时具有一个可以显示内容的可折叠区域）的控件，请使用 <xref:System.Windows.Controls.Expander> 控件。  有关更多信息，请参见 [Expander 概述](../../../../docs/framework/wpf/controls/expander-overview.md)。  
  
<a name="PopupBehaviorandAppearance"></a>   
## Popup 的行为和外观  
 <xref:System.Windows.Controls.Primitives.Popup> 控件提供用于自定义其行为和外观的功能。  例如，您可以设置打开和关闭行为、动画、不透明度和位图效果以及 <xref:System.Windows.Controls.Primitives.Popup> 的大小和位置。  
  
<a name="OpenandCloseBehavior"></a>   
### 打开和关闭行为  
 当 <xref:System.Windows.Controls.Primitives.Popup.IsOpen%2A> 属性设置为 `true` 时，<xref:System.Windows.Controls.Primitives.Popup> 控件显示其内容。  默认情况下，<xref:System.Windows.Controls.Primitives.Popup> 保持为打开状态，除非 <xref:System.Windows.Controls.Primitives.Popup.IsOpen%2A> 属性设置为 `false`。  不过，您可以通过将 <xref:System.Windows.Controls.Primitives.Popup.StaysOpen%2A> 属性设置为 `false` 来更改默认行为。  当您将该属性设置为 `false` 时，<xref:System.Windows.Controls.Primitives.Popup> 内容窗口将获得鼠标捕获。  当鼠标事件发生在 <xref:System.Windows.Controls.Primitives.Popup> 窗口外时，<xref:System.Windows.Controls.Primitives.Popup> 将失去鼠标捕获并且该窗口将关闭。  
  
 当打开或关闭 <xref:System.Windows.Controls.Primitives.Popup> 内容窗口时，将引发 <xref:System.Windows.Controls.Primitives.Popup.Opened> 和 <xref:System.Windows.Controls.Primitives.Popup.Closed> 事件。  
  
<a name="Animation"></a>   
### 动画  
 <xref:System.Windows.Controls.Primitives.Popup> 控件为通常与淡入和滑入之类的行为关联的动画提供内置支持。  可以通过将 <xref:System.Windows.Controls.Primitives.Popup.PopupAnimation%2A> 属性设置为一个 <xref:System.Windows.Controls.Primitives.PopupAnimation> 枚举值来打开这些动画。  若要使 <xref:System.Windows.Controls.Primitives.Popup> 动画能够正常运行，您必须将 <xref:System.Windows.Controls.Primitives.Popup.AllowsTransparency%2A> 属性设置为 `true`。  
  
 您还可以将 <xref:System.Windows.Media.Animation.Storyboard> 之类的动画应用到 <xref:System.Windows.Controls.Primitives.Popup> 控件中。  
  
<a name="OpacityandBitmapEffects"></a>   
### 不透明度和位图效果  
 <xref:System.Windows.Controls.Primitives.Popup> 控件的 <xref:System.Windows.UIElement.Opacity%2A> 属性对其内容没有影响。  默认情况下，<xref:System.Windows.Controls.Primitives.Popup> 内容窗口是不透明的。  若要创建一个透明的 <xref:System.Windows.Controls.Primitives.Popup>，请将 <xref:System.Windows.Controls.Primitives.Popup.AllowsTransparency%2A> 属性设置为 `true`.  
  
 <xref:System.Windows.Controls.Primitives.Popup> 的内容不会继承位图效果（例如 <xref:System.Windows.Media.Effects.DropShadowBitmapEffect>），这样您可以直接在父窗口的 <xref:System.Windows.Controls.Primitives.Popup> 控件上或任何其他元素上进行设置。  若要在 <xref:System.Windows.Controls.Primitives.Popup> 内容上显示位图效果，您必须在其内容上直接设置位图效果。  例如，如果 <xref:System.Windows.Controls.Primitives.Popup> 的子级是 <xref:System.Windows.Controls.StackPanel>，则需要在 <xref:System.Windows.Controls.StackPanel> 上设置位图效果。  
  
<a name="PopupSize"></a>   
### Popup 的大小  
 默认情况下，<xref:System.Windows.Controls.Primitives.Popup> 自动调整大小以适合其内容。  由于为 <xref:System.Windows.Controls.Primitives.Popup> 内容定义的屏幕区域的默认大小的空间有限，不能为要显示的位图效果提供足够的空间，因此在自动调整大小时，某些位图效果可能会隐藏。  
  
 如果在内容上设置 <xref:System.Windows.UIElement.RenderTransform%2A>，<xref:System.Windows.Controls.Primitives.Popup> 的内容也可能会被遮挡住。  在这种情况下，如果转换的 <xref:System.Windows.Controls.Primitives.Popup> 的内容超出了原始 <xref:System.Windows.Controls.Primitives.Popup> 的区域，则某些内容可能会隐藏。  如果位图效果或转换需要较多的空间，则您可以在 <xref:System.Windows.Controls.Primitives.Popup> 内容周围定义一个边距，从而为该控件提供更多的区域。  
  
<a name="DefiningPopupPosition"></a>   
## 定义 Popup 的位置  
 您可以通过设置 <xref:System.Windows.Controls.Primitives.Popup.PlacementTarget%2A>、<xref:System.Windows.Controls.Primitives.Popup.PlacementRectangle%2A>、<xref:System.Windows.Controls.Primitives.Popup.Placement%2A>、<xref:System.Windows.Controls.Primitives.Popup.HorizontalOffset%2A> 和 <xref:System.Windows.Controls.Primitives.Popup.VerticalOffsetProperty> 属性来定位弹出项。  有关更多信息，请参见 [Popup 放置行为](../../../../docs/framework/wpf/controls/popup-placement-behavior.md)。  当 <xref:System.Windows.Controls.Primitives.Popup> 已显示在屏幕上时，如果其父级已重新定位，则其本身不会重新定位。  
  
<a name="CustomizingPopupPlacement"></a>   
### 自定义 Popup 放置  
 通过指定一组相对于 <xref:System.Windows.Controls.Primitives.Popup.PlacementTarget%2A>（您希望在此显示 <xref:System.Windows.Controls.Primitives.Popup>）的坐标，您可以自定义 <xref:System.Windows.Controls.Primitives.Popup> 控件的位置。  
  
 若要自定义位置，请将 <xref:System.Windows.Controls.Primitives.Popup.Placement%2A> 属性设置为 <xref:System.Windows.Controls.Primitives.PlacementMode>。  然后，再定义一个 <xref:System.Windows.Controls.Primitives.CustomPopupPlacementCallback> 委托，该委托按优先顺序为 <xref:System.Windows.Controls.Primitives.Popup> 返回一组可能的位置点和主轴。  此时，显示 <xref:System.Windows.Controls.Primitives.Popup> 最大部分的点将被自动选中。  有关示例，请参见[指定自定义 Popup 位置](../../../../docs/framework/wpf/controls/how-to-specify-a-custom-popup-position.md)。  
  
<a name="PopupandtheVisualTree"></a>   
## Popup 和可视化树  
 <xref:System.Windows.Controls.Primitives.Popup> 控件没有其自己的[可视化树](GTMT)；当调用 <xref:System.Windows.Controls.Primitives.Popup> 的 <xref:System.Windows.Controls.Primitives.Popup.MeasureOverride%2A> 方法时，它返回 0（零）大小。  但是，当您将 <xref:System.Windows.Controls.Primitives.Popup> 的 <xref:System.Windows.Controls.Primitives.Popup.IsOpen%2A> 属性设置为 `true` 时，将创建一个具有其自己的可视化树的新窗口。  该新窗口将包含 <xref:System.Windows.Controls.Primitives.Popup> 的 <xref:System.Windows.Controls.Primitives.Popup.Child%2A> 内容。  新窗口的宽度和高度不能超过屏幕宽度和高度的 75%。  
  
 <xref:System.Windows.Controls.Primitives.Popup> 控件维持一个将其 <xref:System.Windows.Controls.Primitives.Popup.Child%2A> 内容作为逻辑子级的引用。  创建新窗口后，<xref:System.Windows.Controls.Primitives.Popup> 的内容成为该窗口的一个可视化子级并保留 <xref:System.Windows.Controls.Primitives.Popup> 的逻辑子级。  相反，<xref:System.Windows.Controls.Primitives.Popup> 将保持其 <xref:System.Windows.Controls.Primitives.Popup.Child%2A> 内容的逻辑父级。  
  
## 请参阅  
 <xref:System.Windows.Controls.Primitives.Popup>   
 <xref:System.Windows.Controls.Primitives.PopupPrimaryAxis>   
 <xref:System.Windows.Controls.Primitives.PlacementMode>   
 <xref:System.Windows.Controls.Primitives.CustomPopupPlacement>   
 <xref:System.Windows.Controls.Primitives.CustomPopupPlacementCallback>   
 <xref:System.Windows.Controls.ToolTip>   
 <xref:System.Windows.Controls.ToolTipService>   
 [帮助主题](../../../../docs/framework/wpf/controls/popup-how-to-topics.md)   
 [帮助主题](../../../../docs/framework/wpf/controls/tooltip-how-to-topics.md)