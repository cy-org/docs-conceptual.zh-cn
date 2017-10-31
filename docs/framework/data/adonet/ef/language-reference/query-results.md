---
title: "查询结果 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-ado"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "VB"
  - "CSharp"
  - "C++"
ms.assetid: bcd7b699-4e50-4523-8c33-2f54a103d94e
caps.latest.revision: 2
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 2
---
# 查询结果
[!INCLUDE[linq_entities](../../../../../../includes/linq-entities-md.md)] 查询在转换为命令目录树执行之后，通常以下列形式之一返回查询结果：  
  
-   概念模型中零个或多个类型化实体对象的集合或复杂类型的投影。  
  
-   概念模型支持的 CLR 类型。  
  
-   内联集合。  
  
-   匿名类型。  
  
 对数据源执行查询时，结果将具体化为 CLR 类型并返回客户端。  所有对象具体化均由 [!INCLUDE[adonet_ef](../../../../../../includes/adonet-ef-md.md)] 执行。  由于无法在 [!INCLUDE[adonet_ef](../../../../../../includes/adonet-ef-md.md)] 与 CLR 之间进行映射而导致的任何错误都将导致在对象具体化过程中引发异常。  
  
 如果查询执行返回基元概念模型类型，则结果由独立的且与[!INCLUDE[adonet_ef](../../../../../../includes/adonet-ef-md.md)]断开连接的 CLR 类型组成。  但如果查询返回 <xref:System.Data.Objects.ObjectQuery%601> 所表示的类型化实体对象的集合，则这些类型由对象上下文进行跟踪。  所有对象行为（如父\/子集合、更改跟踪、多态性等）都在 [!INCLUDE[adonet_ef](../../../../../../includes/adonet-ef-md.md)] 中定义。  此功能可按照[!INCLUDE[adonet_ef](../../../../../../includes/adonet-ef-md.md)]中的定义使用。有关更多信息，请参见[使用对象](../../../../../../docs/framework/data/adonet/ef/working-with-objects.md)。  
  
 从查询返回的结构类型（如匿名类型和可以为 null 的复杂类型）可以是 `null` 值。  返回的实体的 <xref:System.Data.Objects.DataClasses.EntityCollection%601> 属性也可以是 `null` 值。  投影值为 `null` 的实体的集合属性会导致这种情况，例如，调用没有任何元素的 <xref:System.Data.Objects.ObjectQuery%601> 的 <xref:System.Linq.Queryable.FirstOrDefault%2A>。  
  
 在某些情况下，某个查询在其执行期间看似生成具体化结果，但该查询将在服务器上执行，实体对象绝不会在 CLR 中具体化。  如果对象具体化的副作用对您有很大影响，这可能会导致问题。  
  
 下面的示例包含一个自定义类 `MyContact`，该类有一个 `LastName` 属性。  如果设置 `LastName` 属性，`count` 变量就会递增。  如果执行以下两个查询，则第一个查询将使 `count` 递增，而第二个查询不会。  这是因为：在第二个查询中，将从结果中投影 `LastName` 属性，而绝不会创建 `MyContact` 类，因为这不是对存储区执行查询所必需的。  
  
 [!code-csharp[DP L2E Materialization Example#MaterializationSideEffects](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DP L2E Materialization Example/CS/Program.cs#materializationsideeffects)]
 [!code-vb[DP L2E Materialization Example#MaterializationSideEffects](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DP L2E Materialization Example/VB/Module1.vb#materializationsideeffects)]  
  
 [!code-csharp[DP L2E Materialization Example#MyContactClass](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DP L2E Materialization Example/CS/Program.cs#mycontactclass)]
 [!code-vb[DP L2E Materialization Example#MyContactClass](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DP L2E Materialization Example/VB/Module1.vb#mycontactclass)]