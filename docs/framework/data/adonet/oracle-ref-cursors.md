---
title: "Oracle REF CURSOR | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-ado"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: c6b25b8b-0bdd-41b2-9c7c-661f070c2247
caps.latest.revision: 4
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 4
---
# Oracle REF CURSOR
Oracle .NET Framework 数据提供程序支持 Oracle **REF CURSOR** 数据类型。  在通过数据提供程序使用 Oracle REF CURSOR 时，应考虑下列行为。  
  
> [!NOTE]
>  有些行为与 Microsoft Oracle OLE DB 提供程序 \(MSDAORA\) 的行为不同。  
  
-   因为性能的原因，除非您显式指定，否则，Oracle 数据提供程序不会自动绑定 **REF CURSOR** 数据类型，因为 MSDAORA 会这样做。  
  
-   数据提供程序不支持任何 ODBC 转义序列，包括用于指定 REF CURSOR 参数的 {resultset} 转义。  
  
-   要执行返回 REF CURSOR 的存储过程，必须在 <xref:System.Data.OracleClient.OracleParameterCollection> 中定义参数，包括 **Cursor** 的 <xref:System.Data.OracleClient.OracleType> 以及 **Output** 的 <xref:System.Data.OracleClient.OracleParameter.Direction%2A>。  数据提供程序只支持作为输出参数绑定 REF CURSOR。  提供程序不支持 REF CURSOR 作为输入参数。  
  
-   不支持从参数值获取 <xref:System.Data.OracleClient.OracleDataReader>。  在执行命令后，值属于 <xref:System.DBNull> 类型。  
  
-   适用于 REF CURSOR 的唯一 **CommandBehavior** 枚举值（例如在调用 <xref:System.Data.OracleClient.OracleCommand.ExecuteReader%2A> 时）是 **CloseConnection**；所有其他枚举值均将被忽略。  
  
-   REF CURSOR 在 **OracleDataReader** 中的顺序取决于参数在 **OracleParameterCollection** 中的顺序。  <xref:System.Data.OracleClient.OracleParameter.ParameterName%2A> 属性被忽略。  
  
-   不支持 PL\/SQL **TABLE** 数据类型。  但是，REF CURSOR 的效率更高。  如果必须使用 **TABLE** 数据类型，请使用 OLE DB .NET 数据提供程序和 MSDAORA。  
  
## 本节内容  
 [REF CURSOR 示例](../../../../docs/framework/data/adonet/ref-cursor-examples.md)  
 包含三个示例，演示如何使用 REF CURSOR。  
  
 [OracleDataReader 中的 REF CURSOR 参数](../../../../docs/framework/data/adonet/ref-cursor-parameters-in-an-oracledatareader.md)  
 演示如何执行一个 PL\/SQL 存储过程，返回 REF CURSOR 参数，并将值作为 **OracleDataReader** 读取。  
  
 [使用 OracleDataReader 从多个 REF CURSOR 检索数据](../../../../docs/framework/data/adonet/retrieving-data-from-multiple-ref-cursors.md)  
 演示如何执行一个 PL\/SQL 存储过程，返回两个 REF CURSOR 参数，并使用 **OracleDataReader** 读取值。  
  
 [使用一个或多个 REF CURSOR 填充数据集](../../../../docs/framework/data/adonet/filling-a-dataset-using-one-or-more-ref-cursors.md)  
 演示如何执行一个 PL\/SQL 存储过程，返回两个 REF CURSOR 参数，并使用返回的行填充 <xref:System.Data.DataSet>。  
  
## 请参阅  
 [Oracle 和 ADO.NET](../../../../docs/framework/data/adonet/oracle-and-adonet.md)   
 [ADO.NET 托管提供程序和数据集开发人员中心](http://go.microsoft.com/fwlink/?LinkId=217917)