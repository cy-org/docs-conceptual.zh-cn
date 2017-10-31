---
title: "如何：使用项目数据源绑定数据（WCF 数据服务） | Microsoft Docs"
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
  - "数据绑定, WCF 数据服务"
  - "WCF 数据服务, 数据绑定"
ms.assetid: 2477af0a-676f-44f7-b73d-e66208785509
caps.latest.revision: 2
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 2
---
# 如何：使用项目数据源绑定数据（WCF 数据服务）
可以创建基于 [!INCLUDE[ssAstoria](../../../../includes/ssastoria-md.md)] 客户端应用程序中生成的数据对象的数据源。  使用**“添加服务引用”**对话框添加对数据服务的引用时，会创建项目数据源以及生成客户端数据类。为数据服务公开的每个实体集创建一个数据源。  您可以通过将这些数据源项从**“数据源”**窗口拖到设计器中来创建将显示服务中的数据的窗体。  这些项将成为绑定到该数据源的控件。  执行期间，此数据源绑定到 <xref:System.Data.Services.Client.DataServiceCollection%601> 类的实例，该类填充有数据服务查询返回的对象。  有关详细信息，请参阅[将数据绑定到控件](../../../../docs/framework/data/wcf/binding-data-to-controls-wcf-data-services.md)。  
  
 本主题中的示例使用 Northwind 示例数据服务和自动生成的客户端数据服务类。  此服务和这些客户端数据类是在完成 [WCF 数据服务快速入门](../../../../docs/framework/data/wcf/quickstart-wcf-data-services.md)时创建的。  
  
### 在 WPF 窗口中使用项目数据源  
  
1.  在 WPF 项目中，添加对 Northwind 数据服务的引用。  有关详细信息，请参阅[如何：添加数据服务引用](../../../../docs/framework/data/wcf/how-to-add-a-data-service-reference-wcf-data-services.md)。  
  
2.  在**“数据源”**窗口中，展开**“NorthwindEntities”**项目数据源中的 `Customers` 节点。  
  
3.  单击**“CustomerID”**项，在列表中选择**“组合框”**，然后将**“CustomerID”**项从**“Customers”**节点拖到设计器中。  
  
     这会在 XAML 文件中为此窗口创建以下对象元素：  
  
    -   一个名为 `customersViewSource` 的 <xref:System.Windows.Data.CollectionViewSource> 元素。  将顶级 <xref:System.Windows.Controls.Grid> 对象元素的 <xref:System.Windows.FrameworkElement.DataContext%2A> 属性设置为此新的 <xref:System.Windows.Data.CollectionViewSource>。  
  
    -   一个名为 `CustomerID` 的数据绑定 <xref:System.Windows.Controls.ComboBox>。  
  
    -   <xref:System.Windows.Controls.Label>。  
  
4.  将**“订单”**导航属性拖到设计器中。  
  
     这会在 XAML 文件中为此窗口创建以下附加对象元素：  
  
    -   另一个名为 `customersOrdersViewSource` 的 <xref:System.Windows.Data.CollectionViewSource> 元素，其源为 `customerViewSource`。  
  
    -   一个名为 `ordersDataGrid` 的数据绑定 <xref:System.Windows.Controls.DataGrid> 控件。  
  
5.  （可选）将附加项从**“Customers”**节点拖到设计器中。  
  
6.  打开窗体的代码页，并添加以下 `using` 语句（在 Visual Basic 中为 `Imports`）：  
  
     [!code-csharp[Astoria Northwind Client#CustomersOrdersUsingWpf](../../../../samples/snippets/csharp/VS_Snippets_Misc/astoria northwind client/cs/customerorderswpf2.xaml.cs#customersordersusingwpf)]  
  
7.  在定义窗体的分部类中，添加创建 <xref:System.Data.Objects.ObjectContext> 实例并定义 `customerID` 常量的以下代码。  
  
     [!code-csharp[Astoria Northwind Client#CustomersOrdersDefinitionWpf](../../../../samples/snippets/csharp/VS_Snippets_Misc/astoria northwind client/cs/customerorderswpf2.xaml.cs#customersordersdefinitionwpf)]
     [!code-vb[Astoria Northwind Client#CustomersOrdersDefinitionWpf](../../../../samples/snippets/visualbasic/VS_Snippets_Misc/astoria northwind client/vb/customerorderswpf2.xaml.vb#customersordersdefinitionwpf)]  
  
8.  在设计器中，选择该窗口。  
  
    > [!NOTE]
    >  确保您选择的是该窗口自身，而不是该窗口中的选定内容。  选择该窗口后，**“属性”**窗口顶部附近的**“名称”**文本框应当包含该窗口的名称。  
  
9. 在**“属性”**窗口中选择**“事件”**按钮。  
  
10. 找到**“Loaded”**事件，然后双击此事件旁边的下拉列表。  
  
     Visual Studio 随即打开此窗口的代码隐藏文件，并生成一个 <xref:System.Windows.FrameworkElement.Loaded> 事件处理程序。  
  
11. 在新创建的 <xref:System.Windows.FrameworkElement.Loaded> 事件处理程序中，复制并粘贴以下代码。  
  
     [!code-csharp[Astoria Northwind Client#CustomersOrdersDataBindingWpf](../../../../samples/snippets/csharp/VS_Snippets_Misc/astoria northwind client/cs/customerorderswpf2.xaml.cs#customersordersdatabindingwpf)]
     [!code-vb[Astoria Northwind Client#CustomersOrdersDataBindingWpf](../../../../samples/snippets/visualbasic/VS_Snippets_Misc/astoria northwind client/vb/customerorderswpf2.xaml.vb#customersordersdatabindingwpf)]  
  
12. 此代码根据 LINQ 查询（返回 Northwind 数据服务中 `Customers` 和相关 `Orders` 对象的 <xref:System.Collections.Generic.IEnumerable%601>）的执行情况为 `Customers` 类型创建一个 <xref:System.Data.Services.Client.DataServiceCollection%601> 实例，并将其绑定到 `customersViewSource`。  
  
### 在 Windows 窗体中使用项目数据源  
  
1.  在**“数据源”**窗口中，展开**“NorthwindEntities”**项目数据源中的**“Customers”**节点。  
  
2.  单击**“CustomerID”**项，在列表中选择**“组合框”**，然后将**“CustomerID”**项从**“Customers”**节点拖到设计器中。  
  
     这会在窗体上创建以下控件：  
  
    -   一个名为 `customersBindingSource` 的 <xref:System.Windows.Forms.BindingSource> 实例。  
  
    -   一个名为 `customersBindingNavigator` 的 <xref:System.Windows.Forms.BindingNavigator> 实例。  您可以删除此控件，因为它不是必需的。  
  
    -   一个名为 `CustomerID` 的数据绑定 <xref:System.Windows.Forms.ComboBox>。  
  
    -   <xref:System.Windows.Forms.Label>。  
  
3.  将**“订单”**导航属性拖到窗体中。  
  
4.  这会创建 `ordersBindingSource` 控件，该控件的 <xref:System.Windows.Forms.BindingSource.DataSource%2A> 属性和 <xref:System.Windows.Forms.BindingSource.DataMember%2A> 属性分别设置为 `customersBindingSource` 和 `Customers`。  此外，还会在窗体上创建 `ordersDataGridView` 数据绑定控件，并附带经过相应命名的标签控件。  
  
5.  （可选）将附加项从**“Customers”**节点拖到设计器中。  
  
6.  打开窗体的代码页，并添加以下 `using` 语句（在 Visual Basic 中为 `Imports`）：  
  
     [!code-csharp[Astoria Northwind Client#CustomersOrdersUsing](../../../../samples/snippets/csharp/VS_Snippets_Misc/astoria northwind client/cs/customerorders.cs#customersordersusing)]
     [!code-vb[Astoria Northwind Client#CustomersOrdersUsing](../../../../samples/snippets/visualbasic/VS_Snippets_Misc/astoria northwind client/vb/customerorders.vb#customersordersusing)]  
  
7.  在定义窗体的分部类中，添加创建 <xref:System.Data.Objects.ObjectContext> 实例并定义 `customerID` 常量的以下代码。  
  
     [!code-csharp[Astoria Northwind Client#CustomersOrdersDefinition](../../../../samples/snippets/csharp/VS_Snippets_Misc/astoria northwind client/cs/customerorders.cs#customersordersdefinition)]
     [!code-vb[Astoria Northwind Client#CustomersOrdersDefinition](../../../../samples/snippets/visualbasic/VS_Snippets_Misc/astoria northwind client/vb/customerorders.vb#customersordersdefinition)]  
  
8.  在窗体设计器中，双击窗体。  
  
     这会打开窗体的代码页，并创建用于处理窗体的 `Load` 事件的方法。  
  
9. 在 `Load` 事件处理程序中，复制并粘贴以下代码。  
  
     [!code-csharp[Astoria Northwind Client#CustomersOrdersDataBinding](../../../../samples/snippets/csharp/VS_Snippets_Misc/astoria northwind client/cs/customerorders.cs#customersordersdatabinding)]
     [!code-vb[Astoria Northwind Client#CustomersOrdersDataBinding](../../../../samples/snippets/visualbasic/VS_Snippets_Misc/astoria northwind client/vb/customerorders.vb#customersordersdatabinding)]  
  
10. 此代码根据 <xref:System.Data.Services.Client.DataServiceQuery%601>（返回 Northwind 数据服务中 `Customers` 的 <xref:System.Collections.Generic.IEnumerable%601>）的执行情况为 `Customers` 类型创建一个 <xref:System.Data.Services.Client.DataServiceCollection%601> 实例，并将其绑定到 `customersBindingSource`。  
  
## 请参阅  
 [WCF 数据服务客户端库](../../../../docs/framework/data/wcf/wcf-data-services-client-library.md)   
 [如何：将数据绑定到 Windows Presentation Foundation 元素](../../../../docs/framework/data/wcf/bind-data-to-wpf-elements-wcf-data-services.md)