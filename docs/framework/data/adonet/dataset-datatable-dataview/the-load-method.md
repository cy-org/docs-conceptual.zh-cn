---
title: "Load 方法 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-ado"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: e22e5812-89c6-41f0-9302-bb899a46dbff
caps.latest.revision: 3
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 3
---
# Load 方法
可以使用 <xref:System.Data.DataTable.Load%2A> 方法为 <xref:System.Data.DataTable> 加载数据源中行。  这是一种重载方法，其最简单的形式是接受一个参数 **DataReader**。  在此形式中，将只是为 **DataTable** 加载行。  可以选择指定 **LoadOption** 参数，用于控制如何将数据添加到 **DataTable** 中。  
  
 如果 **DataTable** 中已包含数据行，**LoadOption** 参数非常有用，因为该参数描述从数据源传入的数据如何与表中已有的数据组合在一起。  例如，**PreserveCurrentValues**（默认设置）指定如果 **DataTable** 中的某行标记为 **Added**，**Original** 值或每一列将设置为数据源中匹配行的内容。  **Current** 值将保留在添加行时分配的值，行的 **RowState** 将设置为 **Changed**。  
  
 下表给出了对 <xref:System.Data.LoadOption> 枚举值的简要说明。  
  
|LoadOption 值|描述|  
|------------------|--------|  
|**OverwriteRow**|如果传入行的 **PrimaryKey** 值与 **DataTable** 中已有的某个行相同，每一列的 **Original** 和 **Current** 值将替换为传入行中的值，**RowState** 属性设置为 **Unchanged**。<br /><br /> 如果数据源中的行在 **DataTable** 中尚不存在，那么将以 **RowState** 值 **Unchanged** 添加。<br /><br /> 此选项的作用是刷新 **DataTable** 的内容，使其与数据源的内容匹配。|  
|**PreserveCurrentValues（默认值）**|如果传入行的 **PrimaryKey** 值与 **DataTable** 中已有的某个行相同，**Original** 值将设置为传入行的内容，**Current** 值不变。<br /><br /> 如果 **RowState** 为 **Added** 或 **Modified**，将设置为 **Modified**。<br /><br /> 如果 **RowState** 为 **Deleted**，将仍为 **Deleted**。<br /><br /> 如果数据源中的行在 **DataTable** 中尚不存在，将添加这些行，并将 **RowState** 设置为 **Unchanged**。|  
|**UpdateCurrentValues**|如果传入行的 **PrimaryKey** 值与 **DataTable** 中已有的某个行相同，**Current** 值将复制到 **Original** 值，**Current** 值设置为传入行的内容。<br /><br /> 如果 **DataTable** 中的 **RowState** 为 **Added**，**RowState** 仍为 **Added**。  对于标记为 **Modified** 或 **Deleted** 的行，**RowState** 为 **Modified**。<br /><br /> 将添加数据源中在 **DataTable** 尚不存在的行，**RowState** 设置为 **Added**。|  
  
 以下示例使用 **Load** 方法显示 **Northwind** 数据库中员工的生日列表。  
  
 \[Visual Basic\]  
  
```  
Private Sub LoadBirthdays(ByVal connectionString As String)  
    ' Assumes that connectionString is a valid connection string  
    ' to the Northwind database on SQL Server.  
    Dim queryString As String = _  
    "SELECT LastName, FirstName, BirthDate " & _  
      " FROM dbo.Employees " & _  
      "ORDER BY BirthDate, LastName, FirstName"  
  
    ' Open and fill a DataSet.   
    Dim adapter As SqlDataAdapter = New SqlDataAdapter( _  
        queryString, connectionString)  
    Dim employees As New DataSet  
    adapter.Fill(employees, "Employees")  
  
    ' Create a SqlDataReader for use with the Load Method.  
    Dim reader As DataTableReader = employees.GetDataReader()  
  
    ' Create an instance of DataTable and assign the first  
    ' DataTable in the DataSet.Tables collection to it.  
    Dim dataTableEmp As DataTable = employees.Tables(0)  
  
    ' Fill the DataTable with data by calling Load and  
    ' passing the SqlDataReader.  
    dataTableEmp.Load(reader, LoadOption.OverwriteRow)  
  
    ' Loop through the rows collection and display the values  
    ' in the console window.  
    Dim employeeRow As DataRow  
    For Each employeeRow In dataTableEmp.Rows  
        Console.WriteLine("{0:MM\\dd\\yyyy}" & ControlChars.Tab & _  
          "{1}, {2}", _  
          employeeRow("BirthDate"), _  
          employeeRow("LastName"), _  
          employeeRow("FirstName"))  
    Next employeeRow  
  
    ' Keep the window opened to view the contents.  
    Console.ReadLine()  
End Sub  
```  
  
## 请参阅  
 [在 DataTable 中处理数据](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/manipulating-data-in-a-datatable.md)   
 [ADO.NET 托管提供程序和数据集开发人员中心](http://go.microsoft.com/fwlink/?LinkId=217917)