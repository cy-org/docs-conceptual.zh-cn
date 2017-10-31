---
title: "ADO.NET 中的数据跟踪 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-ado"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: a6a752a5-d2a9-4335-a382-b58690ccb79f
caps.latest.revision: 9
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 9
---
# ADO.NET 中的数据跟踪
ADO.NET 具有内置数据跟踪功能，用于 [!INCLUDE[ssNoVersion](../../../../includes/ssnoversion-md.md)]、Oracle、OLE DB 和 ODBC 的 .NET 数据提供程序以及 ADO.NET <xref:System.Data.DataSet> 和 [!INCLUDE[ssNoVersion](../../../../includes/ssnoversion-md.md)] 网络协议均支持此功能。  
  
 跟踪数据访问 API 调用可以帮助诊断以下问题：  
  
-   客户端程序和数据库之间的架构不匹配。  
  
-   数据库不可用或网络库问题。  
  
-   不正确的 SQL，无论是硬编码还是由应用程序生成。  
  
-   不正确的编程逻辑。  
  
-   多个 ADO.NET 组件之间或 ADO.NET 与您自己的组件之间的交互引发的问题。  
  
 为了支持不同的跟踪技术，跟踪是可扩展的，这样，开发人员可以在任何应用程序堆栈级别上跟踪问题。  尽管跟踪不属于纯 ADO.NET 功能，但是，Microsoft 提供程序利用通用的跟踪和规范 API。  
  
 有关在 ADO.NET 中设置和配置托管跟踪的详细信息，请参阅[跟踪数据访问](http://msdn.microsoft.com/library/hh880086.aspx)（可能为英文网页）。  
  
## 访问扩展事件日志中的诊断信息  
 在用于 [!INCLUDE[ssNoVersion](../../../../includes/ssnoversion-md.md)] 的 [!INCLUDE[dnprdnshort](../../../../includes/dnprdnshort-md.md)] 数据提供程序中，数据访问跟踪（[数据访问跟踪](http://msdn.microsoft.com/library/hh880086.aspx)（可能为英文网页））已更新，从而可以越来越容易地将客户端事件与服务器连接环形缓冲区中的诊断信息（如连接失败）以及扩展事件日志中的应用程序性能信息关联起来。  有关读取扩展事件日志的信息，请参阅[查看事件会话数据](http://msdn.microsoft.com/library/hh710068\(SQL.110\).aspx)（可能为英文网页）。  
  
 对于连接操作，ADO.NET 将发送一个客户端连接 ID。  如果连接失败，则可以访问连接环形缓冲区（[使用连接环形缓冲区解决 SQL Server 2008 中的连接问题](http://go.microsoft.com/fwlink/?LinkId=207752)（可能为英文网页）），并查找 `ClientConnectionID` 字段获取有关连接故障的诊断信息。  如果出现错误，则将客户端连接 ID 记录在环形缓冲区中。  （如果在发送预登录数据包之前连接失败，将不会生成客户端连接 ID。） 客户端连接 ID 为 16 字节的 GUID。  如果 `client_connection_id` 操作已添加到扩展事件会话中的事件，则还可以在扩展事件目标输出中找到查找客户端连接 ID。  如果需要进一步的客户端驱动程序诊断帮助，可以启用数据访问跟踪并重新运行连接命令，然后观察 `ClientConnectionID` 字段。  
  
 还可以通过使用 `SqlConnection.ClientConnectionID` 属性以编程方式获取客户端连接 ID。  
  
 `ClientConnectionID` 可用于成功建立连接的 <xref:System.Data.SqlClient.SqlConnection> 对象。  如果连接尝试失败，则 `ClientConnectionID` 可通过 `SqlException.ToString` 提供。  
  
 ADO.NET 还会发送一个特定于线程的活动 ID。  如果会话最初启动时启用了 TRACK\_CAUSAILITY 选项，则在扩展事件会话中捕获该活动 ID。  有关活动连接的性能问题，可以从客户端的数据访问跟踪获取活动 ID（`ActivityID` 字段），然后查找扩展事件输出中的活动 ID。  扩展事件中的活动 ID 为追加了 4 字节序列号的 16 字节的 GUID（与客户端连接 ID 的 GUID 不同）。  序列号表示请求在线程中的顺序，并指示线程的批处理和 RPC 语句的相对顺序。  启用数据访问跟踪以及数据访问跟踪配置字中的第 18 位处于打开状态时，当前可以针对 SQL 批处理语句和 RPC 请求选择发送 `ActivityID`。  
  
 以下是使用 [!INCLUDE[tsql](../../../../includes/tsql-md.md)] 启动扩展事件会话的一个示例，这些会话将存储在环形缓冲区中并将记录在执行 RPC 和批处理操作时从客户端发送的活动 ID。  
  
```  
create event session MySession on server   
add event connectivity_ring_buffer_recorded,   
add event sql_statement_starting (action (client_connection_id)),   
add event sql_statement_completed (action (client_connection_id)),   
add event rpc_starting (action (client_connection_id)),   
add event rpc_completed (action (client_connection_id))  
add target ring_buffer with (track_causality=on)  
```  
  
## 请参阅  
 [.NET Framework 中的网络跟踪](../../../../docs/framework/network-programming/network-tracing.md)   
 [Tracing and Instrumenting Applications](../../../../docs/framework/debug-trace-profile/tracing-and-instrumenting-applications.md)   
 [ADO.NET 托管提供程序和数据集开发人员中心](http://go.microsoft.com/fwlink/?LinkId=217917)