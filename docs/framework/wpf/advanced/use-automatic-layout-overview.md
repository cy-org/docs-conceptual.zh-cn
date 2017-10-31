---
title: "使用自动布局概述 | Microsoft Docs"
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
  - "自动布局"
  - "布局, 自动"
ms.assetid: 6fed9264-18bb-4d05-8867-1fe356c6f687
caps.latest.revision: 22
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 16
---
# 使用自动布局概述
本主题面向开发人员介绍有关如何编写带有可本地化[!INCLUDE[TLA#tla_ui#plural](../../../../includes/tlasharptla-uisharpplural-md.md)] 的 [!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)] 应用程序的准则。  过去，对 [!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)] 的本地化是一个非常费时的过程。  [!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)] 适应的每种语言都需要按像素逐一调整。  如今，可以利用适当的设计和编码标准构造 [!INCLUDE[TLA2#tla_ui#plural](../../../../includes/tla2sharptla-uisharpplural-md.md)]，从而减少本地化人员调整大小和重新定位的工作量。  编写更易于调整大小和重新定位的应用程序的方法称为自动布局，可以使用 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 应用程序设计来实现此方法。  
  
 本主题包括以下部分。  
  
<a name="autoTopLevelSectionsOUTLINE0"></a>   
-   [使用自动布局的优点](#advantages_of_autolayout)  
  
-   [自动布局和控件](#autolayout_controls)  
  
-   [自动布局和编码标准](#autolayout_coding)  
  
-   [自动布局和网格](#autolay_grids)  
  
-   [使用 IsSharedSizeScope 属性的自动布局和网格](#autolay_grids_issharedsizescope)  
  
-   [相关主题](#seeAlsoToggle)  
  
<a name="advantages_of_autolayout"></a>   
## 使用自动布局的优点  
 由于 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 演示系统非常强大灵活，所以可以利用它对应用程序中的元素设定布局，以便调整元素以适应不同语言的要求。  下面列出了自动布局的部分优点。  
  
-   [!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)] 在任意语言中的显示效果都很良好。  
  
-   减少了在翻译完文本后重新调整控件位置和大小的需要。  
  
-   减少了重新调整窗口大小的需要。  
  
-   [!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)] 布局可以在任意语言中正确呈现。  
  
-   本地化工作可以缩减为仅进行字符串翻译。  
  
<a name="autolayout_controls"></a>   
## 自动布局和控件  
 利用自动布局，应用程序可以自动调整控件的大小。  例如，控件可以更改为适应字符串的长度。  利用此功能，本地化人员可以翻译字符串；他们不再需要调整控件大小以适应翻译后的文本。  下面的示例创建了一个带有英文内容的按钮。  
  
 [!code-xml[LocalizationBtn_snip#1](../../../../samples/snippets/csharp/VS_Snippets_Wpf/LocalizationBtn_snip/CS/Pane1.xaml#1)]  
  
 在此示例中，更改文本后即可生成一个西班牙文按钮。  例如，  
  
 [!code-xml[LocalizationBtn#1](../../../../samples/snippets/csharp/VS_Snippets_Wpf/LocalizationBtn/CS/Pane1.xaml#1)]  
  
 下图演示代码示例的输出。  
  
 ![具有不同语言的文本的同一按钮](../../../../docs/framework/wpf/advanced/media/globalizationbutton.png "GlobalizationButton")  
可自动调整大小的按钮  
  
<a name="autolayout_coding"></a>   
## 自动布局和编码标准  
 使用自动布局方法需要一组编码、设计标准以及生成完全可本地化 [!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)] 的规则。  下列准则将帮助您进行自动布局的编码。  
  
|编码标准|说明|  
|----------|--------|  
|不使用绝对位置。|-   不使用 <xref:System.Windows.Controls.Canvas>，因为它会以绝对方式定位元素。<br />-   使用 <xref:System.Windows.Controls.DockPanel>、<xref:System.Windows.Controls.StackPanel> 和 <xref:System.Windows.Controls.Grid> 定位控件。<br />-   有关各种面板类型的讨论，请参见[面板概述](../../../../docs/framework/wpf/controls/panels-overview.md)。|  
|不要为窗口设定固定大小。|-   请使用 <xref:System.Windows.Window.SizeToContent%2A>。<br />-   例如：<br /><br /> [!code-xml[LocalizationGrid#2](../../../../samples/snippets/csharp/VS_Snippets_Wpf/LocalizationGrid/CS/Pane1.xaml#2)]|  
|添加 <xref:System.Windows.FrameworkElement.FlowDirection%2A>。|<ul><li>将 <xref:System.Windows.FrameworkElement.FlowDirection%2A> 添加到应用程序的根元素中。</li><li>[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 提供了一种支持水平、双向和垂直布局的简便方式。  在演示框架中，<xref:System.Windows.FrameworkElement.FlowDirection%2A> 属性可以用来定义布局。  流方向模式包括：<br /><br /> <ul><li><xref:System.Windows.FlowDirection> \(LrTb\) \- 适用于拉丁语和东亚语言等语言的水平布局。</li><li><xref:System.Windows.FlowDirection> \(RlTb\) \- 适用于阿拉伯语和希伯来语等语言的双向布局。</li></ul></li></ul>|  
|使用复合字体而不是物理字体。|<ul><li>利用复合字体，<xref:System.Windows.Controls.Control.FontFamily%2A> 属性无需进行本地化。</li><li>开发人员可以使用以下字体之一，也可以创建自己的字体。<br /><br /> <ul><li>Global User Interface</li><li>Global San Serif</li><li>Global Serif</li></ul></li></ul>|  
|添加 xml:lang。|-   在 [!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)]的根元素中添加 `xml:lang` 特性，如为英文应用程序添加 `xml:lang="en-US"`。<br />-   因为复合字体使用 `xml:lang` 来确定要使用的字体，请将此属性设置为支持多语言方案。|  
  
<a name="autolay_grids"></a>   
## 自动布局和网格  
 <xref:System.Windows.Controls.Grid> 元素对于自动布局很有用，因为开发人员可以利用它来定位元素。  <xref:System.Windows.Controls.Grid> 控件可以使用列和行排列方式在其子元素中分发可用空间。  [!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)] 元素可以跨多个单元格，并且可能在网格中还有网格。  由于通过网格可以创建和定位复杂的 [!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)]，因此网格很有用。  下面的示例演示使用网格来定位某些按钮和文本。  请注意，单元格的高度和宽度是设置为 <xref:System.Windows.GridUnitType>；因此，包含带图像按钮的单元格会调整为适应该图像。  
  
 [!code-xml[LocalizationGrid#1](../../../../samples/snippets/csharp/VS_Snippets_Wpf/LocalizationGrid/CS/Pane1.xaml#1)]  
  
 下图显示了以上代码生成的网格。  
  
 ![网格示例](../../../../docs/framework/wpf/advanced/media/glob-grid.png "glob\_grid")  
网格  
  
<a name="autolay_grids_issharedsizescope"></a>   
## 使用 IsSharedSizeScope 属性的自动布局和网格  
 <xref:System.Windows.Controls.Grid> 对于在可本地化的应用程序中创建可以调整为适应内容的控件很有用。  不过，有时您可能希望控件无论包含什么内容都可以保持为一个特定的大小。  例如，对于“确定”、“取消”和“浏览”按钮，您可能不希望按钮调整大小以适应内容。  在这种情况下，<xref:System.Windows.Controls.Grid.IsSharedSizeScope%2A?displayProperty=fullName> 附加属性对于在多个网格元素间共享同样的大小很有用。  下面的示例演示如何在多个 <xref:System.Windows.Controls.Grid> 元素之间共享列和行的大小调整数据。  
  
 [!code-xml[gridIssharedsizescopeProp#2](../../../../samples/snippets/csharp/VS_Snippets_Wpf/gridIssharedsizescopeProp/CSharp/Window1.xaml#2)]  
  
 **注意** 有关完整的代码示例，请参见[在网格之间共享大小调整属性](../../../../docs/framework/wpf/controls/how-to-share-sizing-properties-between-grids.md)。  
  
## 请参阅  
 [WPF 的全球化](../../../../docs/framework/wpf/advanced/globalization-for-wpf.md)   
 [使用自动布局创建按钮](../../../../docs/framework/wpf/advanced/how-to-use-automatic-layout-to-create-a-button.md)   
 [使用网格进行自动布局](../../../../docs/framework/wpf/advanced/how-to-use-a-grid-for-automatic-layout.md)