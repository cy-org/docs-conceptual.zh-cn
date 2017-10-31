---
title: "控件 | Microsoft Docs"
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology:
- dotnet-wpf
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- controls [WPF], about WPF controls
ms.assetid: 3f255a8a-35a8-4712-9065-472ff7d75599
caps.latest.revision: 13
author: dotnet-bot
ms.author: dotnetcontent
manager: wpickett
ms.translationtype: Machine Translation
ms.sourcegitcommit: 9f5b8ebb69c9206ff90b05e748c64d29d82f7a16
ms.openlocfilehash: 7652a2e64cdc107546ac3ea51178a3542606bd43
ms.contentlocale: zh-cn
ms.lasthandoff: 05/22/2017

---
# <a name="controls"></a>控件
<a name="introduction"></a> [!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)] 附带许多几乎在所有 Windows 应用程序中都会使用的常见 UI 组件，如              <xref:System.Windows.Controls.Button>、              <xref:System.Windows.Controls.Label>、              <xref:System.Windows.Controls.TextBox>、              <xref:System.Windows.Controls.Menu> 和              <xref:System.Windows.Controls.ListBox>。 以前，这些对象称为控件。 虽然              [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] SDK 继续使用术语“控件”泛指任何代表应用程序中可见对象的类，但请务必注意，类不必从              <xref:System.Windows.Controls.Control> 类继承即可具有可见外观。 从              <xref:System.Windows.Controls.Control> 类继承的类包含一个              <xref:System.Windows.Controls.ControlTemplate>，它允许控件的使用方在无需创建新子类的情况下从根本上改变控件的外观。  本主题讨论在              [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 中使用控件（包括从              <xref:System.Windows.Controls.Control> 类继承的控件以及不从该类继承的控件）的常见方式。  
  
 
  
<a name="creating_an_instance_of_a_control"></a>   
## <a name="creating-an-instance-of-a-control"></a>创建控件的实例  
 可以通过使用                  [!INCLUDE[TLA#tla_xaml](../../../../includes/tlasharptla-xaml-md.md)] 或以代码形式向应用程序添加控件。  下面的示例演示如何创建一个向用户询问其姓名的简单应用程序。  此示例在                  [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] 中创建六个控件：两个标签、两个文本框及两个按钮。 所有控件均可使用相似方式创建。  
  
 [!code-xml[ControlsOverview#1](../../../../samples/snippets/csharp/VS_Snippets_Wpf/ControlsOverview/CSharp/Window1.xaml#1)]  
  
 以下示例在代码中创建相同的应用程序。 为简洁起见，示例中省略了                  <xref:System.Windows.Controls.Grid>、                 `grid1` 的创建过程。                   `grid1` 的列和行定义与前面的                  [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] 示例中所示的相同。  
  
 [!code-csharp[ControlsOverview#2](../../../../samples/snippets/csharp/VS_Snippets_Wpf/ControlsOverview/CSharp/AppInCode.xaml.cs#2)] [!code-vb[ControlsOverview#2](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/ControlsOverview/VisualBasic/AppInCode.xaml.vb#2)]  
  
<a name="changing_the_appearance_of_a_control"></a>   
## <a name="changing-the-appearance-of-a-control"></a>更改控件的外观  
 更改控件的外观以适应应用程序的外观，这是很常见的操作。 可以根据要达到的效果，通过执行以下操作之一来更改控件的外观：  
  
-   更改控件的属性值。  
  
-   为控件创建                          <xref:System.Windows.Style>。  
  
-   为控件新建                          <xref:System.Windows.Controls.ControlTemplate>。  
  
### <a name="changing-a-controls-property-value"></a>更改控件的属性值  
 许多控件具有支持更改控件外观的属性，例如                         <xref:System.Windows.Controls.Button> 的                         <xref:System.Windows.Controls.Control.Background%2A>。 可以在                          [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] 和代码中设置值属性。 下面的示例在                          [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] 中设置 <xref:System.Windows.Controls.Button> 的                         <xref:System.Windows.Controls.Control.Background%2A>、                          <xref:System.Windows.Controls.Control.FontSize%2A> 和                          <xref:System.Windows.Controls.Control.FontWeight%2A> 属性。  
  
 [!code-xml[ControlsOverview#3](../../../../samples/snippets/csharp/VS_Snippets_Wpf/ControlsOverview/CSharp/AppInCode.xaml#3)]  
  
 下面的示例在代码中设置相同的属性。  
  
 [!code-csharp[ControlsOverview#4](../../../../samples/snippets/csharp/VS_Snippets_Wpf/ControlsOverview/CSharp/AppInCode.xaml.cs#4)] [!code-vb[ControlsOverview#4](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/ControlsOverview/VisualBasic/AppInCode.xaml.vb#4)]  
  
### <a name="creating-a-style-for-a-control"></a>为控件创建样式  
 利用 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]，通过创建                          <xref:System.Windows.Style>，可以同时为许多控件指定相同的外观，而不是为应用程序中的每个实例设置属性。                           下面的示例创建一个                          <xref:System.Windows.Style>，它将应用于应用程序中的                          每个                          <xref:System.Windows.Controls.Button>。                          <xref:System.Windows.Style> 定义通常在                           <xref:System.Windows.ResourceDictionary>（例如                         <xref:System.Windows.FrameworkElement> 的                          <xref:System.Windows.FrameworkElement.Resources%2A> 属性）中以                          [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] 形式定义。  
  
 [!code-xml[ControlsOverview#5](../../../../samples/snippets/csharp/VS_Snippets_Wpf/ControlsOverview/CSharp/AppInCode.xaml#5)]  
  
 通过将键分配给样式并在控件的                          `Style` 属性中指定该键，还可将样式仅应用于某些特定类型的控件。  有关样式的详细信息，请参阅                          [样式设置和模板化](../../../../docs/framework/wpf/controls/styling-and-templating.md)。  
  
### <a name="creating-a-controltemplate"></a>创建 ControlTemplate  
 利用                          <xref:System.Windows.Style>，可以一次为多个控件设置属性，但有时除了通过创建                          <xref:System.Windows.Style> 可执行的操作之外，可能还希望自定义                          <xref:System.Windows.Controls.Control> 的外观。 从                         <xref:System.Windows.Controls.Control> 类继承的类具有                         <xref:System.Windows.Controls.ControlTemplate>，它用于定义                          <xref:System.Windows.Controls.Control> 的结构和外观。                         <xref:System.Windows.Controls.Control> 的                          <xref:System.Windows.Controls.Control.Template%2A> 属性是公共属性，因此可以为                          <xref:System.Windows.Controls.Control> 指定非默认的                          <xref:System.Windows.Controls.ControlTemplate>。 通常可以为                          <xref:System.Windows.Controls.Control> 指定新的                          <xref:System.Windows.Controls.ControlTemplate>（而不是从控件继承）以自定义                         <xref:System.Windows.Controls.Control> 的外观。  
  
 请考虑一个很常用的控件                          <xref:System.Windows.Controls.Button>。                           <xref:System.Windows.Controls.Button> 的主要行为是当用户单击它时让应用程序采取某些操作。  默认情况下，                          [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 中的                          <xref:System.Windows.Controls.Button> 显示为一个凸出的矩形。  开发应用程序时，用户可能希望利用                          <xref:System.Windows.Controls.Button> 的行为（即通过处理按钮的单击事件），不过，除了通过更改按钮的属性可以执行的操作外，也可以更改按钮的外观。  在这种情况下，可以创建新的                          <xref:System.Windows.Controls.ControlTemplate>。  
  
 下面的示例为                          <xref:System.Windows.Controls.Button> 创建了一个                          <xref:System.Windows.Controls.ControlTemplate>。                           <xref:System.Windows.Controls.ControlTemplate> 创建一个带圆角和渐变背景的                          <xref:System.Windows.Controls.Button>。                          <xref:System.Windows.Controls.ControlTemplate> 包含一个                          <xref:System.Windows.Controls.Border>，其                         <xref:System.Windows.Controls.Border.Background%2A> 是带有两个                          <xref:System.Windows.Media.GradientStop> 对象的                           <xref:System.Windows.Media.LinearGradientBrush>。  第一个                          <xref:System.Windows.Media.GradientStop> 使用数据绑定将                          <xref:System.Windows.Media.GradientStop> 的                          <xref:System.Windows.Media.GradientStop.Color%2A> 属性绑定到按钮背景的颜色。  当设置                          <xref:System.Windows.Controls.Button> 的                          <xref:System.Windows.Controls.Control.Background%2A> 属性时，该值的颜色将用作第一个                          <xref:System.Windows.Media.GradientStop>。 有关数据绑定的详细信息，请参阅                          [数据绑定概述](../../../../docs/framework/wpf/data/data-binding-overview.md)。 此示例还创建一个                         <xref:System.Windows.Trigger>，用于在                          <xref:System.Windows.Controls.Primitives.ButtonBase.IsPressed%2A> 为                          `true` 时更改                          <xref:System.Windows.Controls.Button> 的外观。  
  
 [!code-xml[ControlsOverview#6](../../../../samples/snippets/csharp/VS_Snippets_Wpf/ControlsOverview/CSharp/Window1.xaml#6)]  
[!code-xml[ControlsOverview#7](../../../../samples/snippets/csharp/VS_Snippets_Wpf/ControlsOverview/CSharp/AppInCode.xaml#7)]  
  
> [!NOTE]
>  为使此示例正常工作，                             <xref:System.Windows.Controls.Button> 的                              <xref:System.Windows.Controls.Control.Background%2A> 属性必须设置为                               <xref:System.Windows.Media.SolidColorBrush>。  
  
<a name="subscribing_to_events"></a>   
## <a name="subscribing-to-events"></a>订阅事件  
 可以使用                  [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] 或代码来订阅控件的事件，但只能在代码中处理事件。  下面的示例演示如何订阅                  <xref:System.Windows.Controls.Button> 的                  `Click` 事件。  
  
 [!code-xml[ControlsOverview#10](../../../../samples/snippets/csharp/VS_Snippets_Wpf/ControlsOverview/CSharp/Window1.xaml#10)]  
  
 [!code-csharp[ControlsOverview#8](../../../../samples/snippets/csharp/VS_Snippets_Wpf/ControlsOverview/CSharp/AppInCode.xaml.cs#8)] [!code-vb[ControlsOverview#8](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/ControlsOverview/VisualBasic/AppInCode.xaml.vb#8)]  
  
 下面的示例处理                  <xref:System.Windows.Controls.Button> 的                  `Click` 事件。  
  
 [!code-csharp[ControlsOverview#9](../../../../samples/snippets/csharp/VS_Snippets_Wpf/ControlsOverview/CSharp/AppInCode.xaml.cs#9)] [!code-vb[ControlsOverview#9](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/ControlsOverview/VisualBasic/AppInCode.xaml.vb#9)]  
  
<a name="rich_content_in_controls"></a>   
## <a name="rich-content-in-controls"></a>控件中的丰富内容  
 从                  <xref:System.Windows.Controls.Control> 类继承的大多数类具有包含丰富内容的能力。 例如，                  <xref:System.Windows.Controls.Label> 可以包含任意对象，例如字符串、                  <xref:System.Windows.Controls.Image> 或                 <xref:System.Windows.Controls.Panel>。  下列类支持丰富内容，可以用作                  [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 中大多数控件的基类。  
  
-   <xref:System.Windows.Controls.ContentControl>-- 从此类继承的类的部分示例包括                          <xref:System.Windows.Controls.Label>、                         <xref:System.Windows.Controls.Button> 和                          <xref:System.Windows.Controls.ToolTip>。  
  
-   <xref:System.Windows.Controls.ItemsControl>-- 从此类继承的类的部分示例包括                          <xref:System.Windows.Controls.ListBox>、                         <xref:System.Windows.Controls.Menu> 和                          <xref:System.Windows.Controls.Primitives.StatusBar>。  
  
-   <xref:System.Windows.Controls.HeaderedContentControl>-- 从此类继承的类的部分示例包括                          <xref:System.Windows.Controls.TabItem>、                         <xref:System.Windows.Controls.GroupBox> 和                          <xref:System.Windows.Controls.Expander>。  
  
-   <xref:System.Windows.Controls.HeaderedItemsControl>-- 从此类继承的类的部分示例包括                          <xref:System.Windows.Controls.MenuItem>、                         <xref:System.Windows.Controls.TreeViewItem> 和                          <xref:System.Windows.Controls.ToolBar>。  
  
-  
  
 有关这些基类的详细信息，请参阅                  [WPF 内容模型](../../../../docs/framework/wpf/controls/wpf-content-model.md)。  
  
## <a name="see-also"></a>另请参阅  
 [样式设置和模板化](../../../../docs/framework/wpf/controls/styling-and-templating.md)   
 [按类别分类的控件](../../../../docs/framework/wpf/controls/controls-by-category.md)   
 [控件库](../../../../docs/framework/wpf/controls/control-library.md)   
 [数据模板化概述](../../../../docs/framework/wpf/data/data-templating-overview.md)   
 [数据绑定概述](../../../../docs/framework/wpf/data/data-binding-overview.md)   
 [输入](../../../../docs/framework/wpf/advanced/input-wpf.md)   
 [启用命令](../../../../docs/framework/wpf/advanced/how-to-enable-a-command.md)   
 [演练：创建自定义的动画按钮](../../../../docs/framework/wpf/controls/walkthroughs-create-a-custom-animated-button.md)   
 [控件自定义](../../../../docs/framework/wpf/controls/control-customization.md)
