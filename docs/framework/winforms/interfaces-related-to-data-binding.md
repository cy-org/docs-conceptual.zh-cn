---
title: "与数据绑定相关的接口 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-winforms"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "jsharp"
helpviewer_keywords: 
  - "数据 [Windows 窗体], 数据绑定接口"
  - "数据绑定, 接口"
  - "IBindingList 接口, Windows 窗体数据绑定"
  - "IBindingListView 接口"
  - "IDataErrorInfo 接口, Windows 窗体数据绑定"
  - "IEditableObject 接口, Windows 窗体数据绑定"
  - "IList 接口, Windows 窗体数据绑定"
  - "INotifyPropertyChanged 接口"
  - "接口, Windows 窗体数据绑定"
ms.assetid: 14e49a2e-3e46-47ca-b491-70d546333277
caps.latest.revision: 23
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 23
---
# 与数据绑定相关的接口
使用 [!INCLUDE[vstecado](../../../includes/vstecado-md.md)]，可以创建许多不同的数据结构，以满足应用程序和正在处理的数据的绑定需要。  您可能希望创建自己的类，以便在 Windows 窗体中提供或使用数据。  这些对象可以提供各种级别的功能和复杂性，从基本的数据绑定，到提供设计时支持、错误检查、更改通知，甚至是支持对数据本身所做更改的结构化回滚。  
  
## 数据绑定接口的使用者  
 以下部分描述两组接口对象。  第一组列出数据源作者在数据源上实现的接口。  这些接口旨在由数据源使用者使用，在多数情况下，这些使用者是 Windows 窗体控件或组件。  第二组列出了针对组件作者的使用而设计的接口。  组件作者在创建支持数据绑定的组件时使用这些接口，以便它们能够被 Windows 窗体数据绑定引擎使用。  可以在与窗体关联的类中实现这些接口以启用数据绑定；每种情况都表示一个类，该类所实现的接口支持与数据进行交互。  [!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)] 快速应用程序开发 \(RAD\) 数据设计体验工具已经利用了该功能。  
  
### 要由数据源作者实现的接口  
 下列接口设计为由 Windows 窗体控件使用：  
  
-   <xref:System.Collections.IList> 接口  
  
     实现 <xref:System.Collections.IList> 接口的类可以是 <xref:System.Array>、<xref:System.Collections.ArrayList> 或 <xref:System.Collections.CollectionBase>。  这些是 <xref:System.Object> 类型的项的索引列表。  这些列表中必须包含相同类型，因为索引中的第一项确定类型。  <xref:System.Collections.IList> 将仅在运行时可用于绑定。  
  
    > [!NOTE]
    >  如果您希望创建要与 Windows 窗体绑定的业务对象列表，则应当考虑使用 <xref:System.ComponentModel.BindingList%601>。  <xref:System.ComponentModel.BindingList%601> 是可扩展的类，该类实现了双向 Windows 窗体数据绑定所需的主要接口。  
  
-   <xref:System.ComponentModel.IBindingList> 接口  
  
     实现 <xref:System.ComponentModel.IBindingList> 接口的类提供了一种更高级别的数据绑定功能。  此实现在列表项更改时（例如，客户列表中的第三项更改了 Address 字段）和列表本身更改时（例如，列表中项的数量增加或减少）都提供基本的排序功能和更改通知。  如果您打算将多个控件绑定到同一个数据，但是希望将在某个控件中进行的数据更改传播到其他绑定控件，则更改通知就非常重要。  
  
    > [!NOTE]
    >  更改通知是通过 <xref:System.ComponentModel.IBindingList.SupportsChangeNotification%2A> 属性为 <xref:System.ComponentModel.IBindingList> 接口启用的，当该属性为 `true` 时，将引发一个 <xref:System.ComponentModel.IBindingList.ListChanged> 事件，指示列表或列表中的项已发生更改。  
  
     更改的类型由 <xref:System.ComponentModel.ListChangedEventArgs> 参数的 <xref:System.ComponentModel.ListChangedType> 属性来描述。  因此，当数据模型进行更新时，任何依赖视图（如绑定到同一个数据源的其他控件）也将进行更新。  但是，包含在列表中的对象在更改时必须通知该列表，以便该列表可引发 <xref:System.ComponentModel.IBindingList.ListChanged> 事件。  
  
    > [!NOTE]
    >  <xref:System.ComponentModel.BindingList%601> 提供 <xref:System.ComponentModel.IBindingList> 接口的泛型实现。  
  
-   <xref:System.ComponentModel.IBindingListView> 接口  
  
     实现 <xref:System.ComponentModel.IBindingListView> 接口的类提供 <xref:System.ComponentModel.IBindingList> 实现的所有功能以及筛选和高级排序功能。  此实现使用属性说明符\/方向对提供基于字符串的筛选和多列排序能力。  
  
-   <xref:System.ComponentModel.IEditableObject> 接口  
  
     实现 <xref:System.ComponentModel.IEditableObject> 接口的类允许对象控制对该对象进行的更改何时成为永久更改。  此实现提供 <xref:System.ComponentModel.IEditableObject.BeginEdit%2A>、<xref:System.ComponentModel.IEditableObject.EndEdit%2A> 和 <xref:System.ComponentModel.IEditableObject.CancelEdit%2A> 方法，这些方法使您得以回滚对对象进行的更改。  下面简述了 <xref:System.ComponentModel.IEditableObject.BeginEdit%2A>、<xref:System.ComponentModel.IEditableObject.EndEdit%2A> 和 <xref:System.ComponentModel.IEditableObject.CancelEdit%2A> 方法的功能以及它们如何一起使用来允许对数据更改进行可能的回滚：  
  
    -   <xref:System.ComponentModel.IEditableObject.BeginEdit%2A> 方法发出开始对一个对象进行编辑的信号。  实现此接口的对象需要存储 <xref:System.ComponentModel.IEditableObject.BeginEdit%2A> 方法调用后的任何更新，这样，如果调用 <xref:System.ComponentModel.IEditableObject.CancelEdit%2A> 方法，则可以放弃这些更新。  在数据绑定 Windows 窗体中，可以在单个编辑事务的范围内多次调用 <xref:System.ComponentModel.IEditableObject.BeginEdit%2A>（例如，<xref:System.ComponentModel.IEditableObject.BeginEdit%2A>、<xref:System.ComponentModel.IEditableObject.BeginEdit%2A> 和 <xref:System.ComponentModel.IEditableObject.EndEdit%2A>）。  <xref:System.ComponentModel.IEditableObject> 的实现应当跟踪 <xref:System.ComponentModel.IEditableObject.BeginEdit%2A> 是否已被调用，并忽略对 <xref:System.ComponentModel.IEditableObject.BeginEdit%2A> 的后续调用。  因为可多次调用此方法，所以对它的后续调用应是非破坏性的，这一点很重要；即，对 <xref:System.ComponentModel.IEditableObject.BeginEdit%2A> 的后续调用不能损坏已进行的更新或更改在第一次调用 <xref:System.ComponentModel.IEditableObject.BeginEdit%2A> 时保存的数据。  
  
    -   如果对象当前处于编辑模式，<xref:System.ComponentModel.IEditableObject.EndEdit%2A> 方法会将自调用 <xref:System.ComponentModel.IEditableObject.BeginEdit%2A> 后进行的任何更改都保存到基础对象中。  
  
    -   <xref:System.ComponentModel.IEditableObject.CancelEdit%2A> 方法放弃对对象所做的任何更改。  
  
     有关 <xref:System.ComponentModel.IEditableObject.BeginEdit%2A>、<xref:System.ComponentModel.IEditableObject.EndEdit%2A> 和 <xref:System.ComponentModel.IEditableObject.CancelEdit%2A> 方法工作方式的更多信息，请参见 [将数据保存在数据集中](../Topic/Save%20data%20back%20to%20the%20database.md)。  
  
     <xref:System.Windows.Forms.DataGridView> 控件使用数据功能的这种事务性概念。  
  
-   <xref:System.ComponentModel.ICancelAddNew> 接口  
  
     实现 <xref:System.ComponentModel.ICancelAddNew> 接口的类通常实现 <xref:System.ComponentModel.IBindingList> 接口，并允许您回滚用 <xref:System.ComponentModel.IBindingList.AddNew%2A> 方法向数据源添加的数据。  如果数据源实现 <xref:System.ComponentModel.IBindingList> 接口，则还应当让其实现 <xref:System.ComponentModel.ICancelAddNew> 接口。  
  
-   <xref:System.ComponentModel.IDataErrorInfo> 接口  
  
     实现 <xref:System.ComponentModel.IDataErrorInfo> 接口的类允许对象向绑定控件提供自定义错误信息：  
  
    -   <xref:System.ComponentModel.IDataErrorInfo.Error%2A> 属性返回常规错误消息文本（例如，“出现错误”）。  
  
    -   <xref:System.ComponentModel.IDataErrorInfo.Item%2A> 属性返回一个包含来自列的具体错误消息的字符串（例如，“`State` 列中的值无效”）。  
  
-   <xref:System.Collections.IEnumerable> 接口  
  
     实现 <xref:System.Collections.IEnumerable> 接口的类通常由 [!INCLUDE[vstecasp](../../../includes/vstecasp-md.md)] 使用。  只能通过 <xref:System.Windows.Forms.BindingSource> 组件来使用 Windows 窗体对此接口的支持。  
  
    > [!NOTE]
    >  <xref:System.Windows.Forms.BindingSource> 组件将所有的 <xref:System.Collections.IEnumerable> 项复制到一个单独的列表中以实现绑定。  
  
-   <xref:System.ComponentModel.ITypedList> 接口  
  
     实现 <xref:System.ComponentModel.ITypedList> 接口的集合类提供如下功能：控制向绑定控件公开的属性集以及这些属性的顺序。  
  
    > [!NOTE]
    >  在实现 <xref:System.ComponentModel.ITypedList.GetItemProperties%2A> 方法时，如果 <xref:System.ComponentModel.PropertyDescriptor> 数组不为 null，则该数组中的最后一项将为属性说明符，它描述作为另一个项列表的列表属性。  
  
-   <xref:System.ComponentModel.ICustomTypeDescriptor> 接口  
  
     实现 <xref:System.ComponentModel.ICustomTypeDescriptor> 接口的类提供有关其自身的动态信息。  此接口与 <xref:System.ComponentModel.ITypedList> 类似，但是它用于对象（而非列表）。  此接口由 <xref:System.Data.DataRowView> 用来设计基础行的架构。  <xref:System.ComponentModel.CustomTypeDescriptor> 类提供 <xref:System.ComponentModel.ICustomTypeDescriptor> 的简单实现。  
  
    > [!NOTE]
    >  若要支持到实现 <xref:System.ComponentModel.ICustomTypeDescriptor> 的类型的设计时绑定，该类型还必须实现 <xref:System.ComponentModel.IComponent> 并且作为实例存在于窗体上。  
  
-   <xref:System.ComponentModel.IListSource> 接口  
  
     实现 <xref:System.ComponentModel.IListSource> 接口的类在非列表对象上启用基于列表的绑定。  <xref:System.ComponentModel.IListSource> 的 <xref:System.ComponentModel.IListSource.GetList%2A> 方法用于从某个对象返回一个不是从 <xref:System.Collections.IList> 继承的可绑定列表。  <xref:System.ComponentModel.IListSource> 由 <xref:System.Data.DataSet> 类使用。  
  
-   <xref:System.ComponentModel.IRaiseItemChangedEvents> 接口  
  
     实现 <xref:System.ComponentModel.IRaiseItemChangedEvents> 接口的类是可绑定的列表，该列表还实现 <xref:System.ComponentModel.IBindingList> 接口。  此接口用于指示类型是否通过其 <xref:System.ComponentModel.IRaiseItemChangedEvents.RaisesItemChangedEvents%2A> 属性引发 <xref:System.ComponentModel.ListChangedType> 类型的 <xref:System.ComponentModel.IBindingList.ListChanged> 事件。  
  
    > [!NOTE]
    >  如果数据源提供用来列出前面描述的事件转换的属性，并且与 <xref:System.Windows.Forms.BindingSource> 组件进行交互，则应当实现 <xref:System.ComponentModel.IRaiseItemChangedEvents>。  否则，<xref:System.Windows.Forms.BindingSource> 还将执行用来列出事件转换的属性，这将导致性能下降。  
  
-   <xref:System.ComponentModel.ISupportInitialize> 接口  
  
     实现 <xref:System.ComponentModel.ISupportInitialize> 接口的组件利用批处理优化来设置属性并初始化共存属性。  <xref:System.ComponentModel.ISupportInitialize> 包含两种方法：  
  
    -   <xref:System.ComponentModel.ISupportInitialize.BeginInit%2A> 发出正在开始对象初始化的信号。  
  
    -   <xref:System.ComponentModel.ISupportInitialize.EndInit%2A> 发出正在完成对象初始化的信号。  
  
-   <xref:System.ComponentModel.ISupportInitializeNotification> 接口  
  
     实现 <xref:System.ComponentModel.ISupportInitializeNotification> 接口的组件还实现 <xref:System.ComponentModel.ISupportInitialize> 接口。  使用此接口，可以通知其他 <xref:System.ComponentModel.ISupportInitialize> 组件初始化已完成。  <xref:System.ComponentModel.ISupportInitializeNotification> 接口包含两个成员：  
  
    -   <xref:System.ComponentModel.ISupportInitializeNotification.IsInitialized%2A> 返回一个 `boolean` 值，该值指示组件是否已初始化。  
  
    -   <xref:System.ComponentModel.ISupportInitializeNotification.Initialized> 在调用 <xref:System.ComponentModel.ISupportInitialize.EndInit%2A> 时发生。  
  
-   <xref:System.ComponentModel.INotifyPropertyChanged> 接口  
  
     实现此接口的类是一个在其任何属性值更改时都会引发事件的类型。  此接口旨在替换控件的每个属性都有一个更改事件这种模式。  用在 <xref:System.ComponentModel.BindingList%601> 中时，业务对象应当实现 <xref:System.ComponentModel.INotifyPropertyChanged> 接口，BindingList\`1 会将 <xref:System.ComponentModel.INotifyPropertyChanged.PropertyChanged> 事件转换为 <xref:System.ComponentModel.ListChangedType> 类型的 <xref:System.ComponentModel.BindingList%601.ListChanged> 事件。  
  
    > [!NOTE]
    >  对于在被绑定客户端和数据源之间的绑定中发生的更改通知，要么应当让绑定数据源类型实现 <xref:System.ComponentModel.INotifyPropertyChanged> 接口（首选方法），要么为绑定类型提供*属性名称*`Changed` 事件，但是不应同时选择这两种方法。  
  
### 要由组件作者实现的接口  
 下列接口设计为由 Windows 窗体数据绑定引擎使用：  
  
-   <xref:System.Windows.Forms.IBindableComponent> 接口  
  
     实现此接口的类是支持数据绑定的非控件组件。  此类通过该接口的 <xref:System.Windows.Forms.IBindableComponent.DataBindings%2A> 和 <xref:System.Windows.Forms.IBindableComponent.BindingContext%2A> 属性返回组件的数据绑定和绑定上下文。  
  
    > [!NOTE]
    >  如果组件从 <xref:System.Windows.Forms.Control> 继承，则无需实现 <xref:System.Windows.Forms.IBindableComponent> 接口。  
  
-   <xref:System.Windows.Forms.ICurrencyManagerProvider> 接口  
  
     实现 <xref:System.Windows.Forms.ICurrencyManagerProvider> 接口的类是一个组件，该组件提供其自己的 <xref:System.Windows.Forms.CurrencyManager>，用来管理与这个特定组件关联的绑定。  对自定义 <xref:System.Windows.Forms.CurrencyManager> 的访问是通过 <xref:System.Windows.Forms.ICurrencyManagerProvider.CurrencyManager%2A> 属性提供的。  
  
    > [!NOTE]
    >  从 <xref:System.Windows.Forms.Control> 继承的类通过它的 <xref:System.Windows.Forms.Control.BindingContext%2A> 属性自动管理绑定，因此，需要实现 <xref:System.Windows.Forms.ICurrencyManagerProvider> 的情况相当罕见。  
  
## 请参阅  
 [数据绑定和 Windows 窗体](../../../docs/framework/winforms/data-binding-and-windows-forms.md)   
 [如何：在 Windows 窗体上创建简单绑定控件](../../../docs/framework/winforms/how-to-create-a-simple-bound-control-on-a-windows-form.md)   
 [Windows 窗体数据绑定](../../../docs/framework/winforms/windows-forms-data-binding.md)