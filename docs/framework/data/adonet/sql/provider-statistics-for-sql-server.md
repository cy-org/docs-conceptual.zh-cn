---
title: "SQL Server 提供程序统计信息 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-ado"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 429c9d09-92ac-46ec-829a-fbff0a9575a2
caps.latest.revision: 6
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 6
---
# SQL Server 提供程序统计信息
从 .NET Framework 2.0 版开始，适用于 SQL Server 的 .NET Framework 数据提供程序支持运行时统计信息。  必须在创建了有效的连接对象后将 <xref:System.Data.SqlClient.SqlConnection> 对象的 <xref:System.Data.SqlClient.SqlConnection.StatisticsEnabled%2A> 属性设置为 `True`，以启用统计信息。  启用了统计信息之后，可以通过 <xref:System.Data.SqlClient.SqlConnection> 对象的 <xref:System.Data.SqlClient.SqlConnection.RetrieveStatistics%2A> 方法检索 <xref:System.Collections.IDictionary> 引用，以将统计信息作为“实时快照”查看。  通过列表作为一组名称\/值对字典条目进行枚举。  这些名称\/值对不排序。  可以随时调用 <xref:System.Data.SqlClient.SqlConnection> 对象的 <xref:System.Data.SqlClient.SqlConnection.ResetStatistics%2A> 方法，以重置计数器。  如果尚未启用统计信息收集功能，则不会生成异常。  此外，如果调用 <xref:System.Data.SqlClient.SqlConnection.RetrieveStatistics%2A> 之前没有先调用 <xref:System.Data.SqlClient.SqlConnection.StatisticsEnabled%2A>，检索到的值是每个条目的初始值。  如果启用了统计信息，运行应用程序一段时间，然后禁用统计信息，检索到的值将反映在禁用统计信息之前收集的值。  所有统计信息值按照连接进行收集。  
  
## 可用的统计信息值  
 当前，Microsoft SQL Server 提供程序中共有 18 个不同的可用项。  可用的项数可以通过 <xref:System.Data.SqlClient.SqlConnection.RetrieveStatistics%2A> 返回的 <xref:System.Collections.IDictionary> 接口引用的 **Count** 属性进行访问。  提供程序统计信息的所有计数器均使用公共语言运行库 <xref:System.Int64> 类型（C\# 和 Visual Basic 中为 **long**），宽度为 64 位。  **int64** 数据类型的最大值由 **int64.MaxValue** 字段定义，最大值为 \(\(2^63\)\-1\)\)。  计数器的值达到此最大值时，应不再将这些值作为准确的值。  这意味着 **int64.MaxValue**\-1 \(\(2^63\)\-2\) 实际上是任何统计信息的最大有效值。  
  
> [!NOTE]
>  字典用于返回提供程序统计信息，因为以后可能会更改返回的统计信息的数目、名称和顺序。  应用程序不应依靠字典中找到的特定值，而应检查该值是否存在并相应进行分支。  
  
 下表说明当前可用的统计信息值。  注意，在 Microsoft .NET Framework 的地区版本中，各个值的键名未本地化。  
  
|键名|描述|  
|--------|--------|  
|`BuffersReceived`|返回在应用程序使用提供程序启动并启用了统计信息之后，提供程序从 SQL Server 接收的表格格式数据流 \(TDS\) 数据包数。|  
|`BuffersSent`|返回在启用了统计信息之后，由提供程序发送到 SQL Server 的 TDS 数据包数。  大命令可能需要多个缓冲区。  例如，如果某个大命令发送到服务器，并且需要六个数据包，`ServerRoundtrips` 将以 1 递增，`BuffersSent` 将以 6 递增。|  
|`BytesReceived`|返回在应用程序使用提供程序启动并启用了统计信息之后，提供程序从 SQL Server 接收的 TDS 数据包中的数据字节数。|  
|`BytesSent`|返回在应用程序使用提供程序启动并启用了统计信息之后，在 TDS 数据包中发送到 SQL Server 的数据字节数。|  
|`ConnectionTime`|连接在统计信息启用之后已打开的时间（单位为毫秒；如果在打开连接之前就启用了统计信息，则为总连接时间）。|  
|`CursorOpens`|返回在应用程序使用提供程序启动并启用了统计信息之后，通过连接打开游标的次数。<br /><br /> 注意，SELECT 语句返回的只读\/只进结果不属于游标，所以不影响此计数器。|  
|`ExecutionTime`|返回在启用统计信息之后提供程序用于处理的累计时间（以毫秒为单位），包括等待服务器答复所用的时间以及执行提供程序本身的代码所用的时间。<br /><br /> 包含计时代码的类如下：<br /><br /> SqlConnection<br /><br /> SqlCommand<br /><br /> SqlDataReader<br /><br /> SqlDataAdapter<br /><br /> SqlTransaction<br /><br /> SqlCommandBuilder<br /><br /> 为了保持对性能要求很高的成员尽可能小，下列成员不计时：<br /><br /> SqlDataReader<br /><br /> this\[\] 运算符（所有重载）<br /><br /> GetBoolean<br /><br /> GetChar<br /><br /> GetDateTime<br /><br /> GetDecimal<br /><br /> GetDouble<br /><br /> GetFloat<br /><br /> GetGuid<br /><br /> GetInt16<br /><br /> GetInt32<br /><br /> GetInt64<br /><br /> GetName<br /><br /> GetOrdinal<br /><br /> GetSqlBinary<br /><br /> GetSqlBoolean<br /><br /> GetSqlByte<br /><br /> GetSqlDateTime<br /><br /> GetSqlDecimal<br /><br /> GetSqlDouble<br /><br /> GetSqlGuid<br /><br /> GetSqlInt16<br /><br /> GetSqlInt32<br /><br /> GetSqlInt64<br /><br /> GetSqlMoney<br /><br /> GetSqlSingle<br /><br /> GetSqlString<br /><br /> GetString<br /><br /> IsDBNull|  
|`IduCount`|返回在应用程序使用提供程序启动并启用了统计信息之后，通过连接执行的 INSERT、DELETE 和 UPDATE 语句的总数。|  
|`IduRows`|返回在应用程序使用提供程序启动并启用了统计信息之后，受到通过连接执行的 INSERT、DELETE 和 UPDATE 语句影响的行的总数。|  
|`NetworkServerTime`|返回在应用程序使用提供程序启动并启用了统计信息之后，提供程序等待服务器答复所用的累计时间（以毫秒为单位）。|  
|`PreparedExecs`|返回在应用程序使用提供程序启动并启用了统计信息之后，通过连接执行的已准备命令数。|  
|`Prepares`|返回在应用程序使用提供程序启动并启用了统计信息之后，通过连接准备的语句数。|  
|`SelectCount`|返回在应用程序使用提供程序启动并启用了统计信息之后，通过连接执行的 SELECT 语句数。  其中包括用于从游标检索行的 FETCH 语句，SELECT 语句的计数在到达 <xref:System.Data.SqlClient.SqlDataReader> 的结尾时更新。|  
|`SelectRows`|返回在应用程序使用提供程序启动并启用了统计信息之后所选的行数。  此计数器反映 SQL 语句生成的所有行，即使是调用方没有真正使用的行。  例如，如果在读取整个结果集之前关闭数据读取器，不会影响该计数。  其中包括通过 FETCH 语句从游标检索的行。|  
|`ServerRoundtrips`|返回在应用程序使用提供程序启动并启用了统计信息之后，连接向服务器发送命令并收到回复的次数。|  
|`SumResultSets`|返回在应用程序使用提供程序启动并启用了统计信息之后使用过的结果集数。  例如，此值可能包括返回到客户端的任何结果集。  对于光标，每个获取或块获取操作都属于独立的结果集。|  
|`Transactions`|返回在应用程序使用提供程序启动并启用了统计信息之后启动的用户事务数（包括回滚）。  如果连接在启用自动提交的情况下运行，则每个命令都属于一个事务。<br /><br /> 只要执行了 BEGIN TRAN 语句，无论事务是提交还是以后回滚，此计数器都会使事务计数递增。|  
|`UnpreparedExecs`|返回在应用程序使用提供程序启动并启用了统计信息之后，通过连接执行的非准备语句数。|  
  
### 检索值  
 以下控制台应用程序显示如何在连接上启用统计信息，如何分别检索四个统计信息值，以及如何将统计信息输出到控制台窗口。  
  
> [!NOTE]
>  下面的示例使用随 [!INCLUDE[ssNoVersion](../../../../../includes/ssnoversion-md.md)] 提供的 **AdventureWorks** 示例数据库。  示例代码中提供的连接字符串假定数据库在本地计算机上已安装并且可用。  根据环境的需要修改连接字符串。  
  
```vb  
Option Strict On  
  
Imports System  
Imports System.Collections  
Imports System.Data  
Imports System.Data.SqlClient  
  
Module Module1  
  
  Sub Main()  
    Dim connectionString As String = GetConnectionString()  
  
    Using awConnection As New SqlConnection(connectionString)  
      ' StatisticsEnabled is False by default.  
      ' It must be set to True to start the   
      ' statistic collection process.  
      awConnection.StatisticsEnabled = True  
  
      Dim productSQL As String = "SELECT * FROM Production.Product"  
      Dim productAdapter As _  
          New SqlDataAdapter(productSQL, awConnection)  
  
      Dim awDataSet As New DataSet()  
  
      awConnection.Open()  
  
      productAdapter.Fill(awDataSet, "ProductTable")  
  
      ' Retrieve the current statistics as  
      ' a collection of values at this point  
      ' and time.  
      Dim currentStatistics As IDictionary = _  
          awConnection.RetrieveStatistics()  
  
      Console.WriteLine("Total Counters: " & _  
          currentStatistics.Count.ToString())  
      Console.WriteLine()  
  
      ' Retrieve a few individual values  
      ' related to the previous command.  
      Dim bytesReceived As Long = _  
          CLng(currentStatistics.Item("BytesReceived"))  
      Dim bytesSent As Long = _  
          CLng(currentStatistics.Item("BytesSent"))  
      Dim selectCount As Long = _  
          CLng(currentStatistics.Item("SelectCount"))  
      Dim selectRows As Long = _  
          CLng(currentStatistics.Item("SelectRows"))  
  
      Console.WriteLine("BytesReceived: " & bytesReceived.ToString())  
      Console.WriteLine("BytesSent: " & bytesSent.ToString())  
      Console.WriteLine("SelectCount: " & selectCount.ToString())  
      Console.WriteLine("SelectRows: " & selectRows.ToString())  
  
      Console.WriteLine()  
      Console.WriteLine("Press any key to continue")  
      Console.ReadLine()  
    End Using  
  
  End Sub  
  
  Function GetConnectionString() As String  
    ' To avoid storing the connection string in your code,  
    ' you can retrive it from a configuration file.  
    Return "Data Source=localhost;Integrated Security=SSPI;" & _  
      "Initial Catalog=AdventureWorks"  
  End Function  
End Module  
```  
  
 \[C\#\]  
  
```  
using System;  
using System.Collections;  
using System.Collections.Generic;  
using System.Data;  
using System.Data.SqlClient;  
  
namespace CS_Stats_Console_GetValue  
{  
  class Program  
  {  
    static void Main(string[] args)  
    {  
      string connectionString = GetConnectionString();  
  
      using (SqlConnection awConnection =   
        new SqlConnection(connectionString))  
      {  
        // StatisticsEnabled is False by default.  
        // It must be set to True to start the   
        // statistic collection process.  
        awConnection.StatisticsEnabled = true;  
  
        string productSQL = "SELECT * FROM Production.Product";  
        SqlDataAdapter productAdapter =   
          new SqlDataAdapter(productSQL, awConnection);  
  
        DataSet awDataSet = new DataSet();  
  
        awConnection.Open();  
  
        productAdapter.Fill(awDataSet, "ProductTable");  
        // Retrieve the current statistics as  
        // a collection of values at this point  
        // and time.  
        IDictionary currentStatistics =  
          awConnection.RetrieveStatistics();  
  
        Console.WriteLine("Total Counters: " +  
          currentStatistics.Count.ToString());  
        Console.WriteLine();  
  
        // Retrieve a few individual values  
        // related to the previous command.  
        long bytesReceived =  
            (long) currentStatistics["BytesReceived"];  
        long bytesSent =  
            (long) currentStatistics["BytesSent"];  
        long selectCount =  
            (long) currentStatistics["SelectCount"];  
        long selectRows =  
            (long) currentStatistics["SelectRows"];  
  
        Console.WriteLine("BytesReceived: " +  
            bytesReceived.ToString());  
        Console.WriteLine("BytesSent: " +  
            bytesSent.ToString());  
        Console.WriteLine("SelectCount: " +  
            selectCount.ToString());  
        Console.WriteLine("SelectRows: " +  
            selectRows.ToString());  
  
        Console.WriteLine();  
        Console.WriteLine("Press any key to continue");  
        Console.ReadLine();  
      }  
  
    }  
    private static string GetConnectionString()  
    {  
      // To avoid storing the connection string in your code,  
      // you can retrive it from a configuration file.  
      return "Data Source=localhost;Integrated Security=SSPI;" +   
        "Initial Catalog=AdventureWorks";  
    }  
  }  
}  
```  
  
### 检索所有值  
 以下控制台应用程序显示如何在连接上启用统计信息，如何使用枚举器检索所有可用统计信息值，以及如何将统计信息输出到控制台窗口。  
  
> [!NOTE]
>  下面的示例使用随 [!INCLUDE[ssNoVersion](../../../../../includes/ssnoversion-md.md)] 提供的 **AdventureWorks** 示例数据库。  示例代码中提供的连接字符串假定数据库在本地计算机上已安装并且可用。  根据环境的需要修改连接字符串。  
  
```vb  
Option Strict On  
  
Imports System  
Imports System.Collections  
Imports System.Data  
Imports System.Data.SqlClient  
  
Module Module1  
  Sub Main()  
    Dim connectionString As String = GetConnectionString()  
  
    Using awConnection As New SqlConnection(connectionString)  
      ' StatisticsEnabled is False by default.  
      ' It must be set to True to start the   
      ' statistic collection process.  
      awConnection.StatisticsEnabled = True  
  
      Dim productSQL As String = "SELECT * FROM Production.Product"  
      Dim productAdapter As _  
          New SqlDataAdapter(productSQL, awConnection)  
  
      Dim awDataSet As New DataSet()  
  
      awConnection.Open()  
  
      productAdapter.Fill(awDataSet, "ProductTable")  
  
      ' Retrieve the current statistics as  
      ' a collection of values at this point  
      ' and time.  
      Dim currentStatistics As IDictionary = _  
          awConnection.RetrieveStatistics()  
  
      Console.WriteLine("Total Counters: " & _  
          currentStatistics.Count.ToString())  
      Console.WriteLine()  
  
      Console.WriteLine("Key Name and Value")  
  
      ' Note the entries are unsorted.  
      For Each entry As DictionaryEntry In currentStatistics  
        Console.WriteLine(entry.Key.ToString() & _  
            ": " & entry.Value.ToString())  
      Next  
  
      Console.WriteLine()  
      Console.WriteLine("Press any key to continue")  
      Console.ReadLine()  
    End Using  
  
  End Sub  
  
  Function GetConnectionString() As String  
    ' To avoid storing the connection string in your code,  
    ' you can retrive it from a configuration file.  
    Return "Data Source=localhost;Integrated Security=SSPI;" & _  
      "Initial Catalog=AdventureWorks"  
  End Function  
End Module  
```  
  
```csharp  
using System;  
using System.Collections;  
using System.Collections.Generic;  
using System.Text;  
using System.Data;  
using System.Data.SqlClient;  
  
namespace CS_Stats_Console_GetAll  
{  
  class Program  
  {  
    static void Main(string[] args)  
    {  
      string connectionString = GetConnectionString();  
  
      using (SqlConnection awConnection =   
        new SqlConnection(connectionString))  
      {  
        // StatisticsEnabled is False by default.  
        // It must be set to True to start the   
        // statistic collection process.  
        awConnection.StatisticsEnabled = true;  
  
        string productSQL = "SELECT * FROM Production.Product";  
        SqlDataAdapter productAdapter =  
            new SqlDataAdapter(productSQL, awConnection);  
  
        DataSet awDataSet = new DataSet();  
  
        awConnection.Open();  
  
        productAdapter.Fill(awDataSet, "ProductTable");  
  
        // Retrieve the current statistics as  
        // a collection of values at this point  
        // and time.  
        IDictionary currentStatistics =  
            awConnection.RetrieveStatistics();  
  
        Console.WriteLine("Total Counters: " +  
            currentStatistics.Count.ToString());  
        Console.WriteLine();  
  
        Console.WriteLine("Key Name and Value");  
  
        // Note the entries are unsorted.  
        foreach (DictionaryEntry entry in currentStatistics)  
        {  
          Console.WriteLine(entry.Key.ToString() +  
              ": " + entry.Value.ToString());  
        }  
  
        Console.WriteLine();  
        Console.WriteLine("Press any key to continue");  
        Console.ReadLine();  
      }  
  
    }  
    private static string GetConnectionString()  
    {  
      // To avoid storing the connection string in your code,  
      // you can retrive it from a configuration file.  
      return "Data Source=localhost;Integrated Security=SSPI;" +   
        "Initial Catalog=AdventureWorks";  
    }  
  }  
}  
```  
  
## 请参阅  
 [SQL Server 和 ADO.NET](../../../../../docs/framework/data/adonet/sql/index.md)   
 [ADO.NET 托管提供程序和数据集开发人员中心](http://go.microsoft.com/fwlink/?LinkId=217917)