---
title: "处理 DataView 事件 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-ado"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: e5675663-fc91-4e0d-87a9-481b25b64c0f
caps.latest.revision: 4
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 4
---
# 处理 DataView 事件
可以使用 <xref:System.Data.DataView> 的 <xref:System.Data.DataView.ListChanged> 事件确定某个视图是否已更新。  引发该事件的更新包括添加、删除或修改基础表中的某行；在基础表的架构中添加或删除某列；更改父或子关系。  **ListChanged** 事件还将通知您所查看的行列表是否已经由于应用新的排序顺序或筛选器而发生重大更改。  
  
 **ListChanged** 事件实现 <xref:System.ComponentModel> 命名空间的 **ListChangedEventHandler** 委托，并将 <xref:System.ComponentModel.ListChangedEventArgs> 对象用作输入。  您可以使用 **ListChangedEventArgs** 对象的 **ListChangedType** 属性中的 <xref:System.ComponentModel.ListChangedType> 枚举值来确定发生了哪一种类型的更改。  对于涉及添加、删除或移动行的更改，可以使用 **ListChangedEventArgs** 对象的 **NewIndex** 属性来访问已添加或已移动的行的新索引以及已删除的行的先前索引。  对于已移动的行，可以使用 **ListChangedEventArgs** 对象的 **OldIndex** 属性来访问已移动的行的先前索引。  
  
 **DataViewManager** 还会公开一个 **ListChanged** 事件来通知您是否已添加或移除表，或者是否已对基础 **DataSet** 的 **Relations** 集合做出更改。  
  
 以下代码示例显示如何添加 **ListChanged** 事件处理程序。  
  
```vb  
AddHandler custView.ListChanged, _  
  New System.ComponentModel.ListChangedEventHandler( _  
  AddressOf OnListChanged)  
  
Private Shared Sub OnListChanged( _  
  sender As Object, args As System.ComponentModel.ListChangedEventArgs)  
  Console.WriteLine("ListChanged:")  
  Console.WriteLine(vbTab & "    Type = " & _  
    System.Enum.GetName(args.ListChangedType.GetType(), _  
    args.ListChangedType))  
  Console.WriteLine(vbTab & "OldIndex = " & args.OldIndex)  
  Console.WriteLine(vbTab & "NewIndex = " & args.NewIndex)  
End Sub  
  
```  
  
```csharp  
custView.ListChanged  += new   
  System.ComponentModel.ListChangedEventHandler(OnListChanged);  
  
protected static void OnListChanged(object sender,   
  System.ComponentModel.ListChangedEventArgs args)  
{  
  Console.WriteLine("ListChanged:");  
  Console.WriteLine("\t    Type = " + args.ListChangedType);  
  Console.WriteLine("\tOldIndex = " + args.OldIndex);  
  Console.WriteLine("\tNewIndex = " + args.NewIndex);  
}  
```  
  
## 请参阅  
 <xref:System.Data.DataView>   
 <xref:System.ComponentModel.ListChangedEventHandler>   
 [DataView](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/dataviews.md)   
 [ADO.NET 托管提供程序和数据集开发人员中心](http://go.microsoft.com/fwlink/?LinkId=217917)