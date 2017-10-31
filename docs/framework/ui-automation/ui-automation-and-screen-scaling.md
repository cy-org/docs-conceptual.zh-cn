---
title: "UI Automation and Screen Scaling | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-bcl"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "scaling, screens"
  - "screens, scaling"
  - "UI (user interface), automation"
  - "UI Automation"
ms.assetid: 4380cad7-e509-448f-b9a5-6de042605fd4
caps.latest.revision: 16
author: "Xansky"
ms.author: "mhopkins"
manager: "markl"
caps.handback.revision: 16
---
# UI Automation and Screen Scaling
> [!NOTE]
>  本文档适用于想要使用 <xref:System.Windows.Automation> 命名空间中定义的托管 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] 类的 .NET Framework 开发人员。 有关 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] 的最新信息，请参阅 [Windows 自动化 API：UI 自动化](http://go.microsoft.com/fwlink/?LinkID=156746)。  
  
 [!INCLUDE[TLA#tla_longhorn](../../../includes/tlasharptla-longhorn-md.md)] 让用户能够更改 [!INCLUDE[TLA#tla_dpi](../../../includes/tlasharptla-dpi-md.md)] 设置，以便屏幕上的大多数 [!INCLUDE[TLA#tla_ui](../../../includes/tlasharptla-ui-md.md)] 元素显示得更大。 虽然 [!INCLUDE[TLA#tla_win](../../../includes/tlasharptla-win-md.md)] 中之前就已提供了此项功能，但在早期版本中，必须由应用程序实现缩放。 在 [!INCLUDE[TLA#tla_longhorn](../../../includes/tlasharptla-longhorn-md.md)] 中，桌面窗口管理器为所有不会处理其自身缩放的应用程序执行默认缩放。 UI 自动化客户端应用程序必须考虑到此功能。  
  
<a name="Scaling_in_Windows_Vista"></a>   
## Windows Vista 中的缩放  
 默认 [!INCLUDE[TLA2#tla_dpi](../../../includes/tla2sharptla-dpi-md.md)] 设置为 96，这意味着 96 像素占名义上一英寸的宽度或高度。 “一英寸”的确切度量取决于监视器的大小和物理分辨率。 例如，在 12 英寸宽、水平分辨率为 1280 像素的监视器上，96 像素的水平线将扩展大约 9\/10 英寸。  
  
 更改 [!INCLUDE[TLA2#tla_dpi](../../../includes/tla2sharptla-dpi-md.md)] 设置与更改屏幕分辨率不同。 通过 [!INCLUDE[TLA2#tla_dpi](../../../includes/tla2sharptla-dpi-md.md)] 缩放，屏幕上的物理像素数保持不变。 但是，缩放将应用于 [!INCLUDE[TLA2#tla_ui](../../../includes/tla2sharptla-ui-md.md)] 元素的大小和位置。 桌面窗口管理器 \(DWM\) 可以自动对桌面和未显式要求缩放的应用程序执行这种扩展。  
  
 实际上，当用户将缩放比例设置为 120 [!INCLUDE[TLA2#tla_dpi](../../../includes/tla2sharptla-dpi-md.md)] 时，屏幕上的垂直或水平英寸将增大 25%。 所有尺寸会相应缩放。 应用程序窗口距屏幕顶端和左边缘的偏移量将增大 25%。 如果启用了应用程序缩放，且应用程序为非 [!INCLUDE[TLA2#tla_dpi](../../../includes/tla2sharptla-dpi-md.md)] 感知应用程序，则窗口的大小按与其包含的所有 [!INCLUDE[TLA2#tla_ui](../../../includes/tla2sharptla-ui-md.md)] 元素的偏移量和大小相同的比例增大。  
  
> [!NOTE]
>  默认情况下，当用户将 [!INCLUDE[TLA2#tla_dpi](../../../includes/tla2sharptla-dpi-md.md)] 设置为 120 时，DWM 不会对非 [!INCLUDE[TLA2#tla_dpi](../../../includes/tla2sharptla-dpi-md.md)] 感知应用程序执行扩展，但当 [!INCLUDE[TLA2#tla_dpi](../../../includes/tla2sharptla-dpi-md.md)] 被设置为自定义值 144 或更高时，将执行扩展。 但是，用户可以重写默认行为。  
  
 屏幕缩放为以任何方式与屏幕坐标有关的应用程序带来了新的挑战。 屏幕现在包含两个坐标系：物理和逻辑。 点的物理坐标是距原点左上部的实际偏移量（以像素为单位）。 如果像素本身进行了缩放，则逻辑坐标为缩放后的偏移量。  
  
 假定你设计了一个对话框，其按钮位于坐标 \(100, 48\) 处。 当此对话框按默认值 96 [!INCLUDE[TLA2#tla_dpi](../../../includes/tla2sharptla-dpi-md.md)] 显示时，该按钮所处的物理坐标为 \(100, 48\)。 当为 120 [!INCLUDE[TLA2#tla_dpi](../../../includes/tla2sharptla-dpi-md.md)] 时，它所处的物理坐标为 \(125, 60\)。 但逻辑坐标与 [!INCLUDE[TLA2#tla_dpi](../../../includes/tla2sharptla-dpi-md.md)] 设置相同：\(100, 48\)。  
  
 逻辑坐标非常重要，因为它们使操作系统和应用程序的行为保持一致，而不考虑 [!INCLUDE[TLA2#tla_dpi](../../../includes/tla2sharptla-dpi-md.md)] 设置。 例如，正常情况下，<xref:System.Windows.Forms.Cursor.Position%2A?displayProperty=fullName> 将返回逻辑坐标。 如果将光标移至对话框中的某个元素，则将返回相同的坐标，而不考虑 [!INCLUDE[TLA2#tla_dpi](../../../includes/tla2sharptla-dpi-md.md)] 设置。 如果你在 \(100, 100\) 处拖动控件，它将被拖到这些逻辑坐标，并将占用与任何 [!INCLUDE[TLA2#tla_dpi](../../../includes/tla2sharptla-dpi-md.md)] 设置相同的相对位置。  
  
<a name="Scaling_in_UI_Automation_Clients"></a>   
## UI 自动化客户端中的缩放  
 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] [!INCLUDE[TLA#tla_api](../../../includes/tlasharptla-api-md.md)] 不使用逻辑坐标。 下面的方法和属性将返回物理坐标或将其用作参数。  
  
-   <xref:System.Windows.Automation.AutomationElement.GetClickablePoint%2A>  
  
-   <xref:System.Windows.Automation.AutomationElement.TryGetClickablePoint%2A>  
  
-   <xref:System.Windows.Automation.AutomationElement.ClickablePointProperty>  
  
-   <xref:System.Windows.Automation.AutomationElement.FromPoint%2A>  
  
-   <xref:System.Windows.Automation.AutomationElement.AutomationElementInformation.BoundingRectangle%2A>  
  
 默认情况下，在非 96 [!INCLUDE[TLA2#tla_dpi](../../../includes/tla2sharptla-dpi-md.md)] 环境中运行的 UI 自动化客户端应用程序将不能从这些方法和属性中获得正确的结果。 例如，由于光标的位置是逻辑坐标，客户端不能仅将这些坐标传递到 <xref:System.Windows.Automation.AutomationElement.FromPoint%2A> 以获取光标下的元素。 此外，该应用程序不能正确将 Windows 放置在其客户端区域之外。  
  
 解决方法分两个部分。  
  
1.  首先，使客户端应用程序成为 [!INCLUDE[TLA2#tla_dpi](../../../includes/tla2sharptla-dpi-md.md)] 感知的应用程序。 若要实现此目的，请在启动时调用 [!INCLUDE[TLA#tla_win32](../../../includes/tlasharptla-win32-md.md)] 函数 `SetProcessDPIAware`。 在托管代码中，以下声明使得此函数可用。  
  
     [!code-csharp[Highlighter#101](../../../samples/snippets/csharp/VS_Snippets_Wpf/Highlighter/CSharp/NativeMethods.cs#101)]
     [!code-vb[Highlighter#101](../../../samples/snippets/visualbasic/VS_Snippets_Wpf/Highlighter/VisualBasic/NativeMethods.vb#101)]  
  
     此函数使得整个进程成为 [!INCLUDE[TLA2#tla_dpi](../../../includes/tla2sharptla-dpi-md.md)] 感知的进程，这意味着属于该进程的所有窗口都不会被缩放。 例如，在 [Highlighter Sample](http://msdn.microsoft.com/zh-cn/19ba4577-753e-4efd-92cc-c02ee67c1b69) 中，构成突出显示矩形的四个窗口位于从 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] 获取的物理坐标上，而非逻辑坐标。 如果该示例不是 [!INCLUDE[TLA2#tla_dpi](../../../includes/tla2sharptla-dpi-md.md)] 感知的，将在桌面上的逻辑坐标处绘制突出显示，这将导致在非 96 [!INCLUDE[TLA2#tla_dpi](../../../includes/tla2sharptla-dpi-md.md)] 环境中错误放置。  
  
2.  若要获取光标坐标，请调用 [!INCLUDE[TLA#tla_win32](../../../includes/tlasharptla-win32-md.md)] 函数 `GetPhysicalCursorPos`。 下面的示例演示如何声明和使用此函数。  
  
     [!code-csharp[UIAClient_snip#185](../../../samples/snippets/csharp/VS_Snippets_Wpf/UIAClient_snip/CSharp/ClientForm.cs#185)]
     [!code-vb[UIAClient_snip#185](../../../samples/snippets/visualbasic/VS_Snippets_Wpf/UIAClient_snip/VisualBasic/ClientForm.vb#185)]  
  
> [!CAUTION]
>  请勿使用 <xref:System.Windows.Forms.Cursor.Position%2A?displayProperty=fullName>。 未定义此属性在扩展环境下客户端窗口以外的行为。  
  
 如果你的应用程序与非 [!INCLUDE[TLA2#tla_dpi](../../../includes/tla2sharptla-dpi-md.md)] 感知应用程序进行直接的跨进程通信，你可能需要通过使用 [!INCLUDE[TLA#tla_win32](../../../includes/tlasharptla-win32-md.md)] 函数 `PhysicalToLogicalPoint` 和 `LogicalToPhysicalPoint` 在逻辑和物理坐标之间转换。  
  
## 请参阅  
 [Highlighter Sample](http://msdn.microsoft.com/zh-cn/19ba4577-753e-4efd-92cc-c02ee67c1b69)