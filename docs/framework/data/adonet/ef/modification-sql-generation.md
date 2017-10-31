---
title: "修改 SQL 生成 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-ado"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 2188a39d-46ed-4a8b-906a-c9f15e6fefd1
caps.latest.revision: 3
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 3
---
# 修改 SQL 生成
本节讨论如何开发用于（符合 SQL:1999 的数据库）提供程序的修改 SQL 生成模块。  此模块负责将修改命令目录树转换成适当的 SQL INSERT、UPDATE 或 DELETE 语句。  
  
 有关 SELECT 语句的 SQL 生成的信息，请参见 [SQL 生成](../../../../../docs/framework/data/adonet/ef/sql-generation.md)。  
  
## 修改命令目录树的概述  
 修改 SQL 生成模块可基于给定的输入 DbModificationCommandTree 生成特定于数据库的修改 SQL 语句。  
  
 DbModificationCommandTree 是继承自 DbCommandTree 的修改 DML 操作（插入、更新或删除操作）的对象模型表示形式。  DbModificationCommandTree 有三种实现：  
  
-   DbInsertCommandTree  
  
-   DbUpdateCommandTree  
  
-   DbDeleteCommandTree  
  
 DbModificationCommandTree 及其实现是由[!INCLUDE[adonet_ef](../../../../../includes/adonet-ef-md.md)]生成的，始终表示单行操作。  本节将介绍这些类型及其在 .NET Framework 版本 3.5 中的约束。  
  
 ![关系图](../../../../../docs/framework/data/adonet/ef/media/558ba7b3-dd19-48d0-b91e-30a76415bf5f.gif "558ba7b3\-dd19\-48d0\-b91e\-30a76415bf5f")  
  
 DbModificationCommandTree 具有 Target 属性，该属性表示修改操作的目标集。  Target 的 Expression 属性定义输入集，始终为 DbScanExpression。  DbScanExpression 可以表示表或视图，如果其 Target 的元数据属性“Defining Query”不为 null，也可以表示使用查询定义的数据集。  
  
 DbScanExpression 表示一个查询，如果使用模型中的定义查询来定义集，但不提供相应的修改操作的功能，则它仅可以获取作为修改目标的提供程序。  提供程序也许不支持此类方案，例如 SqlClient 就不支持。  
  
 DbInsertCommandTree 表示用一个命令目录树代表的单行插入操作。  
  
```  
public sealed class DbInsertCommandTree : DbModificationCommandTree {  
   public IList<DbModificationClause> SetClauses { get }  
   public DbExpression Returning { get }  
}  
```  
  
 DbUpdateCommandTree 表示用一个命令目录树代表的单行更新操作。  
  
 DbDeleteCommandTree 表示单独行删除操作，表示为一个命令目录树。  
  
### 有关修改命令目录树属性的限制  
 下面的信息和限制仅适用于修改命令目录树属性。  
  
#### DbInsertCommandTree 和 DbUpdateCommandTree 中的 Returning  
 当 Returning 不为 null 时，指示该命令返回一个读取器。  否则，该命令应返回一个标量值，指示所影响的（已插入或已更新的）行的数量。  
  
 Returning 值指定基于已插入或已更新的行返回结果投影。  它仅可以属于表示行的 DbNewInstanceExpression 类型，其每个参数均为 DbPropertyExpression 并且位于表示对相应 DbModificationCommandTree 的 Target 的引用的 DbVariableReferenceExpression 之上。  Returning 属性中使用的 DbPropertyExpressions 表示的属性始终为存储生成的值或计算值。  在 DbInsertCommandTree 中，当插入行的表中的属性至少有一个指定为存储生成的值或计算值（在 ssdl 中标记为 StoreGeneratedPattern.Identity 或 StoreGeneratedPattern.Computed）时，Returning 不为 null。  在 DbUpdateCommandTrees 中，当更新行的表中的属性至少有一个指定为存储生成的值或计算值（在 ssdl 中标记为 StoreGeneratedPattern.Computed）时，Returning 不为 null。  
  
#### DbInsertCommandTree 和 DbUpdateCommandTree 中的 SetClauses  
 SetClauses 指定插入或更新集子句的列表，这些子句定义插入或更新操作。  
  
```  
The elements of the list are specified as type DbModificationClause, which specifies a single clause in an insert or update modification operation. DbSetClause inherits from DbModificationClause and specifies the clause in a modification operation that sets the value of a property. Beginning in version 3.5 of the .NET Framework, all elements in SetClauses are of type SetClause.   
```  
  
 Property 指定应进行更新的属性。  它始终是 DbPropertyExpression 并且位于表示对相应 DbModificationCommandTree 的 Target 的引用的 DbVariableReferenceExpression 之上。  
  
 Value 指定用来更新属性的新值。  它是 DbConstantExpression 类型或 DbNullExpression 类型。  
  
#### DbUpdateCommandTree 和 DbDeleteCommandTree 中的 Predicate  
 Predicate 指定用于确定应更新或删除目标集合中的哪些成员的谓词。  它是由 DbExpressions 的下列子集构成的表达式树：  
  
-   Equals 类型的 DbComparisonExpression，其右侧子级为 DbPropertyExression（根据下面的限制要求），左侧子级为 DbConstantExpression。  
  
-   DbConstantExpression  
  
-   根据下面的限制要求，DbIsNullExpression 在 DbPropertyExpresison 之上  
  
-   DbPropertyExpression 在表示对相应 DbModificationCommandTree 的 Target 的引用的 DbVariableReferenceExpression 之上。  
  
-   DbAndExpression  
  
-   DbNotExpression  
  
-   DbOrExpression  
  
## 示例提供程序中的修改 SQL 生成  
 [实体框架示例提供程序](http://go.microsoft.com/fwlink/?LinkId=180616)（可能为英文网页）演示支持 [!INCLUDE[adonet_ef](../../../../../includes/adonet-ef-md.md)] 的 ADO.NET 数据提供程序的组件。  该示例提供程序以 SQL Server 2005 数据库为目标，并在 System.Data.SqlClient ADO.NET 2.0 数据提供程序之上作为一个包装实现。  
  
 该示例提供程序的修改 SQL 生成模块（位于 SQL Generation\\DmlSqlGenerator.cs 文件中）采用一个输入 DbModificationCommandTree，并且生成可能带有 SELECT 语句的单个修改 SQL 语句以返回一个读取器（如果 DbModificationCommandTree 指定了读取器）。  请注意，生成的命令的形式受目标 SQL Server 数据库影响。  
  
### 帮助器类：ExpressionTranslator  
 ExpressionTranslator 用作一个适用于 DbExpression 类型的所有修改命令目录树属性的通用轻型转换器。  它支持仅转换修改命令目录树的属性所限于使用的表达式类型，而且它在构建时应用了特定约束。  
  
 以下信息讨论如何访问特定的表达式类型（忽略具有细微转换的节点）。  
  
### DbComparisonExpression  
 当使用 preserveMemberValues \= true 构造 ExpressionTranslator 并且右侧的常量为 DbConstantExpression（而不是 DbNullExpression）时，它将左操作数（一个 DbPropertyExpressions）与该 DbConstantExpression 关联。  如果需要生成一个返回 Select 语句来标识受影响的行，则使用此类型。  
  
### DbConstantExpression  
 针对每个所访问的常量，创建一个参数。  
  
### DbPropertyExpression  
 假定 DbPropertyExpression 的实例始终表示输入表，除非生成操作已创建一个别名（只会在使用表变量时的更新方案中出现这种情况），否则不需要为输入指定别名；转换默认为属性名。  
  
## 生成插入 SQL 命令  
 对于示例提供程序中给定的 DbInsertCommandTree，生成的插入命令跟在下面两个插入模板中的一个后面。  
  
 第一个模板包含一个命令来执行插入操作（假定值在 SetClauses 列表中）以及一个 SELECT 语句来为插入的行返回在 Returning 属性中指定的属性（如果 Returning 属性不为 null）。  如果插入一行，则谓词元素“@@ROWCOUNT \> 0”为 true。  仅当 keyMemeberI 为存储生成的键时，谓词元素“keyMemberI \=  keyValueI &#124; scope\_identity\(\)”才会呈现“keyMemberI \=  scope\_identity\(\)”形式，这是因为 scope\_identity\(\) 返回插入到标识（存储生成的）列中的最后一个标识值。  
  
```  
-- first insert Template  
INSERT <target>   [ (setClauseProperty0, .. setClausePropertyN)]    
VALUES (setClauseValue0, .. setClauseValueN) |  DEFAULT VALUES   
  
[SELECT <returning>   
 FROM <target>   
 WHERE @@ROWCOUNT > 0 AND keyMember0 = keyValue0 AND .. keyMemberI =  keyValueI | scope_identity()  .. AND  keyMemberN = keyValueN]  
```  
  
 如果插入命令指定插入一行，其中的主键是存储生成的，但不是整数类型，因而不能与 scope\_identity\(\) 一起使用，则需要第二个模板。  如果存在复合存储生成的键，也要使用第二个模板。  
  
```  
-- second insert template  
DECLARE @generated_keys TABLE [(keyMember0, … keyMemberN)  
  
INSERT <target>   [ (setClauseProperty0, .. setClausePropertyN)]    
 OUTPUT inserted.KeyMember0, …, inserted.KeyMemberN INTO @generated_keys  
 VALUES (setClauseValue0, .. setClauseValueN) |  DEFAULT VALUES   
  
[SELECT <returning_over_t>   
 FROM @generated_keys  AS g   
JOIN <target> AS t ON g.KeyMember0 = t.KeyMember0 AND … g.KeyMemberN = t.KeyMemberN  
 WHERE @@ROWCOUNT > 0   
```  
  
 下面的示例使用随示例提供程序提供的模型，  它从 DbInsertCommandTree 生成一个插入命令。  
  
 下面的代码插入一个 Category：  
  
```  
using (NorthwindEntities northwindContext = new NorthwindEntities()) {  
   Category c = new Category();  
   c.CategoryName = "Test Category";  
   c.Description = "A new category for testing";  
   northwindContext.AddObject("Categories", c);  
   northwindContext.SaveChanges();  
}  
```  
  
 此代码生成以下传递给提供程序的命令目录树:  
  
```  
DbInsertCommandTree  
|_Parameters  
|_Target : 'target'  
| |_Scan : dbo.Categories  
|_SetClauses  
| |_DbSetClause  
| | |_Property  
| | | |_Var(target).CategoryName  
| | |_Value  
| |   |_'Test Category'  
| |_DbSetClause  
| | |_Property  
| | | |_Var(target).Description  
| | |_Value  
| |   |_'A new category for testing'  
| |_DbSetClause  
|   |_Property  
|   | |_Var(target).Picture  
|   |_Value  
|     |_null  
|_Returning  
  |_NewInstance : Record['CategoryID'=Edm.Int32]  
    |_Column : 'CategoryID'  
      |_Var(target).CategoryID  
```  
  
 示例提供程序生成的存储命令为下面的 SQL 语句：  
  
```  
insert [dbo].[Categories]([CategoryName], [Description], [Picture])  
values (@p0, @p1, null)  
select [CategoryID]  
from [dbo].[Categories]  
where @@ROWCOUNT > 0 and [CategoryID] = scope_identity()  
```  
  
## 生成更新 SQL 命令  
 对于给定的 DbUpdateCommandTree，生成的更新命令将基于下面的模板：  
  
```  
-- UPDATE Template   
UPDATE <target>   
SET setClauseProprerty0 = setClauseValue0,  .. setClauseProprertyN = setClauseValueN  | @i = 0  
WHERE <predicate>  
  
[SELECT <returning>   
 FROM <target>   
 WHERE @@ROWCOUNT > 0 AND keyMember0 = keyValue0 AND .. keyMemberI =  keyValueI | scope_identity()  .. AND  keyMemberN = keyValueN]  
```  
  
 仅当未指定 set 子句时，set 子句才具有假 set 子句 \("@i \= 0"\)。  这将确保重新计算所有存储计算的列。  
  
 仅当 Returning 属性不为 null 时，才生成 SELECT 语句以返回在 Returning 属性中指定的属性。  
  
 下面的示例使用随示例提供程序提供的模型生成更新命令。  
  
 下面的用户代码更新 Category：  
  
```  
using (NorthwindEntities northwindContext = new NorthwindEntities()) {  
   Category c = northwindContext.Categories.Where(i => i.CategoryName == "Test Category").First();  
   c.CategoryName = "New test name";  
   northwindContext.SaveChanges();  
}  
```  
  
 此用户代码生成以下传递给提供程序的命令目录树：  
  
```  
DbUpdateCommandTree  
|_Parameters  
|_Target : 'target'  
| |_Scan : dbo.Categories  
|_SetClauses  
| |_DbSetClause  
|   |_Property  
|   | |_Var(target).CategoryName  
|   |_Value  
|     |_'New test name'  
|_Predicate  
| |_  
|   |_Var(target).CategoryID  
|   |_=  
|   |_10  
|_Returning   
```  
  
 示例提供程序生成下面的存储命令：  
  
```  
update [dbo].[Categories]  
set [CategoryName] = @p0  
where ([CategoryID] = @p1)   
```  
  
### 生成删除 SQL 命令  
 对于给定的 DbDeleteCommandTree，生成的 DELETE 命令将基于下面的模板：  
  
```  
-- DELETE Template   
DELETE <target>   
WHERE <predicate>  
```  
  
 下面的示例使用随示例提供程序提供的模型生成删除命令。  
  
 下面的用户代码删除 Category：  
  
```  
using (NorthwindEntities northwindContext = new NorthwindEntities()) {  
   Category c = northwindContext.Categories.Where(i => i.CategoryName == "New test name").First();  
   northwindContext.DeleteObject(c);  
   northwindContext.SaveChanges();  
}  
```  
  
 此用户代码生成以下传递给提供程序的命令目录树。  
  
```  
DbDeleteCommandTree  
|_Parameters  
|_Target : 'target'  
| |_Scan : dbo.Categories  
|_Predicate  
  |_  
    |_Var(target).CategoryID  
    |_=  
    |_10  
```  
  
 下面的存储命令由示例提供程序生成：  
  
```  
delete [dbo].[Categories]  
where ([CategoryID] = @p0)  
```  
  
## 请参阅  
 [编写实体框架数据提供程序](../../../../../docs/framework/data/adonet/ef/writing-an-ef-data-provider.md)