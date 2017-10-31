---
title: "演练：使用 ElementHost 控件映射属性 | Microsoft Docs"
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
  - "ElementHost 控件, 映射属性"
  - "映射属性"
ms.assetid: bccd6e0d-2272-4924-9107-ff8ed58b88aa
caps.latest.revision: 14
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 14
---
# 演练：使用 ElementHost 控件映射属性
本演练显示如何使用 <xref:System.Windows.Forms.Integration.ElementHost.PropertyMap%2A> 属性将 [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)]属性映射至承载的 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 元素上的相应属性。  
  
 本演练涉及以下任务：  
  
-   创建项目。  
  
-   定义新的属性映射。  
  
-   移除默认属性映射。  
  
-   扩展默认属性映射。  
  
 有关本演练中所阐释任务的完整代码清单，请参见 [Mapping Properties Using the ElementHost Control Sample](http://go.microsoft.com/fwlink/?LinkID=160018)（使用 ElementHost 控件映射属性示例）。  
  
 完成后，您将能够将 [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)]属性映射至承载的元素上相应的 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 属性。  
  
## 系统必备  
 您需要以下组件来完成本演练：  
  
-   [!INCLUDE[vs_orcas_long](../../../../includes/vs-orcas-long-md.md)].  
  
## 创建项目  
  
#### 创建项目  
  
1.  创建一个名为 `PropertyMappingWithElementHost` 的 [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)]应用程序项目。  有关更多信息，请参见[How to: Create a Windows Application Project](http://msdn.microsoft.com/zh-cn/b2f93fed-c635-4705-8d0e-cf079a264efa)。  
  
2.  在解决方案资源管理器中，添加对以下 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 程序集的引用。  
  
    -   PresentationCore  
  
    -   PresentationFramework  
  
    -   WindowsBase  
  
    -   WindowsFormsIntegration  
  
3.  将下面的代码复制到 `Form1` 代码文件的顶部。  
  
     [!code-csharp[PropertyMappingWithElementHost#10](../../../../samples/snippets/csharp/VS_Snippets_Wpf/PropertyMappingWithElementHost/CSharp/PropertyMappingWithElementHost/Form1.cs#10)]
     [!code-vb[PropertyMappingWithElementHost#10](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/PropertyMappingWithElementHost/VisualBasic/PropertyMappingWithElementHost/Form1.vb#10)]  
  
4.  在 Windows 窗体设计器中打开 `Form1`。  双击窗体为 <xref:System.Windows.Forms.Form.Load> 事件添加事件处理程序。  
  
5.  返回至 Windows 窗体设计器，为该窗体的 <xref:System.Windows.Forms.Control.Resize> 事件添加事件处理程序。  有关更多信息，请参见[How to: Create Event Handlers Using the Designer](http://msdn.microsoft.com/zh-cn/8461e9b8-14e8-406f-936e-3726732b23d2)。  
  
6.  在 `Form1` 类中，声明一个 <xref:System.Windows.Forms.Integration.ElementHost> 字段。  
  
     [!code-csharp[PropertyMappingWithElementHost#16](../../../../samples/snippets/csharp/VS_Snippets_Wpf/PropertyMappingWithElementHost/CSharp/PropertyMappingWithElementHost/Form1.cs#16)]
     [!code-vb[PropertyMappingWithElementHost#16](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/PropertyMappingWithElementHost/VisualBasic/PropertyMappingWithElementHost/Form1.vb#16)]  
  
## 定义新的属性映射。  
 <xref:System.Windows.Forms.Integration.ElementHost> 控件提供若干默认属性映射。  您可以通过对 <xref:System.Windows.Forms.Integration.ElementHost> 控件的 <xref:System.Windows.Forms.Integration.ElementHost.PropertyMap%2A> 调用 <xref:System.Windows.Forms.Integration.PropertyMap.Add%2A> 方法来添加新的属性映射。  
  
#### 定义新的属性映射  
  
1.  将下面的代码复制到 `Form1` 类的定义中。  
  
     [!code-csharp[PropertyMappingWithElementHost#12](../../../../samples/snippets/csharp/VS_Snippets_Wpf/PropertyMappingWithElementHost/CSharp/PropertyMappingWithElementHost/Form1.cs#12)]
     [!code-vb[PropertyMappingWithElementHost#12](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/PropertyMappingWithElementHost/VisualBasic/PropertyMappingWithElementHost/Form1.vb#12)]  
  
     `AddMarginMapping` 方法为 <xref:System.Windows.Forms.Control.Margin%2A> 属性添加一个新的映射。  
  
     `OnMarginChange` 方法将 <xref:System.Windows.Forms.Control.Margin%2A> 属性转换为 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] <xref:System.Windows.FrameworkElement.Margin%2A> 属性。  
  
2.  将下面的代码复制到 `Form1` 类的定义中。  
  
     [!code-csharp[PropertyMappingWithElementHost#14](../../../../samples/snippets/csharp/VS_Snippets_Wpf/PropertyMappingWithElementHost/CSharp/PropertyMappingWithElementHost/Form1.cs#14)]
     [!code-vb[PropertyMappingWithElementHost#14](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/PropertyMappingWithElementHost/VisualBasic/PropertyMappingWithElementHost/Form1.vb#14)]  
  
     `AddRegionMapping` 方法为 <xref:System.Windows.Forms.Control.Region%2A> 属性添加一个新的映射。  
  
     `OnRegionChange` 方法将 <xref:System.Windows.Forms.Control.Region%2A> 属性转换为 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] <xref:System.Windows.UIElement.Clip%2A> 属性。  
  
     `Form1_Resize` 方法处理窗体的 <xref:System.Windows.Forms.Control.Resize> 事件，并调整剪辑区域的大小以适合所承载的元素。  
  
## 移除默认属性映射  
 通过对 <xref:System.Windows.Forms.Integration.ElementHost> 控件的 <xref:System.Windows.Forms.Integration.ElementHost.PropertyMap%2A> 调用 <xref:System.Windows.Forms.Integration.PropertyMap.Remove%2A> 方法来移除默认属性映射。  
  
#### 移除默认属性映射  
  
-   将下面的代码复制到 `Form1` 类的定义中。  
  
     [!code-csharp[PropertyMappingWithElementHost#13](../../../../samples/snippets/csharp/VS_Snippets_Wpf/PropertyMappingWithElementHost/CSharp/PropertyMappingWithElementHost/Form1.cs#13)]
     [!code-vb[PropertyMappingWithElementHost#13](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/PropertyMappingWithElementHost/VisualBasic/PropertyMappingWithElementHost/Form1.vb#13)]  
  
     `RemoveCursorMapping` 方法删除 <xref:System.Windows.Forms.Control.Cursor%2A> 属性的默认映射。  
  
## 扩展默认属性映射  
 您可以使用默认属性映射，也可以利用自己的映射对其进行扩展。  
  
#### 扩展默认属性映射  
  
-   将下面的代码复制到 `Form1` 类的定义中。  
  
     [!code-csharp[PropertyMappingWithElementHost#15](../../../../samples/snippets/csharp/VS_Snippets_Wpf/PropertyMappingWithElementHost/CSharp/PropertyMappingWithElementHost/Form1.cs#15)]
     [!code-vb[PropertyMappingWithElementHost#15](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/PropertyMappingWithElementHost/VisualBasic/PropertyMappingWithElementHost/Form1.vb#15)]  
  
     `ExtendBackColorMapping` 方法将一个自定义的属性转换器添加到现有的 <xref:System.Windows.Forms.Control.BackColor%2A> 属性映射中。  
  
     `OnBackColorChange` 方法将一个特定的图像指定给所承载的控件的 <xref:System.Windows.Controls.Control.Background%2A> 属性。  在应用默认属性映射后，会调用 `OnBackColorChange` 方法。  
  
## 初始化属性映射  
  
#### 初始化属性映射  
  
1.  将下面的代码复制到 `Form1` 类的定义中。  
  
     [!code-csharp[PropertyMappingWithElementHost#11](../../../../samples/snippets/csharp/VS_Snippets_Wpf/PropertyMappingWithElementHost/CSharp/PropertyMappingWithElementHost/Form1.cs#11)]
     [!code-vb[PropertyMappingWithElementHost#11](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/PropertyMappingWithElementHost/VisualBasic/PropertyMappingWithElementHost/Form1.vb#11)]  
  
     `Form1_Load` 方法处理 <xref:System.Windows.Forms.Form.Load> 事件并执行以下初始化。  
  
    -   创建一个 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] <xref:System.Windows.Controls.Button> 元素。  
  
    -   调用在本演练前面部分定义的方法，来设置属性映射。  
  
    -   将初始值赋值给已映射的属性  
  
2.  按 F5 生成并运行该应用程序。  
  
## 请参阅  
 <xref:System.Windows.Forms.Integration.ElementHost.PropertyMap%2A?displayProperty=fullName>   
 <xref:System.Windows.Forms.Integration.WindowsFormsHost.PropertyMap%2A?displayProperty=fullName>   
 <xref:System.Windows.Forms.Integration.WindowsFormsHost>   
 [Windows 窗体和 WPF 属性映射](../../../../docs/framework/wpf/advanced/windows-forms-and-wpf-property-mapping.md)   
 [WPF 设计器](http://msdn.microsoft.com/zh-cn/c6c65214-8411-4e16-b254-163ed4099c26)   
 [演练：在 Windows 窗体中承载 WPF 复合控件](../../../../docs/framework/wpf/advanced/walkthrough-hosting-a-wpf-composite-control-in-windows-forms.md)