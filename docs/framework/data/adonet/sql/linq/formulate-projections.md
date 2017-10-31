---
title: "构建投影 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-ado"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 745742df-0eda-479b-83f8-29bd8a80db96
caps.latest.revision: 2
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 2
---
# 构建投影
下面的示例演示如何将 C\# 中的 `select` 语句和 [!INCLUDE[vbprvb](../../../../../../includes/vbprvb-md.md)] 中的 `Select` 语句与其他功能结合使用以构建查询投影。  
  
## 示例  
 下面的示例使用 [!INCLUDE[vbprvb](../../../../../../includes/vbprvb-md.md)] 中的 `Select` 子句（在 C\# 中为 `select` 子句）返回由 `Customers` 的联系人姓名组成的序列。  
  
 [!code-csharp[DLinqQueryExamples#57](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqQueryExamples/cs/Program.cs#57)]
 [!code-vb[DLinqQueryExamples#57](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqQueryExamples/vb/Module1.vb#57)]  
  
## 示例  
 下面的示例使用 [!INCLUDE[vbprvb](../../../../../../includes/vbprvb-md.md)] 中的 `Select` 子句（在 C\# 中为 `select` 子句）和匿名类型返回由 `Customers` 的联系人姓名和电话号码组成的序列。  
  
 [!code-csharp[DLinqQueryExamples#58](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqQueryExamples/cs/Program.cs#58)]
 [!code-vb[DLinqQueryExamples#58](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqQueryExamples/vb/Module1.vb#58)]  
  
## 示例  
 下面的示例使用 [!INCLUDE[vbprvb](../../../../../../includes/vbprvb-md.md)] 中的 `Select` 子句（在 C\# 中为 `select` 子句）和匿名类型返回由雇员的姓名和电话号码组成的序列。  在产生的序列中，`FirstName` 和 `LastName` 字段组合成单个字段 \(`Name`\)，`HomePhone` 字段重命名为 `Phone`。  
  
 [!code-csharp[DLinqQueryExamples#59](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqQueryExamples/cs/Program.cs#59)]
 [!code-vb[DLinqQueryExamples#59](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqQueryExamples/vb/Module1.vb#59)]  
  
## 示例  
 下面的示例使用 [!INCLUDE[vbprvb](../../../../../../includes/vbprvb-md.md)] 中的 `Select` 子句（在 C\# 中为 `select` 子句）和匿名类型返回由所有 `ProductID` 和名为 `HalfPrice` 的计算所得的值组成的序列。  此值设置为 `UnitPrice` 的 1\/2。  
  
 [!code-csharp[DLinqQueryExamples#60](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqQueryExamples/cs/Program.cs#60)]
 [!code-vb[DLinqQueryExamples#60](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqQueryExamples/vb/Module1.vb#60)]  
  
## 示例  
 下面的示例使用 [!INCLUDE[vbprvb](../../../../../../includes/vbprvb-md.md)] 中的 `Select` 子句（在 C\# 中为 `select` 子句）和一个条件语句返回由产品名和产品可用性组成的序列。  
  
 [!code-csharp[DLinqQueryExamples#61](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqQueryExamples/cs/Program.cs#61)]
 [!code-vb[DLinqQueryExamples#61](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqQueryExamples/vb/Module1.vb#61)]  
  
## 示例  
 下面的示例使用 [!INCLUDE[vbprvb](../../../../../../includes/vbprvb-md.md)] `Select` 子句（在 C\# 中为 `select` 子句）和一个已知类型 \(Name\) 返回由雇员的姓名组成的序列。  
  
 [!code-csharp[DLinqQueryExamples#62](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqQueryExamples/cs/Program.cs#62)]
 [!code-vb[DLinqQueryExamples#62](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqQueryExamples/vb/Module1.vb#62)]  
  
## 示例  
 下面的示例使用 [!INCLUDE[vbprvb](../../../../../../includes/vbprvb-md.md)] 中的 `Select` 和 `Where`（在 C\# 中为 `select` 和 `where`）返回由位于伦敦的客户的联系人姓名组成的筛选序列。  
  
 [!code-csharp[DLinqQueryExamples#63](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqQueryExamples/cs/Program.cs#63)]
 [!code-vb[DLinqQueryExamples#63](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqQueryExamples/vb/Module1.vb#63)]  
  
## 示例  
 下面的示例使用 [!INCLUDE[vbprvb](../../../../../../includes/vbprvb-md.md)] 中的 `Select` 子句（在 C\# 中为 `select` 子句）和匿名类型返回有关客户的数据的成形子集。  
  
 [!code-csharp[DLinqQueryExamples#64](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqQueryExamples/cs/Program.cs#64)]
 [!code-vb[DLinqQueryExamples#64](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqQueryExamples/vb/Module1.vb#64)]  
  
## 示例  
 下面的示例使用嵌套查询返回以下结果：  
  
-   由所有订单及其对应的 `OrderID` 组成的序列。  
  
-   由订单中具有折扣的项组成的子序列。  
  
-   不含运费时节省的资金数额。  
  
 [!code-csharp[DLinqQueryExamples#65](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqQueryExamples/cs/Program.cs#65)]
 [!code-vb[DLinqQueryExamples#65](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqQueryExamples/vb/Module1.vb#65)]  
  
## 请参阅  
 [查询示例](../../../../../../docs/framework/data/adonet/sql/linq/query-examples.md)