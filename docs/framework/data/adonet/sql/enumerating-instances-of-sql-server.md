---
title: "枚举 SQL Server 的实例 (ADO.NET) | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-ado"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: ddf1c83c-9d40-45e6-b04d-9828c6cbbfdc
caps.latest.revision: 8
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 7
---
# 枚举 SQL Server 的实例 (ADO.NET)
[!INCLUDE[ssNoVersion](../../../../../includes/ssnoversion-md.md)] 允许应用程序在当前网络中查找 [!INCLUDE[ssNoVersion](../../../../../includes/ssnoversion-md.md)] 实例。  <xref:System.Data.Sql.SqlDataSourceEnumerator> 类向应用程序开发人员公开此信息，提供包含所有可见服务器的信息的 <xref:System.Data.DataTable>。  此返回的表包含网络上可用服务器实例的列表（该列表与用户尝试创建新连接时提供的列表匹配），并展开“连接属性”对话框上包含所有可用服务器的下拉列表。  显示的结果并非总是完整的。  
  
> [!NOTE]
>  与大多数 Windows 服务一样，最好使用尽可能少的权限运行 SQL 浏览器服务。  有关 SQL Browser 服务以及如何管理其行为的更多信息，请参见 [!INCLUDE[ssNoVersion](../../../../../includes/ssnoversion-md.md)] 联机丛书。  
  
## 检索枚举器实例  
 若要检索包含有关可用 [!INCLUDE[ssNoVersion](../../../../../includes/ssnoversion-md.md)] 实例的信息的表，必须先使用共享\/静态 <xref:System.Data.Sql.SqlDataSourceEnumerator.Instance%2A> 属性来检索枚举器：  
  
```vb  
Dim instance As System.Data.Sql.SqlDataSourceEnumerator = _  
   System.Data.Sql.SqlDataSourceEnumerator.Instance  
```  
  
```csharp  
System.Data.Sql.SqlDataSourceEnumerator instance =   
   System.Data.Sql.SqlDataSourceEnumerator.Instance  
```  
  
 检索到静态实例之后，可以调用 <xref:System.Data.Sql.SqlDataSourceEnumerator.GetDataSources%2A> 方法，该方法返回包含可用服务器信息的 <xref:System.Data.DataTable>：  
  
```vb  
Dim dataTable As System.Data.DataTable = instance.GetDataSources()  
```  
  
```csharp  
System.Data.DataTable dataTable = instance.GetDataSources();  
```  
  
 通过方法调用返回的表包含以下列，所有列均包含 `string` 值：  
  
|列|描述|  
|-------|--------|  
|**ServerName**|服务器的名称。|  
|**InstanceName**|服务器实例的名称。  如果服务器作为默认实例运行，则为空白。|  
|**IsClustered**|指示服务器是否属于群集。|  
|**版本**|服务器的版本。  例如：<br /><br /> -   9.00.x \([!INCLUDE[ssVersion2005](../../../../../includes/ssversion2005-md.md)]\)<br />-   10.0.xx \([!INCLUDE[ssKatmai](../../../../../includes/sskatmai-md.md)]\)<br />-   10.50.x \([!INCLUDE[ssKilimanjaro](../../../../../includes/sskilimanjaro-md.md)]\)<br />-   11.0.xx \([!INCLUDE[ssNoVersion](../../../../../includes/ssnoversion-md.md)] 2012\)|  
  
## 枚举限制  
 所有可用服务器可能会列出，也可能不会列出。  根据超时和网络通信量等因素，列表可能会有所不同。  这可能会使两个连续调用生成不同的列表。  只会列出相同网络上的服务器。  广播包通常不会遍历路由器，这也就是可能会看不到某个服务器列出的原因，但是在各个调用之间是稳定的。  
  
 列出的服务器可能包含其他信息，也可能不包含其他信息，例如 `IsClustered` 和版本。  这取决于获取列表的方式。  通过 [!INCLUDE[ssNoVersion](../../../../../includes/ssnoversion-md.md)] 浏览器服务列出的服务器比通过 Windows 基础结构发现的服务器具有更详细的信息，后者仅列出名称。  
  
> [!NOTE]
>  只有以完全信任模式运行时，才可以使用服务器枚举。  在部分信任的环境中运行的程序集将无法使用服务器枚举，即使这些程序集具有 <xref:System.Data.SqlClient.SqlClientPermission> 代码访问安全性 \(CAS\) 权限。  
  
 [!INCLUDE[ssNoVersion](../../../../../includes/ssnoversion-md.md)] 通过使用名为 SQL Browser 的外部 Windows 服务来提供 <xref:System.Data.Sql.SqlDataSourceEnumerator> 的信息。  默认情况下启用此服务，但是管理员可以关闭或禁用此服务，使服务器实例对此类是不可见的。  
  
## 示例  
 以下控制台应用程序检索所有可见 [!INCLUDE[ssNoVersion](../../../../../includes/ssnoversion-md.md)] 实例的信息，并在控制台窗口中显示该信息。  
  
```vb  
Imports System.Data.Sql  
  
Module Module1  
  Sub Main()  
    ' Retrieve the enumerator instance and then the data.  
    Dim instance As SqlDataSourceEnumerator = _  
     SqlDataSourceEnumerator.Instance  
    Dim table As System.Data.DataTable = instance.GetDataSources()  
  
    ' Display the contents of the table.  
    DisplayData(table)  
  
    Console.WriteLine("Press any key to continue.")  
    Console.ReadKey()  
  End Sub  
  
  Private Sub DisplayData(ByVal table As DataTable)  
    For Each row As DataRow In table.Rows  
      For Each col As DataColumn In table.Columns  
        Console.WriteLine("{0} = {1}", col.ColumnName, row(col))  
      Next  
      Console.WriteLine("============================")  
    Next  
  End Sub  
End Module  
```  
  
```csharp  
using System.Data.Sql;  
  
class Program  
{  
  static void Main()  
  {  
    // Retrieve the enumerator instance and then the data.  
    SqlDataSourceEnumerator instance =  
      SqlDataSourceEnumerator.Instance;  
    System.Data.DataTable table = instance.GetDataSources();  
  
    // Display the contents of the table.  
    DisplayData(table);  
  
    Console.WriteLine("Press any key to continue.");  
    Console.ReadKey();  
  }  
  
  private static void DisplayData(System.Data.DataTable table)  
  {  
    foreach (System.Data.DataRow row in table.Rows)  
    {  
      foreach (System.Data.DataColumn col in table.Columns)  
      {  
        Console.WriteLine("{0} = {1}", col.ColumnName, row[col]);  
      }  
      Console.WriteLine("============================");  
    }  
  }  
}  
```  
  
## 请参阅  
 [SQL Server 和 ADO.NET](../../../../../docs/framework/data/adonet/sql/index.md)   
 [ADO.NET 托管提供程序和数据集开发人员中心](http://go.microsoft.com/fwlink/?LinkId=217917)