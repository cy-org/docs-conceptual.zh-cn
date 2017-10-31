---
title: "缓解：池阻止时间段"
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology:
- dotnet-bcl
- dotnet-clr
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 92d2de20-79be-4df1-b182-144143a8866a
caps.latest.revision: 4
author: rpetrusha
ms.author: ronpet
manager: wpickett
ms.translationtype: HT
ms.sourcegitcommit: 306c608dc7f97594ef6f72ae0f5aaba596c936e1
ms.openlocfilehash: caaaafaff44f2a679b16fe3f1aae59bcf717388e
ms.contentlocale: zh-cn
ms.lasthandoff: 07/28/2017

---
# <a name="mitigation-pool-blocking-period"></a>缓解：池阻止时间段
与 Azure SQL 数据库的连接已删除连接池阻止时间段。  
  
## <a name="additional-description"></a>其他说明  
 在 [!INCLUDE[net_v461](../../../includes/net-v461-md.md)] 和早期版本中，当应用在连接到数据库过程中遇到暂时性连接失败时，无法快速重试连接，因为连接池会缓存错误，并在 5 秒至 1 分钟后重新引发该错误。有关详细信息，请参阅 [SQL Server 连接池 (ADO.NET)](../../../docs/framework/data/adonet/sql-server-connection-pooling.md)。 这种行为会给 Azure SQL 数据库连接带来问题，因为经常会因暂时性错误而导致连接失败，这些错误通常在几秒内便会恢复。 连接池阻止功能意味着，应用在很长一段时间内都无法连接到数据库，即使数据库可用也不行。 对于连接到 Azure SQL 数据库以及需要在几秒内呈现的 Web 应用，这种行为带来的问题尤为明显。  
  
 对于发送到已知 Azure SQL 数据库（*.database.windows.net、\*.database.chinacloudapi.cn、\*.database.usgovcloudapi.net、\*.database.cloudapi.de）的打开连接请求（开头为 [!INCLUDE[net_v462](../../../includes/net-v462-md.md)]），将不会缓存打开连接错误。 对于其他所有连接尝试，连接池阻止时间段还会继续强制执行。  
  
## <a name="impact"></a>影响  
 此更改允许立即重新尝试打开 Azure SQL 数据库的连接，从而改进了已启用云的应用的性能。  
  
## <a name="mitigation"></a>缓解操作  
 对于受到此更改不利影响的应用，连接池阻止时间段可通过设置新 <xref:System.Data.SqlClient.SqlConnectionStringBuilder.PoolBlockingPeriod%2A> 属性进行配置。  该属性的值属于 <xref:System.Data.SqlClient.PoolBlockingPeriod?displayProperty=fullName> 枚举，可采用以下三个值中的任意一个：  
  
-   `PoolBlockingPeriod.AlwaysBlock` 
  
-   `PoolBlockingPeriod.Auto`  
  
-   `PoolBlockingPeriod.NeverBlock` 
  
 可以通过将 <xref:System.Data.SqlClient.SqlConnectionStringBuilder.PoolBlockingPeriod%2A> 属性设置为 `PoolBlockingPeriod.AlwaysBlock` 来还原以前的行为。  
  
## <a name="see-also"></a>另请参阅  
 [运行时更改](../../../docs/framework/migration-guide/runtime-changes-in-the-net-framework-4-6-2.md)

