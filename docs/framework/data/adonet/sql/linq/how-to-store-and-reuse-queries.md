---
title: "如何：存储和重用查询 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-ado"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: a012bd79-1809-45e3-adea-0229532396cc
caps.latest.revision: 2
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 2
---
# 如何：存储和重用查询
当您的应用程序多次执行结构上相似的查询时，您通常可以通过如下方法提高性能：编译此查询一次，然后用不同的参数执行它若干次。  例如，应用程序可能需要检索位于特定城市的所有客户，其中此城市是在运行时由用户在窗体中指定的。  [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] 支持使用已编译查询来实现此目的。  
  
> [!NOTE]
>  这种使用模式代表了已编译查询最常见的用途。  也可以使用其他方法。  例如，已编译查询可以存储为扩展设计器所生成代码的分部类的静态成员。  
  
## 示例  
 在很多情况下，您可能需要跨线程边界重复使用查询。  在这种情况下，将已编译查询存储在静态变量中特别有效。  下面的代码示例采用设计用于存储已编译查询的 `Queries`，并采用表示强类型化 <xref:System.Data.Linq.DataContext> 的 Northwind 类。  
  
 [!code-csharp[DLinqQuerying#6](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqQuerying/cs/Program.cs#6)]
 [!code-vb[DLinqQuerying#6](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqQuerying/vb/Module1.vb#6)]  
  
 [!code-csharp[DLinqQuerying#7](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqQuerying/cs/Program.cs#7)]
 [!code-vb[DLinqQuerying#7](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqQuerying/vb/Module1.vb#7)]  
  
## 示例  
 目前您无法存储（存储在静态变量中）返回匿名类型的查询，因为类型没有可作为泛型参数提供的名称。  下面的示例演示如何创建可表示结果的类型，然后将其用作泛型参数，从而解决该问题。  
  
 [!code-csharp[DLinqQuerying#8](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqQuerying/cs/Program.cs#8)]
 [!code-vb[DLinqQuerying#8](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqQuerying/vb/Module1.vb#8)]  
  
## 请参阅  
 <xref:System.Data.Linq.CompiledQuery>   
 [查询概念](../../../../../../docs/framework/data/adonet/sql/linq/query-concepts.md)   
 [查询数据库](../../../../../../docs/framework/data/adonet/sql/linq/querying-the-database.md)