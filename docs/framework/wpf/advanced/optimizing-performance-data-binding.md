---
title: "优化性能：数据绑定 | Microsoft Docs"
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
  - "绑定数据, 性能"
  - "数据绑定, 性能"
ms.assetid: 1506a35d-c009-43db-9f1e-4e230ad5be73
caps.latest.revision: 8
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 7
---
# 优化性能：数据绑定
[!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)] 数据绑定为应用程序提供了一种简单而一致的方法来显示数据以及与数据交互。  元素能够以 [!INCLUDE[TLA2#tla_clr](../../../../includes/tla2sharptla-clr-md.md)] 对象和 [!INCLUDE[TLA#tla_xml](../../../../includes/tlasharptla-xml-md.md)] 形式绑定到来自各种数据源的数据。  
  
 本主题提供了一些数据绑定性能的建议。  
  
   
  
<a name="HowDataBindingReferencesAreResolved"></a>   
## 如何解析数据绑定引用  
 在讨论数据绑定性能问题之前，有必要先介绍 [!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)] 数据绑定引擎如何解析对象的绑定引用。  
  
 [!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)] 数据绑定的源可以是任何 [!INCLUDE[TLA2#tla_clr](../../../../includes/tla2sharptla-clr-md.md)] 对象。  可以将数据绑定到 [!INCLUDE[TLA2#tla_clr](../../../../includes/tla2sharptla-clr-md.md)] 对象的属性、子属性或索引器。  绑定引用是通过使用 [!INCLUDE[TLA#tla_avalonwinfx](../../../../includes/tlasharptla-avalonwinfx-md.md)]反射或 <xref:System.ComponentModel.ICustomTypeDescriptor> 来解析的。  下面是三种用来解析对象绑定引用的方法。  
  
 第一种方法涉及到使用反射。  在这种情况下，使用 <xref:System.Reflection.PropertyInfo> 对象来发现属性的特性并提供对属性元数据的访问。  在使用 <xref:System.ComponentModel.ICustomTypeDescriptor> 接口时，数据绑定引擎使用此接口来访问属性值。  当对象没有静态属性集时，<xref:System.ComponentModel.ICustomTypeDescriptor> 接口尤其有用。  
  
 属性更改通知可以通过实现 <xref:System.ComponentModel.INotifyPropertyChanged> 接口或者通过使用与 <xref:System.ComponentModel.TypeDescriptor> 相关联的更改通知来提供。  但是，用来实现属性更改通知的首选策略是使用 <xref:System.ComponentModel.INotifyPropertyChanged>。  
  
 如果源对象是 [!INCLUDE[TLA2#tla_clr](../../../../includes/tla2sharptla-clr-md.md)] 对象，源属性是 [!INCLUDE[TLA2#tla_clr](../../../../includes/tla2sharptla-clr-md.md)] 属性，那么，[!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)] 数据绑定引擎必须首先使用源对象上的反射来获取 <xref:System.ComponentModel.TypeDescriptor>，然后查询 <xref:System.ComponentModel.PropertyDescriptor>。  从性能的角度看，这个反射操作序列可能会非常耗时。  
  
 解析对象引用的第二种方法涉及到一个用于实现 <xref:System.ComponentModel.INotifyPropertyChanged> 接口的 [!INCLUDE[TLA2#tla_clr](../../../../includes/tla2sharptla-clr-md.md)] 源对象和一个作为 [!INCLUDE[TLA2#tla_clr](../../../../includes/tla2sharptla-clr-md.md)] 属性的源属性。  在这种情况下，数据绑定引擎直接在源类型上使用反射并获取所需的属性。  这依旧不是最佳方法，但是它在工作集要求上的代价小于第一种方法。  
  
 解析对象引用的第三种方法涉及到一个作为 <xref:System.Windows.DependencyObject> 的源对象和一个作为 <xref:System.Windows.DependencyProperty> 的源属性。  在这种情况下，数据绑定引擎不需要使用反射，  而是由属性引擎和数据绑定引擎一起单独解析属性引用。  这是解析用于数据绑定的对象引用的最佳方法。  
  
 下表对使用这三种方法针对一千个 <xref:System.Windows.Controls.TextBlock> 元素的 <xref:System.Windows.Controls.TextBlock.Text%2A> 属性进行数据绑定的速度进行了比较。  
  
|**将 TextBlock 的 Text 属性绑定到**|**绑定时间（毫秒）**|**包括绑定时间在内的呈现时间（毫秒）**|  
|----------------------------------|------------------|---------------------------|  
|[!INCLUDE[TLA2#tla_clr](../../../../includes/tla2sharptla-clr-md.md)] 对象的属性|115|314|  
|用来实现 <xref:System.ComponentModel.INotifyPropertyChanged> 的 [!INCLUDE[TLA2#tla_clr](../../../../includes/tla2sharptla-clr-md.md)] 对象的属性|115|305|  
|<xref:System.Windows.DependencyObject> 的 <xref:System.Windows.DependencyProperty>。|90|263|  
  
<a name="Binding_to_Large_CLR_Objects"></a>   
## 绑定到较大的 CLR 对象  
 将数据绑定到一个具有数千个属性的 [!INCLUDE[TLA2#tla_clr](../../../../includes/tla2sharptla-clr-md.md)] 对象时，会对性能产生很大的影响。  可以通过将单个对象划分成多个具有较少属性的 [!INCLUDE[TLA2#tla_clr](../../../../includes/tla2sharptla-clr-md.md)] 对象来尽可能降低这种影响。  下表显示了将数据绑定到一个较大的 [!INCLUDE[TLA2#tla_clr](../../../../includes/tla2sharptla-clr-md.md)] 对象与绑定到多个较小的对象时所需的绑定时间和呈现时间。  
  
|**将 1000 个 TextBlock 对象的数据绑定到**|**绑定时间（毫秒）**|**包括绑定时间在内的呈现时间（毫秒）**|  
|-------------------------------------|------------------|---------------------------|  
|一个具有 1000 个属性的 [!INCLUDE[TLA2#tla_clr](../../../../includes/tla2sharptla-clr-md.md)] 对象|950|1200|  
|1000 个具有一个属性的 [!INCLUDE[TLA2#tla_clr](../../../../includes/tla2sharptla-clr-md.md)] 对象|115|314|  
  
<a name="Binding_to_an_ItemsSource"></a>   
## 绑定到 ItemsSource  
 假设有这样一种情况：您具有一个包含雇员列表的 [!INCLUDE[TLA2#tla_clr](../../../../includes/tla2sharptla-clr-md.md)] <xref:System.Collections.Generic.List%601> 对象，您希望在 <xref:System.Windows.Controls.ListBox> 中显示该雇员列表。  若要在这两个对象之间创建对应关系，应当将雇员列表绑定到 <xref:System.Windows.Controls.ListBox> 的 <xref:System.Windows.Controls.ItemsControl.ItemsSource%2A> 属性。  但是，假设有一个新雇员加入您的组。  您可能会认为，为了将这个新雇员插入到您所绑定到的 <xref:System.Windows.Controls.ListBox> 值中，只需要将这个雇员添加到雇员列表中，并希望数据绑定引擎能够自动识别这种更改。  这种假设被证明是错误的；实际上，这种更改不会自动反映在 <xref:System.Windows.Controls.ListBox> 中。  这是由于 [!INCLUDE[TLA2#tla_clr](../../../../includes/tla2sharptla-clr-md.md)] <xref:System.Collections.Generic.List%601> 对象不会自动引发集合更改事件。  为了使 <xref:System.Windows.Controls.ListBox> 能够识别所做的更改，必须重新创建雇员列表并将其重新附加到 <xref:System.Windows.Controls.ListBox> 的 <xref:System.Windows.Controls.ItemsControl.ItemsSource%2A> 属性。  使用该解决方案会对性能产生巨大影响。  每当您将 <xref:System.Windows.Controls.ListBox> 的 <xref:System.Windows.Controls.ItemsControl.ItemsSource%2A> 重新分配给新对象时，<xref:System.Windows.Controls.ListBox> 都会首先丢弃其以前的项并重新生成整个列表。  如果 <xref:System.Windows.Controls.ListBox> 映射到复杂的 <xref:System.Windows.DataTemplate>，则对性能的影响会更大。  
  
 此问题的一个非常高效的解决方案是，使雇员列表成为一个 <xref:System.Collections.ObjectModel.ObservableCollection%601>。  <xref:System.Collections.ObjectModel.ObservableCollection%601> 对象将引发一个数据绑定引擎可以收到的更改通知。  该事件会在 <xref:System.Windows.Controls.ItemsControl> 中添加或移除项，而无需重新生成整个列表。  
  
 下表显示在添加了一个项的情况下，在 UI 虚拟化功能处于关闭状态时更新 <xref:System.Windows.Controls.ListBox> 所花费的时间。  第一行中的数字表示将 [!INCLUDE[TLA2#tla_clr](../../../../includes/tla2sharptla-clr-md.md)] <xref:System.Collections.Generic.List%601> 对象绑定到 <xref:System.Windows.Controls.ListBox> 元素的 <xref:System.Windows.Controls.ItemsControl.ItemsSource%2A> 时的运行时间。  第二行中的数字表示将 <xref:System.Collections.ObjectModel.ObservableCollection%601> 绑定到 <xref:System.Windows.Controls.ListBox> 元素的 <xref:System.Windows.Controls.ItemsControl.ItemsSource%2A> 时的运行时间。  请注意，使用 <xref:System.Collections.ObjectModel.ObservableCollection%601> 数据绑定策略可大大节省时间。  
  
|**将 ItemsSource 数据绑定到**|**1 个项的更新时间（毫秒）**|  
|-----------------------------|-----------------------|  
|[!INCLUDE[TLA2#tla_clr](../../../../includes/tla2sharptla-clr-md.md)] <xref:System.Collections.Generic.List%601> 对象|1656|  
|<xref:System.Collections.ObjectModel.ObservableCollection%601>|20|  
  
<a name="Binding_IList_to_ItemsControl_not_IEnumerable"></a>   
## 将 IList（而非 IEnumerable）绑定到 ItemsControl  
 如果您需要选择是将 <xref:System.Collections.Generic.IList%601> 还是 <xref:System.Collections.IEnumerable> 绑定到 <xref:System.Windows.Controls.ItemsControl> 对象，请选择 <xref:System.Collections.Generic.IList%601> 对象。  将 <xref:System.Collections.IEnumerable> 绑定到 <xref:System.Windows.Controls.ItemsControl> 会强制 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 创建一个 <xref:System.Collections.Generic.IList%601> 包装对象，这意味着性能会受到第二个对象的不必要开销的影响。  
  
<a name="Do_not_Convert_CLR_objects_to_Xml_Just_For_Data_Binding"></a>   
## 请不要只是为了绑定数据而将 CLR 对象转换为 XML。  
 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 允许将数据绑定到 [!INCLUDE[TLA#tla_xml](../../../../includes/tlasharptla-xml-md.md)] 内容。但是，将数据绑定到 [!INCLUDE[TLA#tla_xml](../../../../includes/tlasharptla-xml-md.md)] 内容比绑定到 [!INCLUDE[TLA2#tla_clr](../../../../includes/tla2sharptla-clr-md.md)] 对象慢。  请不要只是为了绑定数据而将 [!INCLUDE[TLA2#tla_clr](../../../../includes/tla2sharptla-clr-md.md)] 对象数据转换为 XML。  
  
## 请参阅  
 [优化 WPF 应用程序性能](../../../../docs/framework/wpf/advanced/optimizing-wpf-application-performance.md)   
 [规划应用程序性能](../../../../docs/framework/wpf/advanced/planning-for-application-performance.md)   
 [利用硬件](../../../../docs/framework/wpf/advanced/optimizing-performance-taking-advantage-of-hardware.md)   
 [布局和设计](../../../../docs/framework/wpf/advanced/optimizing-performance-layout-and-design.md)   
 [二维图形和图像处理](../../../../docs/framework/wpf/advanced/optimizing-performance-2d-graphics-and-imaging.md)   
 [对象行为](../../../../docs/framework/wpf/advanced/optimizing-performance-object-behavior.md)   
 [应用程序资源](../../../../docs/framework/wpf/advanced/optimizing-performance-application-resources.md)   
 [Text](../../../../docs/framework/wpf/advanced/optimizing-performance-text.md)   
 [其他性能建议](../../../../docs/framework/wpf/advanced/optimizing-performance-other-recommendations.md)   
 [数据绑定概述](../../../../docs/framework/wpf/data/data-binding-overview.md)   
 [演练：在 WPF 应用程序中缓存应用程序数据](../../../../docs/framework/wpf/advanced/walkthrough-caching-application-data-in-a-wpf-application.md)