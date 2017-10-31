---
title: "如何：定位 ToolTip | Microsoft Docs"
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
  - "定位 ToolTip 控件"
  - "ToolTip 控件, 定位"
ms.assetid: cddf3757-9e5f-4ce3-a6eb-44489cf3804a
caps.latest.revision: 14
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 14
---
# 如何：定位 ToolTip
此示例演示如何指定工具提示在屏幕上的位置。  
  
## 示例  
 通过使用在 <xref:System.Windows.Controls.ToolTip> 和 <xref:System.Windows.Controls.ToolTipService> 类中定义的一组属性（包含五个属性），可以定位工具提示。  下表显示了这两组属性（每组中包含五个属性），并根据类提供了指向其参考文档的链接。  
  
### 与类相对应的工具提示属性  
  
|<xref:System.Windows.Controls.ToolTip?displayProperty=fullName> 类属性|<xref:System.Windows.Controls.ToolTipService?displayProperty=fullName> 类属性|  
|-------------------------------------------------------------------------------------------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------|  
|<xref:System.Windows.Controls.ToolTip.Placement%2A?displayProperty=fullName>|<xref:System.Windows.Controls.ToolTipService.Placement%2A?displayProperty=fullName>|  
|<xref:System.Windows.Controls.ToolTip.PlacementTarget%2A?displayProperty=fullName>|<xref:System.Windows.Controls.ToolTipService.PlacementTarget%2A?displayProperty=fullName>|  
|<xref:System.Windows.Controls.ToolTip.PlacementRectangle%2A?displayProperty=fullName>|<xref:System.Windows.Controls.ToolTipService.PlacementRectangle%2A?displayProperty=fullName>|  
|<xref:System.Windows.Controls.ToolTip.HorizontalOffset%2A?displayProperty=fullName>|<xref:System.Windows.Controls.ToolTipService.HorizontalOffset%2A?displayProperty=fullName>|  
|<xref:System.Windows.Controls.ToolTip.VerticalOffset%2A?displayProperty=fullName>|<xref:System.Windows.Controls.ToolTipService.VerticalOffset%2A?displayProperty=fullName>|  
  
 如果使用 <xref:System.Windows.Controls.ToolTip> 对象定义工具提示的内容，则可以使用任一类的属性；但是，<xref:System.Windows.Controls.ToolTipService> 属性优先级较高。  对未定义为 <xref:System.Windows.Controls.ToolTip> 对象的工具提示使用 <xref:System.Windows.Controls.ToolTipService> 属性。  
  
 下图演示如何使用这些属性定位工具提示。  虽然，这些图中的 [!INCLUDE[TLA#tla_xaml](../../../../includes/tlasharptla-xaml-md.md)] 示例演示了如何设置由 <xref:System.Windows.Controls.ToolTip> 类定义的属性，但是 <xref:System.Windows.Controls.ToolTipService> 类的对应属性仍然遵循相同的布局规则。  有关可能的 Placement 属性值的更多信息，请参见[Popup 放置行为](../../../../docs/framework/wpf/controls/popup-placement-behavior.md)。  
  
 ![ToolTip 定位](../../../../docs/framework/wpf/controls/media/tooltipplacement.png "ToolTipPlacement")  
使用 Placement 属性定位工具提示  
  
 ![通过使用定位矩形来定位 ToolTip](../../../../docs/framework/wpf/controls/media/tooltipplacementrectangle.png "ToolTipPlacementRectangle")  
使用 Placement 和 PlacementRectangle 属性定位工具提示  
  
 ![ToolTip 定位示意图](../../../../docs/framework/wpf/controls/media/tooltipplacementprhv.png "ToolTipPlacementPRHV")  
使用 Placement、PlacementRectangle 和 Offset 属性定位工具提示  
  
 下面的示例演示如何使用 <xref:System.Windows.Controls.ToolTip> 属性指定内容为 <xref:System.Windows.Controls.ToolTip> 对象的工具提示的位置。  
  
 [!code-xml[ToolTipService#ToolTip](../../../../samples/snippets/csharp/VS_Snippets_Wpf/ToolTipService/CSharp/Pane1.xaml#tooltip)]  
  
 [!code-csharp[ToolTipService#ToolTipCode](../../../../samples/snippets/csharp/VS_Snippets_Wpf/ToolTipService/CSharp/Pane1.xaml.cs#tooltipcode)]
 [!code-vb[ToolTipService#ToolTipCode](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/ToolTipService/visualbasic/pane1.xaml.vb#tooltipcode)]  
  
 下面的示例演示如何使用 <xref:System.Windows.Controls.ToolTipService> 属性指定内容不是 <xref:System.Windows.Controls.ToolTip> 对象的工具提示的位置。  
  
 [!code-xml[ToolTipService#NoToolTip](../../../../samples/snippets/csharp/VS_Snippets_Wpf/ToolTipService/CSharp/Pane1.xaml#notooltip)]  
  
 [!code-csharp[ToolTipService#NoToolTipCode](../../../../samples/snippets/csharp/VS_Snippets_Wpf/ToolTipService/CSharp/Pane1.xaml.cs#notooltipcode)]
 [!code-vb[ToolTipService#NoToolTipCode](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/ToolTipService/visualbasic/pane1.xaml.vb#notooltipcode)]  
  
## 请参阅  
 <xref:System.Windows.Controls.ToolTip>   
 <xref:System.Windows.Controls.ToolTipService>   
 [帮助主题](../../../../docs/framework/wpf/controls/tooltip-how-to-topics.md)   
 [ToolTip 概述](../../../../docs/framework/wpf/controls/tooltip-overview.md)   
 [Use the ContextMenuService and ToolTipService](http://msdn.microsoft.com/zh-cn/809b0e9c-d612-4cda-b8af-1a698c68f4d1)