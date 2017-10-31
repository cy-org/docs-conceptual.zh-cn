---
title: "ADO.NET 代码示例 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-ado"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: c119657a-9ce6-4940-91e4-ac1d5f0d9584
caps.latest.revision: 7
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 7
---
# ADO.NET 代码示例
本主题中的代码列表演示如何使用下面的 ADO.NET 技术从数据库中检索数据：  
  
-   ADO.NET 数据提供程序：  
  
    -   [SqlClient](#_SqlClient) (`System.Data.SqlClient`)  
  
    -   [OleDb](#_OleDb) (`System.Data.OleDb`)  
  
    -   [Odbc](#_Odbc) (`System.Data.Odbc`)  
  
    -   [OracleClient](#_OracleClient) (`System.Data.OracleClient`)  
  
-   ADO.NET 实体框架：  
  
    -   [LINQ to Entities](#_LINQ)  
  
    -   [类型化的 ObjectQuery](#_QBM)  
  
    -   [EntityClient](#_EntityClient) (`System.Data.EntityClient`)  
  
-   [LINQ to SQL](#_LINQ2SQL)  
  
## <a name="adonet-data-provider-examples"></a>ADO.NET 数据提供程序示例  
 以下代码列表演示如何使用 ADO.NET 数据提供程序从数据库中检索数据。 数据在一个 `DataReader` 中返回。 有关详细信息，请参阅[使用 DataReader 检索数据](../../../../docs/framework/data/adonet/retrieving-data-using-a-datareader.md)。  
  
<a name="_SqlClient"></a>   
### <a name="sqlclient"></a>SqlClient  
 此示例中的代码假定您可以连接到 Microsoft `Northwind` 上的 [!INCLUDE[ssNoVersion](../../../../includes/ssnoversion-md.md)] 示例数据库。 该代码将创建<xref:System.Data.SqlClient.SqlCommand>以从 Products 表中，选择行添加<xref:System.Data.SqlClient.SqlParameter>将结果限制为其 UnitPrice 大于指定的参数值，在此情形 5 行。 <xref:System.Data.SqlClient.SqlConnection>内打开`using`块中，这将确保关闭和释放在代码退出时会资源。 该代码通过使用执行命令<xref:System.Data.SqlClient.SqlDataReader>，并在控制台窗口中显示结果。  
  
  [DataWorks SampleApp.SqlClient#1](../CodeSnippet/VS_Snippets_ADO.NET/DataWorks SampleApp.SqlClient#1)]  
  
 [[Top]](#_TOP)  
  
<a name="_OleDb"></a>   
### <a name="oledb"></a>OleDb  
 此示例中的代码假定你可以连接到 Microsoft Access Northwind 示例数据库。 该代码将创建<xref:System.Data.OleDb.OleDbCommand>以从 Products 表中，选择行添加<xref:System.Data.OleDb.OleDbParameter>将结果限制为其 UnitPrice 大于指定的参数值，在此情形 5 行。 <xref:System.Data.OleDb.OleDbConnection>内打开`using`块中，这将确保关闭和释放在代码退出时会资源。 该代码通过使用执行命令<xref:System.Data.OleDb.OleDbDataReader>，并在控制台窗口中显示结果。  
  
  [DataWorks SampleApp.OleDb#1](../CodeSnippet/VS_Snippets_ADO.NET/DataWorks SampleApp.OleDb#1)]  
  
 [[Top]](#_TOP)  
  
<a name="_Odbc"></a>   
### <a name="odbc"></a>Odbc  
 此示例中的代码假定你可以连接到 Microsoft Access Northwind 示例数据库。 该代码将创建<xref:System.Data.Odbc.OdbcCommand>以从 Products 表中，选择行添加<xref:System.Data.Odbc.OdbcParameter>将结果限制为其 UnitPrice 大于指定的参数值，在此情形 5 行。 <xref:System.Data.Odbc.OdbcConnection>内打开`using`块中，这将确保关闭和释放在代码退出时会资源。 通过使用执行命令<xref:System.Data.Odbc.OdbcDataReader>，并在控制台窗口中显示结果。  
  
<!-- TODO: review snippet reference  [!CODE [DataWorksSampleApp.Odbc#1](DataWorksSampleApp.Odbc#1)]  -->  
  
 [[Top]](#_TOP)  
  
<a name="_OracleClient"></a>   
### <a name="oracleclient"></a>OracleClient  
 此示例中的代码假定已建立与 Oracle 服务器上的 DEMO.CUSTOMER 的连接。 您还必须添加对 System.Data.OracleClient.dll 的引用。 代码也会返回中的数据<xref:System.Data.OracleClient.OracleDataReader>。  
  
  [DataWorks SampleApp.Oracle#1](../CodeSnippet/VS_Snippets_ADO.NET/DataWorks SampleApp.Oracle#1)]  
  
 [[Top]](#_TOP)  
  
## <a name="entity-framework-examples"></a>实体框架示例  
 以下代码列表演示如何通过查询实体数据模型 (EDM) 中的实体来从数据源检索数据。 这些示例使用[Northwind 模型](http://msdn.microsoft.com/zh-cn/74521f8c-e974-48cb-8858-c08deff52638)。 有关详细信息，请参阅[实体框架概述](../../../../docs/framework/data/adonet/ef/overview.md)。  
  
<a name="_LINQ"></a>   
### <a name="linq-to-entities"></a>LINQ to Entities  
 此示例中的代码使用 LINQ 查询以 Categories 对象的形式返回数据，这些对象将作为仅包含 CategoryID 和 CategoryName 属性的匿名类型提取。 有关详细信息，请参阅[LINQ to Entities 概述](http://msdn.microsoft.com/zh-cn/86d87a27-c17a-45ac-b28d-72c8500333c6)。  
  
```  
Option Explicit On  
Option Strict On  
  
Imports System  
Imports System.Linq  
Imports System.Data.Objects  
Imports NorthwindModel  
  
Class LinqSample  
    Public Shared Sub ExecuteQuery()  
        Using context As NorthwindEntities = New NorthwindEntities()  
            Try  
                Dim query = From category In context.Categories _  
                            Select New With _  
                            { _  
                                .categoryID = category.CategoryID, _  
                                .categoryName = category.CategoryName _  
                            }  
  
                For Each categoryInfo In query  
                    Console.WriteLine(vbTab & "{0}" & vbTab & "{1}", _  
                        categoryInfo.categoryID, categoryInfo.categoryName)  
                Next  
            Catch ex As Exception  
                Console.WriteLine(ex.Message)  
            End Try  
        End Using  
    End Sub  
End Class  
```  
  
 在 C# 中：  
  
```  
using System;  
using System.Linq;  
using System.Data.Objects;  
using NorthwindModel;  
  
class LinqSample  
{  
    public static void ExecuteQuery()  
    {  
        using (NorthwindEntities context = new NorthwindEntities())  
        {  
            try  
            {  
                var query = from category in context.Categories  
                            select new  
                            {  
                                categoryID = category.CategoryID,  
                                categoryName = category.CategoryName  
                            };  
  
                foreach (var categoryInfo in query)  
                {  
                    Console.WriteLine("\t{0}\t{1}",  
                        categoryInfo.categoryID, categoryInfo.categoryName);  
                }  
            }  
            catch (Exception ex)  
            {  
                Console.WriteLine(ex.Message);  
            }  
        }  
    }  
}  
```  
  
 [[Top]](#_TOP)  
  
<a name="_QBM"></a>   
### <a name="typed-objectquery"></a>类型化 ObjectQuery  
 在此示例中的代码使用<xref:System.Data.Objects.ObjectQuery%601>以 Categories 对象形式返回数据。 有关详细信息，请参阅[对象查询](http://msdn.microsoft.com/zh-cn/0768033c-876f-471d-85d5-264884349276)。  
  
```  
Option Explicit On  
Option Strict On  
  
Imports System  
Imports System.Data.Objects  
Imports NorthwindModel  
  
Class ObjectQuerySample  
    Public Shared Sub ExecuteQuery()  
        Using context As NorthwindEntities = New NorthwindEntities()  
            Dim categoryQuery As ObjectQuery(Of Categories) = context.Categories  
  
            For Each category As Categories In _  
                categoryQuery.Execute(MergeOption.AppendOnly)  
                Console.WriteLine(vbTab & "{0}" & vbTab & "{1}", _  
                    category.CategoryID, category.CategoryName)  
            Next  
        End Using  
    End Sub  
End Class  
```  
  
 在 C# 中：  
  
```  
using System;  
using System.Data.Objects;  
using NorthwindModel;  
  
class ObjectQuerySample  
{  
    public static void ExecuteQuery()  
    {  
        using (NorthwindEntities context = new NorthwindEntities())  
        {  
            ObjectQuery<Categories> categoryQuery = context.Categories;  
  
            foreach (Categories category in   
                categoryQuery.Execute(MergeOption.AppendOnly))  
            {  
                Console.WriteLine("\t{0}\t{1}",  
                    category.CategoryID, category.CategoryName);  
            }  
        }  
    }  
}  
```  
  
 [[Top]](#_TOP)  
  
<a name="_EntityClient"></a>   
### <a name="entityclient"></a>EntityClient  
 在此示例中的代码使用<xref:System.Data.EntityClient.EntityCommand>来执行实体 SQL 查询。 此查询会返回表示 Categories 实体类型的实例的记录的列表。 <xref:System.Data.EntityClient.EntityDataReader>用于访问结果集中的数据记录。 有关详细信息，请参阅[用于实体框架的 EntityClient 提供程序](../../../../docs/framework/data/adonet/ef/entityclient-provider-for-the-entity-framework.md)。  
  
```  
Option Explicit On  
Option Strict On  
  
Imports System  
Imports System.Data  
Imports System.Data.Common  
Imports System.Data.EntityClient  
Imports NorthwindModel  
  
Class EntityClientSample  
    Public Shared Sub ExecuteQuery()  
        Dim queryString As String = _  
            "SELECT c.CategoryID, c.CategoryName " & _  
                "FROM NorthwindEntities.Categories AS c"  
  
        Using conn As EntityConnection = _  
            New EntityConnection("name=NorthwindEntities")  
  
            Try  
                conn.Open()  
                Using query As EntityCommand = _  
                New EntityCommand(queryString, conn)  
                    Using rdr As DbDataReader = _  
                        query.ExecuteReader(CommandBehavior.SequentialAccess)  
                        While rdr.Read()  
                            Console.WriteLine(vbTab & "{0}" & vbTab & "{1}", _  
                                              rdr(0), rdr(1))  
                        End While  
                    End Using  
                End Using  
            Catch ex As Exception  
                Console.WriteLine(ex.Message)  
            End Try  
        End Using   
    End Sub  
End Class  
```  
  
 在 C# 中：  
  
```  
using System;  
using System.Data;  
using System.Data.Common;  
using System.Data.EntityClient;  
using NorthwindModel;  
  
class EntityClientSample  
{  
    public static void ExecuteQuery()  
    {  
        string queryString =  
            @"SELECT c.CategoryID, c.CategoryName   
                FROM NorthwindEntities.Categories AS c";  
  
        using (EntityConnection conn =  
            new EntityConnection("name=NorthwindEntities"))  
        {  
            try  
            {  
                conn.Open();  
                using (EntityCommand query = new EntityCommand(queryString, conn))  
                {  
                    using (DbDataReader rdr =   
                        query.ExecuteReader(CommandBehavior.SequentialAccess))  
                    {  
                        while (rdr.Read())  
                        {  
                            Console.WriteLine("\t{0}\t{1}", rdr[0], rdr[1]);  
                        }  
                    }  
                }  
            }  
            catch (Exception ex)  
            {  
                Console.WriteLine(ex.Message);  
            }  
        }  
    }  
}  
```  
  
 [[Top]](#_TOP)  
  
<a name="_LINQ2SQL"></a>   
## <a name="linq-to-sql"></a>LINQ to SQL  
 此示例中的代码使用 LINQ 查询以 Categories 对象的形式返回数据，这些对象将作为仅包含 CategoryID 和 CategoryName 属性的匿名类型提取。 此示例基于 Northwind 数据上下文。 有关详细信息，请参阅[入门](../../../../docs/framework/data/adonet/sql/linq/getting-started.md)。  
  
```  
Option Explicit On  
Option Strict On  
  
Imports System  
Imports System.Collections.Generic  
Imports System.Linq  
Imports System.Text  
Imports Northwind  
  
Class LinqSqlSample  
    Public Shared Sub ExecuteQuery()  
        Using db As NorthwindDataContext = New NorthwindDataContext()  
            Try  
                Dim query = From category In db.Categories _  
                                Select New With _  
                                { _  
                                    .categoryID = category.CategoryID, _  
                                    .categoryName = category.CategoryName _  
                                }  
  
                For Each categoryInfo In query  
                    Console.WriteLine(vbTab & "{0}" & vbTab & "{1}", _  
                            categoryInfo.categoryID, categoryInfo.categoryName)  
                Next  
            Catch ex As Exception  
                Console.WriteLine(ex.Message)  
            End Try  
            End Using   
    End Sub  
End Class  
```  
  
 在 C# 中：  
  
```  
using System;  
using System.Collections.Generic;  
using System.Linq;  
using System.Text;  
using Northwind;  
  
    class LinqSqlSample  
    {  
        public static void ExecuteQuery()  
        {  
            using (NorthwindDataContext db = new NorthwindDataContext())  
            {  
                try  
                {  
                    var query = from category in db.Categories  
                                select new  
                                {  
                                    categoryID = category.CategoryID,  
                                    categoryName = category.CategoryName  
                                };  
  
                    foreach (var categoryInfo in query)  
                    {  
                        Console.WriteLine("vbTab {0} vbTab {1}",  
                            categoryInfo.categoryID, categoryInfo.categoryName);  
                    }  
                }  
                catch (Exception ex)  
                {  
                    Console.WriteLine(ex.Message);  
                }  
            }  
        }  
    }  
```  
  
 [[Top]](#_TOP)  
  
## <a name="see-also"></a>另请参阅  
 [ADO.NET 概述](../../../../docs/framework/data/adonet/ado-net-overview.md)   
 [检索和修改 ADO.NET 中的数据](../../../../docs/framework/data/adonet/retrieving-and-modifying-data.md)   
 [创建数据应用程序](../Topic/Creating%20Data%20Applications.md)   
 [查询实体数据模型 （实体框架任务）](http://msdn.microsoft.com/zh-cn/187f1caa-e4d3-4e31-bd99-5d5c2b329c77)   
 [如何︰ 执行返回匿名类型对象的查询](http://msdn.microsoft.com/zh-cn/3b264025-e911-4d73-90ce-992d2b9d189d)   
 [ADO.NET 托管提供程序和数据集开发人员中心](http://go.microsoft.com/fwlink/?LinkId=217917)