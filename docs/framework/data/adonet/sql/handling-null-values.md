---
title: "处理 Null 值 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-ado"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: f18b288f-b265-4bbe-957f-c6833c0645ef
caps.latest.revision: 6
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 6
---
# 处理 Null 值
在列中的值未知或缺失时，在关系数据库中使用空值。  空既不是空字符串（对于 character 或 datetime 数据类型），也不是零值（对于 numeric 数据类型）。  ANSI SQL\-92 规范规定，空必须对于所有数据类型均相同，以便以一致的方式处理所有空。  <xref:System.Data.SqlTypes> 命名空间通过实现 <xref:System.Data.SqlTypes.INullable> 接口，提供空语义。  <xref:System.Data.SqlTypes> 中的每种数据类型都有其自己的 `IsNull` 属性和可分配给该数据类型的实例的 `Null` 值。  
  
> [!NOTE]
>  .NET Framework 2.0 版引入了对可以为 null 的类型的支持，这允许程序员扩展值类型以表示基础类型的所有值。  这些 CLR 可以为 null 的类型表示 <xref:System.Nullable> 结构的一个实例。  当值类型为装箱和未装箱，从而增强与对象类型的兼容性时，这个功能特别有用。  CLR 可以为 null 的类型不用于存储数据库 null 值，因为 ANSI SQL null 值的行为与 `null` 引用（或 Visual Basic 中的 `Nothing`）不同。  为了使用数据库 ANSI SQL null 值，请使用 <xref:System.Data.SqlTypes> null 值而不使用 <xref:System.Nullable>。  有关在 Visual Basic 中使用 CLR 可以为 null 的类型的更多信息，请参见[可以为 Null 的值类型](../Topic/Nullable%20Value%20Types%20\(Visual%20Basic\).md)，有关 C\# 的更多信息，请参见[使用可以为 null 的类型](../Topic/Using%20Nullable%20Types%20\(C%23%20Programming%20Guide\).md)。  
  
## 空和三值逻辑  
 在列定义中允许空值将三值逻辑引入您的应用程序。  可以将比较计算为以下三个条件之一：  
  
-   True  
  
-   False  
  
-   未知  
  
 因为空被视作未知，所以，对两个空值进行彼此比较，其结果不被视为相等。  在使用算术运算符的表达式中，如果任何操作数为空，结果也为空。  
  
## 空和 SqlBoolean  
 任意 <xref:System.Data.SqlTypes> 之间的比较都将返回 <xref:System.Data.SqlTypes.SqlBoolean>。  每个 `SqlType` 的 `IsNull` 函数都可返回一个 <xref:System.Data.SqlTypes.SqlBoolean> 并可用于检查 null 值。  下面的真值表显示在存在空值时 AND、OR 和 NOT 这三个运算符的计算方式。  （T\=true，F\=false，U\=unknown 或空。）  
  
 ![真值表](../../../../../docs/framework/data/adonet/sql/media/truthtable-bpuedev11.png "TruthTable\_bpuedev11")  
  
### 理解 ANSI\_NULLS 选项  
 <xref:System.Data.SqlTypes> 提供与在 SQL Server 中设置 ANSI\_NULLS 选项时相同的语义。  如果上述任何操作数或参数为空，则所有算术运算符（\+、\-、\*、\/、%）、位运算符（~、&、&#124;）和大多数函数都返回空，只有属性 `IsNull` 除外。  
  
 ANSI SQL\-92 标准不支持 WHERE 子句中的 *columnName* \= NULL。  在 SQL Server 中，ANSI\_NULLS 选项既控制数据库中的默认可空性，也控制对空值的比较计算。  如果启用 ANSI\_NULLS（这是默认设置），则在测试空值时在表达式中必须使用 IS NULL 运算符。  例如，在 ANSI\_NULLS 为 on 时，以下比较始终生成 unknown：  
  
```  
  
colname > NULL  
```  
  
 与包含空值的变量的比较也生成 unknown：  
  
```  
  
colname > @MyVariable  
```  
  
 使用 IS NULL 或 IS NOT NULL 谓词来测试是否有空值。  这可能会增加 WHERE 子句的复杂性。  例如，AdventureWorks 客户表中的 TerritoryID 列允许 null 值。  如果 SELECT 语句用于测试是否有空值以及测试其他内容，则它必须包含 IS NULL 谓词：  
  
```  
SELECT CustomerID, AccountNumber, TerritoryID  
FROM AdventureWorks.Sales.Customer  
WHERE TerritoryID IN (1, 2, 3)  
   OR TerritoryID IS NULL  
```  
  
 如果在 SQL Server 中将 ANSI\_NULLS 设置为 off，则可以创建使用等于运算符来比较空值的表达式。  但是，您无法阻止不同的连接为该连接设置空选项。  不管连接的 ANSI\_NULLS 设置如何，使用 IS NULL 测试是否有空值始终有效。  
  
 不支持在 `DataSet` 中将 ANSI\_NULLS 设置为 off，因为前者总是遵守 ANSI SQL\-92 标准来处理 <xref:System.Data.SqlTypes> 中的 null 值。  
  
## 赋予 Null 值  
 空值是特殊的值类型，并且其存储和赋值语义在不同类型系统和存储系统中是不同的。  `Dataset` 已设计为可与不同的类型和存储系统一起使用。  
  
 本节描述用于在不同类型系统中将空值赋给 <xref:System.Data.DataRow> 中的 <xref:System.Data.DataColumn> 的空语义。  
  
 `DBNull.Value`  
 此赋值对于任何类型的 `DataColumn` 都有效。  如果该类型实现 `INullable`，则会将 `DBNull.Value` 强制为相应强类型的 Null 值。  
  
 `SqlType.Null`  
 所有 <xref:System.Data.SqlTypes> 数据类型均实现 `INullable`。  如果可以使用隐式强制转换运算符将强类型的空值转换为该列的数据类型，则应该进行赋值。  否则，将引发无效强制转换异常。  
  
 `null`  
 如果“null”是给定 `DataColumn` 数据类型的合法值，则会将其强制为相应的 `DbNull.Value` 或与 `INullable` 类型关联的 `Null` \(`SqlType.Null`\)。  
  
 `derivedUdt.Null`  
 对于 UDT 列，null 值始终根据与 `DataColumn` 关联的类型来存储。  设想这样的情况：与 `DataColumn` 关联的 UDT 不实现 `INullable`，但其子类实现。  在这种情况下，如果分配了与派生类关联的强类型 null 值，则它被存储为非类型化的 `DbNull.Value`，因为空存储始终与 DataColumn 的数据类型一致。  
  
> [!NOTE]
>  `DataSet` 中当前不支持 `Nullable<T>` 或 <xref:System.Nullable> 结构。  
  
### 多列（行）赋值  
 `DataTable.Add`、`DataTable.LoadDataRow` 或其他接受 <xref:System.Data.DataRow.ItemArray%2A>（映射到行）的 API 会将“null”映射到 DataColumn 的默认值。  如果数组中的对象包含 `DbNull.Value` 或其强类型对应项，则上述规则同样适用。  
  
 此外，下面的规则适用于 `DataRow.["columnName"]` null 赋值的实例：  
  
1.  对于所有列，*默认值*值为 `DbNull.Value`，但强类型 null 列除外，强类型 null 列的默认值是相应的强类型 null 值。  
  
2.  在序列化为 XML 文件（如在“xsi:nil”中）期间，永远不写出空值。  
  
3.  在序列化为 XML 时始终写出所有非空值，包括默认值。  这与 XSD\/XML 语义不同。在 XSD\/XML 语义中，空值 \(xsi:nil\) 是显式的并且默认值是隐式的（如果在 XML 中不提供，则验证分析程序可以从关联的 XSD 架构获取它）。  对于 `DataTable`，反过来也成立：空值是隐式的，默认值是显式的。  
  
4.  对于从 XML 输入读取的行的所有缺少的列值，都赋予 NULL。  使用 <xref:System.Data.DataTable.NewRow%2A> 或类似方法创建的行被赋予 DataColumn 的默认值。  
  
5.  对于 `DbNull.Value` 和 `INullable.Null`，<xref:System.Data.DataRow.IsNull%2A> 方法均返回 `true`。  
  
## 赋予 Null 值  
 任何 <xref:System.Data.SqlTypes> 实例的默认值都是空。  
  
 <xref:System.Data.SqlTypes> 中的 null 值是类型特定的，不能由单个值（如 `DbNull`）来表示。  使用 `IsNull` 属性可以检查是否有空值。  
  
 空值可被赋给 <xref:System.Data.DataColumn>，如以下代码示例所示。  您可以将空值直接赋给 `SqlTypes` 变量，而不会引发异常。  
  
### 示例  
 以下代码示例创建一个 <xref:System.Data.DataTable>，它具有两列，分别定义为 <xref:System.Data.SqlTypes.SqlInt32> 和 <xref:System.Data.SqlTypes.SqlString>。  该代码添加一行已知值和一行空值，然后循环访问 <xref:System.Data.DataTable>，将这些值赋给变量并在控制台窗口中显示输出。  
  
 [!code-csharp[DataWorks SqlTypes.IsNull#1](../../../../../samples/snippets/csharp/VS_Snippets_ADO.NET/DataWorks SqlTypes.IsNull/CS/source.cs#1)]
 [!code-vb[DataWorks SqlTypes.IsNull#1](../../../../../samples/snippets/visualbasic/VS_Snippets_ADO.NET/DataWorks SqlTypes.IsNull/VB/source.vb#1)]  
  
 此示例显示以下结果：  
  
```  
isColumnNull=False, ID=123, Description=Side Mirror  
isColumnNull=True, ID=Null, Description=Null  
```  
  
## 将空值与 SqlTypes 和 CLR 类型进行比较  
 比较 null 值时，必须了解 `Equals` 方法在 <xref:System.Data.SqlTypes> 中计算 null 值的方式与处理 CLR 类型的方式之间的差别。  所有 <xref:System.Data.SqlTypes> `Equals` 方法都使用数据库语义计算 null 值：如果其中任何一个值为空或两个值都为空，则比较结果将为空。  另一方面，如果两个 <xref:System.Data.SqlTypes> 都为 null，则对其使用 CLR `Equals` 方法将生成 true。  这反映了使用实例方法（如 CLR `String.Equals` 方法）和使用静态\/共享方法 `SqlString.Equals` 之间的差别。  
  
 下面的示例演示为 `SqlString.Equals` 方法和 `String.Equals` 方法传递一对 null 值，然后传递一对空字符串时，这两种方法生成的结果之间存在的差异。  
  
 [!code-csharp[DataWorks SqlTypes.CompareNulls#1](../../../../../samples/snippets/csharp/VS_Snippets_ADO.NET/DataWorks SqlTypes.CompareNulls/CS/source.cs#1)]
 [!code-vb[DataWorks SqlTypes.CompareNulls#1](../../../../../samples/snippets/visualbasic/VS_Snippets_ADO.NET/DataWorks SqlTypes.CompareNulls/VB/source.vb#1)]  
  
 此代码生成以下输出内容：  
  
```  
SqlString.Equals shared/static method:  
  Two nulls=Null  
  
String.Equals instance method:  
  Two nulls=True  
  
SqlString.Equals shared/static method:  
  Two empty strings=True  
  
String.Equals instance method:  
  Two empty strings=True   
```  
  
## 请参阅  
 [SQL Server 数据类型和 ADO.NET](../../../../../docs/framework/data/adonet/sql/sql-server-data-types.md)   
 [ADO.NET 托管提供程序和数据集开发人员中心](http://go.microsoft.com/fwlink/?LinkId=217917)