---
title: "DataView | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-ado"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 0fe5dfa2-c1cd-435f-90b6-b4dd2e3ef34b
caps.latest.revision: 4
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 4
---
# DataView
您可以利用 <xref:System.Data.DataView> 创建存储在 <xref:System.Data.DataTable>（一种通常在数据绑定应用程序中使用的功能）中的数据的不同视图。  使用 **DataView**，您可以使用不同排序顺序显示表中的数据，并且可以按行状态或基于筛选器表达式来筛选数据。  
  
 **DataView** 提供基础 **DataTable** 中的数据的动态视图：内容、排序和成员资格会实时反映它们的更改。  此行为与 **DataTable** 的 **Select** 方法不同，该方法从基于特定筛选器和\/排序顺序的表中返回 <xref:System.Data.DataRow> 数组：虽然此内容可反映对基础表的更改，但其成员资格和顺序却保持不变。  **DataView** 的动态功能使其成为数据绑定应用程序的理想选择。  
  
 与数据库视图类似，**DataView** 为您提供了可向其应用不同排序和筛选条件的单个数据集的动态视图。  但是，与数据库视图不同的是，**DataView** 不能作为表来对待，无法提供联接的表的视图。  另外，还不能排除存在于源表中的列，也不能追加不存在于源表中的列（如计算列）。  
  
 可以使用 <xref:System.Data.DataView.DataViewManager%2A> 来管理 **DataSet** 中所有表的视图设置。  **DataViewManager** 为您提供了一种方便的方法来管理每个表的默认视图设置。  在将一个控件绑定到 **DataSet** 的多个表时，绑定到 **DataViewManager** 是理想的选择。  
  
## 本节内容  
 [创建 DataView](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/creating-a-dataview.md)  
 描述如何为 **DataTable** 创建 **DataView**。  
  
 [排序和筛选数据](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/sorting-and-filtering-data.md)  
 描述如何设置 **DataView** 的属性，以返回符合特定筛选条件的数据行的子集或以特定排序顺序返回数据。  
  
 [DataRow 和 DataRowView](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/datarows-and-datarowviews.md)  
 描述如何访问由 **DataView** 公开的数据。  
  
 [查找行](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/finding-rows.md)  
 描述如何在 **DataView** 中查找特定行。  
  
 [ChildView 和关系](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/childviews-and-relations.md)  
 描述如何使用 **DataView** 创建父子关系数据的视图。  
  
 [修改 DataView](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/modifying-dataviews.md)  
 描述如何通过 **DataView** 修改基础 **DataTable** 中的数据（包括启用或禁用更新）。  
  
 [处理 DataView 事件](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/handling-dataview-events.md)  
 描述如何使用 **ListChanged** 事件接收在 **DataView** 的内容或顺序得到更新时发出的通知。  
  
 [管理 DataView](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/managing-dataviews.md)  
 描述如何使用 **DataViewManager** 来管理 **DataSet** 中每个表的 **DataView** 设置。  
  
## 相关章节  
 [ASP.NET Web Applications](http://msdn.microsoft.com/zh-cn/a812d7b7-049e-4234-a4c2-6acf690301f6)  
 提供创建 ASP.NET 应用程序、Web 窗体和 Web 服务的概述和详细步骤信息。  
  
 [Windows Applications](http://msdn.microsoft.com/zh-cn/a6bb2180-09b1-4738-b9fd-7fb05fc92f23)  
 提供有关使用 Windows 窗体和控制台应用程序的详细信息。  
  
 [DataSet、DataTable 和 DataView](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/index.md)  
 描述 **DataSet** 对象，并说明如何使用它来管理应用程序数据。  
  
 [DataTable](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/datatables.md)  
 描述 **DataTable** 对象，并说明如何使用它来管理应用程序数据本身或将其当作 **DataSet** 的一部分来管理。  
  
 [ADO.NET](../../../../../docs/framework/data/adonet/index.md)  
 描述 ADO.NET 结构和组件，并说明如何使用 ADO.NET 来访问现有的数据源和管理应用程序数据。  
  
## 请参阅  
 [ADO.NET 托管提供程序和数据集开发人员中心](http://go.microsoft.com/fwlink/?LinkId=217917)