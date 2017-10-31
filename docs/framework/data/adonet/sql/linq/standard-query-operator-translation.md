---
title: "标准查询运算符转换 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-ado"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: a60c30fa-1e68-45fe-b984-f6abb9ede40e
caps.latest.revision: 2
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 2
---
# 标准查询运算符转换
[!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] 将标准查询运算符转换为 SQL 命令。  数据库的查询处理器决定了 SQL 转换的执行语义。  
  
 标准查询运算符是针对序列定义的。  序列是有序的并依赖于该序列每个元素的引用标识。  有关详细信息，请参阅[Standard Query Operators Overview](../../../../../../ocs/visual-basic/programming-guide/concepts/linq/standard-query-operators-overview.md)。  
  
 SQL 主要处理无序值集。  排序通常是显式声明的后续处理操作，应用于查询的最终结果而不是中间结果。  标识由值定义。  因此，将 SQL 查询理解为处理多重集（包）而非集合。  
  
 以下各段介绍了标准查询运算符与其针对用于 [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] 的 SQL Server 提供程序的 SQL 转换结果之间的差异。  
  
## 运算符支持  
  
### Concat  
 <xref:System.Linq.Enumerable.Concat%2A> 方法是为有序多重集定义的，其中接收方的顺序与参数的顺序相同。  <xref:System.Linq.Enumerable.Concat%2A> 的作用等效于对多重集执行 `UNION ALL`，紧接着再执行常见排序。  
  
 在产生结果前，最后一步是在 SQL 中排序。  <xref:System.Linq.Enumerable.Concat%2A> 不保留其参数的顺序。  为确保顺序合适，您必须显式对 <xref:System.Linq.Enumerable.Concat%2A> 的结果进行排序。  
  
### Intersect、Except、Union  
 <xref:System.Linq.Enumerable.Intersect%2A> 和 <xref:System.Linq.Enumerable.Except%2A> 方法仅对集合而言是定义完善的。  针对多重集的语义尚未定义。  
  
 <xref:System.Linq.Enumerable.Union%2A> 方法是为多重集定义的，定义为多重集的无序串联（实际上是 SQL 中的 UNION ALL 子句的执行结果）。  
  
### Take、Skip  
 <xref:System.Linq.Enumerable.Take%2A> 和 <xref:System.Linq.Enumerable.Skip%2A> 方法仅对有序集而言是定义完善的。  未定义针对无序集或多重集的语义。  
  
> [!NOTE]
>  <xref:System.Linq.Enumerable.Take%2A> 和 <xref:System.Linq.Enumerable.Skip%2A> 用在针对 SQL Server 2000 的查询中时存在一定的限制。  有关更多信息，请参见[疑难解答](../../../../../../docs/framework/data/adonet/sql/linq/troubleshooting.md) 中的“SQL Server 2000 中的 Skip 和 Take 异常”项。  
  
 由于 SQL 中的排序存在限制，因此 [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] 会设法将这些方法的参数的排序操作移到相应方法的结果中进行。  例如，请考虑下面这个 [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] 查询：  
  
 [!code-csharp[DLinqSQOTranslation#1](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqSQOTranslation/cs/Program.cs#1)]
 [!code-vb[DLinqSQOTranslation#1](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqSQOTranslation/vb/Module1.vb#1)]  
  
 为此代码生成的 SQL 会将排序移到结尾，如下所示：  
  
```  
SELECT TOP 1 [t0].[CustomerID], [t0].[CompanyName],  
FROM [Customers] AS [t0]  
WHERE (NOT (EXISTS(  
    SELECT NULL AS [EMPTY]  
    FROM (  
        SELECT TOP 1 [t1].[CustomerID]  
        FROM [Customers] AS [t1]  
        WHERE [t1].[City] = @p0  
        ORDER BY [t1].[CustomerID]  
        ) AS [t2]  
    WHERE [t0].[CustomerID] = [t2].[CustomerID]  
    ))) AND ([t0].[City] = @p1)  
ORDER BY [t0].[CustomerID]  
```  
  
 显而易见，当 <xref:System.Linq.Enumerable.Take%2A> 和 <xref:System.Linq.Enumerable.Skip%2A> 链接在一起时，所有指定的排序必须一致。  否则，结果将是不确定的。  
  
 对于非负的、基于标准查询运算符规范的整型常量参数，<xref:System.Linq.Enumerable.Take%2A> 和 <xref:System.Linq.Enumerable.Skip%2A> 都是定义完善的。  
  
### 不进行转换的运算符  
 [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] 不对以下方法进行转换。  最常见的原因是无序多重集与序列之间存在差异。  
  
|运算符|阐释|  
|---------|--------|  
|<xref:System.Linq.Enumerable.TakeWhile%2A>, <xref:System.Linq.Enumerable.SkipWhile%2A>|SQL 查询是对多重集执行的，而不是对序列执行的。  `ORDER BY` 必须是最后一个应用于结果的子句。  因此，不存在适用于这两个方法的通用转换。|  
|<xref:System.Linq.Enumerable.Reverse%2A>|此方法的转换对于有序集而言是可行的，但目前 [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] 未对它进行转换。|  
|<xref:System.Linq.Enumerable.Last%2A>, <xref:System.Linq.Enumerable.LastOrDefault%2A>|这些方法的转换对于有序集而言是可行的，但目前 [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] 未对它们进行转换。|  
|<xref:System.Linq.Enumerable.ElementAt%2A>, <xref:System.Linq.Enumerable.ElementAtOrDefault%2A>|SQL 查询是对多重集执行的，而不是对可建立索引的序列执行的。|  
|<xref:System.Linq.Enumerable.DefaultIfEmpty%2A>（带默认参数的重载）|一般而言，无法为任意元组指定默认值。  在某些情况下，可以通过外部联接为元组指定 Null 值。|  
  
## 表达式转换  
  
### Null 语义  
 [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] 不会将 null 比较语义施加在 SQL 上。  比较运算符在语法上被转换为其 SQL 等效项。  因此，该语义反映了由服务器或连接设置定义的 SQL 语义。  例如，在默认的 SQL Server 设置下，两个 null 值被视为不相等，但您可以更改这些设置以更改语义。  [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] 在转换查询时不考虑服务器设置。  
  
 对文本型 null 的比较被转换为相应的 SQL 版本（`is null` 或 `is not null`）。  
  
 排序规则中的 `null` 值是由 SQL Server 定义的。  [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] 不会更改排序规则。  
  
### 聚合  
 使用标准查询运算符的聚合方法 <xref:System.Linq.Enumerable.Sum%2A> 计算空序列或只包含 null 的序列时，所得结果为零。  在 [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] 中，SQL 的语义保持不变，并且使用 <xref:System.Linq.Enumerable.Sum%2A> 计算空序列或只包含 null 的序列时，所得结果为 `null` 而非零。  
  
 针对中间结果的 SQL 限制适用于 [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] 中的聚合。  32 位整型量的 <xref:System.Linq.Enumerable.Sum%2A> 不是使用 64 位结果计算的。在 [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] 转换 <xref:System.Linq.Enumerable.Sum%2A> 时，可能会发生溢出，即使对于内存中的对应序列，标准查询运算符的实现不会造成溢出，仍存在这种可能性。  
  
 同样，使用经 [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] 转换后的 <xref:System.Linq.Enumerable.Average%2A> 计算整数值时，所得结果的数据类型为 `integer`，而非 `double`。  
  
### 实体参数  
 [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] 允许在 <xref:System.Linq.Enumerable.GroupBy%2A> 和 <xref:System.Linq.Enumerable.OrderBy%2A> 方法中使用实体类型。  在这些运算符的转换过程中，使用一种类型的参数被视为等效于指定该类型的所有成员。  例如，下面的代码是等效的：  
  
 [!code-csharp[DLinqSQOTranslation#2](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqSQOTranslation/cs/Program.cs#2)]
 [!code-vb[DLinqSQOTranslation#2](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqSQOTranslation/vb/Module1.vb#2)]  
  
### 可相等\/可比较参数  
 在以下方法的实现中，要求参数相等：  
  
 <xref:System.Linq.Enumerable.Contains%2A>  
  
 <xref:System.Linq.Enumerable.Skip%2A>  
  
 <xref:System.Linq.Enumerable.Union%2A>  
  
 <xref:System.Linq.Enumerable.Intersect%2A>  
  
 <xref:System.Linq.Enumerable.Except%2A>  
  
 [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] 支持对平参数执行相等和比较运算，但对作为序列或包含序列的参数则不支持这两种运算。  平参数是一种能映射到 SQL 行的类型。  可以静态方式确定不包含序列的一个或多个实体类型的投影被视为平参数。  
  
 以下是平参数的一些示例：  
  
 [!code-csharp[DLinqSQOTranslation#3](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqSQOTranslation/cs/Program.cs#3)]
 [!code-vb[DLinqSQOTranslation#3](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqSQOTranslation/vb/Module1.vb#3)]  
  
 以下是非平（分层）参数的一些示例。  
  
 [!code-csharp[DLinqSQOTranslation#4](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqSQOTranslation/cs/Program.cs#4)]
 [!code-vb[DLinqSQOTranslation#4](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqSQOTranslation/vb/Module1.vb#4)]  
  
### Visual Basic 函数转换  
 Visual Basic 编译器使用的以下 Helper 函数转换为对应的 SQL 运算符和函数：  
  
 `CompareString`  
  
 `DateTime.Compare`  
  
 `Decimal.Compare`  
  
 `IIf (in Microsoft.VisualBasic.Interaction)`  
  
 转换方法：  
  
|||||  
|-|-|-|-|  
|ToBoolean|ToSByte|ToByte|ToChar|  
|ToCharArrayRankOne|ToDate|ToDecimal|ToDouble|  
|ToInteger|ToUInteger|ToLong|ToULong|  
|ToShort|ToUShort|ToSingle|ToString|  
  
## 层次结构支持  
  
### 继承映射限制  
 有关详细信息，请参阅[如何：映射继承层次结构](../../../../../../docs/framework/data/adonet/sql/linq/how-to-map-inheritance-hierarchies.md)。  
  
### 查询中的继承  
 仅支持在投影中使用 C\# 强制转换。  在其他地方使用的强制转换不会进行转换且会被忽略。  除 SQL 函数名以外，SQL 确实仅执行公共语言运行库 \(CLR\) <xref:System.Convert> 的等效项。  也就是说，SQL 可以将一种类型的值更改为另一类型。  CLR 强制转换不存在等效项，这是因为不存在这样的概念：重新解释与另一类型的位相同的位。  正因如此，C\# 强制转换只能在本地使用。  它无法以远程方式使用。  
  
 运算符 `is` 和 `as` 以及 `GetType` 方法并不限于 `Select` 运算符。  它们还可以用在其他查询运算符中。  
  
## SQL Server 2008 支持  
 从 .NET Framework 3.5 SP1 开始，LINQ to SQL 支持映射到在 SQL Server 2008 中引入的新的日期和时间类型。  但是，对于您可以在操作映射到这些新类型的值时使用的 LINQ to SQL 查询运算符有一些限制。  
  
### 不支持的查询运算符  
 映射到新的 SQL Server 日期和时间类型的值不支持下面的查询运算符：`DATETIME2`、`DATE`、`TIME` 和 `DATETIMEOFFSET`。  
  
-   `Aggregate`  
  
-   `Average`  
  
-   `LastOrDefault`  
  
-   `OfType`  
  
-   `Sum`  
  
 有关映射到这些 SQL Server 日期和时间类型的更多信息，请参见 [SQL\-CLR 类型映射](../../../../../../docs/framework/data/adonet/sql/linq/sql-clr-type-mapping.md)。  
  
## SQL Server 2005 支持  
 [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] 不支持以下 SQL Server 2005 功能：  
  
-   为 SQL CLR 编写的存储过程。  
  
-   用户定义的类型。  
  
-   XML 查询功能。  
  
## SQL Server 2000 支持  
 以下 [!INCLUDE[ss2k](../../../../../../includes/ss2k-md.md)] 局限性（与 [!INCLUDE[sqprsqext](../../../../../../includes/sqprsqext-md.md)] 相比）会影响 [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] 支持。  
  
### Cross Apply 和 Outer Apply 运算符  
 这些运算符在 [!INCLUDE[ss2k](../../../../../../includes/ss2k-md.md)] 中不可用。  [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] 设法通过一系列的重写来将它们替换为适当的联接。  
  
 `Cross Apply` 和 `Outer Apply` 是为关系导航生成的。  可以进行这种重写的查询集定义不完善。  因此，[!INCLUDE[ss2k](../../../../../../includes/ss2k-md.md)] 支持的最小查询集是不涉及关系导航的集合。  
  
### text \/ ntext  
 在 [!INCLUDE[sqprsqext](../../../../../../includes/sqprsqext-md.md)] 支持的针对 `varchar(max)`\/`nvarchar(max)` 的某些查询操作中，不能使用 `text`\/`ntext` 数据类型。  
  
 不存在解决此限制的方法。  具体而言，您不能对包含映射到 `text` 或 `ntext` 列的成员的任何结果使用 `Distinct()`。  
  
### 由嵌套查询触发的行为  
 [!INCLUDE[ss2k](../../../../../../includes/ss2k-md.md)]（一直到 SP4）联编程序具有由嵌套查询触发的一些特性。  触发这些特性的 SQL 查询集定义不完善。  因此，您不能定义可能会引发 SQL Server 异常的 [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] 查询集。  
  
### Skip 和 Take 运算符  
 <xref:System.Linq.Enumerable.Take%2A> 和 <xref:System.Linq.Enumerable.Skip%2A> 用在针对 [!INCLUDE[ss2k](../../../../../../includes/ss2k-md.md)] 的查询中时存在一定的限制。  有关更多信息，请参见[疑难解答](../../../../../../docs/framework/data/adonet/sql/linq/troubleshooting.md) 中的“SQL Server 2000 中的 Skip 和 Take 异常”项。  
  
## 对象具体化  
 具体化过程用一个或多个 SQL 查询返回的行创建 CLR 对象。  
  
-   以下调用作为具体化过程的一部分在本地执行：  
  
    -   构造函数  
  
    -   投影中的 `ToString` 方法  
  
    -   投影中的类型强制转换  
  
-   紧跟 <xref:System.Linq.Enumerable.AsEnumerable%2A> 方法之后的方法在本地执行。  此方法不会导致直接执行。  
  
-   您可以将 `struct` 用作查询结果的返回类型或结果类型的成员。  实体需要变成类。  匿名类型具体化为类的实例，但命名结构（非实体）可在投影中使用。  
  
-   查询结果的返回类型的成员可以为 <xref:System.Linq.IQueryable%601> 类型。  它具体化为本地集合。  
  
-   以下方法导致直接具体化应用这些方法的序列：  
  
    -   <xref:System.Linq.Enumerable.ToList%2A>  
  
    -   <xref:System.Linq.Enumerable.ToDictionary%2A>  
  
    -   <xref:System.Linq.Enumerable.ToArray%2A>  
  
## 请参阅  
 [参考](../../../../../../docs/framework/data/adonet/sql/linq/reference.md)   
 [返回或跳过序列中的元素](../../../../../../docs/framework/data/adonet/sql/linq/return-or-skip-elements-in-a-sequence.md)   
 [串联两个序列](../../../../../../docs/framework/data/adonet/sql/linq/concatenate-two-sequences.md)   
 [返回两个序列之间的差集](../../../../../../docs/framework/data/adonet/sql/linq/return-the-set-difference-between-two-sequences.md)   
 [返回两个序列的交集](../../../../../../docs/framework/data/adonet/sql/linq/return-the-set-intersection-of-two-sequences.md)   
 [返回两个序列的并集](../../../../../../docs/framework/data/adonet/sql/linq/return-the-set-union-of-two-sequences.md)