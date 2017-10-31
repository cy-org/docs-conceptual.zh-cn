---
title: "Windows 窗体和 WPF 属性映射 | Microsoft Docs"
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
  - "互操作性 [WPF], Windows 窗体"
  - "属性映射 [WPF 互操作性]"
  - "Windows 窗体 [WPF], 互操作性"
  - "Windows 窗体, WPF 互操作"
  - "WindowsFormsHost 元素属性映射"
ms.assetid: 999d8298-9c04-467d-a453-86e41002057d
caps.latest.revision: 21
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 21
---
# Windows 窗体和 WPF 属性映射
[!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)]和 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 技术具有两个相似但又各不相同的属性模型。  属性映射支持在两种体系结构中的互操作，并提供下列功能：  
  
-   简化了将宿主环境中的相关属性更改映射到承载的控件或元素的操作。  
  
-   提供了对映射最常用属性的默认处理。  
  
-   简化了对默认属性的删除、重写或扩展操作。  
  
-   确保可自动检测宿主上的属性值更改并可转换为承载的控件或元素。  
  
> [!NOTE]
>  属性更改事件不会传播到承载控件或元素层次结构中。  如果由于直接设置、样式、继承、数据绑定或其他更改属性值的机制原因，属性的本地值未发生更改，则不会执行属性转换。  
  
 使用 <xref:System.Windows.Forms.Integration.WindowsFormsHost> 元素上的 <xref:System.Windows.Forms.Integration.WindowsFormsHost.PropertyMap%2A> 属性和 <xref:System.Windows.Forms.Integration.ElementHost> 控件上的 <xref:System.Windows.Forms.Integration.ElementHost.PropertyMap%2A> 属性访问属性映射。  
  
## 使用 WindowsFormsHost 元素映射属性  
 <xref:System.Windows.Forms.Integration.WindowsFormsHost> 元素使用以下转换表将默认的 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 属性转换为其 [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)]等效项。  
  
|Windows Presentation Foundation 宿主|Windows 窗体|互操作行为|  
|----------------------------------------|----------------|-----------|  
|<xref:System.Windows.Controls.Control.Background%2A><br /><br /> \(<xref:System.Windows.Media.Brush?displayProperty=fullName>\)|<xref:System.Windows.Forms.Control.BackColor%2A><br /><br /> \(<xref:System.Drawing.Color?displayProperty=fullName>\)|<xref:System.Windows.Forms.Integration.WindowsFormsHost> 元素将设置承载的控件的 <xref:System.Windows.Forms.Control.BackColor%2A> 属性和 <xref:System.Windows.Forms.Control.BackgroundImage%2A> 属性。  将使用下列规则执行映射：<br /><br /> -   如果 <xref:System.Windows.Controls.Control.Background%2A> 是纯色，则将其转换并用于设置承载的控件的 <xref:System.Windows.Forms.Control.BackColor%2A> 属性。  未在承载的控件上设置 <xref:System.Windows.Forms.Control.BackColor%2A> 属性，因为承载的控件可以继承 <xref:System.Windows.Forms.Control.BackColor%2A> 属性的值。 **Note:**  承载的控件不支持透明。  分配到 <xref:System.Windows.Forms.Control.BackColor%2A> 的任何颜色都必须是完全不透明的，且 alpha 值为 0xFF。 <br /><br /> -   如果 <xref:System.Windows.Controls.Control.Background%2A> 不是纯色，则 <xref:System.Windows.Forms.Integration.WindowsFormsHost> 控件将根据 <xref:System.Windows.Controls.Control.Background%2A> 属性创建一个位图。  <xref:System.Windows.Forms.Integration.WindowsFormsHost> 控件将此位图分配到承载的控件的 <xref:System.Windows.Forms.Control.BackgroundImage%2A> 属性。  这样，就可以呈现一种类似于透明的效果。 **Note:**  您可以重写此行为，也可以移除 <xref:System.Windows.Controls.Control.Background%2A> 属性映射。|  
|<xref:System.Windows.FrameworkElement.Cursor%2A>|<xref:System.Windows.Forms.Control.Cursor%2A>|如果未重新分配默认映射，则 <xref:System.Windows.Forms.Integration.WindowsFormsHost> 控件将遍历其上级层次结构，直到找到已设置其 <xref:System.Windows.FrameworkElement.Cursor%2A> 属性的上级为止。  此值将转换为最接近的对应 [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)]光标。<br /><br /> 如果尚未重新分配 <xref:System.Windows.FrameworkElement.ForceCursor%2A> 属性的默认映射，则遍历将在第一个 <xref:System.Windows.FrameworkElement.ForceCursor%2A> 设置为 `true` 的上级处停止。|  
|<xref:System.Windows.FrameworkElement.FlowDirection%2A><br /><br /> \(<xref:System.Windows.FlowDirection?displayProperty=fullName>\)|<xref:System.Windows.Forms.Control.RightToLeft%2A><br /><br /> \(<xref:System.Windows.Forms.RightToLeft?displayProperty=fullName>\)|<xref:System.Windows.FlowDirection> 映射到 <xref:System.Windows.Forms.RightToLeft>。<br /><br /> <xref:System.Windows.FlowDirection> 映射到 <xref:System.Windows.Forms.RightToLeft>。<br /><br /> 不映射 <xref:System.Windows.Forms.RightToLeft>。<br /><br /> <xref:System.Windows.FlowDirection?displayProperty=fullName> 映射为 <xref:System.Windows.Forms.RightToLeft?displayProperty=fullName>。|  
|<xref:System.Windows.Controls.Control.FontStyle%2A>|位于承载的控件的 <xref:System.Drawing.Font?displayProperty=fullName> 中的 <xref:System.Drawing.Font.Style%2A>|[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 属性集将转换为相应的 <xref:System.Drawing.Font>。  当这些属性中的一种发生更改时，将创建新的 <xref:System.Drawing.Font>。  对于 <xref:System.Windows.FontStyles.Normal%2A>：已禁用 <xref:System.Drawing.FontStyle>。  对于 <xref:System.Windows.FontStyles.Italic%2A> 或 <xref:System.Windows.FontStyles.Oblique%2A>：已启用 <xref:System.Drawing.FontStyle>。|  
|<xref:System.Windows.Controls.Control.FontWeight%2A>|位于承载的控件的 <xref:System.Drawing.Font?displayProperty=fullName> 中的 <xref:System.Drawing.Font.Style%2A>|[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 属性集将转换为相应的 <xref:System.Drawing.Font>。  当这些属性中的一种发生更改时，将创建新的 <xref:System.Drawing.Font>。  对于 <xref:System.Windows.FontWeights.Black%2A>、<xref:System.Windows.FontWeights.Bold%2A>、<xref:System.Windows.FontWeights.DemiBold%2A>、<xref:System.Windows.FontWeights.ExtraBold%2A>、<xref:System.Windows.FontWeights.Heavy%2A>、<xref:System.Windows.FontWeights.Medium%2A>、<xref:System.Windows.FontWeights.SemiBold%2A> 或 <xref:System.Windows.FontWeights.UltraBold%2A>：已启用 <xref:System.Drawing.FontStyle>。  对于 <xref:System.Windows.FontWeights.ExtraLight%2A>、<xref:System.Windows.FontWeights.Light%2A>、<xref:System.Windows.FontWeights.Normal%2A>、<xref:System.Windows.FontWeights.Regular%2A>、<xref:System.Windows.FontWeights.Thin%2A> 或 <xref:System.Windows.FontWeights.UltraLight%2A>：已禁用 <xref:System.Drawing.FontStyle>。|  
|<xref:System.Windows.Controls.Control.FontFamily%2A><br /><br /> <xref:System.Windows.Controls.Control.FontSize%2A><br /><br /> <xref:System.Windows.Controls.Control.FontStretch%2A><br /><br /> <xref:System.Windows.Controls.Control.FontStyle%2A><br /><br /> <xref:System.Windows.Controls.Control.FontWeight%2A>|<xref:System.Windows.Forms.Control.Font%2A><br /><br /> \(<xref:System.Drawing.Font?displayProperty=fullName>\)|[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 属性集将转换为相应的 <xref:System.Drawing.Font>。  当这些属性中的一种发生更改时，将创建新的 <xref:System.Drawing.Font>。  将根据字号调整承载的 [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)]控件的大小。<br /><br /> [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 中的字号表示为 1\/96 英寸，而 [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)]中则是 1\/72 英寸。  对应的转换公式为：<br /><br /> [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)]字号 \= [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 字号 \* 72.0 \/ 96.0。|  
|<xref:System.Windows.Controls.Control.Foreground%2A><br /><br /> \(<xref:System.Windows.Media.Brush?displayProperty=fullName>\)|<xref:System.Windows.Forms.Control.ForeColor%2A><br /><br /> \(<xref:System.Drawing.Color?displayProperty=fullName>\)|将使用下列规则执行 <xref:System.Windows.Controls.Control.Foreground%2A> 属性映射：<br /><br /> -   如果 <xref:System.Windows.Controls.Control.Foreground%2A> 是 <xref:System.Windows.Media.SolidColorBrush>，请对 <xref:System.Windows.Forms.Control.ForeColor%2A> 使用 <xref:System.Windows.Media.SolidColorBrush.Color%2A>。<br />-   如果 <xref:System.Windows.Controls.Control.Foreground%2A> 是 <xref:System.Windows.Media.GradientBrush>，请对 <xref:System.Windows.Forms.Control.ForeColor%2A> 使用偏移量值最低的 <xref:System.Windows.Media.GradientStop> 的颜色。<br />-   对于任何其他 <xref:System.Windows.Media.Brush> 类型，不更改 <xref:System.Windows.Forms.Control.ForeColor%2A>。  也就是说，使用默认值。|  
|<xref:System.Windows.UIElement.IsEnabled%2A>|<xref:System.Windows.Forms.Control.Enabled%2A>|设置 <xref:System.Windows.UIElement.IsEnabled%2A> 时，<xref:System.Windows.Forms.Integration.WindowsFormsHost> 元素将设置承载的控件上的 <xref:System.Windows.Forms.Control.Enabled%2A> 属性。|  
|<xref:System.Windows.Controls.Control.Padding%2A>|<xref:System.Windows.Forms.Control.Padding%2A>|承载的 [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)]控件上的所有四个 <xref:System.Windows.Forms.Control.Padding%2A> 属性值将设置为相同的 <xref:System.Windows.Thickness> 值。<br /><br /> -   大于 <xref:System.Int32.MaxValue> 的值均设置为 <xref:System.Int32.MaxValue>。<br />-   小于 <xref:System.Int32.MinValue> 的值均设置为 <xref:System.Int32.MinValue>。|  
|<xref:System.Windows.UIElement.Visibility%2A>|<xref:System.Windows.Forms.Control.Visible%2A>|-   <xref:System.Windows.Visibility> 映射为 <xref:System.Windows.Forms.Control.Visible%2A> \= `true`。  承载的 [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)]控件是可见的。  建议您不要将承载的控件上的 <xref:System.Windows.Forms.Control.Visible%2A> 属性显式设置为 `false`。<br />-   <xref:System.Windows.Visibility> 映射为 <xref:System.Windows.Forms.Control.Visible%2A> \= `true` 或 `false`.  不会绘制承载的 [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)]控件，其区域将折叠起来。<br />-   <xref:System.Windows.Visibility>：承载的 [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)]控件占用布局空间，但不可见。  在这种情况下，<xref:System.Windows.Forms.Control.Visible%2A> 属性设置为 `true`。  建议您不要将承载的控件上的 <xref:System.Windows.Forms.Control.Visible%2A> 属性显式设置为 `false`。|  
  
 <xref:System.Windows.Forms.Integration.WindowsFormsHost> 元素完全支持容器元素上的附加属性。  
  
 有关更多信息，请参见[演练：使用 WindowsFormsHost 元素映射属性](../../../../docs/framework/wpf/advanced/walkthrough-mapping-properties-using-the-windowsformshost-element.md)。  
  
## 更新到父属性  
 大部分父属性的更改都将导致向承载的子控件发出通知。  以下列表描述了其值更改时不会发送通知的属性。  
  
-   <xref:System.Windows.Controls.Control.Background%2A>  
  
-   <xref:System.Windows.FrameworkElement.Cursor%2A>  
  
-   <xref:System.Windows.FrameworkElement.ForceCursor%2A>  
  
-   <xref:System.Windows.UIElement.Visibility%2A>  
  
 例如，如果更改了 <xref:System.Windows.Forms.Integration.WindowsFormsHost> 元素的 <xref:System.Windows.Controls.Control.Background%2A> 属性的值，则承载的控件的 <xref:System.Windows.Forms.Control.BackColor%2A> 属性不会更改。  
  
## 使用 ElementHost 控件映射属性  
 下列属性提供了内置的更改通知。  在映射这些属性时，请不要调用 <xref:System.Windows.FrameworkElement.OnPropertyChanged%2A> 方法：  
  
-   AutoSize  
  
-   BackColor  
  
-   BackgroundImage  
  
-   BackgroundImageLayout  
  
-   BindingContext  
  
-   CausesValidation  
  
-   ContextMenu  
  
-   ContextMenuStrip  
  
-   光标  
  
-   Dock  
  
-   Enabled  
  
-   字体  
  
-   前景色  
  
-   位置  
  
-   Margin  
  
-   填充  
  
-   父级  
  
-   Region  
  
-   RightToLeft  
  
-   大小  
  
-   TabIndex  
  
-   TabStop  
  
-   Text  
  
-   Visible  
  
 <xref:System.Windows.Forms.Integration.ElementHost> 控件使用以下转换表将默认的 [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)]属性转换为其 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 等效项。  
  
 有关更多信息，请参见[演练：使用 ElementHost 控件映射属性](../../../../docs/framework/wpf/advanced/walkthrough-mapping-properties-using-the-elementhost-control.md)。  
  
|Windows 窗体宿主|Windows Presentation Foundation|互操作行为|  
|------------------|-------------------------------------|-----------|  
|<xref:System.Windows.Forms.Control.BackColor%2A><br /><br /> \(<xref:System.Drawing.Color?displayProperty=fullName>\)|<xref:System.Windows.Controls.Control.Background%2A><br /><br /> 承载的元素上的 \(<xref:System.Windows.Media.Brush?displayProperty=fullName>\)|设置此属性将强制使用 <xref:System.Windows.Media.ImageBrush> 重新绘制。  如果 <xref:System.Windows.Forms.Integration.ElementHost.BackColorTransparent%2A> 属性设置为 `false`（默认值），则此 <xref:System.Windows.Media.ImageBrush> 将以 <xref:System.Windows.Forms.Integration.ElementHost> 控件的外观为基础，包括其 <xref:System.Windows.Forms.Control.BackColor%2A>、<xref:System.Windows.Forms.Control.BackgroundImage%2A> 和 <xref:System.Windows.Forms.Control.BackgroundImageLayout%2A> 属性，以及任何附加的绘图处理程序。<br /><br /> 如果 <xref:System.Windows.Forms.Integration.ElementHost.BackColorTransparent%2A> 属性设置为 `true`，则 <xref:System.Windows.Media.ImageBrush> 将以 <xref:System.Windows.Forms.Integration.ElementHost> 控件的父级的外观为基础，包括该父级的 <xref:System.Windows.Forms.Control.BackColor%2A>、<xref:System.Windows.Forms.Control.BackgroundImage%2A> 和 <xref:System.Windows.Forms.Control.BackgroundImageLayout%2A> 属性，以及任何附加的绘图处理程序。|  
|<xref:System.Windows.Forms.Control.BackgroundImage%2A><br /><br /> \(<xref:System.Drawing.Image?displayProperty=fullName>\)|<xref:System.Windows.Controls.Control.Background%2A><br /><br /> 承载的元素上的 \(<xref:System.Windows.Media.Brush?displayProperty=fullName>\)|设置此属性，将导致产生的行为与 <xref:System.Windows.Forms.Control.BackColor%2A> 映射所描述的行为相同。|  
|<xref:System.Windows.Forms.Control.BackgroundImageLayout%2A>|<xref:System.Windows.Controls.Control.Background%2A><br /><br /> 承载的元素上的 \(<xref:System.Windows.Media.Brush?displayProperty=fullName>\)|设置此属性，将导致产生的行为与 <xref:System.Windows.Forms.Control.BackColor%2A> 映射所描述的行为相同。|  
|<xref:System.Windows.Forms.Control.Cursor%2A><br /><br /> \(<xref:System.Windows.Forms.Cursor?displayProperty=fullName>\)|<xref:System.Windows.FrameworkElement.Cursor%2A><br /><br /> \(<xref:System.Windows.Input.Cursor?displayProperty=fullName>\)|[!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)]标准光标将转换为相应的 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 标准光标。  如果 [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)]不是一个标准光标，则将分配默认值。|  
|<xref:System.Windows.Forms.Control.Enabled%2A>|<xref:System.Windows.UIElement.IsEnabled%2A>|设置 <xref:System.Windows.Forms.Control.Enabled%2A> 时，<xref:System.Windows.Forms.Integration.ElementHost> 控件将设置承载的元素上的 <xref:System.Windows.UIElement.IsEnabled%2A> 属性。|  
|<xref:System.Windows.Forms.Control.Font%2A><br /><br /> \(<xref:System.Drawing.Font?displayProperty=fullName>\)|<xref:System.Windows.Controls.Control.FontFamily%2A><br /><br /> <xref:System.Windows.Controls.Control.FontSize%2A><br /><br /> <xref:System.Windows.Controls.Control.FontStretch%2A><br /><br /> <xref:System.Windows.Controls.Control.FontStyle%2A><br /><br /> <xref:System.Windows.Controls.Control.FontWeight%2A>|<xref:System.Windows.Forms.Control.Font%2A> 值将转换为相应 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 字体属性集。|  
|<xref:System.Drawing.Font.Bold%2A>|承载的元素上的 <xref:System.Windows.Controls.Control.FontWeight%2A>|如果 <xref:System.Drawing.Font.Bold%2A> 为 `true`，则 <xref:System.Windows.Controls.Control.FontWeight%2A> 设置为 <xref:System.Windows.FontWeights.Bold%2A>。<br /><br /> 如果 <xref:System.Drawing.Font.Bold%2A> 为 `false`，则 <xref:System.Windows.Controls.Control.FontWeight%2A> 设置为 <xref:System.Windows.FontWeights.Normal%2A>。|  
|<xref:System.Drawing.Font.Italic%2A>|承载的元素上的 <xref:System.Windows.Controls.Control.FontStyle%2A>|如果 <xref:System.Drawing.Font.Italic%2A> 为 `true`，则 <xref:System.Windows.Controls.Control.FontStyle%2A> 设置为 <xref:System.Windows.FontStyles.Italic%2A>。<br /><br /> 如果 <xref:System.Drawing.Font.Italic%2A> 为 `false`，则 <xref:System.Windows.Controls.Control.FontStyle%2A> 设置为 <xref:System.Windows.FontStyles.Normal%2A>。|  
|<xref:System.Drawing.Font.Strikeout%2A>|承载的元素上的 <xref:System.Windows.TextDecorations>|仅当承载 <xref:System.Windows.Controls.TextBlock> 控件时才适用。|  
|<xref:System.Drawing.Font.Underline%2A>|承载的元素上的 <xref:System.Windows.TextDecorations>|仅当承载 <xref:System.Windows.Controls.TextBlock> 控件时才适用。|  
|<xref:System.Windows.Forms.Control.RightToLeft%2A><br /><br /> \(<xref:System.Windows.Forms.RightToLeft?displayProperty=fullName>\)|<xref:System.Windows.FrameworkElement.FlowDirection%2A><br /><br /> \(<xref:System.Windows.FlowDirection>\)|<xref:System.Windows.Forms.RightToLeft> 映射到 <xref:System.Windows.FlowDirection>。<br /><br /> <xref:System.Windows.Forms.RightToLeft> 映射到 <xref:System.Windows.FlowDirection>。|  
|<xref:System.Windows.Forms.Control.Visible%2A>|<xref:System.Windows.UIElement.Visibility%2A>|<xref:System.Windows.Forms.Integration.ElementHost> 控件通过使用下列规则设置承载的元素上的 <xref:System.Windows.UIElement.Visibility%2A> 属性：<br /><br /> -   <xref:System.Windows.Forms.Control.Visible%2A> \= `true` 映射为 <xref:System.Windows.Visibility>。<br />-   <xref:System.Windows.Forms.Control.Visible%2A> \= `false` 映射为 <xref:System.Windows.Visibility>。|  
  
## 请参阅  
 <xref:System.Windows.Forms.Integration.ElementHost>   
 <xref:System.Windows.Forms.Integration.WindowsFormsHost>   
 [WPF 和 Win32 互操作](../../../../docs/framework/wpf/advanced/wpf-and-win32-interoperation.md)   
 [WPF 和 Windows 窗体互操作](../../../../docs/framework/wpf/advanced/wpf-and-windows-forms-interoperation.md)   
 [演练：使用 WindowsFormsHost 元素映射属性](../../../../docs/framework/wpf/advanced/walkthrough-mapping-properties-using-the-windowsformshost-element.md)   
 [演练：使用 ElementHost 控件映射属性](../../../../docs/framework/wpf/advanced/walkthrough-mapping-properties-using-the-elementhost-control.md)