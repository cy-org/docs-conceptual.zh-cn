---
title: "查找行 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-ado"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 5da300e2-74c0-4d13-9202-fc20ed8212d8
caps.latest.revision: 3
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 3
---
# 查找行
可以使用 <xref:System.Data.DataView> 的 <xref:System.Data.DataView.Find%2A> 和 <xref:System.Data.DataView.FindRows%2A> 方法，根据排序关键字值搜索行。  **Find** 和 **FindRows** 方法中的搜索值是否区分大小写取决于基础 <xref:System.Data.DataTable> 的 **CaseSensitive** 属性。  搜索值必须完全匹配现有排序关键字值才能返回结果。  
  
 **Find** 方法返回一个整数，该整数表示匹配搜索条件的 <xref:System.Data.DataRowView> 的索引。  如果多个行匹配搜索条件，则只返回第一个匹配 **DataRowView** 的索引。  如果未找到匹配项，**Find** 将返回 \-1。  
  
 若要返回匹配多个行的搜索结果，可以使用 **FindRows** 方法。  **FindRows** 的工作方式与 **Find** 方法类似，不同的只是前者返回引用 **DataView** 中所有匹配行的 **DataRowView** 数组。  如果未找到匹配项，**DataRowView** 数组将为空。  
  
 若要使用 **Find** 或 **FindRows** 方法，必须通过将 **ApplyDefaultSort** 设置为 **true** 或通过使用 **Sort** 属性来指定排序顺序。  如果未指定排序顺序，则将引发异常。  
  
 **Find** 和 **FindRows** 方法将一个值数组用作输入，该数组的长度与排序顺序所包含的列数相匹配。  在对单个列进行排序的情况下，可以传递单个值。  对于包含多个列的排序顺序，可传递一个对象数组。  请注意，当对多个列进行排序时，对象数组中的值必须匹配在 **DataView** 的 **Sort** 属性中指定的列的顺序。  
  
 以下代码示例显示对具有单个列排序顺序的 **DataView** 调用的 **Find** 方法。  
  
```vb  
Dim custView As DataView = _  
  New DataView(custDS.Tables("Customers"), "", _  
  "CompanyName", DataViewRowState.CurrentRows)  
  
Dim rowIndex As Integer = custView.Find("The Cracker Box")  
  
If rowIndex = -1 Then  
  Console.WriteLine("No match found.")  
Else  
  Console.WriteLine("{0}, {1}", _  
    custView(rowIndex)("CustomerID").ToString(), _  
    custView(rowIndex)("CompanyName").ToString())  
End If  
  
```  
  
```csharp  
DataView custView = new DataView(custDS.Tables["Customers"], "",   
  "CompanyName", DataViewRowState.CurrentRows);  
  
int rowIndex = custView.Find("The Cracker Box");  
  
if (rowIndex == -1)  
  Console.WriteLine("No match found.");  
else  
  Console.WriteLine("{0}, {1}",  
    custView[rowIndex]["CustomerID"].ToString(),  
    custView[rowIndex]["CompanyName"].ToString());  
```  
  
 如果 **Sort** 属性指定多个列，则必须按 **Sort** 属性指定的顺序为每个列传递包含搜索值的对象数组，如以下代码示例所示。  
  
```vb  
Dim custView As DataView = _  
  New DataView(custDS.Tables("Customers"), "", _  
  "CompanyName, ContactName", _  
  DataViewRowState.CurrentRows)  
  
Dim foundRows() As DataRowView = _  
  custView.FindRows(New object() {"The Cracker Box", "Liu Wong"})  
  
If foundRows.Length = 0 Then  
  Console.WriteLine("No match found.")  
Else  
  Dim myDRV As DataRowView  
  For Each myDRV In foundRows  
    Console.WriteLine("{0}, {1}", _  
      myDRV("CompanyName").ToString(), myDRV("ContactName").ToString())  
  Next  
End If  
  
```  
  
```csharp  
DataView custView = new DataView(custDS.Tables["Customers"], "",  
  "CompanyName, ContactName",  
  DataViewRowState.CurrentRows);  
  
DataRowView[] foundRows =   
  custView.FindRows(new object[] {"The Cracker Box", "Liu Wong"});  
  
if (foundRows.Length == 0)  
  Console.WriteLine("No match found.");  
else  
  foreach (DataRowView myDRV in foundRows)  
    Console.WriteLine("{0}, {1}", myDRV["CompanyName"].ToString(),   
      myDRV["ContactName"].ToString());  
```  
  
## 请参阅  
 <xref:System.Data.DataTable>   
 <xref:System.Data.DataView>   
 [DataView](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/dataviews.md)   
 [ADO.NET 托管提供程序和数据集开发人员中心](http://go.microsoft.com/fwlink/?LinkId=217917)