---
title: "WPF 版本 4.5 的新增功能 | Microsoft Docs"
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
  - "Windows Presentation Foundation, 新增功能"
  - "WPF, 新增功能"
ms.assetid: db086ae4-70bb-4862-95db-2eaca5216bc3
caps.latest.revision: 55
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 55
---
# WPF 版本 4.5 的新增功能
<a name="introduction"></a> 本主题包含有关 [!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)] 版本 4.5 中的新增功能和增强功能的信息。  
  
 本主题包含以下各节：  
  
-   [功能区控件](#ribbon_control)  
  
-   [改善性能，当显示大时设置分组数据](#grouped_virtualization)  
  
-   [VirtualizingPanel的新功能](#VirtualizingPanel)  
  
-   [绑定到静态属性](#static_properties)  
  
-   [在非UI线程访问集合](#xthread_access)  
  
-   [同步和异步验证数据](#INotifyDataErrorInfo)  
  
-   [自动更新数据绑定源](#delay)  
  
-   [绑定到实现ICustomTypeProvider的类型](#ICustomTypeProvider)  
  
-   [检索数据绑定信息从一个约束表达式](#binding_state)  
  
-   [检查有效的DataContext对象](#DisconnectedSource)  
  
-   [重新定位数据作为数据值请更改\(Live建模\)](#live_shaping)  
  
-   [改进用于建立弱支持对事件](#weak_event_pattern)  
  
-   [计划程序选件类的新方法](#async)  
  
-   [事件的标记扩展](#events_markup_extenions)  
  
<a name="ribbon_control"></a>   
## 功能区控件  
 WPF 4.5随承载一个快速访问工具栏、应用程序菜单和选项的 <xref:System.Windows.Controls.Ribbon.Ribbon> 控件。  有关更多信息，请参见[功能区概述](../Topic/Ribbon%20Overview.md)。  
  
<a name="grouped_virtualization"></a>   
## 改善性能，当显示大时设置分组数据  
 用户界面虚拟化发生，当用户界面\(UI\)元素的子集从的数据项时根据哪些项目中生成出现在屏幕上。  <xref:System.Windows.Controls.VirtualizingPanel> 定义启用分组的数据用户界面虚拟化的 <xref:System.Windows.Controls.VirtualizingPanel.IsVirtualizingWhenGrouping%2A> 附加属性。  有关分组的数据的更多信息，请参见如何:使用在XAML，的视图排序和组数据。  有关有效分组数据的更多信息，请参见中的 <xref:System.Windows.Controls.VirtualizingPanel.IsVirtualizingWhenGrouping%2A> 附加属性。  
  
<a name="VirtualizingPanel"></a>   
## VirtualizingPanel的新功能  
  
1.  可以指定 <xref:System.Windows.Controls.VirtualizingPanel>，例如 <xref:System.Windows.Controls.VirtualizingStackPanel>，使用该 <xref:System.Windows.Controls.VirtualizingPanel.ScrollUnit%2A> 附加属性，是否显示分部项目。  如果 <xref:System.Windows.Controls.VirtualizingPanel.ScrollUnit%2A> 设置为 <xref:System.Windows.Controls.ScrollUnit>， <xref:System.Windows.Controls.VirtualizingPanel> 将仅显示完全可见的项目。  如果 <xref:System.Windows.Controls.VirtualizingPanel.ScrollUnit%2A> 设置为 <xref:System.Windows.Controls.ScrollUnit>， <xref:System.Windows.Controls.VirtualizingPanel> 可以显示部分可见项。  
  
2.  使用该 <xref:System.Windows.Controls.VirtualizingPanel.CacheLength%2A> 附加属性时，，那么，当 <xref:System.Windows.Controls.VirtualizingPanel> 有效可以指定缓存的范围在视区之前或之后。  缓存是空间量在或项目没有活动视区下面。  使用缓存避免生成UI元素，并滚动到视图可以提高性能。  缓存填充在较低优先级，以便应用程序不会无响应在操作中。  <xref:System.Windows.Controls.VirtualizingPanel.CacheLengthUnit%2A?displayProperty=fullName> 属性确定 <xref:System.Windows.Controls.VirtualizingPanel.CacheLength%2A?displayProperty=fullName>使用的度量单位。  
  
<a name="static_properties"></a>   
## 绑定到静态属性  
 可以使用静态属性作为数据绑定源。  数据绑定引擎识别属性值更改时，如果静态引发事件。  例如，因此，如果选件类 `SomeClass` 定义名为 `MyProperty`的静态属性， `SomeClass` 可以定义引发的静态事件，当 `MyProperty` 的值发生更改时。  该静态事件可以使用以下签名之一。  
  
-   `public static event EventHandler MyPropertyChanged;`  
  
-   `public static event EventHandler<PropertyChangedEventArgs> StaticPropertyChanged;`  
  
 请注意在第一种情况下，选件类公开通过 <xref:System.EventArgs> 到事件处理程序命名 *PropertyName*的静态事件`Changed` 。  在第二种情况下，选件类公开通过 <xref:System.ComponentModel.PropertyChangedEventArgs> 到事件处理程序命名 `StaticPropertyChanged` 的静态事件。  实现由静态属性使用任一方法，的选件类可以选择引发属性更改通知。  
  
<a name="xthread_access"></a>   
## 在非UI线程访问集合  
 WPF可以访问和修改在线程的数据收集除了创建集合内容之外。  这使您可以使用后台线程接收从外部源的数据，如数据库，并显示用户界面线程的数据。  使用修改集合的另一个线程，用户界面保持响应对用户交互。  
  
<a name="INotifyDataErrorInfo"></a>   
## 同步和异步验证数据  
 <xref:System.ComponentModel.INotifyDataErrorInfo> 接口允许数据实体选件类实现自定义验证规则和显示验证结果异步。  此接口还支持自定义错误对象、多个错误每个属性，该属性错误和实体级错误。  有关更多信息，请参见<xref:System.ComponentModel.INotifyDataErrorInfo>。  
  
<a name="delay"></a>   
## 自动更新数据绑定源  
 如果您使用绑定到数据源的数据更新数据源，可以使用 <xref:System.Windows.Data.BindingBase.Delay%2A> 属性指定时间通过，属性在目标将更新数据源之前之后。  例如，假设有其 <xref:System.Windows.Controls.Primitives.RangeBase.Value%2A> 属性数据双向绑定到数据对象属性，并 <xref:System.Windows.Data.Binding.UpdateSourceTrigger%2A> 属性设置为 <xref:System.Windows.Data.UpdateSourceTrigger>的有 <xref:System.Windows.Controls.Slider> 。  在此示例中，那么，当用户移动 <xref:System.Windows.Controls.Slider>， <xref:System.Windows.Controls.Slider> 移动的每个像素的源更新。  ，仅当滑块的 <xref:System.Windows.Controls.Primitives.RangeBase.Value%2A> 停止更改时，源对象通常需要滑块的值。  若要防止太经常更新数据源，请使用 <xref:System.Windows.Data.BindingBase.Delay%2A> 指定源不应更新，直到一段时间段，在滚动块停止移动后。  
  
<a name="ICustomTypeProvider"></a>   
## 绑定到实现ICustomTypeProvider的类型  
 WPF支持绑定到实现 <xref:System.Reflection.ICustomTypeProvider>对象的数据，也称为自定义类型。  可以在以下情况下使用自定义类型。  
  
1.  为数据绑定的 <xref:System.Windows.PropertyPath> 。  例如， <xref:System.Windows.Data.Binding> 的 <xref:System.Windows.Data.Binding.Path%2A> 属性可以引用一个自定义类型的属性。  
  
2.  作为 <xref:System.Windows.DataTemplate.DataType%2A> 属性的值。  
  
3.  为确定在 <xref:System.Windows.Controls.DataGrid>的自动生成的列的类型。  
  
<a name="binding_state"></a>   
## 检索数据绑定信息从一个约束表达式  
 在某些情况下，您可能会收到 <xref:System.Windows.Data.Binding> 和所需信息的 <xref:System.Windows.Data.BindingExpression> 有关绑定的源和目标对象。  新API添加允许您获取源或目标对象或该关联的属性。  当您具有 <xref:System.Windows.Data.BindingExpression>时，请使用有关目标与源的以下API获取信息。  
  
|查找绑定的该值|使用此API|  
|-------------|------------|  
|目标对象|<xref:System.Windows.Data.BindingExpressionBase.Target%2A?displayProperty=fullName>|  
|目标属性|<xref:System.Windows.Data.BindingExpressionBase.TargetProperty%2A?displayProperty=fullName>|  
|源对象|<xref:System.Windows.Data.BindingExpression.ResolvedSource%2A?displayProperty=fullName>|  
|源属性|<xref:System.Windows.Data.BindingExpression.ResolvedSourcePropertyName%2A?displayProperty=fullName>|  
|<xref:System.Windows.Data.BindingExpression> 是否属于 <xref:System.Windows.Data.BindingGroup>|<xref:System.Windows.Data.BindingExpressionBase.BindingGroup%2A?displayProperty=fullName>|  
|<xref:System.Windows.Data.BindingGroup>的所有者|<xref:System.Windows.Data.BindingGroup.Owner%2A>|  
  
<a name="DisconnectedSource"></a>   
## 检查有效的DataContext对象  
 有了项目容器 <xref:System.Windows.FrameworkElement.DataContext%2A> 在 <xref:System.Windows.Controls.ItemsControl> 的断开连接的情况。  项容器是显示在 <xref:System.Windows.Controls.ItemsControl>的项目的UI元素。  当 <xref:System.Windows.Controls.ItemsControl> 的数据绑定到集合时，项容器为每个项目生成。  在某些情况下，项目容器从可视化树中移除。  项目容器中移除的两个典型的情况是项目从基础集合中移除，并在虚拟化在 <xref:System.Windows.Controls.ItemsControl>启用。  在这些情况下，项目容器的 <xref:System.Windows.FrameworkElement.DataContext%2A> 属性将设置为由 <xref:System.Windows.Data.BindingOperations.DisconnectedSource%2A?displayProperty=fullName> 静态属性返回的sentinel。对象。  您应检查 <xref:System.Windows.FrameworkElement.DataContext%2A> 是否与 <xref:System.Windows.Data.BindingOperations.DisconnectedSource%2A> 对象相同在访问项容器的 <xref:System.Windows.FrameworkElement.DataContext%2A> 之前。  
  
<a name="live_shaping"></a>   
## 重新定位数据作为数据值请更改\(Live建模\)  
 可以将一个数据，排序或筛选。  ，当修改时， WPF 4.5使数据重新排列该数据。  例如，假设应用程序在一个股票上使用 <xref:System.Windows.Controls.DataGrid> 股票列表，并股票由股票值排序。  活动对股票的 <xref:System.Windows.Data.CollectionView>有效，在 <xref:System.Windows.Controls.DataGrid> 的股票的位置移动，则该股票的值大于另一个常用的值将成为大于还是小于。  有关更多信息，请参见 <xref:System.ComponentModel.ICollectionViewLiveShaping> 接口。  
  
<a name="weak_event_pattern"></a>   
## 改进用于建立弱支持对事件  
 实现弱事件模式现在是更加容易，因为操作的用户可以参与，而不需要实现一额外的接口。  ，如果专用 <xref:System.Windows.WeakEventManager> 为某个特定事件，不存在泛型 <xref:System.Windows.WeakEventManager> 选件类还使用户能够参与弱事件模式。  有关更多信息，请参见[弱事件模式](../../../../docs/framework/wpf/advanced/weak-event-patterns.md)。  
  
<a name="async"></a>   
## 计划程序选件类的新方法  
 计划程序选件类定义同步和异步操作的新方法。  同步 <xref:System.Windows.Threading.Dispatcher.Invoke%2A> 方法定义采用 <xref:System.Action> 或 <xref:System.Func%601> 参数的重载。  新的异步方法， <xref:System.Windows.Threading.Dispatcher.InvokeAsync%2A>，也采用 <xref:System.Action> 或 <xref:System.Func%601> 作为回调参数并返回 <xref:System.Windows.Threading.DispatcherOperation> 或 <xref:System.Windows.Threading.DispatcherOperation%601>。  <xref:System.Windows.Threading.DispatcherOperation> 和 <xref:System.Windows.Threading.DispatcherOperation%601> 选件类定义一个 <xref:System.Threading.Tasks.Task> 属性。  当您调用 <xref:System.Windows.Threading.Dispatcher.InvokeAsync%2A>时，可以使用 <xref:System.Windows.Threading.DispatcherOperation> 或关联的 <xref:System.Threading.Tasks.Task>的 `await` 关键字。  如果所 <xref:System.Windows.Threading.DispatcherOperation> 或 <xref:System.Windows.Threading.DispatcherOperation%601>返回的需要同步等待 <xref:System.Threading.Tasks.Task> ，请调用 <xref:System.Windows.Threading.TaskExtensions.DispatcherOperationWait%2A> 扩展方法。  ;如果操作在调用线程，排队调用 <xref:System.Threading.Tasks.Task.Wait%2A?displayProperty=fullName> 导致死锁。  有关使用 <xref:System.Threading.Tasks.Task> 的更多信息执行异步操作，请参见 [任务并行（任务并行库）](../../../../docs/standard/parallel-programming/task-based-asynchronous-programming.md)。  
  
<a name="events_markup_extenions"></a>   
## 事件的标记扩展  
 WPF 4.5支持操作的标记扩展。  在WPF不定义为事件期间使用的标记扩展，第三方可以创建可用于事件的标记扩展。  
  
## 请参阅  
 [.NET Framework 中的新增功能](../../../../docs/framework/whats-new/index.md)