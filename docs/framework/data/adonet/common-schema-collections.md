---
title: "通用架构集合 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-ado"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 50127ced-2ac8-4d7a-9cd1-5c98c655ff03
caps.latest.revision: 3
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 3
---
# 通用架构集合
通用架构集合是每个 .NET Framework 托管提供程序均实现的架构集合。  可以通过调用没有参数或包含架构集合名称“MetaDataCollections”的 **GetSchema** 方法来查询由 .NET Framework 管理的提供程序，以确定支持的架构集合列表。  此时将返回 <xref:System.Data.DataTable>，包含支持的架构集合列表、每个架构集合支持的限制数以及所使用的标识符部分数。  这些集合描述所有必需的列。  提供程序可以根据需要随意添加其他列。  例如，`SqlClient` 和 `OracleClient` 向限制集合中添加 ParameterName。  
  
 如果提供程序无法确定所需列的值，将返回空值。  
  
 有关使用 **GetSchema** 方法的更多信息，请参见[GetSchema 和架构集合](../../../../docs/framework/data/adonet/getschema-and-schema-collections.md)。  
  
## MetaDataCollections  
 此架构集合为当前用于连接到数据库上的 .NET Framework 管理的应用程序公开所支持的所有架构集合的有关信息。  
  
|列名|数据类型|描述|  
|--------|----------|--------|  
|CollectionName|string|为返回集合传递给 **GetSchema** 方法的集合名称。|  
|NumberOfRestriction|int|可以为集合指定的限制数。|  
|NumberOfIdentifierParts|int|复合标识符\/数据库对象名称中的部分数。  例如，在 SQL Server 中，表为 3，列为 4。  在 Oracle 中，表为 2，列为 3。|  
  
## DataSourceInformation  
 此架构集合为 .NET Framework 管理的提供程序当前连接到的数据源公开有关信息。  
  
|列名|数据类型|描述|  
|--------|----------|--------|  
|CompositeIdentifierSeparatorPattern|string|匹配复合标识符中的复合分隔符的正则表达式。  例如：“\\.”（针对 SQL Server）或“@&#124;\\.”（针对 Oracle）。<br /><br /> 通常对数据库对象名使用复合标识符，例如：pubs.dbo.authors or pubs@dbo.authors。<br /><br /> 对于 SQL Server，使用正则表达式“\\.”。  对于 OracleClient，使用“@&#124;\\.”。<br /><br /> 对于 ODBC，使用 Catalog\_name\_seperator。<br /><br /> 对于 OLE DB，使用 DBLITERAL\_CATALOG\_SEPARATOR 或 DBLITERAL\_SCHEMA\_SEPARATOR。|  
|DataSourceProductName|string|通过提供程序访问的产品名称，例如“Oracle”或“SQLServer”。|  
|DataSourceProductVersion|string|指示提供程序访问的产品版本，采用数据源本机格式，而不是 Microsoft 格式。<br /><br /> 有时，DataSourceProductVersion 和 DataSourceProductVersionNormalized 的值相同。  对于 OLE DB 和 ODBC，这两个值始终相同，因为它们映射到基础本机 API 中相同的函数调用。|  
|DataSourceProductVersionNormalized|string|数据源的标准化版本，以便可以使用 `String.Compare()` 进行比较。  对于提供程序的所有版本，此值的格式一致，以避免版本 10 排序在版本 1 和版本 2 之间。<br /><br /> 例如，Oracle 提供程序的标准化版本使用“nn.  nn.  nn.  nn.  nn”格式，这样，Oracle 8i 数据源将返回“08.01.07.04.01”。  SQL Server 使用典型的 Microsoft“nn.  nn.  nnnn”格式。<br /><br /> 有时，DataSourceProductVersion 和 DataSourceProductVersionNormalized 的值相同。  对于 OLE DB 和 ODBC，这两个值始终相同，因为它们映射到基础本机 API 中相同的函数调用。|  
|GroupByBehavior|<xref:System.Data.Common.GroupByBehavior>|指定 GROUP BY 子句中的列与选择列表中的非聚合列之间的关系。|  
|IdentifierPattern|string|匹配标识符并且包含标识符的匹配值的正则表达式。  例如“\[A\-Za\-z0\-9\_\#$\]”。|  
|IdentifierCase|<xref:System.Data.Common.IdentifierCase>|表示未加引号的标识符是否区分大小写。|  
|OrderByColumnsInSelect|bool|指定 ORDER BY 子句中的列是否必须在选择列表中。  如果值为 true，表示这些列必须在选择列表中，如果值为 false，表示这些列不必在选择列表中。|  
|ParameterMarkerFormat|string|表示如何格式化参数的格式化字符串。<br /><br /> 如果数据源不支持命名的参数，此字符串中的第一个占位符应是格式化参数名的位置。<br /><br /> 例如，如果数据源期望参数以“:”为前缀，此字符串将为“:{0}”。  在使用参数名“p1”格式化此字符串时，生成的字符串为“:p1”。<br /><br /> 如果数据源期望参数以“@”为前缀，但是名称中已包含该符号，此字符串将为“{0}”，格式化名为“@p1”的参数的结果将只是“@p1”。<br /><br /> 如果数据源不期望使用命名参数，而期望使用‘?’字符，格式字符串可以只指定为‘?’，这样将忽略参数名。  对于 OLE DB，将返回‘?’。|  
|ParameterMarkerPattern|string|匹配参数标记的正则表达式。  该表达式将包含参数名的匹配值（如果有）。<br /><br /> 例如，如果受支持命名参数包含将包括在参数名中的“@”引导字符，则为：“\(@\[A\-Za\-z0\-9\_$\#\]\*\)”。<br /><br /> 但是，如果受支持命名参数以“:”作为引导字符，并且该字符并非参数名的一部分，则为：“:\(\[A\-Za\-z0\-9\_$\#\]\*\)”。<br /><br /> 当然，如果数据源不支持命名参数，将只为“?”。|  
|ParameterNameMaxLength|int|参数名的最大长度（字符数）。  Visual Studio 期望如果支持参数名，最大长度的最小值为 30 个字符。<br /><br /> 如果数据源不支持命名参数，此属性将返回零。|  
|ParameterNamePattern|string|匹配有效参数名的正则表达式。  对于参数名可以使用的字符，不同的数据源采用不同的规则。<br /><br /> Visual Studio 期望如果支持参数名，字符“\\p{Lu}\\p{Ll}\\p{Lt}\\p{Lm}\\p{Lo}\\p{Nl}\\p{Nd}”是参数名支持的最小有效字符集。|  
|QuotedIdentifierPattern|string|匹配加引号的标识符并且包含标识符本身（不加引号）的匹配值的正则表达式。  例如，如果数据源使用双引号标识加引号的标识符，将为“\(\(\[^\\"\]&#124;\\"\\"\)\*\)”。|  
|QuotedIdentifierCase|<xref:System.Data.Common.IdentifierCase>|表示加引号的标识符是否区分大小写。|  
|StatementSeparatorPattern|string|匹配语句分隔符的正则表达式。|  
|StringLiteralPattern|string|匹配字符串文本并且包含文本本身的匹配值的正则表达式。  例如，如果数据源使用单引号标识字符串，将为“\('\(\[^'\]&#124;''\)\*'\)”。|  
|SupportedJoinOperators|<xref:System.Data.Common.SupportedJoinOperators>|指定数据源支持的 SQL join 语句类型。|  
  
## DataTypes  
 此架构集合为 .NET Framework 管理的提供程序当前连接到的数据库公开所支持的数据类型的有关信息。  
  
|列名|数据类型|描述|  
|--------|----------|--------|  
|TypeName|string|提供程序特定的数据类型名称。|  
|ProviderDbType|int|在指定参数类型时应使用的提供程序特定的类型值。  例如 SqlDbType.Money 或 OracleType.Blob。|  
|ColumnSize|long|非数值列或参数的长度是指提供程序为此类型定义的最大值或长度。<br /><br /> 对于字符数据，此值是指最大值或定义长度，单位由数据源定义。  对于某些字符数据类型，Oracle 的观念是先指定长度，然后指定实际存储大小。  对于 Oracle，此值仅定义长度（单位）。<br /><br /> 对于日期时间数据类型，此值是指字符串表示形式的长度（假定小数秒元素允许的最大精度）。<br /><br /> 如果数据类型为数值，则是数据类型的最大精度的上限。|  
|CreateFormat|string|格式化字符串，表示如何将此列添加到数据定义语句中，例如 CREATE TABLE。  CreateParameter 数组中的每个元素应通过格式字符串中的“参数标记”表示。<br /><br /> 例如，SQL 数据类型 DECIMAL 需要精度和小数位数。  在此情况下，格式字符串将为“DECIMAL\({0},{1}\)”。|  
|CreateParameters|string|创建此数据类型的列时必须指定的创建参数。  每个创建参数按照要提供的顺序在该字符串中列出，使用逗号分隔。<br /><br /> 例如，SQL 数据类型 DECIMAL 需要精度和小数位数。  在此情况下，创建参数应包含字符串“精度, 小数位数”。<br /><br /> 在创建精度为 10、小数位数为 2 的 DECIMAL 列的文本命令中，CreateFormat 列的值可能为 DECIMAL\({0},{1}\)，完整的类型说明将为 DECIMAL\(10,2\)。|  
|数据类型|string|数据类型的 .NET Framework 类型的名称。|  
|IsAutoincrementable|bool|true — 此数据类型的值可能是自动递增的。<br /><br /> false — 此数据类型的值可能不是自动递增的。<br /><br /> 注意，这只是表示此数据类型的列可能是自动递增的，而不是表示所有此类型的列都是自动递增的。|  
|IsBestMatch|bool|true — 数据类型是数据存储中的所有数据类型与 DataType 列中的值指示的 .NET Framework 数据类型之间的最佳匹配。<br /><br /> false — 数据类型不是最佳匹配。<br /><br /> 对于 DataType 列的值相同的每组行，IsBestMatch 列只在一行中设置为 true。|  
|IsCaseSensitive|bool|true — 数据类型是字符类型，并且区分大小写。<br /><br /> false — 数据类型不是字符类型，或不区分大小写。|  
|IsFixedLength|bool|true — 通过数据定义语言 \(DDL\) 创建的此数据类型的列将为固定长度。<br /><br /> false — 通过 DDL 创建的此数据类型的列将为可变长度。<br /><br /> DBNull.Value — 不知道提供程序将此字段与固定长度列还是可变程度列映射。|  
|IsFixedPrecisionScale|bool|true — 数据类型具有固定的精度和小数位数。<br /><br /> false — 数据类型没有固定的精度和小数位数。|  
|IsLong|bool|true — 数据类型包含的数据很长；很长数据的定义是提供程序特定的。<br /><br /> false — 数据类型未包含很长的数据。|  
|IsNullable|bool|true — 数据类型可为空。<br /><br /> false — 数据类型不可为空。<br /><br /> DBNull.Value — 不知道数据类型是否可为空。|  
|IsSearchable|bool|true — 数据类型可以在包含除 LIKE 谓词以外的任何运算符的 WHERE 子句中使用。<br /><br /> false — 数据类型不能在包含除 LIKE 谓词以外的任何运算符的 WHERE 子句中使用。|  
|IsSearchableWithLike|bool|true — 数据类型可以与 LIKE 谓词一起使用。<br /><br /> false — 数据类型不能与 LIKE 谓词一起使用。|  
|IsUnsigned|bool|true — 数据类型无符号。<br /><br /> false — 数据类型有符号。<br /><br /> DBNull.Value — 不适用于数据类型。|  
|MaximumScale|short|如果类型指示符为数值类型，是指小数点右侧允许的最大位数。  否则为 DBNull.Value。|  
|MinimumScale|short|如果类型指示符为数值类型，是指小数点右侧允许的最小位数。  否则为 DBNull.Value。|  
|IsConcurrencyType|bool|true – 每次行更改并且列值与所有以前的值不同时，由数据库更新数据类型。<br /><br /> false – 每次行更改时，数据库不更新数据类型。<br /><br /> DBNull.Value – 数据库不支持此数据类型的类型。|  
|IsLiteralsSupported|bool|true – 数据类型可以以文本形式表示。<br /><br /> false – 数据类型不能以文本形式表示。|  
|LiteralPrefix|string|应用于给定文本的前缀。|  
|LitteralSuffix|string|应用于给定文本的后缀。|  
|NativeDataType|String|NativeDataType 是 OLE DB 特定的列，用于公开数据类型的 OLE DB 类型。|  
  
## 限制  
 此架构集合为当前用于连接到数据库的 .NET Framework 管理的提供程序公开所支持的限制的有关信息。  
  
|列名|数据类型|描述|  
|--------|----------|--------|  
|CollectionName|string|应用这些限制的集合的名称。|  
|RestrictionName|string|集合中的限制的名称。|  
|RestrictionDefault|string|已忽略。|  
|RestrictionNumber|int|此特定限制在限制集合中的实际位置。|  
  
## ReservedWords  
 此架构集合为 .NET Framework 管理的提供程序当前连接到的数据库公开所保留的关键字的有关信息。  
  
|列名|数据类型|描述|  
|--------|----------|--------|  
|ReservedWords|string|提供程序特定的保留字。|  
  
## 请参阅  
 [检索数据库架构信息](../../../../docs/framework/data/adonet/retrieving-database-schema-information.md)   
 [GetSchema 和架构集合](../../../../docs/framework/data/adonet/getschema-and-schema-collections.md)   
 [ADO.NET 托管提供程序和数据集开发人员中心](http://go.microsoft.com/fwlink/?LinkId=217917)