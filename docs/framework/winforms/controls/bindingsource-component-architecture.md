---
title: "BindingSource 组件体系结构 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-winforms"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "jsharp"
helpviewer_keywords: 
  - "BindingSource 组件 [Windows 窗体], 关于 BindingSource 组件"
  - "BindingSource 组件, 体系结构"
  - "数据绑定, BindingSource 组件"
  - "Windows 窗体, 数据绑定"
ms.assetid: 7bc69c90-8a11-48b1-9336-3adab5b41591
caps.latest.revision: 23
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 23
---
# BindingSource 组件体系结构
通过 <xref:System.Windows.Forms.BindingSource> 组件，可以将所有 Windows 窗体控件通用绑定到数据源。  
  
 <xref:System.Windows.Forms.BindingSource> 组件简化了将控件绑定到数据源的过程，并且在以下几个方面优于传统的数据绑定：  
  
-   允许设计时绑定到业务对象。  
  
-   可以在设计时封装 <xref:System.Windows.Forms.CurrencyManager> 功能，并公开 <xref:System.Windows.Forms.CurrencyManager> 事件。  
  
-   通过为本身不支持列表更改通知的数据源提供列表更改通知，简化了支持 <xref:System.ComponentModel.IBindingList> 接口的列表创建过程。  
  
-   为 <xref:System.ComponentModel.IBindingList.AddNew%2A?displayProperty=fullName> 方法提供了可扩展点。  
  
-   在数据源与控件之间提供了一个间接寻址级别。  如果数据源有可能在运行时发生更改，则此间接功能很重要。  
  
-   与其他数据相关的 Windows 窗体控件（特别是 <xref:System.Windows.Forms.BindingNavigator> 和 <xref:System.Windows.Forms.DataGridView> 控件）进行交互操作。  
  
 基于以上原因，<xref:System.Windows.Forms.BindingSource> 组件是将 Windows 窗体控件绑定到数据源的首选方式。  
  
## BindingSource 功能  
 <xref:System.Windows.Forms.BindingSource> 组件提供了若干用于将控件绑定到数据的功能。  通过这些功能，您几乎不用编写代码就能实现大部分的数据绑定方案。  
  
 <xref:System.Windows.Forms.BindingSource> 组件为访问多种不同类型的数据源提供了一致性的接口，从而实现了这一功能。  这意味着可以将同一个绑定过程用于任何类型的数据。  例如，可以将 <xref:System.Windows.Forms.BindingSource.DataSource%2A> 属性附加到 <xref:System.Data.DataSet>，也可以将该属性附加到某个业务对象，在这两种情况下，都可以使用同一组属性、方法和事件对数据源进行操作。  
  
 <xref:System.Windows.Forms.BindingSource> 组件提供的一致性接口极大地简化了数据到控件的绑定过程。  对于提供更改通知的数据源类型，<xref:System.Windows.Forms.BindingSource> 组件自动在控件与数据源之间传递更改；  对于不提供更改通知的数据源类型，该组件提供的事件可用于引发更改通知。  下表显示 <xref:System.Windows.Forms.BindingSource> 组件支持的功能：  
  
-   间接寻址。  
  
-   货币管理。  
  
-   作为列表的数据源。  
  
-   作为 <xref:System.ComponentModel.IBindingList> 的 <xref:System.Windows.Forms.BindingSource>。  
  
-   创建自定义项。  
  
-   创建事务性项。  
  
-   <xref:System.Collections.IEnumerable> 支持。  
  
-   设计时支持。  
  
-   静态 <xref:System.Windows.Forms.ListBindingHelper> 方法。  
  
-   使用 <xref:System.ComponentModel.IBindingListView> 接口进行排序和筛选。  
  
-   与 <xref:System.Windows.Forms.BindingNavigator> 集成。  
  
### 间接寻址  
 <xref:System.Windows.Forms.BindingSource> 组件在控件与数据源之间提供了一个间接寻址级别。  控件不是直接绑定到数据源，而是先将控件绑定到 <xref:System.Windows.Forms.BindingSource>，然后再将数据源附加到该 <xref:System.Windows.Forms.BindingSource> 组件的 <xref:System.Windows.Forms.BindingSource.DataSource%2A> 属性。  
  
 使用此间接寻址级别，无需重置控件绑定即可更改数据源，  这就为您提供了以下功能：  
  
-   在保留当前的控件绑定的同时，可以将 <xref:System.Windows.Forms.BindingSource> 附加到不同的数据源。  
  
-   可以更改数据源中的项并通知绑定控件。  有关更多信息，请参见 [如何：使用 BindingSource 在 Windows 窗体控件中反映数据源更新](../../../../docs/framework/winforms/controls/reflect-data-source-updates-in-a-wf-control-with-the-bindingsource.md)。  
  
-   可以绑定到 <xref:System.Type>，而不是绑定到内存中的某个对象。  有关更多信息，请参见 [如何：将 Windows 窗体控件绑定到类型](../../../../docs/framework/winforms/controls/how-to-bind-a-windows-forms-control-to-a-type.md)。  此后可以在运行时再绑定到对象。  
  
### 货币管理  
 <xref:System.Windows.Forms.BindingSource> 组件实现 <xref:System.Windows.Forms.ICurrencyManagerProvider> 接口来为您处理货币管理。  通过 <xref:System.Windows.Forms.ICurrencyManagerProvider> 接口，除可以访问绑定到同一 <xref:System.Windows.Forms.BindingSource.DataMember%2A> 的其他 <xref:System.Windows.Forms.BindingSource> 的货币管理器外，您还可以访问 <xref:System.Windows.Forms.BindingSource> 的货币管理器。  
  
 <xref:System.Windows.Forms.BindingSource> 组件封装 <xref:System.Windows.Forms.CurrencyManager> 功能，并公开最常用的 <xref:System.Windows.Forms.CurrencyManager> 属性和事件。  下表描述了一些与货币管理相关的成员。  
  
 <xref:System.Windows.Forms.ICurrencyManagerProvider.CurrencyManager%2A> 属性  
 获取与 <xref:System.Windows.Forms.BindingSource> 关联的货币管理器。  
  
 <xref:System.Windows.Forms.ICurrencyManagerProvider.GetRelatedCurrencyManager%2A> 方法  
 如果还有其他 <xref:System.Windows.Forms.BindingSource> 绑定到指定的数据成员，则获取其货币管理器。  
  
 <xref:System.Windows.Forms.BindingSource.Current%2A> 属性  
 获取数据源的当前项。  
  
 <xref:System.Windows.Forms.BindingSource.Position%2A> 属性  
 获取或设置基础列表中的当前位置。  
  
 <xref:System.Windows.Forms.BindingSource.EndEdit%2A> 方法  
 将挂起的更改应用于基础数据源。  
  
 <xref:System.Windows.Forms.BindingSource.CancelEdit%2A> 方法  
 取消当前的编辑操作。  
  
### 作为列表的数据源  
 <xref:System.Windows.Forms.BindingSource> 组件实现 <xref:System.ComponentModel.IBindingListView> 和 <xref:System.ComponentModel.ITypedList> 接口。  有了这一实现，便可以将 <xref:System.Windows.Forms.BindingSource> 组件本身作为数据源，而不需要借助任何外部存储。  
  
 <xref:System.Windows.Forms.BindingSource> 组件被附加到某个数据源以后，便将该数据源作为列表进行公开。  
  
 可以将 <xref:System.Windows.Forms.BindingSource.DataSource%2A> 属性设置为几个数据源。  这些数据源包括类型、对象和类型列表。  结果数据源将作为列表进行公开。  下表显示一些常用的数据源和列表结果。  
  
|DataSource 属性|列表结果|  
|-------------------|----------|  
|空引用（Visual Basic 中的 `Nothing`）|一个对象的空 <xref:System.ComponentModel.IBindingList>。  添加一个项会将该列表设置为添加项的类型。|  
|对 <xref:System.Windows.Forms.BindingSource.DataMember%2A> 集的空引用（Visual Basic 中的 `Nothing`）|不支持；引发 <xref:System.ArgumentException>。|  
|非列表类型或类型为“T”的对象|一个“T”类型的空 <xref:System.ComponentModel.IBindingList>。|  
|数组实例|一个包含数组元素的 <xref:System.ComponentModel.IBindingList>。|  
|<xref:System.Collections.IEnumerable> 实例|一个包含 <xref:System.Collections.IEnumerable> 项的 <xref:System.ComponentModel.IBindingList>。|  
|包含类型“T”的列表实例|一个包含类型“T”的 <xref:System.ComponentModel.IBindingList> 实例。|  
  
 此外，还可以将 <xref:System.Windows.Forms.BindingSource.DataSource%2A> 设置为其他列表类型，如 <xref:System.ComponentModel.IListSource> 和 <xref:System.ComponentModel.ITypedList>，<xref:System.Windows.Forms.BindingSource> 将对其进行相应的处理。  在此情况下，列表中包含的类型应具有默认的构造函数。  
  
### 作为 IBindingList 的 BindingSource  
 <xref:System.Windows.Forms.BindingSource> 组件提供成员，以访问和操作作为 <xref:System.ComponentModel.IBindingList> 的基础数据。  下表描述了其中的一些成员。  
  
|成员|说明|  
|--------|--------|  
|<xref:System.Windows.Forms.BindingSource.List%2A> 属性|获取 <xref:System.Windows.Forms.BindingSource.DataSource%2A> 或 <xref:System.Windows.Forms.BindingSource.DataMember%2A> 属性的计算结果的列表。|  
|<xref:System.Windows.Forms.BindingSource.AddNew%2A> 方法|在基础列表中添加一个新项。  应用于满足以下两个条件的数据源：实现 <xref:System.ComponentModel.IBindingList> 接口并允许添加项（即 <xref:System.Windows.Forms.BindingSource.AllowNew%2A> 属性被设置为 `true`）。|  
  
### 创建自定义项  
 您可以处理 <xref:System.Windows.Forms.BindingSource.AddingNew> 事件，以提供自己的项创建逻辑。  <xref:System.Windows.Forms.BindingSource.AddingNew> 事件在新对象添加到 <xref:System.Windows.Forms.BindingSource> 之前发生。  此事件在调用 <xref:System.Windows.Forms.BindingSource.AddNew%2A> 方法之后、新项目添加到基础列表之前引发。  通过处理此事件，您可以提供自定义项创建行为，而无需从 <xref:System.Windows.Forms.BindingSource> 类派生。  有关更多信息，请参见 [如何：使用 Windows 窗体 BindingSource 自定义项添加](../../../../docs/framework/winforms/controls/how-to-customize-item-addition-with-the-windows-forms-bindingsource.md)。  
  
### 创建事务性项  
 <xref:System.Windows.Forms.BindingSource> 组件实现 <xref:System.ComponentModel.ICancelAddNew> 接口，从而启用事务性项的创建。  通过调用 <xref:System.Windows.Forms.BindingSource.AddNew%2A> 临时创建一个新项之后，可以采用下列方式提交或回滚该添加项：  
  
-   <xref:System.ComponentModel.ICancelAddNew.EndNew%2A> 方法显式提交挂起的新项。  
  
-   执行其他集合操作（如插入、移除或移动）隐式提交挂起的新项。  
  
-   如果尚未提交 <xref:System.ComponentModel.ICancelAddNew.CancelNew%2A> 方法，则此方法将回滚挂起的新项。  
  
### IEnumerable 支持  
 <xref:System.Windows.Forms.BindingSource> 组件启用控件到 <xref:System.Collections.IEnumerable> 数据源的绑定。  使用此组件可以绑定到某个数据源，如 <xref:System.Data.SqlClient.SqlDataReader?displayProperty=fullName>。  
  
 将 <xref:System.Collections.IEnumerable> 数据源分配给 <xref:System.Windows.Forms.BindingSource> 组件以后，<xref:System.Windows.Forms.BindingSource> 将创建一个 <xref:System.ComponentModel.IBindingList>，并将 <xref:System.Collections.IEnumerable> 数据源的内容添加到列表中。  
  
### 设计时支持  
 有些对象类型不能在设计时创建，例如，从工厂类创建的对象或由 Web 服务返回的对象。  但有时您可能必须在设计时将自己的控件绑定到这些类型，即使内存中不存在可以作为控件绑定目标的对象。  例如，您可能需要使用自定义类型的公共属性的名称来标记 <xref:System.Windows.Forms.DataGridView> 控件的列标头。  
  
 为了支持这一需求，<xref:System.Windows.Forms.BindingSource> 组件支持到 <xref:System.Type> 的绑定。  将 <xref:System.Type> 分配给 <xref:System.Windows.Forms.BindingSource.DataSource%2A> 属性以后，<xref:System.Windows.Forms.BindingSource> 组件将创建一个 <xref:System.Type> 项的空 <xref:System.ComponentModel.BindingList%601>。  此后，只要您将任意控件绑定到 <xref:System.Windows.Forms.BindingSource> 组件，在设计时或运行时就会提醒您存在相应类型的属性或架构。  有关更多信息，请参见 [如何：将 Windows 窗体控件绑定到类型](../../../../docs/framework/winforms/controls/how-to-bind-a-windows-forms-control-to-a-type.md)。  
  
### 静态 ListBindingHelper 方法  
 <xref:System.Windows.Forms.BindingContext?displayProperty=fullName>、<xref:System.Windows.Forms.CurrencyManager?displayProperty=fullName> 和 <xref:System.Windows.Forms.BindingSource> 类型共享公共逻辑，以便根据 `DataSource`\/`DataMember` 对生成列表。  此外，将公开此公共逻辑，以供控件作者和其他第三方在下列 `static` 方法中使用：  
  
-   <xref:System.Windows.Forms.ListBindingHelper.GetListItemProperties%2A>  
  
-   <xref:System.Windows.Forms.ListBindingHelper.GetList%2A>.  
  
-   <xref:System.Windows.Forms.ListBindingHelper.GetListName%2A>  
  
-   <xref:System.Windows.Forms.ListBindingHelper.GetListItemType%2A>  
  
### 使用 IBindingListView 接口进行排序和筛选  
 <xref:System.Windows.Forms.BindingSource> 组件实现了 <xref:System.ComponentModel.IBindingListView> 接口，从而扩展了 <xref:System.ComponentModel.IBindingList> 接口。  <xref:System.ComponentModel.IBindingList> 提供单个列排序，而 <xref:System.ComponentModel.IBindingListView> 提供高级排序和筛选。  如果数据源也实现这些接口中的一个，则您可以使用 <xref:System.ComponentModel.IBindingListView> 对数据源中的项进行排序和筛选。  <xref:System.Windows.Forms.BindingSource> 组件不提供这些成员的引用实现，  而是将调用转发给基础列表。  
  
 下表描述用于排序和筛选的属性。  
  
|成员|说明|  
|--------|--------|  
|<xref:System.Windows.Forms.BindingSource.Filter%2A> 属性|如果数据源是 <xref:System.ComponentModel.IBindingListView>，则会获取或设置用于筛选所查看行的表达式。|  
|<xref:System.Windows.Forms.BindingSource.Sort%2A> 属性|如果数据源为 <xref:System.ComponentModel.IBindingList>，则获取或设置用于排序和排序顺序信息的列名。<br /><br /> \- 或 \-<br /><br /> 如果数据源为 <xref:System.ComponentModel.IBindingListView> 并且支持高级排序，则获取用于排序和排序顺序的多个列名。|  
  
### 与 BindingNavigator 集成  
 您可以使用 <xref:System.Windows.Forms.BindingSource> 组件将任何一个 Windows 窗体控件绑定到某个数据源，但 <xref:System.Windows.Forms.BindingNavigator> 控件专用于 <xref:System.Windows.Forms.BindingSource> 组件。  <xref:System.Windows.Forms.BindingNavigator> 控件提供了一个用户界面，以控制 <xref:System.Windows.Forms.BindingSource> 组件的当前项。  默认情况下，<xref:System.Windows.Forms.BindingNavigator> 控件提供的按钮对应于 <xref:System.Windows.Forms.BindingSource> 组件中的导航方法。  有关更多信息，请参见[如何：使用 Windows 窗体 BindingNavigator 控件定位数据](../../../../docs/framework/winforms/controls/how-to-navigate-data-with-the-windows-forms-bindingnavigator-control.md)。  
  
## 请参阅  
 <xref:System.Windows.Forms.BindingSource>   
 <xref:System.Windows.Forms.BindingNavigator>   
 [BindingSource 组件概述](../../../../docs/framework/winforms/controls/bindingsource-component-overview.md)   
 [BindingNavigator 控件](../../../../docs/framework/winforms/controls/bindingnavigator-control-windows-forms.md)   
 [Windows 窗体数据绑定](../../../../docs/framework/winforms/windows-forms-data-binding.md)   
 [在 Windows 窗体上使用的控件](../../../../docs/framework/winforms/controls/controls-to-use-on-windows-forms.md)   
 [如何：将 Windows 窗体控件绑定到类型](../../../../docs/framework/winforms/controls/how-to-bind-a-windows-forms-control-to-a-type.md)   
 [如何：使用 BindingSource 在 Windows 窗体控件中反映数据源更新](../../../../docs/framework/winforms/controls/reflect-data-source-updates-in-a-wf-control-with-the-bindingsource.md)