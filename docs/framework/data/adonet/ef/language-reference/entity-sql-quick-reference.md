---
title: "Entity SQL 快速参考 | Microsoft Docs"
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
ms.assetid: e53dad9e-5e83-426e-abb4-be3e78e3d6dc
caps.latest.revision: 2
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 2
---
# Entity SQL 快速参考
本主题提供 [!INCLUDE[esql](../../../../../../includes/esql-md.md)] 查询的快速参考。  本主题中的查询基于 AdventureWorks 销售模型。  
  
## 文本  
  
### String  
 字符串分为 Unicode 字符串和非 Unicode 字符串。  Unicode 字符串前面附有 N。  例如 `N'hello'`。  
  
 下面是非 Unicode 字符串的示例：  
  
```  
'hello'  
--same as  
"hello"  
```  
  
 输出：  
  
|值|  
|-------|  
|hello|  
  
### DateTime  
 在日期时间文本中，日期部分和时间部分是必须存在的。  这里没有默认值。  
  
 示例：  
  
```  
DATETIME '2006-12-25 01:01:00.000'   
--same as  
DATETIME '2006-12-25 01:01'  
```  
  
 输出：  
  
|值|  
|-------|  
|25.12.06 01:01:00|  
  
### Integer  
 整数文本可以为 Int32 \(123\)、UInt32 \(123U\)、Int64 \(123L\) 和 UInt64 \(123UL\) 类型。  
  
 示例：  
  
```  
--a collection of integers  
{1, 2, 3}  
```  
  
 输出：  
  
|值|  
|-------|  
|1|  
|2|  
|3|  
  
### 其他  
 [!INCLUDE[esql](../../../../../../includes/esql-md.md)] 支持的其他文字为、Guid、二进制、浮点\/双精度型、十进制和 `null`。  [!INCLUDE[esql](../../../../../../includes/esql-md.md)] 中的 null 文本视为与概念模型中的每一种其他类型兼容。  
  
## 类型构造函数  
  
### ROW  
 [ROW](../../../../../../docs/framework/data/adonet/ef/language-reference/row-entity-sql.md) 构造一个匿名的结构化类型（记录）值，如下所示：`ROW(1 AS myNumber, ‘Name’ AS myName).`  
  
 示例：  
  
```  
SELECT VALUE row (product.ProductID as ProductID, product.Name   
    as ProductName) FROM AdventureWorksEntities.Product AS product  
```  
  
 输出：  
  
|ProductID|名称|  
|---------------|--------|  
|1|Adjustable Race|  
|879|All\-Purpose Bike Stand|  
|712|AWC Logo Cap|  
|...|...|  
  
### MULTISET  
 [MULTISET](../../../../../../docs/framework/data/adonet/ef/language-reference/multiset-entity-sql.md) 构造集合，如：  
  
 `MULTISET(1,2,2,3)` `--same as`\-`{1,2,2,3}.`  
  
 示例：  
  
```  
SELECT VALUE product FROM AdventureWorksEntities.Product AS product WHERE product.ListPrice IN MultiSet (125, 300)  
```  
  
 输出：  
  
|ProductID|名称|ProductNumber|…|  
|---------------|--------|-------------------|-------|  
|842|Touring\-Panniers, Large|PA\-T100|…|  
  
### 对象  
 [命名类型构造函数](../../../../../../docs/framework/data/adonet/ef/language-reference/named-type-constructor-entity-sql.md) 构造（命名的）用户定义对象，如 `person("abc", 12)`。  
  
 示例：  
  
```  
SELECT VALUE AdventureWorksModel.SalesOrderDetail (o.SalesOrderDetailID, o.CarrierTrackingNumber, o.OrderQty,   
o.ProductID, o.SpecialOfferID, o.UnitPrice, o.UnitPriceDiscount,   
o.rowguid, o.ModifiedDate) FROM AdventureWorksEntities.SalesOrderDetail   
AS o  
```  
  
 输出：  
  
|SalesOrderDetailID|CarrierTrackingNumber|OrderQty|ProductID|...|  
|------------------------|---------------------------|--------------|---------------|---------|  
|1|4911\-403C\-98|1|776|...|  
|2|4911\-403C\-98|3|777|...|  
|...|...|...|...|...|  
  
## 参考资料  
  
### REF  
 [REF](../../../../../../docs/framework/data/adonet/ef/language-reference/ref-entity-sql.md) 创建对实体类型实例的引用。  例如，下面的查询返回对 Orders 实体集中每一个 Order 实体的引用：  
  
```  
SELECT REF(o) AS OrderID FROM Orders AS o  
```  
  
 输出：  
  
|值|  
|-------|  
|1|  
|2|  
|3|  
|...|  
  
 下面的示例使用属性提取运算符 \(.\) 访问实体的属性。  在使用属性提取运算符时，引用将自动被反引用。  
  
 示例：  
  
```  
SELECT VALUE REF(p).Name FROM   
    AdventureWorksEntities.Product as p  
```  
  
 输出：  
  
|值|  
|-------|  
|Adjustable Race|  
|All\-Purpose Bike Stand|  
|AWC Logo Cap|  
|...|  
  
### DEREF  
 [DEREF](../../../../../../docs/framework/data/adonet/ef/language-reference/deref-entity-sql.md) 反引用一个引用值，并生成该反引用的结果。  例如，下面的查询生成 Orders 实体集中每一个 Order 的 Order 实体：`SELECT DEREF(o2.r) FROM (SELECT REF(o) AS r FROM LOB.Orders AS o) AS o2`。  
  
 示例：  
  
```  
SELECT VALUE DEREF(REF(p)).Name FROM   
    AdventureWorksEntities.Product as p  
```  
  
 输出：  
  
|值|  
|-------|  
|Adjustable Race|  
|All\-Purpose Bike Stand|  
|AWC Logo Cap|  
|...|  
  
### CREATEREF 和 KEY  
 [CREATEREF](../../../../../../docs/framework/data/adonet/ef/language-reference/createref-entity-sql.md) 创建一个传递键的引用。  [KEY](../../../../../../docs/framework/data/adonet/ef/language-reference/key-entity-sql.md) 用类型引用提取表达式的键部分。  
  
 示例：  
  
```  
SELECT VALUE Key(CreateRef(AdventureWorksEntities.Product, row(p.ProductID)))   
    FROM AdventureWorksEntities.Product as p  
```  
  
 输出：  
  
|ProductID|  
|---------------|  
|980|  
|365|  
|771|  
|...|  
  
## 函数  
  
### 规范  
 [规范函数](../../../../../../docs/framework/data/adonet/ef/language-reference/canonical-functions.md)的命名空间为 Edm，如 `Edm.Length("string")` 中所示。  您无需指定命名空间，除非导入的另一个命名空间中包含与规范函数同名的函数。  如果两个命名空间有相同的函数，用户应指定完整名称。  
  
 示例：  
  
```  
SELECT Length(c. FirstName) As NameLen FROM   
    AdventureWorksEntities.Contact AS c   
    WHERE c.ContactID BETWEEN 10 AND 12  
```  
  
 输出：  
  
|NameLen|  
|-------------|  
|6|  
|6|  
|5|  
  
### 特定于 Microsoft 提供程序  
 [特定于 Microsoft 提供程序的函数](../../../../../../docs/framework/data/adonet/ef/sqlclient-for-ef-functions.md)位于 `SqlServer` 命名空间中。  
  
 示例：  
  
```  
SELECT SqlServer.LEN(c.EmailAddress) As EmailLen FROM   
    AdventureWorksEntities.Contact AS c WHERE   
    c.ContactID BETWEEN 10 AND 12  
```  
  
 输出：  
  
|EmailLen|  
|--------------|  
|27|  
|27|  
|26|  
  
## 命名空间  
 [USING](../../../../../../docs/framework/data/adonet/ef/language-reference/using-entity-sql.md) 指定查询表达式中使用的命名空间。  
  
 示例：  
  
```  
using SqlServer; LOWER('AA');  
```  
  
 输出：  
  
|值|  
|-------|  
|aa|  
  
## 分页  
 可通过对 [ORDER BY](../../../../../../docs/framework/data/adonet/ef/language-reference/order-by-entity-sql.md) 子句声明 [SKIP](../../../../../../docs/framework/data/adonet/ef/language-reference/skip-entity-sql.md) 和 [LIMIT](../../../../../../docs/framework/data/adonet/ef/language-reference/limit-entity-sql.md) 子子句来表示分页。  
  
 示例：  
  
```  
SELECT c.ContactID as ID, c.LastName as Name FROM   
    AdventureWorks.Contact AS c ORDER BY c.ContactID SKIP 9 LIMIT 3;  
```  
  
 输出：  
  
|ID|名称|  
|--------|--------|  
|10|Adina|  
|11|Agcaoili|  
|12|Aguilar|  
  
## 分组  
 [GROUPING BY](../../../../../../docs/framework/data/adonet/ef/language-reference/group-by-entity-sql.md) 指定查询 \([SELECT](../../../../../../docs/framework/data/adonet/ef/language-reference/select-entity-sql.md)\) 表达式返回的对象要分成的组。  
  
 示例：  
  
```  
SELECT VALUE name FROM AdventureWorksEntities.Product as P   
    GROUP BY P.Name HAVING MAX(P.ListPrice) > 5  
```  
  
 输出：  
  
|name|  
|----------|  
|LL Mountain Seat Assembly|  
|ML Mountain Seat Assembly|  
|HL Mountain Seat Assembly|  
|...|  
  
## 导航  
 关系导航运算符用于导航从一个实体（起始端）到另一个实体（结束端）的关系。  [NAVIGATE](../../../../../../docs/framework/data/adonet/ef/language-reference/navigate-entity-sql.md) 接受限定为 \<命名空间\>.\<关系类型名称\> 的关系类型。  如果结束端的基数为 1，导航将返回 Ref\<T\>。  如果结束端的基数为 n，将返回 Collection\<Ref\<T\>\>。  
  
 示例：  
  
```  
SELECT a.AddressID, (SELECT VALUE DEREF(v) FROM   
    NAVIGATE(a, AdventureWorksModel.FK_SalesOrderHeader_Address_BillToAddressID) AS v)   
    FROM AdventureWorksEntities.Address AS a  
```  
  
 输出：  
  
|AddressID|  
|---------------|  
|1|  
|2|  
|3|  
|...|  
  
## SELECT VALUE 和 SELECT  
  
### SELECT VALUE  
 [!INCLUDE[esql](../../../../../../includes/esql-md.md)] 提供了 SELECT VALUE 子句以跳过隐式行构造。  SELECT VALUE 子句中只能指定一项。  在使用这样的子句时，将不会对 SELECT 子句中的项构造行包装器，并且可生成所要形状的集合，例如：`SELECT VALUE a`。  
  
 示例：  
  
```  
SELECT VALUE p.Name FROM AdventureWorksEntities.Product as p  
```  
  
 输出：  
  
|名称|  
|--------|  
|Adjustable Race|  
|All\-Purpose Bike Stand|  
|AWC Logo Cap|  
|...|  
  
### SELECT  
 [!INCLUDE[esql](../../../../../../includes/esql-md.md)] 还提供了用于构造任意行的行构造函数。  SELECT 接受投影中的一个或多个元素，并生成含有字段的数据记录，例如：`SELECT a, b, c`。  
  
 示例：  
  
 SELECT p.Name, p.ProductID FROM AdventureWorksEntities.Product as p Output:  
  
|名称|ProductID|  
|--------|---------------|  
|Adjustable Race|1|  
|All\-Purpose Bike Stand|879|  
|AWC Logo Cap|712|  
|...|...|  
  
## CASE 表达式  
 [case 表达式](../../../../../../docs/framework/data/adonet/ef/language-reference/case-entity-sql.md)计算一组布尔表达式的值以确定结果。  
  
 示例：  
  
```  
CASE WHEN AVG({25,12,11}) < 100 THEN TRUE ELSE FALSE END  
```  
  
 输出：  
  
|值|  
|-------|  
|TRUE|  
  
## 请参阅  
 [Entity SQL 参考](../../../../../../docs/framework/data/adonet/ef/language-reference/entity-sql-reference.md)   
 [Entity SQL 概述](../../../../../../docs/framework/data/adonet/ef/language-reference/entity-sql-overview.md)