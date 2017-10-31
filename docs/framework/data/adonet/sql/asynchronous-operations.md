---
title: "异步操作 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-ado"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: e7d32c3c-bf78-4bfc-a357-c9e82e4a4b3c
caps.latest.revision: 5
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 5
---
# 异步操作
某些数据库操作（例如命令执行）可能要花费很长时间才能完成。  在此类情况下，单线程应用程序必须阻塞其他操作，并且等待该命令完成，然后才可以继续执行它们自己的操作。  比较而言，如果能够将长时间运行的操作分配给某个后台线程，就可以允许前台线程在整个操作期间保持活动状态。  例如，在 Windows 应用程序中，通过将长时间运行的操作委托给后台线程，可允许用户界面线程在操作执行时保持响应状态。  
  
 .NET Framework 提供若干标准异步设计模式，开发人员可以通过这些模式充分利用后台线程并释放用户界面线程或高优先级的线程以完成其他操作。  ADO.NET 在其 <xref:System.Data.SqlClient.SqlCommand> 类中支持相同的设计模式。  具体而言，<xref:System.Data.SqlClient.SqlCommand.BeginExecuteNonQuery%2A>、<xref:System.Data.SqlClient.SqlCommand.BeginExecuteReader%2A> 和 <xref:System.Data.SqlClient.SqlCommand.BeginExecuteXmlReader%2A> 方法（与 <xref:System.Data.SqlClient.SqlCommand.EndExecuteNonQuery%2A>、<xref:System.Data.SqlClient.SqlCommand.EndExecuteReader%2A> 和 <xref:System.Data.SqlClient.SqlCommand.EndExecuteXmlReader%2A> 方法搭配）提供异步支持。  
  
> [!NOTE]
>  异步编程是 .NET Framework 的核心功能，并且 ADO.NET 充分利用了标准设计模式。  有关可供开发人员使用的不同异步技术的更多信息，请参见[Calling Synchronous Methods Asynchronously](../../../../../docs/standard/asynchronous-programming-patterns/calling-synchronous-methods-asynchronously.md)。  
  
 尽管将异步技术与 ADO.NET 功能一起使用没有什么新增的需特别注意的事项，但与 .NET Framework 的其他领域相比，很可能更多的开发人员将在 ADO.NET 中使用异步功能。  了解创建多线程应用程序的优缺点十分重要。  本节之后的那些示例指出了若干重要问题，开发人员在开发纳入了多线程功能的应用程序时将需要考虑这些问题。  
  
## 本节内容  
 [使用回调的 Windows 应用程序](../../../../../docs/framework/data/adonet/sql/windows-applications-using-callbacks.md)  
 提供一个示例，演示如何安全地执行异步命令，并且通过单独线程正确处理与某一窗体及其内容的交互。  
  
 [使用等待句柄的 ASP.NET 应用程序](../../../../../docs/framework/data/adonet/sql/aspnet-apps-using-wait-handles.md)  
 提供一个示例，演示如何从 ASP.NET 页执行多个并行命令，并且使用等待处理管理在所有命令都完成时的操作。  
  
 [在控制台应用程序中轮询](../../../../../docs/framework/data/adonet/sql/polling-in-console-applications.md)  
 提供一个示例，演示如何在控制台应用程序中使用轮询来等待异步命令执行的完成。  在类库或没有用户界面的其他应用程序中此技术同样有效。  
  
## 请参阅  
 [SQL Server 和 ADO.NET](../../../../../docs/framework/data/adonet/sql/index.md)   
 [Calling Synchronous Methods Asynchronously](../../../../../docs/standard/asynchronous-programming-patterns/calling-synchronous-methods-asynchronously.md)   
 [ADO.NET 托管提供程序和数据集开发人员中心](http://go.microsoft.com/fwlink/?LinkId=217917)