---
title: "如何：将列表示为时间戳列或版本列 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-ado"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 5afd5ce8-1d20-4bc3-a34f-49d95449f493
caps.latest.revision: 2
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 2
---
# 如何：将列表示为时间戳列或版本列
使用 <xref:System.Data.Linq.Mapping.ColumnAttribute> 属性 \(Attribute\) 的 [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] <xref:System.Data.Linq.Mapping.ColumnAttribute.IsVersion%2A> 属性 \(Property\) 可将字段或属性指定为表示保存数据库时间戳或版本号的数据库列。  
  
 有关代码示例，请参见<xref:System.Data.Linq.Mapping.ColumnAttribute.IsVersion%2A>。  
  
### 将字段或属性指定为表示时间戳列或版本列  
  
1.  将 <xref:System.Data.Linq.Mapping.ColumnAttribute.IsVersion%2A> 属性 \(Property\) 添加到 <xref:System.Data.Linq.Mapping.ColumnAttribute> 属性 \(Attribute\)。  
  
2.  将 <xref:System.Data.Linq.Mapping.ColumnAttribute.IsVersion%2A> 属性值设置为 `true`。  
  
## 请参阅  
 [LINQ to SQL 对象模型](../../../../../../docs/framework/data/adonet/sql/linq/the-linq-to-sql-object-model.md)   
 [如何：指定测试哪些成员是否发生并发冲突](../../../../../../docs/framework/data/adonet/sql/linq/how-to-specify-which-members-are-tested-for-concurrency-conflicts.md)   
 [如何：使用代码编辑器自定义实体类](../../../../../../docs/framework/data/adonet/sql/linq/how-to-customize-entity-classes-by-using-the-code-editor.md)