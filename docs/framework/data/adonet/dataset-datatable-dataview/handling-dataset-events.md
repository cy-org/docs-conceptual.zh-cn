---
title: "处理数据集事件 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-ado"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 54edefe0-bc38-419b-b486-3d8a0c356f13
caps.latest.revision: 4
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 4
---
# 处理数据集事件
<xref:System.Data.DataSet> 对象提供三个事件：<xref:System.ComponentModel.MarshalByValueComponent.Disposed>、<xref:System.Data.DataSet.Initialized> 和 <xref:System.Data.DataSet.MergeFailed>。  
  
## MergeFailed 事件  
 `DataSet` 对象的最常用事件是 `MergeFailed`，当要合并的 `DataSet` 对象的架构发生冲突时，会引发该事件。 当目标和源 <xref:System.Data.DataRow> 有相同的主键值，且 <xref:System.Data.DataSet.EnforceConstraints%2A> 属性设置为 `true` 时会发生这种情况。 例如，如果所合并表的主键列与两个 `DataSet` 对象中的表的相同，则将发生异常并引发 `MergeFailed` 事件。 传递给 <xref:System.Data.MergeFailedEventArgs> 事件的 `MergeFailed` 对象具有 <xref:System.Data.MergeFailedEventArgs.Conflict%2A> 属性（标识两个 `DataSet` 对象之间的架构冲突）和 <xref:System.Data.MergeFailedEventArgs.Table%2A> 属性（标识发生冲突的表的名称）。  
  
 下面的代码段演示如何为 `MergeFailed` 事件添加事件处理程序。  
  
```vb  
AddHandler workDS.MergeFailed, New MergeFailedEventHandler( _  
  AddressOf DataSetMergeFailed)  
  
Private Shared Sub DataSetMergeFailed(  _  
  sender As Object,args As MergeFailedEventArgs)  
  Console.WriteLine("Merge failed for table " & args.Table.TableName)  
  Console.WriteLine("Conflict = " & args.Conflict)  
End Sub  
  
```  
  
```csharp  
workDS.MergeFailed += new MergeFailedEventHandler(DataSetMergeFailed);  
  
private static void DataSetMergeFailed(  
  object sender, MergeFailedEventArgs args)  
{  
  Console.WriteLine("Merge failed for table " + args.Table.TableName);  
  Console.WriteLine("Conflict = " + args.Conflict);  
}  
```  
  
## 初始化事件  
 在 <xref:System.Data.DataSet.Initialized> 构造函数初始化 `DataSet` 的新实例后会发生 `DataSet` 事件。  
  
 如果 <xref:System.Data.DataSet.IsInitialized%2A> 已完成初始化，`true` 属性会返回 `DataSet`；否则，返回 `false`。<xref:System.Data.DataSet.BeginInit%2A> 方法，它开始初始化 `DataSet`，将 <xref:System.Data.DataSet.IsInitialized%2A> 设置为 `false`。<xref:System.Data.DataSet.EndInit%2A> 方法（用于结束 `DataSet` 的初始化）将它设置为 `true`。[!INCLUDE[vsprvs](../../../../../includes/vsprvs-md.md)] 设计环境使用这些方法初始化其他组件使用的 `DataSet`。 通常不会在代码中使用这些方法。  
  
## 释放事件  
 `DataSet` 派生自 <xref:System.ComponentModel.MarshalByValueComponent> 类，该类可公开 <xref:System.ComponentModel.MarshalByValueComponent.Dispose%2A> 方法和 <xref:System.ComponentModel.MarshalByValueComponent.Disposed> 事件。<xref:System.ComponentModel.MarshalByValueComponent.Disposed>事件添加了一个事件处理程序以侦听组件上已释放的事件。 如果您要在调用 <xref:System.ComponentModel.MarshalByValueComponent.Disposed>方法时执行代码，则可以使用 `DataSet` 的 <xref:System.ComponentModel.MarshalByValueComponent.Dispose%2A>事件。<xref:System.ComponentModel.MarshalByValueComponent.Dispose%2A>释放由 <xref:System.ComponentModel.MarshalByValueComponent> 使用的资源。  
  
> [!NOTE]
>  `DataSet` 和 `DataTable` 对象从 <xref:System.ComponentModel.MarshalByValueComponent>继承而来，并且支持用于远程处理的 <xref:System.Runtime.Serialization.ISerializable> 接口。 这两个对象是唯一可远程处理的 ADO.NET 对象。 有关详细信息，请参阅[Remote Objects](http://msdn.microsoft.com/zh-cn/515686e6-0a8d-42f7-8188-73abede57c58)。  
  
 有关使用 `DataSet` 时的其他可用事件的信息，请参阅[处理 DataTable 事件](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/handling-datatable-events.md)和[处理 DataAdapter 事件](../../../../../docs/framework/data/adonet/handling-dataadapter-events.md)。  
  
## 请参阅  
 [DataSet、DataTable 和 DataView](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/index.md)   
 [验证数据](../Topic/Validating%20Data.md)   
 [在 ADO.NET 中检索和修改数据](../../../../../docs/framework/data/adonet/retrieving-and-modifying-data.md)   
 [ADO.NET 托管提供程序和 DataSet 开发人员中心](http://go.microsoft.com/fwlink/?LinkId=217917)