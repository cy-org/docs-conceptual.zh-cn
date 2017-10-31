---
title: "如何：指定数据库名称 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-ado"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: b80f0fd2-7f75-45fe-9e12-496f80f183df
caps.latest.revision: 2
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 2
---
# 如何：指定数据库名称
使用 <xref:System.Data.Linq.Mapping.DatabaseAttribute> 属性 \(Attribute\) 的 <xref:System.Data.Linq.Mapping.DatabaseAttribute.Name%2A> 属性 \(Property\) 可在连接未提供名称时指定数据库的名称。  
  
 有关代码示例，请参见<xref:System.Data.Linq.Mapping.DatabaseAttribute.Name%2A>。  
  
### 指定数据库的名称  
  
1.  将 <xref:System.Data.Linq.Mapping.DatabaseAttribute> 属性添加到数据库的类声明中。  
  
2.  将 <xref:System.Data.Linq.Mapping.DatabaseAttribute.Name%2A> 属性 \(Property\) 添加到 <xref:System.Data.Linq.Mapping.DatabaseAttribute> 属性 \(Attribute\)。  
  
3.  将 <xref:System.Data.Linq.Mapping.DatabaseAttribute.Name%2A> 属性值设置为您要指定的名称。  
  
## 请参阅  
 [LINQ to SQL 对象模型](../../../../../../docs/framework/data/adonet/sql/linq/the-linq-to-sql-object-model.md)   
 [如何：使用代码编辑器自定义实体类](../../../../../../docs/framework/data/adonet/sql/linq/how-to-customize-entity-classes-by-using-the-code-editor.md)