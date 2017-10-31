---
title: "Windows 窗体支持的数据源 | Microsoft Docs"
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
  - "数组 [Windows 窗体]"
  - "集合 [Windows 窗体], 绑定"
  - "数据 [Windows 窗体], 数据提供程序"
  - "数据提供程序 [Windows 窗体]"
  - "数据源 [Windows 窗体]"
  - "DataColumn 类"
  - "DataSet 类, 绑定和 Windows 窗体"
  - "DataTable 类, 绑定和 Windows 窗体"
  - "DataView 类, 绑定和 Windows 窗体"
  - "DataViewManager 类, 绑定和 Windows 窗体"
  - "OLE DB 提供程序, Windows 窗体"
  - "Windows 窗体, 数据绑定"
  - "Windows 窗体, 源数据"
ms.assetid: 3d2c43f6-462b-4d35-9c86-13e9afe012e1
caps.latest.revision: 15
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 15
---
# Windows 窗体支持的数据源
传统上，在应用程序内使用数据绑定以利用数据库中存储的数据。  使用 Windows 窗体数据绑定功能，可以访问数据库中的数据和其他结构中的数据（如数组和集合），但前提是已满足某些最低要求。  
  
## 要绑定到的结构  
 在 Windows 窗体中，可以绑定到广泛的结构，从简单对象（简单绑定）到诸如 ADO.NET 数据表之类的复杂列表（复杂绑定）。  对于简单绑定，Windows 窗体支持绑定到简单对象的公共属性。  基于 Windows 窗体列表的绑定通常要求对象支持 <xref:System.Collections.IList> 或 <xref:System.ComponentModel.IListSource> 接口。  另外，如果要通过 <xref:System.Windows.Forms.BindingSource> 组件进行绑定，则可以绑定到支持 <xref:System.Collections.IEnumerable> 接口的对象。  有关与数据绑定相关的接口的更多信息，请参见 [与数据绑定相关的接口](../../../docs/framework/winforms/interfaces-related-to-data-binding.md)。  
  
 下面的列表演示 Windows 窗体中可绑定到的结构。  
  
 <xref:System.Windows.Forms.BindingSource>  
 <xref:System.Windows.Forms.BindingSource> 是最常见的 Windows 窗体数据源，并充当数据源和 Windows 窗体控件之间的代理。  常规 <xref:System.Windows.Forms.BindingSource> 使用模式如下：将控件绑定到 <xref:System.Windows.Forms.BindingSource>，将 <xref:System.Windows.Forms.BindingSource> 绑定到数据源（例如，ADO.NET 数据表或业务对象）。  <xref:System.Windows.Forms.BindingSource> 提供的服务可启用并提高数据绑定支持级别。  例如，基于 Windows 窗体列表的控件（如 <xref:System.Windows.Forms.DataGridView> 和 <xref:System.Windows.Forms.ComboBox>）不直接支持到 <xref:System.Collections.IEnumerable> 数据源的绑定，但是，可以通过 <xref:System.Windows.Forms.BindingSource> 由绑定功能启用此方案。  在这种情况下，<xref:System.Windows.Forms.BindingSource> 会将数据源转换为 <xref:System.Collections.IList>。  
  
 简单对象  
 Windows 窗体支持使用 <xref:System.Windows.Forms.Binding> 类型，将控件属性的数据绑定到对象实例的公共属性。  在使用 <xref:System.Windows.Forms.BindingSource> 时，Windows 窗体还支持将基于列表的控件（如 <xref:System.Windows.Forms.ListControl>）绑定到对象实例。  
  
 数组或集合  
 若要充当数据源，列表必须实现 <xref:System.Collections.IList> 接口；它的一个示例将是作为 <xref:System.Array> 类的实例的数组。  有关数组的更多信息，请参见[How to: Create an Array of Objects \(Visual Basic\)](http://msdn.microsoft.com/zh-cn/6b64e069-0387-400c-9081-3bdc581020c3)。  
  
 通常，当创建用于数据绑定的对象的列表时，应当使用 <xref:System.ComponentModel.BindingList%601>。  <xref:System.ComponentModel.BindingList%601> 是 <xref:System.ComponentModel.IBindingList> 接口的一个泛型版本。  <xref:System.ComponentModel.IBindingList> 接口通过添加双向数据绑定所需的属性、方法和事件来扩展 <xref:System.Collections.IList> 接口。  
  
 <xref:System.Collections.IEnumerable>  
 如果要通过 <xref:System.Windows.Forms.BindingSource> 组件进行绑定，则可以将 Windows 窗体控件绑定到仅支持 <xref:System.Collections.IEnumerable> 接口的数据源。  
  
 [!INCLUDE[vstecado](../../../includes/vstecado-md.md)] 数据对象  
 [!INCLUDE[vstecado](../../../includes/vstecado-md.md)] 提供大量适于绑定到的数据结构。  这些结构在复杂程度和复杂性方面各不相同。  
  
-   <xref:System.Data.DataColumn>.  <xref:System.Data.DataColumn> 是 <xref:System.Data.DataTable> 的基本构造块，因为表是由许多列组成的。  每个 <xref:System.Data.DataColumn> 都有一个 <xref:System.Data.DataColumn.DataType%2A> 属性，此属性确定该列保存的数据种类（例如，描述汽车的表中的汽车组成部分）。  可以将控件（如 <xref:System.Windows.Forms.TextBox> 控件的 <xref:System.Windows.Forms.Control.Text%2A> 属性）简单绑定到数据表内的某列。  
  
-   <xref:System.Data.DataTable>.  <xref:System.Data.DataTable> 是 [!INCLUDE[vstecado](../../../includes/vstecado-md.md)] 中对包含行和列的表的表示形式。  数据表中包含两个集合：<xref:System.Data.DataColumn> 和 <xref:System.Data.DataRow>，前者表示给定表中的数据列（这会最终确定可在该表中输入的数据种类），后者表示给定表中的数据行。  可以将控件复杂绑定到数据表中包含的信息（例如将 <xref:System.Windows.Forms.DataGridView> 控件绑定到数据表）。  但是，当绑定到 <xref:System.Data.DataTable> 时，实际上是绑定到该表的默认视图。  
  
-   <xref:System.Data.DataView>.  <xref:System.Data.DataView> 是可筛选或排序的单个数据表的自定义视图。  数据视图是复杂绑定控件使用的数据“快照”。  可以简单绑定或复杂绑定到数据视图中的数据，但请注意，绑定到的是数据的固定“图片”而不是一个干净的、不断更新的数据源。  
  
-   <xref:System.Data.DataSet>.  <xref:System.Data.DataSet> 是数据库中表、关系和数据约束的集合。  可以简单绑定或复杂绑定到数据集内的数据，但请注意，绑定到的是 <xref:System.Data.DataSet> 的默认 <xref:System.Data.DataViewManager>（请参见下一个项目符号的内容）。  
  
-   <xref:System.Data.DataViewManager>.  <xref:System.Data.DataViewManager> 是整个 <xref:System.Data.DataView> 的自定义视图，它与 <xref:System.Data.DataSet> 类似，但其中包括各种关系。  使用 <xref:System.Data.DataViewManager.DataViewSettings%2A> 集合，可以为给定表的 <xref:System.Data.DataViewManager> 具有的任何视图设置默认筛选器和排序选项。  
  
## 请参阅  
 [Windows 窗体数据绑定中的更改通知](../../../docs/framework/winforms/change-notification-in-windows-forms-data-binding.md)   
 [数据绑定和 Windows 窗体](../../../docs/framework/winforms/data-binding-and-windows-forms.md)   
 [Windows 窗体数据绑定](../../../docs/framework/winforms/windows-forms-data-binding.md)