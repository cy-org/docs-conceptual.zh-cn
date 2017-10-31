---
title: "LINQ to SQL 查询 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-ado"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: f4897aaa-7f44-4c20-a471-b948c2971aae
caps.latest.revision: 4
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 4
---
# LINQ to SQL 查询
定义 [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] 查询所用的语法与在 [!INCLUDE[vbteclinq](../../../../../../includes/vbteclinq-md.md)] 中使用的语法相同。  唯一的差异是您的查询中引用的对象映射到数据库中的元素。  有关详细信息，请参阅 [Introduction to LINQ Queries \(C\#\)](../Topic/Introduction%20to%20LINQ%20Queries%20\(C%23\).md)。  
  
 [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] 将您编写的查询转换成等效的 SQL 查询，然后将它们发送至服务器进行处理。 更具体地说，您的应用程序使用 [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] API 来请求查询执行。  [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] 提供程序随后会将查询转换成 SQL 文本，并委托 ADO 提供程序执行。 ADO 提供程序将查询结果作为 `DataReader` 返回。  [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] 提供程序将 ADO 结果转换成用户对象的 <xref:System.Linq.IQueryable> 集合。  
  
> [!NOTE]
>  [!INCLUDE[dnprdnshort](../../../../../../includes/dnprdnshort-md.md)] 内置类型中的大多数方法和运算符都能直接转换成 SQL。  [!INCLUDE[vbteclinq](../../../../../../includes/vbteclinq-md.md)] 无法转换的那些方法和运算符会产生运行时异常。  有关详细信息，请参阅[SQL\-CLR 类型映射](../../../../../../docs/framework/data/adonet/sql/linq/sql-clr-type-mapping.md)。  
  
 下表显示了 [!INCLUDE[vbteclinq](../../../../../../includes/vbteclinq-md.md)] 与 [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] 查询项之间的相似和不同之处。  
  
|项|LINQ 查询|[!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] 查询|  
|-------|-------------|-------------------------------------------------------------------|  
|保存查询的局部变量的返回类型（对于返回序列的查询而言）|泛型 `IEnumerable`|泛型 `IQueryable`|  
|指定数据源|使用 `From` \([!INCLUDE[vbprvb](../../../../../../includes/vbprvb-md.md)]\) 或 `from` \(C\#\) 子句|相同|  
|筛选|使用 `Where`\/`where` 子句|相同|  
|分组|使用 `Group…By`\/`groupby` 子句|相同|  
|选择（投影）|使用 `Select`\/`select` 子句|相同|  
|延迟执行与立即执行|请参阅 [Introduction to LINQ Queries \(C\#\)](../Topic/Introduction%20to%20LINQ%20Queries%20\(C%23\).md)|相同|  
|实现联接|使用 `Join`\/`join` 子句|可以使用 `Join`\/`join` 子句，但使用 <xref:System.Data.Linq.Mapping.AssociationAttribute> 属性更有效。  有关详细信息，请参阅[跨关系查询](../../../../../../docs/framework/data/adonet/sql/linq/querying-across-relationships.md)。|  
|远程执行与本地执行||有关详细信息，请参见 [远程执行与本地执行](../../../../../../docs/framework/data/adonet/sql/linq/remote-vs-local-execution.md)。|  
|流式查询与缓存查询|在本地内存情况中不适用||  
  
## 请参阅  
 [Introduction to LINQ Queries \(C\#\)](../Topic/Introduction%20to%20LINQ%20Queries%20\(C%23\).md)   
 [Basic LINQ Query Operations](../Topic/Basic%20LINQ%20Query%20Operations%20\(C%23\).md)   
 [Type Relationships in LINQ Query Operations](../Topic/Type%20Relationships%20in%20LINQ%20Query%20Operations%20\(C%23\).md)   
 [查询概念](../../../../../../docs/framework/data/adonet/sql/linq/query-concepts.md)