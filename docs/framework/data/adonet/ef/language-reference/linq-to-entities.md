---
title: "LINQ to Entities | Microsoft Docs"
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
ms.assetid: 641f9b68-9046-47a1-abb0-1c8eaeda0e2d
caps.latest.revision: 2
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 2
---
# LINQ to Entities
LINQ to Entities 提供语言集成查询 \(LINQ\) 支持，它允许开发人员使用 Visual Basic 或 Visual C\# 根据实体框架概念模型编写查询。  针对实体框架的查询由针对对象上下文执行的命令目录树查询表示。  LINQ to Entities 将语言集成查询 \(LINQ\) 查询转换为命令目录树查询，针对实体框架执行这些查询，并返回可同时由实体框架和 LINQ 使用的对象。  以下是创建和执行 LINQ to Entities 查询的过程：  
  
1.  从 <xref:System.Data.Objects.ObjectContext> 构造 <xref:System.Data.Objects.ObjectQuery%601> 实例。  
  
2.  通过使用 <xref:System.Data.Objects.ObjectQuery%601> 实例在 C\# 或 Visual Basic 中编写 LINQ to Entities 查询。  
  
3.  将 LINQ 标准查询运算符和表达式将转换为命令目录树。  
  
4.  对数据源执行命令目录树表示形式的查询。  执行过程中在数据源上引发的任何异常都将直接向上传递到客户端。  
  
5.  将查询结果返回到客户端。  
  
## 构造 ObjectQuery 实例  
 <xref:System.Data.Objects.ObjectQuery%601> 泛型类表示一个查询，此查询返回由零个或零个以上类型化实体组成的集合。  对象查询通常从现有对象上下文中构造（而不是手动构造），并且始终属于该对象上下文。  此上下文提供了编写和执行查询所需的连接和元数据信息。  <xref:System.Data.Objects.ObjectQuery%601> 泛型类实现 <xref:System.Linq.IQueryable%601> 泛型接口，借助于该接口的生成器方法，能够以增量方式生成 LINQ 查询。  也可以使用 C\# `var` 关键字（在 Visual Basic 中为 `Dim`，启用局部类型推理）让编译器推断实体的类型。  
  
## 编写查询  
 <xref:System.Data.Objects.ObjectQuery%601> 泛型类（可实现泛型 <xref:System.Linq.IQueryable%601> 接口）的实例可充当 LINQ to Entities 查询的数据源。  在查询中，您可以确切指定要从数据源检索哪些信息。  查询也可以指定返回信息之前信息的排序、分组和表现方式。  在 LINQ 中，查询存储在变量中。  此查询变量不执行任何操作，也不返回任何数据；它只存储查询信息。  创建查询后必须执行该查询以检索任何数据。  
  
 可以通过两种语法编写 LINQ to Entities 查询：查询表达式语法和基于方法的查询语法。  查询表达式语法和基于方法的查询语法是 C\# 3.0 和 Visual Basic 9.0 中的新增功能。  
  
 有关详细信息，请参阅[LINQ to Entities 中的查询](../../../../../../docs/framework/data/adonet/ef/language-reference/queries-in-linq-to-entities.md)。  
  
## 查询转换  
 若要针对实体框架执行 LINQ to Entities 查询，必须将 LINQ 查询转换为可针对实体框架执行的命令目录树表示形式。  
  
 LINQ to Entities 查询由 LINQ 标准查询运算符（如 <xref:System.Linq.Queryable.Select%2A>、<xref:System.Linq.Queryable.Where%2A> 和 <xref:System.Linq.Queryable.GroupBy%2A>）和表达式（x \> 10、Contact.LastName 等等）组成。  LINQ 运算符并非由类定义，而是由类中的方法定义。  在 LINQ 中，表达式可包含 <xref:System.Linq.Expressions> 命名空间内的类型所允许的任何内容，并且，通过扩展，可包含可在 lambda 函数中表示的任何内容。  这是实体框架允许的表达式的超集，这些表达式在定义上限于数据库所允许的操作，并且受到 <xref:System.Data.Objects.ObjectQuery%601> 支持。  
  
 在实体框架中，运算符和表达式同时由单一类型层次结构表示，这些运算符和表达式随后会放入命令目录树中。  实体框架使用命令目录树来执行此查询。  如果 LINQ 查询无法表示为命令目录树，则当转换查询时，将引发异常。  LINQ to Entities 查询的转换涉及两个子转换：标准查询运算符的转换和表达式转换。  
  
 一些 LINQ 标准查询运算符在 LINQ to Entities 中没有有效的转换。  尝试使用这些运算符将在查询转换期间导致异常。  有关所支持的 LINQ to Entities 运算符的列表，请参见[支持和不支持的 LINQ 方法 \(LINQ to Entities\)](../../../../../../docs/framework/data/adonet/ef/language-reference/supported-and-unsupported-linq-methods-linq-to-entities.md)。  
  
 有关使用 LINQ to Entities 中的标准查询运算符的更多信息，请参见 [LINQ to Entities 查询中的标准查询运算符](../../../../../../docs/framework/data/adonet/ef/language-reference/standard-query-operators-in-linq-to-entities-queries.md)。  
  
 通常，LINQ to Entities 中的表达式将在服务器上求值，这样，表达式的行为不会遵循 CLR 语义。  有关详细信息，请参阅[LINQ to Entities 查询中的表达式](../../../../../../docs/framework/data/adonet/ef/language-reference/expressions-in-linq-to-entities-queries.md)。  
  
 有关 CLR 方法调用如何映射到数据源中的规范函数的信息，请参见 [规范函数映射的 CLR 方法](../../../../../../docs/framework/data/adonet/ef/language-reference/clr-method-to-canonical-function-mapping.md)。  
  
 有关如何从 [!INCLUDE[linq_entities](../../../../../../includes/linq-entities-md.md)] 查询中调用规范函数、数据库函数和自定义函数的信息，请参见[调用 LINQ to Entities 查询中的函数](../../../../../../docs/framework/data/adonet/ef/language-reference/calling-functions-in-linq-to-entities-queries.md)。  
  
## 查询执行  
 在用户创建 LINQ 查询之后，该查询将转换为与实体框架兼容的表示形式（采用命令目录树形式），然后针对数据源执行此查询。  在查询执行时间，将在客户端或服务器上计算所有查询表达式（或查询的组成部分）的值。  这包括在结果具体化或实体投影中使用的表达式。  有关详细信息，请参阅[查询执行](../../../../../../docs/framework/data/adonet/ef/language-reference/query-execution.md)。  有关如何通过编译查询一次，然后使用不同的参数将其执行多次来提高性能的信息，请参见[已编译的查询 \(LINQ to Entities\)](../../../../../../docs/framework/data/adonet/ef/language-reference/compiled-queries-linq-to-entities.md)。  
  
## 具体化  
 具体化是将查询结果作为 CLR 类型返回到客户端的过程。  在 LINQ to Entities 中，从不返回查询结果数据记录；始终存在一个后备 CLR 类型，该类型由用户或实体框架定义，或者由编译器生成（匿名类型）。  所有对象具体化均由实体框架执行。  由于无法在实体框架与 CLR 之间进行映射而导致的任何错误都将导致在对象具体化过程中引发异常。  
  
 查询结果通常以下面的某一种形式返回：  
  
-   概念模型中定义的零个或多个类型化实体对象的集合或复杂类型的投影。  
  
-   [!INCLUDE[adonet_ef](../../../../../../includes/adonet-ef-md.md)]支持的 CLR 类型。  
  
-   内联集合。  
  
-   匿名类型。  
  
 有关详细信息，请参阅[查询结果](../../../../../../docs/framework/data/adonet/ef/language-reference/query-results.md)。  
  
## 本节内容  
 [LINQ to Entities 中的查询](../../../../../../docs/framework/data/adonet/ef/language-reference/queries-in-linq-to-entities.md)  
  
 [LINQ to Entities 查询中的表达式](../../../../../../docs/framework/data/adonet/ef/language-reference/expressions-in-linq-to-entities-queries.md)  
  
 [调用 LINQ to Entities 查询中的函数](../../../../../../docs/framework/data/adonet/ef/language-reference/calling-functions-in-linq-to-entities-queries.md)  
  
 [已编译的查询 \(LINQ to Entities\)](../../../../../../docs/framework/data/adonet/ef/language-reference/compiled-queries-linq-to-entities.md)  
  
 [查询执行](../../../../../../docs/framework/data/adonet/ef/language-reference/query-execution.md)  
  
 [查询结果](../../../../../../docs/framework/data/adonet/ef/language-reference/query-results.md)  
  
 [LINQ to Entities 查询中的标准查询运算符](../../../../../../docs/framework/data/adonet/ef/language-reference/standard-query-operators-in-linq-to-entities-queries.md)  
  
 [规范函数映射的 CLR 方法](../../../../../../docs/framework/data/adonet/ef/language-reference/clr-method-to-canonical-function-mapping.md)  
  
 [支持和不支持的 LINQ 方法 \(LINQ to Entities\)](../../../../../../docs/framework/data/adonet/ef/language-reference/supported-and-unsupported-linq-methods-linq-to-entities.md)  
  
 [LINQ to Entities 的已知问题和注意事项](../../../../../../docs/framework/data/adonet/ef/language-reference/known-issues-and-considerations-in-linq-to-entities.md)  
  
## 请参阅  
 [LINQ to Entities 的已知问题和注意事项](../../../../../../docs/framework/data/adonet/ef/language-reference/known-issues-and-considerations-in-linq-to-entities.md)   
 [LINQ \(Language\-Integrated Query\)](../Topic/LINQ%20\(Language-Integrated%20Query\).md)   
 [LINQ 和 ADO.NET](../../../../../../docs/framework/data/adonet/linq-and-ado-net.md)   
 [ADO.NET 实体框架](../../../../../../docs/framework/data/adonet/ef/index.md)