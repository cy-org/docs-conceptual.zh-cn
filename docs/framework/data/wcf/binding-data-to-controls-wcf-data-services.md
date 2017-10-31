---
title: "将数据绑定到控件（WCF 数据服务） | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-oob"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "客户端应用程序, WCF 数据服务"
  - "数据绑定, WCF 数据服务"
  - "WCF 数据服务, 客户端库"
ms.assetid: b32e1d49-c214-4cb1-867e-88fbb3d08c8d
caps.latest.revision: 3
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 3
---
# 将数据绑定到控件（WCF 数据服务）
借助 [!INCLUDE[ssAstoria](../../../../includes/ssastoria-md.md)]，您可以将控件（如 `ComboBox` 和 `ListView`）绑定到 <xref:System.Data.Services.Client.DataServiceCollection%601> 类的实例。该集合（继承自 <xref:System.Collections.ObjectModel.ObservableCollection%601> 类）包含来自[!INCLUDE[ssODataFull](../../../../includes/ssodatafull-md.md)] 源的数据。  此类表示一个动态数据集合，在添加项或移除项时，此集合将提供通知。  使用 <xref:System.Data.Services.Client.DataServiceCollection%601> 的实例用于数据绑定时，[!INCLUDE[ssAstoria](../../../../includes/ssastoria-md.md)] 客户端库处理这些事件来确保由 <xref:System.Data.Services.Client.DataServiceContext> 跟踪的对象与绑定 UI 元素中的数据保持同步。  
  
 <xref:System.Data.Services.Client.DataServiceCollection%601> 类（间接）实现 <xref:System.Collections.Specialized.INotifyCollectionChanged> 接口以从集合中添加或移除对象时警告上下文。  与 <xref:System.Data.Services.Client.DataServiceCollection%601> 一起使用的数据服务类型对象还必须实现 <xref:System.ComponentModel.INotifyPropertyChanged> 接口，才能在绑定集合中对象的属性发生更改时警告 <xref:System.Data.Services.Client.DataServiceCollection%601>。  
  
> [!NOTE]
>  将**“添加服务引用”**对话框或[DataSvcUtil.exe](../../../../docs/framework/data/wcf/wcf-data-service-client-utility-datasvcutil-exe.md) 工具用于 `/dataservicecollection` 选项生成客户端数据服务类时，生成的数据类将实现 <xref:System.ComponentModel.INotifyPropertyChanged> 接口。  有关详细信息，请参阅[如何：手动生成客户端数据服务类](../../../../docs/framework/data/wcf/how-to-manually-generate-client-data-service-classes-wcf-data-services.md)。  
  
## 创建绑定集合  
 可以通过使用提供的 <xref:System.Data.Services.Client.DataServiceContext> 实例调用其中一个类构造函数方法创建 <xref:System.Data.Services.Client.DataServiceCollection%601> 类的新实例，还可以创建 <xref:System.Data.Services.Client.DataServiceQuery%601> 或返回 <xref:System.Collections.Generic.IEnumerable%601> 实例的 LINQ 查询（执行时）。  此 <xref:System.Collections.Generic.IEnumerable%601> 提供对象的源用于从 [!INCLUDE[ssODataShort](../../../../includes/ssodatashort-md.md)] 源中具体化的绑定集合。  有关详细信息，请参阅[对象具体化](../../../../docs/framework/data/wcf/object-materialization-wcf-data-services.md)。  默认情况下，对绑定对象所做的更改和插入到集合的项自动由 <xref:System.Data.Services.Client.DataServiceContext> 跟踪。  如果需要手动跟踪这些更改，请调用采用 `trackingMode` 参数的构造函数方法之一并指定 <xref:System.Data.Services.Client.TrackingMode> 的值。  
  
 下面的示例演示如何基于提供的 <xref:System.Data.Services.Client.DataServiceContext> 和返回具有相关订单的所有客户的 <xref:System.Data.Services.Client.DataServiceQuery%601> 创建 <xref:System.Data.Services.Client.DataServiceCollection%601> 的实例：  
  
 [!code-csharp[Astoria Northwind Client#CustomersOrders2Binding](../../../../samples/snippets/csharp/VS_Snippets_Misc/astoria northwind client/cs/customerorders2.cs#customersorders2binding)]
 [!code-vb[Astoria Northwind Client#CustomersOrders2Binding](../../../../samples/snippets/visualbasic/VS_Snippets_Misc/astoria northwind client/vb/customerorders2.vb#customersorders2binding)]  
  
## 将数据绑定到 Windows Presentation Foundation 元素  
 因为 <xref:System.Data.Services.Client.DataServiceCollection%601> 类从 <xref:System.Collections.ObjectModel.ObservableCollection%601> 类继承，所以可以在 Windows Presentation Foundation \(WPF\) 应用程序中将对象绑定到元素或控件，像使用 <xref:System.Collections.ObjectModel.ObservableCollection%601> 类用于绑定时一样。  有关更多信息，请参见[数据绑定 \(Windows Presentation Foundation\)](../../../../docs/framework/wpf/data/data-binding-wpf.md)。  将数据服务数据绑定到 WPF 控件的一种方法是将元素的 `DataContext` 属性设置为包含查询结果的 <xref:System.Data.Services.Client.DataServiceCollection%601> 类的实例。  在本例中，使用 <xref:System.Windows.Controls.ItemsControl.ItemsSource%2A> 属性设置该控件的对象源。  使用 <xref:System.Windows.Controls.ItemsControl.DisplayMemberPath%2A> 属性指定要显示的绑定对象的属性。  若要将元素绑定到导航属性所返回的相关对象，请在为 <xref:System.Windows.Controls.ItemsControl.ItemsSource%2A> 属性定义的绑定中包含相应的路径。  该路径相对于父控件的 <xref:System.Windows.FrameworkElement.DataContext%2A> 属性所设置的根对象。  下面的示例设置 <xref:System.Windows.Controls.StackPanel> 元素的 <xref:System.Windows.FrameworkElement.DataContext%2A> 属性以将父控件绑定到客户对象的 <xref:System.Data.Services.Client.DataServiceCollection%601>：  
  
 [!code-csharp[Astoria Northwind Client#MasterDetailBinding](../../../../samples/snippets/csharp/VS_Snippets_Misc/astoria northwind client/cs/customerorderscustom.xaml.cs#masterdetailbinding)]
 [!code-csharp[Astoria Northwind Client#MasterDetailBinding](../../../../samples/snippets/csharp/VS_Snippets_Misc/astoria northwind client/cs/customerorderswpf.xaml.cs#masterdetailbinding)]
 [!code-vb[Astoria Northwind Client#MasterDetailBinding](../../../../samples/snippets/visualbasic/VS_Snippets_Misc/astoria northwind client/vb/customerorderscustom.xaml.vb#masterdetailbinding)]
 [!code-vb[Astoria Northwind Client#MasterDetailBinding](../../../../samples/snippets/visualbasic/VS_Snippets_Misc/astoria northwind client/vb/customerorderswpf.xaml.vb#masterdetailbinding)]
 [!code-vb[Astoria Northwind Client#MasterDetailBinding](../../../../samples/snippets/visualbasic/VS_Snippets_Misc/astoria northwind client/vb/customerorderscustom2.xaml.vb#masterdetailbinding)]  
  
 下面的示例显示 <xref:System.Windows.Controls.DataGrid> 和 <xref:System.Windows.Controls.ComboBox> 子控件的 XAML 绑定定义：  
  
 [!code-xml[Astoria Northwind Client#MasterDetailXaml](../../../../samples/snippets/visualbasic/VS_Snippets_Misc/astoria northwind client/vb/customerorderswpf.xaml#masterdetailxaml)]  
  
 有关详细信息，请参阅[如何：将数据绑定到 Windows Presentation Foundation 元素](../../../../docs/framework/data/wcf/bind-data-to-wpf-elements-wcf-data-services.md)。  
  
 如果某实体参与一对多或多对多关系，该关系的导航属性返回相关对象的集合。  使用**“添加服务引用”**对话框或 DataSvcUtil.exe 工具生成客户端数据服务类时，导航属性返回 <xref:System.Data.Services.Client.DataServiceCollection%601> 的实例。  这使您可以将相关对象绑定到控件，并支持常见的 WPF 绑定方案，例如相关实体的主\/从绑定模式。  在上面的 XAML 示例中，XAML 代码将主 <xref:System.Data.Services.Client.DataServiceCollection%601> 绑定到根数据元素。  然后订单 <xref:System.Windows.Controls.DataGrid> 绑定到从所选的 Customers 对象返回的订单 <xref:System.Data.Services.Client.DataServiceCollection%601>，后者又绑定到 <xref:System.Windows.Window> 的根数据元素。  
  
## 将数据绑定到 Windows 窗体控件  
 若要将对象绑定到 Windows 窗体控件，请将该控件的 `DataSource` 属性设置为包含查询结果的 <xref:System.Data.Services.Client.DataServiceCollection%601> 类的实例。  
  
> [!NOTE]
>  只有通过实现 <xref:System.Collections.Specialized.INotifyCollectionChanged> 和 <xref:System.ComponentModel.INotifyPropertyChanged> 接口侦听更改事件的控件才支持数据绑定。  如果控件不支持这种类型的更改通知，则绑定控件中不会反映对基础 <xref:System.Data.Services.Client.DataServiceCollection%601> 所做的更改。  
  
 下面的示例将 <xref:System.Data.Services.Client.DataServiceCollection%601> 绑定到 <xref:System.Windows.Forms.ComboBox> 控件：  
  
 [!code-csharp[Astoria Northwind Client#CustomersOrdersDataBindingSpecific](../../../../samples/snippets/csharp/VS_Snippets_Misc/astoria northwind client/cs/customerorders.cs#customersordersdatabindingspecific)]
 [!code-vb[Astoria Northwind Client#CustomersOrdersDataBindingSpecific](../../../../samples/snippets/visualbasic/VS_Snippets_Misc/astoria northwind client/vb/customerorders.vb#customersordersdatabindingspecific)]  
  
 使用**“添加服务引用”**对话框生成客户端数据服务类时，还创建了基于生成的 <xref:System.Data.Services.Client.DataServiceContext> 的项目数据源。  使用该数据源，只需将项从**“数据源”**窗口拖动到设计器上，即可创建显示数据服务中数据的 UI 元素或控件。  这些项将成为绑定到数据源的应用程序 UI 中的元素。  有关详细信息，请参阅[如何：使用项目数据源绑定数据](../../../../docs/framework/data/wcf/how-to-bind-data-using-a-project-data-source-wcf-data-services.md)。  
  
## 绑定分页数据  
 可以配置数据服务来限制单个响应消息中返回的查询数据量。  有关详细信息，请参阅[配置数据服务](../../../../docs/framework/data/wcf/configuring-the-data-service-wcf-data-services.md)。  数据服务分页响应数据时，每个响应包含用于返回下一页结果的链接。  有关详细信息，请参阅[加载延迟的内容](../../../../docs/framework/data/wcf/loading-deferred-content-wcf-data-services.md)。  在这种情况下，必须通过传递从 <xref:System.Data.Services.Client.DataServiceQueryContinuation.NextLinkUri%2A> 属性获取的 URI，对 <xref:System.Data.Services.Client.DataServiceCollection%601> 调用 <xref:System.Data.Services.Client.DataServiceCollection%601.Load%2A> 方法来显式加载页，如下面的示例所示：  
  
 [!code-csharp[Astoria Northwind Client#BindPagedDataSpecific](../../../../samples/snippets/csharp/VS_Snippets_Misc/astoria northwind client/cs/customerorderswpf3.xaml.cs#bindpageddataspecific)]
 [!code-vb[Astoria Northwind Client#BindPagedDataSpecific](../../../../samples/snippets/visualbasic/VS_Snippets_Misc/astoria northwind client/vb/customerorderswpf3.xaml.vb#bindpageddataspecific)]  
  
 相关对象以类似方式进行加载。  有关详细信息，请参阅[如何：将数据绑定到 Windows Presentation Foundation 元素](../../../../docs/framework/data/wcf/bind-data-to-wpf-elements-wcf-data-services.md)。  
  
## 自定义数据绑定行为  
 使用 <xref:System.Data.Services.Client.DataServiceCollection%601> 类可以截获对集合进行更改时（例如正在添加或移除对象）和对集合中对象的属性进行更改时引发的事件。  可以修改数据绑定事件以重写默认行为，该行为包括以下约束：  
  
-   委托内未执行验证。  
  
-   添加实体自动添加相关实体。  
  
-   删除实体不删除相关实体。  
  
 创建 <xref:System.Data.Services.Client.DataServiceCollection%601> 的新实例时，可以选择指定以下参数，定义对处理绑定对象更改后引发事件的方法的委托：  
  
-   `entityChanged` \- 绑定对象的属性更改后调用的方法。  此 <xref:System.Func%602> 委托接受一个 <xref:System.Data.Services.Client.EntityChangedParams> 对象并返回一个布尔值，该值指示对 <xref:System.Data.Services.Client.DataServiceContext> 调用 <xref:System.Data.Services.Client.DataServiceContext.UpdateObject%2A> 这一默认行为是否仍应发生。  
  
-   `entityCollectionChanged` \- 从绑定集合添加或移除对象时调用的方法。  此 <xref:System.Func%602> 委托接受一个 <xref:System.Data.Services.Client.EntityCollectionChangedParams> 对象并返回一个布尔值，该值指示默认行为（即对 <xref:System.Data.Services.Client.DataServiceContext> 调用 <xref:System.Collections.Specialized.NotifyCollectionChangedAction> 操作的 <xref:System.Data.Services.Client.DataServiceContext.AddObject%2A> 或 <xref:System.Collections.Specialized.NotifyCollectionChangedAction> 操作的 <xref:System.Data.Services.Client.DataServiceContext.DeleteObject%2A>）是否仍应发生。  
  
> [!NOTE]
>  [!INCLUDE[ssAstoria](../../../../includes/ssastoria-md.md)] 不执行在这些委托中实现的自定义行为的验证。  
  
 在下面的示例中，自定义 <xref:System.Collections.Specialized.NotifyCollectionChangedAction> 操作以调用 <xref:System.Data.Services.Client.DataServiceContext.DeleteLink%2A> 和 <xref:System.Data.Services.Client.DataServiceContext.DeleteObject%2A> 方法来移除属于删除的 `Orders` 实体的 `Orders_Details` 实体。  执行此自定义操作的原因是，删除父实体时不会自动删除依赖实体。  
  
 [!code-csharp[Astoria Northwind Client#CustomersOrdersDeleteRelated](../../../../samples/snippets/csharp/VS_Snippets_Misc/astoria northwind client/cs/customerorderscustom.xaml.cs#customersordersdeleterelated)]
 [!code-vb[Astoria Northwind Client#CustomersOrdersDeleteRelated](../../../../samples/snippets/visualbasic/VS_Snippets_Misc/astoria northwind client/vb/customerorderscustom.xaml.vb#customersordersdeleterelated)]
 [!code-vb[Astoria Northwind Client#CustomersOrdersDeleteRelated](../../../../samples/snippets/visualbasic/VS_Snippets_Misc/astoria northwind client/vb/customerorderscustom2.xaml.vb#customersordersdeleterelated)]  
  
 有关详细信息，请参阅[如何：自定义数据绑定行为](../../../../docs/framework/data/wcf/how-to-customize-data-binding-behaviors-wcf-data-services.md)。  
  
 使用 <xref:System.Collections.ObjectModel.Collection%601.Remove%2A> 方法从 <xref:System.Data.Services.Client.DataServiceCollection%601> 移除对象时的默认行为是，该对象还在 <xref:System.Data.Services.Client.DataServiceContext> 中标记为已删除。  若要更改此行为，可以在发生 <xref:System.Collections.Specialized.INotifyCollectionChanged.CollectionChanged> 事件时所调用的 `entityCollectionChanged` 参数中指定对方法的委托。  
  
## 使用自定义客户端数据类的数据绑定  
 若要能够将对象加载到 <xref:System.Data.Services.Client.DataServiceCollection%601>，对象本身必须实现 <xref:System.ComponentModel.INotifyPropertyChanged> 接口。  使用**“添加服务引用”**对话框或 [DataSvcUtil.exe](../../../../docs/framework/data/wcf/wcf-data-service-client-utility-datasvcutil-exe.md) 工具实现此接口时生成数据服务客户端类。  如果提供您自己的客户端数据类，必须将其他类型的集合用于数据绑定。  如果对象更改，必须在数据绑定控件中处理事件以调用 <xref:System.Data.Services.Client.DataServiceContext> 类的以下方法：  
  
-   <xref:System.Data.Services.Client.DataServiceContext.AddObject%2A> \- 新对象添加到集合时。  
  
-   <xref:System.Data.Services.Client.DataServiceContext.DeleteObject%2A> \- 从集合中移除对象时。  
  
-   <xref:System.Data.Services.Client.DataServiceContext.UpdateObject%2A> \- 在集合中的对象上更改属性时。  
  
-   <xref:System.Data.Services.Client.DataServiceContext.AddLink%2A> \- 对象添加到相关对象的集合时。  
  
-   <xref:System.Data.Services.Client.DataServiceContext.SetLink%2A> \- 对象添加到相关对象的集合时。  
  
 有关详细信息，请参阅[更新数据服务](../../../../docs/framework/data/wcf/updating-the-data-service-wcf-data-services.md)。  
  
## 请参阅  
 [如何：手动生成客户端数据服务类](../../../../docs/framework/data/wcf/how-to-manually-generate-client-data-service-classes-wcf-data-services.md)   
 [如何：添加数据服务引用](../../../../docs/framework/data/wcf/how-to-add-a-data-service-reference-wcf-data-services.md)