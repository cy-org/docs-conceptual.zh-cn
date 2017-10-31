---
title: "SQL Server 中的数据库镜像 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-ado"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 89befaff-bb46-4290-8382-e67cdb0e3de9
caps.latest.revision: 6
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 6
---
# SQL Server 中的数据库镜像
通过 SQL Server 中的数据库镜像，可以在备用服务器上保留 SQL Server 数据库的副本（即镜像）。  镜像可以确保数据始终存在两个独立的副本，从而提供高可用性和完整的数据冗余。  用于 SQL Server 的 .NET 数据提供程序提供了数据库镜像的隐式支持，这样，在为 SQL Server 数据库配置了镜像之后，开发人员无需采取任何措施或编写任何代码。  此外，<xref:System.Data.SqlClient.SqlConnection> 对象支持显式连接模式，该模式允许在 <xref:System.Data.SqlClient.SqlConnection.ConnectionString%2A> 中提供故障转移合作伙伴服务器的名称。  
  
 对于连接目标为某个配置为镜像的数据库的 <xref:System.Data.SqlClient.SqlConnection> 对象将发生以下简化的事件序列：  
  
1.  客户端应用程序成功连接到主体数据库上，服务器发送回合作伙伴服务器的名称，然后将该名称缓存在客户端上。  
  
2.  如果包含主体数据库的服务器失败或连接中断，连接和事务状态将丢失。  客户端应用程序尝试重新建立与主体数据库的连接，但是失败。  
  
3.  然后，客户端应用程序透明地尝试与合作伙伴服务器上的镜像数据库建立连接。  如果成功，连接将重定向到镜像数据库，而该镜像数据库将成为新的主体数据库。  
  
## 在连接字符串中指定故障转移合作伙伴  
 如果在连接字符串中提供故障转移合作伙伴服务器的名称，当客户端应用程序初次连接时，主体数据库不可用，客户端将直接尝试与故障转移合作伙伴建立连接。  
  
```  
";Failover Partner=PartnerServerName"  
```  
  
 如果省略故障转移合作伙伴服务器的名称且客户端应用程序初次连接时主体数据库不可用，则引发 <xref:System.Data.SqlClient.SqlException>。  
  
 成功打开 <xref:System.Data.SqlClient.SqlConnection> 后，故障转移合作伙伴名称由服务器返回，取代连接字符串中提供的任何值。  
  
> [!NOTE]
>  您必须在连接字符串中显式指定数据库镜像方案的初始编录或数据库名称。  如果客户端收到没有显式指定初始编录或数据库的连接的故障转移信息，故障转移信息不会缓存，应用程序也不会在主体服务器出现故障时尝试进行故障转移。  如果连接字符串包含故障转移合作伙伴的值，但是没有包含初始编录或数据库的值，则会引发 `InvalidArgumentException`。  
  
## 检索当前服务器名称  
 如果进行故障转移，可以使用 <xref:System.Data.SqlClient.SqlConnection> 对象的 <xref:System.Data.SqlClient.SqlConnection.DataSource%2A> 属性来检索当前连接实际连接到的服务器的名称。  以下代码段检索活动服务器的名称，假定连接变量引用打开的 <xref:System.Data.SqlClient.SqlConnection>。  
  
 在发生故障转移事件并且连接切换到镜像服务器时，**DataSource** 属性将更新，以反映镜像名称。  
  
```vb  
Dim activeServer As String = connection.DataSource  
```  
  
```csharp  
string activeServer = connection.DataSource;  
```  
  
## SqlClient 镜像行为  
 客户端总是尝试连接当前的主体服务器。  如果失败，将尝试连接故障转移合作伙伴。  如果镜像数据库已切换为合作伙伴服务器上的主体角色，连接将成功，新的主体\/镜像映射将发送到客户端，并在调用 <xref:System.AppDomain> 的生存期期间进行缓存。  映射不会存储在永久存储中，也无法供其他 **AppDomain** 或进程中的后续连接使用。  但是，可以供相同 **AppDomain** 中的后续连接使用。  注意，在相同或不同的计算机上运行的其他 **AppDomain** 或进程总是拥有自己的连接池，这些连接不会重置。  在这种情况下，如果主数据库关闭，每个进程或 **AppDomain** 将失败，将自动清除池。  
  
> [!NOTE]
>  每个数据库都要在服务器上配置镜像支持。  如果对不在主体\/镜像数据库集中的其他数据库执行数据操作，那么无论使用多部分名称还是更改当前数据库，在失败时都不会传播对这些数据库的更改。  修改未镜像的数据库中的数据时，不会生成错误。  开发人员必须评估此类操作可能产生的影响。  
  
## 数据库镜像资源  
 有关配置、部署和管理镜像的概念性文档及信息，请参见“SQL Server 联机丛书”中的下列资源。  
  
|资源|描述|  
|--------|--------|  
|SQL Server 联机丛书中的[数据库镜像](http://msdn.microsoft.com/library/bb934127.aspx)（可能为英文网页）|说明如何在 SQL Server 中设置和配置镜像。|  
  
## 请参阅  
 [ADO.NET 托管提供程序和数据集开发人员中心](http://go.microsoft.com/fwlink/?LinkId=217917)