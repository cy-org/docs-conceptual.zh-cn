---
title: "如何：指定数据库数据类型 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-ado"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 2228fdad-7e6a-4b1b-b4d1-79d0198b7c28
caps.latest.revision: 2
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 2
---
# 如何：指定数据库数据类型
使用 <xref:System.Data.Linq.Mapping.ColumnAttribute> 属性 \(Attribute\) 的 [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] <xref:System.Data.Linq.Mapping.ColumnAttribute.DbType%2A> 属性 \(Property\) 可指定定义 T\-SQL 表声明中列的确切文本。  
  
 仅当您打算使用 <xref:System.Data.Linq.DataContext.CreateDatabase%2A> 来创建数据库实例时，才必须指定 <xref:System.Data.Linq.Mapping.ColumnAttribute.DbType%2A> 属性。  
  
 有关代码示例，请参见<xref:System.Data.Linq.Mapping.ColumnAttribute.DbType%2A>。  
  
### 指定用于定义 T\-SQL 表中数据类型的文本  
  
1.  将 <xref:System.Data.Linq.Mapping.ColumnAttribute.DbType%2A> 属性 \(Property\) 添加到 <xref:System.Data.Linq.Mapping.ColumnAttribute> 属性 \(Attribute\)。  
  
2.  将 <xref:System.Data.Linq.Mapping.ColumnAttribute.DbType%2A> 属性的值设置为 T\-SQL 使用的确切文本。  
  
## 请参阅  
 [LINQ to SQL 对象模型](../../../../../../docs/framework/data/adonet/sql/linq/the-linq-to-sql-object-model.md)   
 [如何：使用代码编辑器自定义实体类](../../../../../../docs/framework/data/adonet/sql/linq/how-to-customize-entity-classes-by-using-the-code-editor.md)