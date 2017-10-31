---
title: "如何：调用规范函数 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-ado"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: b3d84873-7403-4957-8e20-b4ae39f50214
caps.latest.revision: 3
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 3
---
# 如何：调用规范函数
<xref:System.Data.Objects.EntityFunctions> 类包含公开要在 LINQ to Entities 查询中使用的规范函数的方法。  有关规范函数的信息，请参见[规范函数](../../../../../../docs/framework/data/adonet/ef/language-reference/canonical-functions.md)。  
  
> [!NOTE]
>  <xref:System.Data.Objects.EntityFunctions> 类中的 <xref:System.Data.Objects.EntityFunctions.AsUnicode%2A> 和 <xref:System.Data.Objects.EntityFunctions.AsNonUnicode%2A> 方法不具有规范函数等效性。  
  
 可以直接调用对一组值执行计算并返回单个值的规范函数（也成为聚合规范函数）。  其他规范函数只能作为 LINQ to Entities 查询的一部分调用。  若要直接调用聚合函数，必须将 <xref:System.Data.Objects.ObjectQuery%601> 传递到此函数。  有关更多信息，请参见下面的第二个示例。  
  
 可以在 LINQ to Entities 查询中使用公共语言运行时 \(CLR\) 方法调用某些规范函数。  有关映射到规范函数的 CLR 方法的列表，请参见 [规范函数映射的 CLR 方法](../../../../../../docs/framework/data/adonet/ef/language-reference/clr-method-to-canonical-function-mapping.md)。  
  
## 示例  
 下面的示例使用 [AdventureWorks Sales Model](http://msdn.microsoft.com/zh-cn/f16cd988-673f-4376-b034-129ca93c7832)。  此示例执行一个 LINQ to Entities 查询，该查询使用 <xref:System.Data.Objects.EntityFunctions.DiffDays%2A> 方法返回 `SellEndDate` 与 `SellStartDate` 之间相差小于 365 天的所有产品：  
  
 [!code-csharp[DP L2E CanonicalAndStoreFunctions#1](../../../../../../samples/snippets/csharp/VS_Snippets_Data/dp l2e canonicalandstorefunctions/cs/program.cs#1)]
 [!code-vb[DP L2E CanonicalAndStoreFunctions#1](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/dp l2e canonicalandstorefunctions/vb/module1.vb#1)]  
  
## 示例  
 下面的示例使用 [AdventureWorks Sales Model](http://msdn.microsoft.com/zh-cn/f16cd988-673f-4376-b034-129ca93c7832)。  此示例直接调用聚合 <xref:System.Data.Objects.EntityFunctions.StandardDeviation%2A> 方法，以返回 `SalesOrderHeader` 小计的标准偏差。  请注意，应将 <xref:System.Data.Objects.ObjectQuery%601> 传递给此函数，这样，就可以调用它而不需要使它成为 LINQ to Entities 查询的一部分。  
  
 [!code-csharp[DP L2E CanonicalAndStoreFunctions#2](../../../../../../samples/snippets/csharp/VS_Snippets_Data/dp l2e canonicalandstorefunctions/cs/program.cs#2)]
 [!code-vb[DP L2E CanonicalAndStoreFunctions#2](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/dp l2e canonicalandstorefunctions/vb/module1.vb#2)]  
  
## 请参阅  
 [调用 LINQ to Entities 查询中的函数](../../../../../../docs/framework/data/adonet/ef/language-reference/calling-functions-in-linq-to-entities-queries.md)   
 [LINQ to Entities 中的查询](../../../../../../docs/framework/data/adonet/ef/language-reference/queries-in-linq-to-entities.md)