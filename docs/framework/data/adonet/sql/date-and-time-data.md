---
title: "日期和时间数据 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-ado"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 6f5ff56a-a57e-49d7-8ae9-bbed697e42e3
caps.latest.revision: 7
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 7
---
# 日期和时间数据
SQL Server 2008 引入了用于处理日期和时间信息的新数据类型。  新的数据类型包括单独的日期和时间类型以及具有更大范围、更高精度和更强时区感知能力的扩展数据类型。  从 .NET Framework 3.5 Service Pack \(SP\) 1 开始，适用于 SQL Server 的 .NET Framework 数据提供程序 \(<xref:System.Data.SqlClient>\) 完全支持 SQL Server 2008 数据库引擎的所有新功能。  您必须安装 .NET Framework 3.5 SP1（或更高版本）才能将这些新功能与 SqlClient 一起使用。  
  
 SQL Server 2008 之前的 SQL Server 版本仅具有两种用于处理日期和时间值的数据类型：`datetime` 和 `smalldatetime`。  这两种数据类型同时包含日期值和时间值，因而难以仅使用日期值或仅使用时间值。  此外，这些数据类型仅支持自 1753 年英国引入公历日历以来的日期。  另一个限制是这些旧的数据类型无法识别时区，因此难以使用来自多个时区的数据。  
  
 有关 SQL Server 数据类型的完整文档可从 SQL Server 联机丛书中获得。  下表列出了有关日期和时间数据的因版本而异的入门级主题。  
  
 **SQL Server 联机丛书**  
  
1.  [使用日期和时间数据](http://go.microsoft.com/fwlink/?LinkID=98361)（可能为英文网页）  
  
## SQL Server 2008 中引入的日期\/时间数据类型  
 下表描述了新的日期和时间数据类型。  
  
|SQL Server 数据类型|描述|  
|---------------------|--------|  
|`date`|`date` 数据类型的范围从 01 年 1 月 1 日到 9999 年 12 月 31 日，精度为 1 天。  默认值为 1900 年 1月 1日。  存储大小为 3 字节。|  
|`time`|`time` 数据类型仅存储时间值，并且采用 24 小时制。  `time` 数据类型的范围从 00:00:00.0000000 到 23:59:59.9999999，精确到 100 毫微秒。  默认值为 00:00:00.0000000（午夜）。  `time` 数据类型支持用户定义的小数秒精度，存储大小根据指定的精度在 3 字节到 6 字节之间变化。|  
|`datetime2`|`datetime2` 数据类型将 `date` 和 `time` 数据类型的范围和精度组合成单个数据类型。<br /><br /> 默认值和字符串格式与 `date` 和 `time` 数据类型中定义的相同。|  
|`datetimeoffset`|`datetimeoffset` 数据类型具有 `datetime2` 的所有功能，并附加了时区偏移量。  时区偏移量表示为 \[\+&#124;\-\] HH:MM。  HH 是范围从 00 到 14 的 2 位数，表示时区偏移量的小时数。  MM 是范围从 00 到 59 的 2 位数，表示时区偏移量的附加分钟数。  时间格式支持的精度为 100 毫微秒。  必需的 \+ 或 \- 符号指示在 UTC（通用协调时间或格林尼治标准时间）中是加上还是减去时区偏移量以获取本地时间。|  
  
> [!NOTE]
>  有关使用 `Type System Version` 关键字的更多信息，请参见 <xref:System.Data.SqlClient.SqlConnection.ConnectionString%2A>。  
  
## 日期格式和日期顺序  
 SQL Server 分析日期和时间值的方式不仅依赖于类型系统版本和服务器版本，还依赖于服务器的默认语言和格式设置。  如果由使用不同语言和日期格式设置的连接执行查询，则可能无法识别仅适用于一种语言的日期格式的日期字符串。  
  
 Transact\-SQL SET LANGUAGE 语句隐式设置可确定日期各个部分的顺序的 DATEFORMAT。  可以对连接使用 SET DATEFORMAT Transact\-SQL 语句，通过按 MDY、DMY、YMD、YDM、MYD 或 DYM 顺序对日期的各个部分进行排序来消除日期值的歧义。  
  
 如果没有为连接指定任何 DATEFORMAT，则 SQL Server 将使用与连接关联的默认语言。  例如，在使用美国英语语言设置的服务器上，日期字符串“01\/02\/03”将解释为 MDY（2003 年 1 月 2 日），而在使用英国英语语言设置的服务器上，将解释为 DMY（2003 年 2 月 1 日）。  年份是通过使用 SQL Server 的截止年份规则确定的，该规则定义用于分配世纪值的截止日期。  有关更多信息，请参见 SQL Server 联机丛书中的 [two digit year cutoff 选项](http://go.microsoft.com/fwlink/?LinkId=120473)（可能为英文网页）。  
  
> [!NOTE]
>  从字符串格式转换为 `date`、`time`、`datetime2` 或 `datetimeoffset` 时不支持 YDM 日期格式。  
  
 有关 SQL Server 如何解释日期和时间数据的更多信息，请参见 SQL Server 2008 联机丛书中的[使用日期和时间数据](http://go.microsoft.com/fwlink/?LinkID=98361)（可能为英文网页）。  
  
## 日期\/时间数据类型和参数  
 通过使用 <xref:System.Data.SqlDbType> 枚举之一，可以指定 <xref:System.Data.SqlClient.SqlParameter> 的数据类型。  <xref:System.Data.SqlDbType> 中已添加了下面的枚举，以支持新的日期和时间数据类型。  
  
-   `SqlDbType.Date`  
  
-   `SqlDbType.Time`  
  
-   `SqlDbType.DateTime2`  
  
-   `SqlDbType.DateTimeOffSet`  
  
 也可以通过将 `SqlParameter` 对象的 <xref:System.Data.SqlClient.SqlParameter.DbType%2A> 属性设置为特定的 <xref:System.Data.DbType> 枚举值，按照通常的方式来指定 <xref:System.Data.SqlClient.SqlParameter> 的类型。  <xref:System.Data.DbType> 中已添加了下面的枚举值，以支持 `datetime2` 和 `datetimeoffset` 数据类型：  
  
-   DbType.DateTime2  
  
-   DbType.DateTimeOffset  
  
 这些新枚举补充了早期版本的 .NET Framework 中存在的 `Date`、`Time` 和 `DateTime` 枚举。  
  
 某一参数对象的 .NET Framework 数据提供程序类型是从该参数对象的 .NET Framework 类型或该参数对象的 `DbType` 推断而来的。  没有引入新的 <xref:System.Data.SqlTypes> 数据类型来支持新的日期和时间数据类型。  下表说明 SQL Server 2008 日期和时间数据类型和 CLR 数据类型之间的映射。  
  
|SQL Server 数据类型|.NET Framework 类型|System.Data.SqlDbType|System.Data.DbType|  
|---------------------|-----------------------|---------------------------|------------------------|  
|date|System.DateTime|日期|日期|  
|时间|System.TimeSpan|时间|时间|  
|datetime2|System.DateTime|DateTime2|DateTime2|  
|datetimeoffset|System.DateTimeOffset|DateTimeOffset|DateTimeOffset|  
|datetime|System.DateTime|DateTime|DateTime|  
|smalldatetime|System.DateTime|DateTime|DateTime|  
  
### SqlParameter 属性  
 下表描述了与日期和时间数据类型相关的 `SqlParameter` 属性。  
  
|属性|描述|  
|--------|--------|  
|<xref:System.Data.SqlClient.SqlParameter.IsNullable%2A>|获取或设置值是否可以为 null。  在向服务器发送 null 参数值时，必须指定 <xref:System.DBNull> 而非 `null`（在 Visual Basic 中为 `Nothing`）。  有关数据库 null 值的更多信息，请参见[处理 Null 值](../../../../../docs/framework/data/adonet/sql/handling-null-values.md)。|  
|<xref:System.Data.SqlClient.SqlParameter.Precision%2A>|获取或设置用来表示值的最大位数。  对于日期和时间数据类型，忽略此设置。|  
|<xref:System.Data.SqlClient.SqlParameter.Scale%2A>|获取或设置要为 `Time`、`DateTime2` `` 和 `DateTimeOffset` 解析的值的时间部分的小数位数。  默认值为 0。这意味着实际小数位数从值推断出来并发送给服务器。|  
|<xref:System.Data.SqlClient.SqlParameter.Size%2A>|对于日期和时间数据类型，忽略此设置。|  
|<xref:System.Data.SqlClient.SqlParameter.Value%2A>|获取或设置参数值。|  
|<xref:System.Data.SqlClient.SqlParameter.SqlValue%2A>|获取或设置参数值。|  
  
> [!NOTE]
>  小于 0 或大于等于 24 小时的时间值将引发 <xref:System.ArgumentException>。  
  
### 创建参数  
 可以通过以下方法来创建 <xref:System.Data.SqlClient.SqlParameter> 对象：使用相应的构造函数；或者通过调用 <xref:System.Data.SqlClient.SqlParameterCollection> 的 `Add` 方法将其添加到 <xref:System.Data.SqlClient.SqlCommand> <xref:System.Data.SqlClient.SqlCommand.Parameters%2A> 集合。  `Add` 方法将采用构造函数参数或现有的参数对象用作输入。  
  
 本主题中的以下各部分提供了如何指定日期和时间参数的示例。  有关使用参数的其他示例，请参见[配置参数和参数数据类型](../../../../../docs/framework/data/adonet/configuring-parameters-and-parameter-data-types.md)和 [DataAdapter 参数](../../../../../docs/framework/data/adonet/dataadapter-parameters.md)。  
  
### date 示例  
 下面的代码段演示如何指定 `date` 参数。  
  
```csharp  
SqlParameter parameter = new SqlParameter();  
parameter.ParameterName = "@Date";  
parameter.SqlDbType = SqlDbType.Date;  
parameter.Value = "2007/12/1";  
```  
  
```vb  
Dim parameter As New SqlParameter()  
parameter.ParameterName = "@Date"  
parameter.SqlDbType = SqlDbType.Date  
parameter.Value = "2007/12/1"  
```  
  
### time 示例  
 下面的代码段演示如何指定 `time` 参数。  
  
```csharp  
SqlParameter parameter = new SqlParameter();  
parameter.ParameterName = "@time";  
parameter.SqlDbType = SqlDbType.Time;  
parameter.Value = DateTime.Parse("23:59:59").TimeOfDay;  
```  
  
```vb  
Dim parameter As New SqlParameter()  
parameter.ParameterName = "@Time"  
parameter.SqlDbType = SqlDbType.Time  
parameter.Value = DateTime.Parse("23:59:59").TimeOfDay;  
```  
  
### datetime2 示例  
 下面的代码段演示如何指定同时具有日期和时间部分的 `datetime2` 参数。  
  
```csharp  
SqlParameter parameter = new SqlParameter();  
parameter.ParameterName = "@Datetime2";  
parameter.SqlDbType = SqlDbType.DateTime2;  
parameter.Value = DateTime.Parse("1666-09-02 1:00:00");  
```  
  
```vb  
Dim parameter As New SqlParameter()  
parameter.ParameterName = "@Datetime2"  
parameter.SqlDbType = SqlDbType.DateTime2  
parameter.Value = DateTime.Parse("1666-09-02 1:00:00");  
```  
  
### DateTimeOffSet 示例  
 下面的代码段演示如何指定具有日期、时间和偏移量为 0 的时区的 `DateTimeOffSet` 参数。  
  
```csharp  
SqlParameter parameter = new SqlParameter();  
parameter.ParameterName = "@DateTimeOffSet";  
parameter.SqlDbType = SqlDbType.DateTimeOffSet;  
parameter.Value = DateTimeOffset.Parse("1666-09-02 1:00:00+0");  
```  
  
```vb  
Dim parameter As New SqlParameter()  
parameter.ParameterName = "@DateTimeOffSet"  
parameter.SqlDbType = SqlDbType.DateTimeOffSet  
parameter.Value = DateTimeOffset.Parse("1666-09-02 1:00:00+0");  
```  
  
### AddWithValue  
 也可以通过使用 <xref:System.Data.SqlClient.SqlCommand> 的 `AddWithValue` 方法来提供参数，如下面的代码段所示。  不过，不能使用 `AddWithValue` 方法为参数指定 <xref:System.Data.SqlClient.SqlParameter.DbType%2A> 或 <xref:System.Data.SqlClient.SqlParameter.SqlDbType%2A>。  
  
```csharp  
command.Parameters.AddWithValue(   
    "@date", DateTimeOffset.Parse("16660902"));  
```  
  
```vb  
command.Parameters.AddWithValue( _  
    "@date", DateTimeOffset.Parse("16660902"))  
```  
  
 `@date` 参数可映射到服务器上的 `date`、`datetime` 或 `datetime2` 数据类型。  使用新的 `datetime` 数据类型时，必须将参数的 <xref:System.Data.SqlDbType> 属性显式设置为实例的数据类型。  如果使用 <xref:System.Data.SqlDbType> 或隐式提供参数值，则会导致与 `datetime` 和 `smalldatetime` 数据类型的向后兼容问题。  
  
 下表显示可从哪些 CLR 类型中推断出哪些 `SqlDbTypes`：  
  
|CLR 类型|推断出的 SqlDbType|  
|------------|--------------------|  
|DateTime|SqlDbType.DateTime|  
|TimeSpan|SqlDbType.Time|  
|DateTimeOffset|SqlDbType.DateTimeOffset|  
  
## 检索日期和时间数据  
 下表说明可用于检索 SQL Server 2008 日期和时间值的方法。  
  
|SqlClient 方法|描述|  
|------------------|--------|  
|<xref:System.Data.SqlClient.SqlDataReader.GetDateTime%2A>|以 <xref:System.DateTime> 结构形式检索指定的列值。|  
|<xref:System.Data.SqlClient.SqlDataReader.GetDateTimeOffset%2A>|以 <xref:System.DateTimeOffset> 结构形式检索指定的列值。|  
|<xref:System.Data.SqlClient.SqlDataReader.GetProviderSpecificFieldType%2A>|返回作为该字段基础提供程序特定类型的类型。  返回新日期和时间类型的与 `GetFieldType` 相同的类型。|  
|<xref:System.Data.SqlClient.SqlDataReader.GetProviderSpecificValue%2A>|检索指定列的值。  返回新日期和时间类型的与 `GetValue` 相同的类型。|  
|<xref:System.Data.SqlClient.SqlDataReader.GetProviderSpecificValues%2A>|检索指定数组中的值。|  
|<xref:System.Data.SqlClient.SqlDataReader.GetSqlString%2A>|以 <xref:System.Data.SqlTypes.SqlString> 形式检索列值。  如果数据无法表示为 `SqlString`，则发生 <xref:System.InvalidCastException>。|  
|<xref:System.Data.SqlClient.SqlDataReader.GetSqlValue%2A>|检索列数据作为其默认 `SqlDbType`。  返回新日期和时间类型的与 `GetValue` 相同的类型。|  
|<xref:System.Data.SqlClient.SqlDataReader.GetSqlValues%2A>|检索指定数组中的值。|  
|<xref:System.Data.SqlClient.SqlDataReader.GetString%2A>|如果 Type System Version 设置为 SQL Server 2005，则以字符串形式检索列值。  如果数据无法表示为字符串，则发生 <xref:System.InvalidCastException>。|  
|<xref:System.Data.SqlClient.SqlDataReader.GetTimeSpan%2A>|以 <xref:System.Timespan> 结构形式检索指定的列值。|  
|<xref:System.Data.SqlClient.SqlDataReader.GetValue%2A>|检索指定的列值作为其基础 CLR 类型。|  
|<xref:System.Data.SqlClient.SqlDataReader.GetValues%2A>|检索数组中的列值。|  
|<xref:System.Data.SqlClient.SqlDataReader.GetSchemaTable%2A>|返回一个 <xref:System.Data.DataTable>，说明结果集的元数据。|  
  
> [!NOTE]
>  对于 SQL Server 中在进程内执行的代码，不支持新的日期和时间 `SqlDbTypes`。  如果将这些类型之一传递给服务器，则将引发异常。  
  
## 作为文字指定日期和时间值  
 可以通过使用各种不同的文字字符串格式指定日期和时间数据类型，然后 SQL Server 在运行时执行相关计算以将这些文字字符串转换为内部的日期\/时间结构。  SQL Server 可识别用单引号 \('\) 括起来的日期和时间数据。  下面的示例演示了一些格式：  
  
-   字母日期格式，例如 `'October 15, 2006'`。  
  
-   数值日期格式，例如 `'10/15/2006'`。  
  
-   未分隔的字符串格式，例如 `'20061015'`。如果您使用的是 ISO 标准日期格式，则该字符串将解释为 2006 年 10 月 15 日。  
  
> [!NOTE]
>  在 SQL Server 联机丛书中，您可以找到有关日期和时间数据类型的所有文字字符串格式以及其他功能的完整文档。  
  
 小于 0 或大于等于 24 小时的时间值将引发 <xref:System.ArgumentException>。  
  
## SQL Server 2008 联机丛书中的资源  
 有关如何在 SQL Server 2008 中使用日期和时间值的更多信息，请参见 SQL Server 2008 联机丛书中的以下资源。  
  
|主题|描述|  
|--------|--------|  
|[日期和时间数据类型和函数 \(Transact\-SQL\)](http://go.microsoft.com/fwlink/?LinkId=98360)（可能为英文网页）|概述所有 Transact\-SQL 日期和时间数据类型和函数。|  
|[使用日期和时间数据](http://go.microsoft.com/fwlink/?LinkId=98361)（可能为英文网页）|提供有关日期和时间数据类型和函数的信息及相应的用法示例。|  
|[数据类型 \(Transact\-SQL\)](http://go.microsoft.com/fwlink/?LinkId=98362)（可能为英文网页）|介绍 SQL Server 2008 中的系统数据类型。|  
  
## 请参阅  
 [SQL Server 数据类型映射](../../../../../docs/framework/data/adonet/sql-server-data-type-mappings.md)   
 [配置参数和参数数据类型](../../../../../docs/framework/data/adonet/configuring-parameters-and-parameter-data-types.md)   
 [SQL Server 数据类型和 ADO.NET](../../../../../docs/framework/data/adonet/sql/sql-server-data-types.md)   
 [ADO.NET 托管提供程序和数据集开发人员中心](http://go.microsoft.com/fwlink/?LinkId=217917)