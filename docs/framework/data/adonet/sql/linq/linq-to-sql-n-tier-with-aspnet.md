---
title: "具有 ASP.NET 的 LINQ to SQL N 层 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-ado"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: f6cc863a-d6a6-4281-ba8b-197c01cf6c6f
caps.latest.revision: 3
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 3
---
# 具有 ASP.NET 的 LINQ to SQL N 层
在使用 [!INCLUDE[vstecasp](../../../../../../includes/vstecasp-md.md)] 的 [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] 应用程序中，可以使用 <xref:System.Web.UI.WebControls.LinqDataSource> Web 服务器控件。 此控件处理查询 [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] 时必须使用的大部分逻辑，将数据传递到浏览器，检索数据，并将数据提交给 [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] <xref:System.Data.Linq.DataContext>，然后由其更新数据库。 只需要在标记中配置该控件，然后由该控件处理 [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] 和浏览器之间的所有数据传输。 由于该控件处理与表示层之间的交互，[!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] 处理与数据层之间的通信，因此对于 [!INCLUDE[vstecasp](../../../../../../includes/vstecasp-md.md)] 多层应用程序，您的主要重点是编写自定义业务逻辑。  
  
 有关 `LINQDataSource` 的详细信息，请参阅 [NIB：LinqDataSource Web 服务器控件概述](http://msdn.microsoft.com/zh-cn/104cfc3f-7385-47d3-8a51-830dfa791136)。  
  
## 请参阅  
 [使用 LINQ to SQL 的 N 层应用程序和远程应用程序](../../../../../../docs/framework/data/adonet/sql/linq/n-tier-and-remote-applications-with-linq-to-sql.md)