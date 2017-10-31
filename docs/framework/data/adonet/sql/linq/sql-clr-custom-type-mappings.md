---
title: "SQL-CLR 自定义类型映射 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-ado"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: d916c7fb-4b56-4214-acbe-5e23365047b2
caps.latest.revision: 2
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 2
---
# SQL-CLR 自定义类型映射
当使用 SQLMetal 命令行工具和对象关系设计器（O\/R 设计器）时，将自动指定 SQL Server 与公共语言运行库 \(CLR\) 之间的类型映射。  
  
 如果没有执行任何自定义映射，则这些工具将分配默认的类型映射，如 [SQL\-CLR 类型映射](../../../../../../docs/framework/data/adonet/sql/linq/sql-clr-type-mapping.md) 中所述。  如果要执行不同于这些默认映射的类型映射，则需要自定义类型映射的一些设置。  
  
 自定义类型映射时，建议的方法是在一个中间 DBML 文件中做出更改。  然后，在使用 SQLMetal 或 O\/R 设计器创建代码和映射文件时，应使用自定义的 DBML 文件。  
  
 从代码和映射文件实例化 <xref:System.Data.Linq.DataContext> 对象后，<xref:System.Data.Linq.DataContext.CreateDatabase%2A?displayProperty=fullName> 方法将根据指定的类型映射创建数据库。  如果映射中未指定任何 CLR `type` 属性，则将使用默认类型映射。  
  
## 使用 SQLMetal 或 O\/R 设计器进行自定义  
 通过使用 SQLMetal 和 O\/R 设计器，可以自动创建一个包括代码文件内部或外部的类型映射信息的对象模型。  由于这些文件可被 SQLMetal 或 O\/R 设计器覆盖，因此在每次重新创建映射时，指定自定义类型映射的建议方法是自定义一个 DBML 文件。  
  
 若要使用 SQLMetal 或 O\/R 设计器自定义类型映射，请首先生成一个 DBML 文件。  然后，在生成代码文件或映射文件之前，修改该 DBML 文件以标识所需的类型映射。  使用 SQLMetal 时，您必须在 DBML 文件中手动更改 `Type` 和 `DbType` 属性才能自定义您的类型映射。  使用 O\/R 设计器时，您可以在设计器中进行更改。  有关使用 O\/R 设计器的更多方法，请参见[LINQ to SQL 工具在 Visual Studio 中](../Topic/LINQ%20to%20SQL%20Tools%20in%20Visual%20Studio2.md)。  
  
> [!NOTE]
>  在进行数据库转换时，某些类型映射可能会导致溢出或数据丢失异常。  进行任何自定义设置之前，请认真查看 [SQL\-CLR 类型映射](../../../../../../docs/framework/data/adonet/sql/linq/sql-clr-type-mapping.md) 中的类型映射运行时行为矩阵。  
  
 若要使 SQLMetal 或 O\/R 设计器能够识别您的类型映射自定义项，需确保在生成代码文件或外部映射文件时，提供给这些工具的路径为自定义 DBML 文件的路径。  建议您始终将类型映射信息与代码文件分开并生成附加的外部类型映射文件，尽管这对于类型映射自定义不是必需的。  这样做将不需要重新编译代码文件，从而可保留一些灵活性。  
  
## 合并数据库更改  
 更改数据库时，您需要更新 DBML 文件以反映这些更改。  完成此任务的一种方式是自动新建一个 DBML 文件，然后重新执行类型映射自定义。  或者，可以比较新 DBML 文件与自定义 DBML 文件之间的差异，并手动更新自定义 DBML 文件以反映数据库更改。  
  
## 请参阅  
 [SQL\-CLR 类型映射](../../../../../../docs/framework/data/adonet/sql/linq/sql-clr-type-mapping.md)   
 [LINQ to SQL 中的代码生成](../../../../../../docs/framework/data/adonet/sql/linq/code-generation-in-linq-to-sql.md)