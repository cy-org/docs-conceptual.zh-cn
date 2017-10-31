---
title: "数据绑定 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-ado"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: cbec8b02-a1e8-4ae8-a83b-bb5190413ac5
caps.latest.revision: 2
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 2
---
# 数据绑定
[!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] 支持绑定到公共控件，如网格控件。  具体而言，[!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] 定义用于绑定到数据网格和处理主\-从绑定的基本模式，这两者都与显示和更新有关。  
  
## 基本原理  
 [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] 将 [!INCLUDE[vbteclinq](../../../../../../includes/vbteclinq-md.md)] 查询转换成 SQL 以便在数据库上执行。  所得结果为强类型化的 `IEnumerable`。  由于这些对象是一般的公共语言运行库 \(CLR\) 对象，因此可以使用一般的对象数据绑定来显示结果。  另一方面，更改操作（插入、更新和删除）则需要额外的步骤。  
  
## 操作  
 隐式绑定到 Windows 窗体控件是通过实现 <xref:System.ComponentModel.IListSource> 完成的。  数据源泛型 <xref:System.Data.Linq.Table%601>（C\# 中的 `Table<T>` 或 [!INCLUDE[vbprvb](../../../../../../includes/vbprvb-md.md)] 中的 `Table(Of T)`）和泛型 `DataQuery` 都已更新以实现 <xref:System.ComponentModel.IListSource>。用户界面 \(UI\) 数据绑定引擎（Windows 窗体和 Windows Presentation Foundation）都会测试其数据源是否实现了 <xref:System.ComponentModel.IListSource>。  因此，如果将查询的直接影响结果写入控件的数据源，则会隐式调用 [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] 集合生成，如下例中所示：  
  
 [!code-csharp[DLinqDataBinding#1](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqDataBinding/cs/Program.cs#1)]
 [!code-vb[DLinqDataBinding#1](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqDataBinding/vb/Module1.vb#1)]  
  
 对于 Windows Presentation Foundation 而言也是如此：  
  
 [!code-csharp[DLinqDataBinding#2](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqDataBinding/cs/Program.cs#2)]
 [!code-vb[DLinqDataBinding#2](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqDataBinding/vb/Module1.vb#2)]  
  
 集合生成是由泛型 <xref:System.Data.Linq.Table%601> 和泛型 `DataQuery` 在 <xref:System.ComponentModel.IListSource.GetList%2A> 中实现的。  
  
## IListSource 实现  
 [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] 在两个位置实现 <xref:System.ComponentModel.IListSource>：  
  
-   数据源为 <xref:System.Data.Linq.Table%601>：[!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] 浏览相应的表以填充在该表中保留引用的 `DataBindingList` 集合。  
  
-   数据源为 <xref:System.Linq.IQueryable%601>。  存在两种情况：  
  
    -   如果 [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] 从 <xref:System.Linq.IQueryable%601> 中找到基础 <xref:System.Data.Linq.Table%601>，则源允许进行编辑，这种情形与第一项中的情形相同。  
  
    -   如果 [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] 找不到基础 <xref:System.Data.Linq.Table%601>，则源不允许进行编辑（例如，`groupby`）。[!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] 会浏览相应的查询以填充泛型 `SortableBindingList`（是一个简单的 <xref:System.ComponentModel.BindingList%601>，实现根据给定属性对 T 实体进行排序的功能）。  
  
## 专用集合  
 对于本文档前面部分介绍的许多功能而言，已将 <xref:System.ComponentModel.BindingList%601> 专门用于某些不同的类。  这些类为泛型 `SortableBindingList` 和泛型 `DataBindingList`。  这两种类都声明为内部类。  
  
### 泛型 SortableBindingList  
 此类继承自 <xref:System.ComponentModel.BindingList%601>，是 <xref:System.ComponentModel.BindingList%601> 的可排序版本。  排序是在内存中完成的解决方案，绝不会接触到数据库本身。  <xref:System.ComponentModel.BindingList%601> 实现 <xref:System.ComponentModel.IBindingList>，但默认情况下不支持排序。  但是，<xref:System.ComponentModel.BindingList%601> 使用虚拟核心方法实现 <xref:System.ComponentModel.IBindingList>。  您可以很容易地重写这些方法。  泛型 `SortableBindingList` 可以重写 <xref:System.ComponentModel.BindingList%601.SupportsSortingCore%2A>、<xref:System.ComponentModel.BindingList%601.SortPropertyCore%2A>、<xref:System.ComponentModel.BindingList%601.SortDirectionCore%2A> 和 <xref:System.ComponentModel.BindingList%601.ApplySortCore%2A>。  `ApplySortCore` 由 <xref:System.ComponentModel.IBindingList.ApplySort%2A> 调用，用于对给定属性的 T 项列表进行排序。  
  
 如果相应属性不属于 T，则会引发异常。  
  
 为实现排序，[!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] 创建一个泛型 `SortableBindingList.PropertyComparer` 类，此类继承自泛型 <xref:System.Collections.Generic.Comparer%601.System%23Collections%23IComparer%23Compare%2A> 并实现一个用于给定类型 T 的默认比较器、一个 `PropertyDescriptor` 和一个方向。  此类可以动态地创建 T 的 `Comparer`，其中 T 是 `PropertyDescriptor` 的 `PropertyType`。  然后，将从静态泛型 `Comparer` 中检索默认比较器。  默认实例是通过使用反射获取的。  
  
 泛型 `SortableBindingList` 也是 `DataBindingList` 的基类。  泛型 `SortableBindingList` 提供两个虚方法，用于挂起或继续项的添加\/移除跟踪。  这两个方法可以用于像排序这样的基本功能，但实际上将由像泛型 `DataBindingList` 这样的上层类实现。  
  
### 泛型 DataBindingList  
 此类继承自泛型 `SortableBindingLIst`。  泛型 `DataBindingList` 保留对用于在最初填充集合的泛型 `IQueryable` 的基础泛型 `Table` 的引用。  泛型 `DatabindingList` 通过重写 `InsertItem`\(\) 和 `RemoveItem`\(\) 将对项添加\/移除操作的跟踪添加到集合。  它还可以实现抽象的挂起\/继续跟踪功能，以使跟踪成为有条件的跟踪。  此功能使泛型 `DataBindingList` 能利用父类跟踪功能的所有多态用法。  
  
## 绑定到 EntitySet  
 绑定到 `EntitySet` 是一种特殊情况，因为 `EntitySet` 已经是实现 <xref:System.ComponentModel.IBindingList> 的集合。  [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] 增加了排序和取消 \(<xref:System.ComponentModel.ICancelAddNew>\) 支持。  `EntitySet` 类使用内部列表来存储实体。  此列表是一个基于泛型数组（泛型 `ItemList` 类）的底层集合。  
  
### 添加排序功能  
 数组提供一个可以与 T 的 `Comparer` 一起使用的排序方法 \(`Array.Sort()`\)。  [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] 使用本主题前面部分介绍的泛型 `SortableBindingList.PropertyComparer` 类来获取属性的这个 `Comparer` 以及排序方向。  将 `ApplySort` 方法添加到泛型 `ItemList`，以调用此功能。  
  
 在 `EntitySet` 端，您现在必须声明排序支持：  
  
-   <xref:System.ComponentModel.IBindingList.SupportsSorting%2A> 返回 `true`。  
  
-   <xref:System.ComponentModel.IBindingList.ApplySort%2A> 调用 `entities.ApplySort()`，然后调用 `OnListChanged()`。  
  
-   <xref:System.ComponentModel.IBindingList.SortDirection%2A> 和 <xref:System.ComponentModel.IBindingList.SortProperty%2A> 属性公开本地成员中存储的当前排序定义。  
  
 当使用 System.Windows.Forms.BindingSource 并将 EntitySet\<TEntity\> 绑定到 System.Windows.Forms.BindingSource.DataSource 时，必须调用 EntitySet\<Tentity\>.GetNewBindingList 来更新 BindingSource.List。  
  
 如果使用 System.Windows.Forms.BindingSource，设置 BindingSource.DataMember 属性，并将 BindingSource.DataSource 设置为具有名为 BindingSource.DataMember 的属性（该属性公开 EntitySet\<TEntity\>）的类，则无需调用 EntitySet\<Tentity\>.GetNewBindingList 来更新 BindingSource.List，但将失去排序功能。  
  
## 缓存  
 [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] 查询实现 <xref:System.ComponentModel.IListSource.GetList%2A>。  当 Windows 窗体 BindingSource 类遇到此接口时，它会为单个连接调用 GetList\(\) 三次。  为避免出现这种情况，[!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] 为每个实例实现一个缓存，以存储并始终返回生成的同一个集合。  
  
## 取消  
 <xref:System.ComponentModel.IBindingList> 定义一个 <xref:System.ComponentModel.IBindingList.AddNew%2A> 方法，控件使用此方法从绑定的集合中创建新项。  `DataGridView` 控件在最后一个可见行在其标题中包含星号时会很好地演示此功能。  此星号向您说明您可以添加新项。  
  
 除此功能以外，集合还可以实现 <xref:System.ComponentModel.ICancelAddNew>。  此功能允许控件取消新编辑的项或验证此项是否已经过验证。  
  
 <xref:System.ComponentModel.ICancelAddNew> 是在所有 [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] 数据绑定集合（泛型 `SortableBindingList` 和泛型 `EntitySet`）中实现的。在两种实现中，代码均执行以下操作：  
  
-   允许向集合中插入项，然后将其从集合中移除。  
  
-   只要 UI 不提交编辑内容，就不会跟踪更改。  
  
-   只要已取消 \(<xref:System.ComponentModel.ICancelAddNew.CancelNew%2A>\) 编辑，就不会跟踪更改。  
  
-   允许在提交 \(<xref:System.ComponentModel.ICancelAddNew.EndNew%2A>\) 编辑内容时进行跟踪。  
  
-   如果新项不是来自 <xref:System.ComponentModel.IBindingList.AddNew%2A>，则让集合正常工作。  
  
## 疑难解答  
 本部分提出几点可能有助于您解决 [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] 数据绑定应用程序难题的事项。  
  
-   您必须使用属性；仅使用字段是不够的。  Windows 窗体需要这种用法。  
  
-   默认情况下，`image`、`varbinary` 和 `timestamp` 数据库类型映射到字节数组。  由于在这种方案中不支持 `ToString()`，因此无法显示这些对象。  
  
-   映射到主键的类成员具有 setter，但 [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] 不支持对象标识更改。  因此，在映射中使用的主键\/唯一键无法在数据库中更新。  当您调用 <xref:System.Data.Linq.DataContext.SubmitChanges%2A> 时，如果网格中发生更改，则会引发异常。  
  
-   如果一个实体绑定在两个不同的网格（例如，一个是主网格，另一个是从网格）中，则不会将主网格中发生的 `Delete` 传播到从网格。  
  
## 请参阅  
 [背景信息](../../../../../../docs/framework/data/adonet/sql/linq/background-information.md)