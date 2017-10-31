---
title: "演练：使用 WindowsFormsHost 元素映射属性 | Microsoft Docs"
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
  - "映射属性"
  - "WindowsFormsHost 元素属性映射"
ms.assetid: 74809167-bf8e-48b7-a2e7-b4ea08bc7d8c
caps.latest.revision: 21
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 21
---
# 演练：使用 WindowsFormsHost 元素映射属性
本演练演示如何使用<xref:System.Windows.Forms.Integration.WindowsFormsHost.PropertyMap%2A>属性进行映射[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]属性添加到上一个承载的相应属性[!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)]控件。  
  
 本演练涉及以下任务：  
  
-   创建项目。  
  
-   定义应用程序布局。  
  
-   定义新的属性映射。  
  
-   正在删除的默认属性映射。  
  
-   正在替换的默认属性映射。  
  
-   扩展默认属性映射。  
  
 在本演练中所示的任务的完整代码列表，请参阅[映射属性使用 WindowsFormsHost 元素示例](http://go.microsoft.com/fwlink/?LinkID=160019)。  
  
 当完成后，您将能够映射[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]属性添加到上一个承载的相应属性[!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)]控件。  
  
## <a name="prerequisites"></a>先决条件  
 你需要以下组件来完成本演练：  
  
-   [!INCLUDE[vs_orcas_long](../../../../includes/vs-orcas-long-md.md)]。  
  
## <a name="creating-the-project"></a>创建项目  
  
#### <a name="to-create-and-set-up-the-project"></a>若要创建并设置项目  
  
1.  创建一个名为的 WPF 应用程序项目`PropertyMappingWithWfhSample`。  
  
2.  在解决方案资源管理器，将添加到名为 WindowsFormsIntegration.dll 的 WindowsFormsIntegration 程序集的引用。  
  
3.  在解决方案资源管理器，添加对 System.Drawing 和 System.Windows.Forms 程序集的引用。  
  
## <a name="defining-the-application-layout"></a>定义应用程序布局  
 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]-基于应用程序使用<xref:System.Windows.Forms.Integration.WindowsFormsHost>元素来承载[!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)]控件。  
  
#### <a name="to-define-the-application-layout"></a>若要定义应用程序布局  
  
1.  打开 Window1.xaml 中的[!INCLUDE[wpfdesigner_current_short](../../../../includes/wpfdesigner-current-short-md.md)]。  
  
2.  用下面的代码替换现有代码。  
  
     [!code-xml[PropertyMappingWithWfhSample#1](../../../../samples/snippets/csharp/VS_Snippets_Wpf/PropertyMappingWithWfhSample/CSharp/PropertyMappingWithWfh/Window1.xaml#1)]  
  
3.  在代码编辑器中打开 window1.xaml.cs。  
  
4.  在文件顶部导入以下命名空间。  
  
     [!code-csharp[PropertyMappingWithWfhSample#20](../../../../samples/snippets/csharp/VS_Snippets_Wpf/PropertyMappingWithWfhSample/CSharp/PropertyMappingWithWfh/Window1.xaml.cs#20)]
     [!code-vb[PropertyMappingWithWfhSample#20](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/PropertyMappingWithWfhSample/VisualBasic/PropertyMappingWithWfh/Window1.xaml.vb#20)]  
  
## <a name="defining-a-new-property-mapping"></a>定义新的属性映射  
 <xref:System.Windows.Forms.Integration.WindowsFormsHost>元素提供了一些默认属性的映射。 通过调用将添加新的属性映射<xref:System.Windows.Forms.Integration.PropertyMap.Add%2A>方法<xref:System.Windows.Forms.Integration.WindowsFormsHost>元素的<xref:System.Windows.Forms.Integration.WindowsFormsHost.PropertyMap%2A>。  
  
#### <a name="to-define-a-new-property-mapping"></a>若要定义新的属性映射  
  
-   将以下代码复制到的定义`Window1`类。  
  
     [!code-csharp[PropertyMappingWithWfhSample#14](../../../../samples/snippets/csharp/VS_Snippets_Wpf/PropertyMappingWithWfhSample/CSharp/PropertyMappingWithWfh/Window1.xaml.cs#14)]
     [!code-vb[PropertyMappingWithWfhSample#14](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/PropertyMappingWithWfhSample/VisualBasic/PropertyMappingWithWfh/Window1.xaml.vb#14)]  
  
     `AddClipMapping`方法添加的新映射<xref:System.Windows.UIElement.Clip%2A>属性。  
  
     `OnClipChange`方法转换为<xref:System.Windows.UIElement.Clip%2A>属性设置为[!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)]<xref:System.Windows.Forms.Control.Region%2A>属性。  
  
     `Window1_SizeChanged`方法处理窗口的<xref:System.Windows.FrameworkElement.SizeChanged>事件并调整其大小以适应应用程序窗口的剪辑区域。  
  
## <a name="removing-a-default-property-mapping"></a>删除默认属性映射  
 通过调用来移除默认属性映射<xref:System.Windows.Forms.Integration.PropertyMap.Remove%2A>方法<xref:System.Windows.Forms.Integration.WindowsFormsHost>元素的<xref:System.Windows.Forms.Integration.WindowsFormsHost.PropertyMap%2A>。  
  
#### <a name="to-remove-a-default-property-mapping"></a>若要删除的默认属性映射  
  
-   将以下代码复制到的定义`Window1`类。  
  
     [!code-csharp[PropertyMappingWithWfhSample#13](../../../../samples/snippets/csharp/VS_Snippets_Wpf/PropertyMappingWithWfhSample/CSharp/PropertyMappingWithWfh/Window1.xaml.cs#13)]
     [!code-vb[PropertyMappingWithWfhSample#13](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/PropertyMappingWithWfhSample/VisualBasic/PropertyMappingWithWfh/Window1.xaml.vb#13)]  
  
     `RemoveCursorMapping`方法中删除的默认映射<xref:System.Windows.FrameworkElement.Cursor%2A>属性。  
  
## <a name="replacing-a-default-property-mapping"></a>替换默认属性映射  
 通过删除默认映射，并调用替换默认属性映射<xref:System.Windows.Forms.Integration.PropertyMap.Add%2A>方法<xref:System.Windows.Forms.Integration.WindowsFormsHost>元素的<xref:System.Windows.Forms.Integration.WindowsFormsHost.PropertyMap%2A>。  
  
#### <a name="to-replace-a-default-property-mapping"></a>若要替换的默认属性映射  
  
-   将以下代码复制到的定义`Window1`类。  
  
     [!code-csharp[PropertyMappingWithWfhSample#12](../../../../samples/snippets/csharp/VS_Snippets_Wpf/PropertyMappingWithWfhSample/CSharp/PropertyMappingWithWfh/Window1.xaml.cs#12)]
     [!code-vb[PropertyMappingWithWfhSample#12](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/PropertyMappingWithWfhSample/VisualBasic/PropertyMappingWithWfh/Window1.xaml.vb#12)]  
  
     `ReplaceFlowDirectionMapping`方法会将替换的默认映射<xref:System.Windows.FrameworkElement.FlowDirection%2A>属性。  
  
     `OnFlowDirectionChange`方法转换为<xref:System.Windows.FrameworkElement.FlowDirection%2A>属性设置为[!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)] <xref:System.Windows.Forms.Control.RightToLeft%2A>属性。  
  
     `cb_CheckedChanged`方法将处理<xref:System.Windows.Forms.CheckBox.CheckedChanged>上的事件<xref:System.Windows.Forms.CheckBox>控件。 它将分配<xref:System.Windows.FrameworkElement.FlowDirection%2A>基于属性的值的<xref:System.Windows.Forms.CheckBox.CheckState%2A>属性  
  
## <a name="extending-a-default-property-mapping"></a>扩展默认属性映射  
 可以使用的默认属性映射，并还可以使用自己的映射进行扩展。  
  
#### <a name="to-extend-a-default-property-mapping"></a>若要扩展默认属性映射  
  
-   将以下代码复制到的定义`Window1`类。  
  
     [!code-csharp[PropertyMappingWithWfhSample#15](../../../../samples/snippets/csharp/VS_Snippets_Wpf/PropertyMappingWithWfhSample/CSharp/PropertyMappingWithWfh/Window1.xaml.cs#15)]
     [!code-vb[PropertyMappingWithWfhSample#15](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/PropertyMappingWithWfhSample/VisualBasic/PropertyMappingWithWfh/Window1.xaml.vb#15)]  
  
     `ExtendBackgroundMapping`方法添加到现有的自定义属性翻译人员<xref:System.Windows.Controls.Control.Background%2A>属性映射。  
  
     `OnBackgroundChange`方法分配给承载的控件的特定映像<xref:System.Windows.Forms.Control.BackgroundImage%2A>属性。 `OnBackgroundChange`应用默认属性映射后调用方法。  
  
## <a name="initializing-your-property-mappings"></a>初始化属性映射  
 通过调用前面所述的方法中设置了属性映射<xref:System.Windows.FrameworkElement.Loaded>事件处理程序。  
  
#### <a name="to-initialize-your-property-mappings"></a>若要初始化属性映射  
  
1.  将以下代码复制到的定义`Window1`类。  
  
     [!code-csharp[PropertyMappingWithWfhSample#11](../../../../samples/snippets/csharp/VS_Snippets_Wpf/PropertyMappingWithWfhSample/CSharp/PropertyMappingWithWfh/Window1.xaml.cs#11)]
     [!code-vb[PropertyMappingWithWfhSample#11](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/PropertyMappingWithWfhSample/VisualBasic/PropertyMappingWithWfh/Window1.xaml.vb#11)]  
  
     `WindowLoaded`方法将处理<xref:System.Windows.FrameworkElement.Loaded>事件并执行以下初始化。  
  
    -   创建[!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)]<xref:System.Windows.Forms.CheckBox>控件。  
  
    -   调用先前在本演练来设置属性映射中定义的方法。  
  
    -   分配到映射的属性的初始值。  
  
2.  按 F5 生成并运行该应用程序。 单击复选框可看到的效果<xref:System.Windows.FrameworkElement.FlowDirection%2A>映射。 单击复选框时，布局会反转其左右方向。  
  
## <a name="see-also"></a>另请参阅  
 <xref:System.Windows.Forms.Integration.WindowsFormsHost.PropertyMap%2A?displayProperty=fullName>   
 <xref:System.Windows.Forms.Integration.ElementHost.PropertyMap%2A?displayProperty=fullName>   
 <xref:System.Windows.Forms.Integration.WindowsFormsHost>   
 [Windows 窗体和 WPF 属性映射](../../../../docs/framework/wpf/advanced/windows-forms-and-wpf-property-mapping.md)   
 [WPF 设计器](http://msdn.microsoft.com/zh-cn/c6c65214-8411-4e16-b254-163ed4099c26)   
 [演练︰ 承载在 WPF 中的 Windows 窗体控件](../../../../docs/framework/wpf/advanced/walkthrough-hosting-a-windows-forms-control-in-wpf.md)