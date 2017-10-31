---
title: "SQL Server 架构集合 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-ado"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: c6403cc3-d78b-4f85-bab1-ada7a3446ec5
caps.latest.revision: 5
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 5
---
# SQL Server 架构集合
除了通用架构集合之外，适用于 SQL Server 的 Microsoft .NET Framework 数据提供程序还支持其他架构集合。  架构集合因使用的 SQL Server 的版本而稍有不同。  要确定支持的架构集合列表，请以无参数的形式或使用架构集合名称“MetaDataCollections”调用 **GetSchema** 方法。  此时将返回 <xref:System.Data.DataTable>，包含支持的架构集合列表、每个架构集合支持的限制数以及所使用的标识符部分数。  
  
## 数据库  
  
|列名|数据类型|描述|  
|--------|----------|--------|  
|database\_name|String|数据库的名称。|  
|Dbid|Int16|数据库 ID。|  
|create\_date|DateTime|数据库的创建日期。|  
  
## Foreign Keys  
  
|列名|数据类型|描述|  
|--------|----------|--------|  
|constraint\_catalog|String|约束所属的编录。|  
|constraint\_schema|String|包含约束的架构。|  
|constraint\_name|String|名称。|  
|table\_catalog|String|约束所属的表名。|  
|table\_schema|String|包含表的架构。|  
|table\_name|String|表名称|  
|constraint\_type|String|约束的类型。  只允许“FOREIGN KEY”。|  
|is\_deferrable|String|指定约束是否可以推迟。  返回 NO。|  
|initially\_deferred|String|指定约束最初是否可以推迟。  返回 NO。|  
  
## 索引  
  
|列名|数据类型|描述|  
|--------|----------|--------|  
|constraint\_catalog|String|索引所属的编录。|  
|constraint\_schema|String|包含索引的架构。|  
|constraint\_name|String|索引的名称。|  
|table\_catalog|String|索引关联的表名。|  
|table\_schema|String|包含索引关联的表的架构。|  
|table\_name|String|表名。|  
  
### Indexes \(SQL Server 2008\)  
 从 .NET Framework 版本 3.5 SP1 和 SQL Server 2008 开始，以下列已经添加到 Indexes 架构集合以支持新的空间类型、文件流和稀疏列。  早期版本的 .NET Framework 和 SQL Server 不支持这些列。  
  
|列名|数据类型|描述|  
|--------|----------|--------|  
|type\_desc|String|索引类型可以为以下值之一：<br /><br /> -   HEAP<br />-   CLUSTERED<br />-   NONCLUSTERED<br />-   XML<br />-   SPATIAL|  
  
## IndexColumns  
  
|列名|数据类型|描述|  
|--------|----------|--------|  
|constraint\_catalog|String|索引所属的编录。|  
|constraint\_schema|String|包含索引的架构。|  
|constraint\_name|String|索引的名称。|  
|table\_catalog|String|索引关联的表名。|  
|table\_schema|String|包含索引关联的表的架构。|  
|table\_name|String|表名。|  
|column\_name|String|索引关联的列名。|  
|ordinal\_position|Int32|列的序号位置。|  
|KeyType|UInt16|对象的类型。|  
  
## 过程  
  
|列名|数据类型|描述|  
|--------|----------|--------|  
|specific\_catalog|String|编录的特定名称。|  
|specific\_schema|String|架构的特定名称。|  
|specific\_name|String|编录的特定名称。|  
|routine\_catalog|String|存储过程所属的编录。|  
|routine\_schema|String|包含存储过程的架构。|  
|routine\_name|String|存储过程的名称。|  
|routine\_type|String|对于存储过程，返回 PROCEDURE，对于函数，返回 FUNCTION。|  
|created|DateTime|过程的创建时间。|  
|last\_altered|DateTime|上次修改过程的时间。|  
  
## Procedure Parameters  
  
|列名|数据类型|描述|  
|--------|----------|--------|  
|specific\_catalog|String|此参数所属的过程的编录名称。|  
|specific\_schema|String|包含此参数所属的过程的架构。|  
|specific\_name|String|此参数所属的过程的名称。|  
|ordinal\_position|Int16|参数的序号位置，从 1 开始。  对于过程的返回值，此位置为 0。|  
|parameter\_mode|String|如果是输入参数，返回 IN，如果是输出参数，返回 OUT，如果是输入\/输出参数，返回 INOUT。|  
|is\_result|String|如果指示属于函数的过程的结果，返回 YES。  否则，返回 NO。|  
|as\_locator|String|如果声明为定位符，返回 YES。  否则，返回 NO。|  
|parameter\_name|String|参数的名称。  如果对应于函数的返回值，返回 NULL。|  
|data\_type|String|系统提供的数据类型。|  
|character\_maximum\_length|Int32|二进制或字符数据类型的最大长度（字符数）。  否则，返回 NULL。|  
|character\_octet\_length|Int32|二进制或字符数据类型的最大长度（字节数）。  否则，返回 NULL。|  
|collation\_catalog|String|参数排序规则的编录名称。  如果不属于某种字符类型，返回 NULL。|  
|collation\_schema|String|始终返回 NULL。|  
|collation\_name|String|参数分页的名称。  如果不属于某种字符类型，返回 NULL。|  
|character\_set\_catalog|String|参数字符集的编录名称。  如果不属于某种字符类型，返回 NULL。|  
|character\_set\_schema|String|始终返回 NULL。|  
|character\_set\_name|String|参数字符集的名称。  如果不属于某种字符类型，返回 NULL。|  
|numeric\_precision|Byte|近似数值数据、精确数值数据、整数数据或货币数据的精度。  否则，返回 NULL。|  
|numeric\_precision\_radix|Int16|近似数值数据、精确数值数据、整数数据或货币数据的精度基数。  否则，返回 NULL。|  
|numeric\_scale|Int32|近似数值数据、精确数值数据、整数数据或货币数据的小数位数。  否则，返回 NULL。|  
|datetime\_precision|Int16|如果参数类型为 datetime 或 smalldatetime，则为小数秒数的精度。  否则，返回 NULL。|  
|interval\_type|String|NULL。  保留供 SQL Server 以后使用。|  
|interval\_precision|Int16|NULL。  保留供 SQL Server 以后使用。|  
  
## 表  
  
|列名|数据类型|描述|  
|--------|----------|--------|  
|table\_catalog|String|表的编录。|  
|table\_schema|String|包含表的架构。|  
|table\_name|String|表名。|  
|table\_type|String|表的类型。  可以是 VIEW 或 BASE TABLE。|  
  
## Columns  
  
|列名|数据类型|描述|  
|--------|----------|--------|  
|table\_catalog|String|表的编录。|  
|table\_schema|String|包含表的架构。|  
|table\_name|String|表名。|  
|column\_name|String|列名称。|  
|ordinal\_position|Int16|列标识号。|  
|column\_default|String|列的默认值。|  
|is\_nullable|String|列的可空性。  如果此列允许 NULL，此列将返回 YES。  否则，返回 No。|  
|data\_type|String|系统提供的数据类型。|  
|character\_maximum\_length|Int32 – Sql8、Int16 – Sql7|二进制数据、字符数据或文本和图像数据的最大长度（字符数）。  否则，返回 NULL。|  
|character\_octet\_length|Int32 – SQL8、Int16 – Sql7|二进制数据、字符数据或文本和图像数据的最大长度（字节数）。  否则，返回 NULL。|  
|numeric\_precision|Unsigned Byte|近似数值数据、精确数值数据、整数数据或货币数据的精度。  否则，返回 NULL。|  
|numeric\_precision\_radix|Int16|近似数值数据、精确数值数据、整数数据或货币数据的精度基数。  否则，返回 NULL。|  
|numeric\_scale|Int32|近似数值数据、精确数值数据、整数数据或货币数据的小数位数。  否则，返回 NULL。|  
|datetime\_precision|Int16|datetime 和 SQL\-92 interval 数据类型的子类型代码。  对于其他数据类型，返回 NULL。|  
|character\_set\_catalog|String|如果列为字符数据或文本数据类型，则返回 master，指示字符集所处的数据库。  否则，返回 NULL。|  
|character\_set\_schema|String|始终返回 NULL。|  
|character\_set\_name|String|如果此列为字符数据或文本数据类型，则返回字符集的唯一名称。  否则，返回 NULL。|  
|collation\_catalog|String|如果列为字符数据或文本数据类型，则返回 master，指示定义分页的数据库。  否则，此列为 NULL.|  
  
### Columns \(SQL Server 2008\)  
 从 .NET Framework 版本 3.5 SP1 和 SQL Server 2008 开始，以下列已经添加到 Colums 架构集合以支持新的空间类型、文件流和稀疏列。  早期版本的 .NET Framework 和 SQL Server 不支持这些列。  
  
|列名|数据类型|描述|  
|--------|----------|--------|  
|IS\_FILESTREAM|String|YES       FILESTREAM<br /><br /> NO，如果列不具有 FILESTREAM 属性。|  
|IS\_SPARSE|String|YES，如果列是稀疏列。<br /><br /> NO，如果列不是稀疏列。|  
|IS\_COLUMN\_SET|String|YES，如果列是一个列集列。<br /><br /> NO|  
  
### AllColumns \(SQL Server 2008\)  
 从 .NET Framework 版本 3.5 SP1 和 SQL Server 2008 开始，添加了 AllColumns 架构集合以支持稀疏列。  早期版本的 .NET Framework 和 SQL Server 不支持 AllColumns。  
  
 AllColumns 与 Columns 架构集合具有相同的限制和生成的 DataTable 架构。  唯一的区别是 AllColumns 包含 Columns 架构集合中未包含的列集列。  下表介绍了这些列。  
  
|列名|数据类型|描述|  
|--------|----------|--------|  
|table\_catalog|String|表的编录。|  
|table\_schema|String|包含表的架构。|  
|table\_name|String|表名。|  
|column\_name|String|列名称。|  
|ordinal\_position|Int16|列标识号。|  
|column\_default|String|列的默认值。|  
|is\_nullable|String|列的可空性。  如果此列允许 NULL，此列将返回 YES。  否则，返回 NO。|  
|data\_type|String|系统提供的数据类型。|  
|character\_maximum\_length|Int32|二进制数据、字符数据或文本和图像数据的最大长度（字符数）。  否则，返回 NULL。|  
|character\_octet\_length|Int32|二进制数据、字符数据或文本和图像数据的最大长度（字节数）。  否则，返回 NULL。|  
|numeric\_precision|Unsigned Byte|近似数值数据、精确数值数据、整数数据或货币数据的精度。  否则，返回 NULL。|  
|numeric\_precision\_radix|Int16|近似数值数据、精确数值数据、整数数据或货币数据的精度基数。  否则，返回 NULL。|  
|numeric\_scale|Int32|近似数值数据、精确数值数据、整数数据或货币数据的小数位数。  否则，返回 NULL。|  
|datetime\_precision|Int16|datetime 和 SQL\-92 interval 数据类型的子类型代码。  对于其他数据类型，返回 NULL。|  
|character\_set\_catalog|String|如果列为字符数据或文本数据类型，则返回 master，指示字符集所处的数据库。  否则，返回 NULL。|  
|character\_set\_schema|String|始终返回 NULL。|  
|character\_set\_name|String|如果此列为字符数据或文本数据类型，则返回字符集的唯一名称。  否则，返回 NULL。|  
|collation\_catalog|String|如果列为字符数据或文本数据类型，则返回 master，指示定义分页的数据库。  否则，此列为 NULL.|  
|IS\_FILESTREAM|String|YES       FILESTREAM<br /><br /> NO，如果列不具有 FILESTREAM 属性。|  
|IS\_SPARSE|String|YES，如果列是稀疏列。<br /><br /> NO，如果列不是稀疏列。|  
|IS\_COLUMN\_SET|String|YES，如果列是一个列集列。<br /><br /> NO|  
  
### ColumnSetColumns \(SQL Server 2008\)  
 从 .NET Framework 版本 3.5 SP1 和 SQL Server 2008 开始，添加了 ColumnSetColumns 架构集合以支持稀疏列。  早期版本的 .NET Framework 和 SQL Server 不支持 ColumnSetColumns。  ColumnSetColumns 架构集合返回列集中所有列的架构。  下表介绍了这些列。  
  
|列名|数据类型|描述|  
|--------|----------|--------|  
|table\_catalog|String|表的编录。|  
|table\_schema|String|包含表的架构。|  
|table\_name|String|表名。|  
|column\_name|String|列名称。|  
|ordinal\_position|Int16|列标识号。|  
|column\_default|String|列的默认值。|  
|is\_nullable|String|列的可空性。  如果此列允许 NULL，此列将返回 YES。  否则，返回 NO。|  
|data\_type|String|系统提供的数据类型。|  
|character\_maximum\_length|Int32|二进制数据、字符数据或文本和图像数据的最大长度（字符数）。  否则，返回 NULL。|  
|character\_octet\_length|Int32|二进制数据、字符数据或文本和图像数据的最大长度（字节数）。  否则，返回 NULL。|  
|numeric\_precision|Unsigned Byte|近似数值数据、精确数值数据、整数数据或货币数据的精度。  否则，返回 NULL。|  
|numeric\_precision\_radix|Int16|近似数值数据、精确数值数据、整数数据或货币数据的精度基数。  否则，返回 NULL。|  
|numeric\_scale|Int32|近似数值数据、精确数值数据、整数数据或货币数据的小数位数。  否则，返回 NULL。|  
|datetime\_precision|Int16|datetime 和 SQL\-92 interval 数据类型的子类型代码。  对于其他数据类型，返回 NULL。|  
|character\_set\_catalog|String|如果列为字符数据或文本数据类型，则返回 master，指示字符集所处的数据库。  否则，返回 NULL。|  
|character\_set\_schema|String|始终返回 NULL。|  
|character\_set\_name|String|如果此列为字符数据或文本数据类型，则返回字符集的唯一名称。  否则，返回 NULL。|  
|collation\_catalog|String|如果列为字符数据或文本数据类型，则返回 master，指示定义分页的数据库。  否则，此列为 NULL.|  
|IS\_FILESTREAM|String|YES       FILESTREAM<br /><br /> NO，如果列不具有 FILESTREAM 属性。|  
|IS\_SPARSE|String|YES，如果列是稀疏列。<br /><br /> NO，如果列不是稀疏列。|  
|IS\_COLUMN\_SET|String|YES，如果列是一个列集列。<br /><br /> NO|  
  
## Users  
  
|列名|数据类型|描述|  
|--------|----------|--------|  
|uid|Int16|在此数据库中唯一的用户 ID。  1 为数据库所有者。|  
|name|String|在此数据库中唯一的用户名和组名。|  
|createdate|DateTime|添加帐户的日期。|  
|updatedate|DateTime|上次更改帐户的日期。|  
  
## 视图  
  
|列名|数据类型|描述|  
|--------|----------|--------|  
|table\_catalog|String|视图的编录。|  
|table\_schema|String|包含视图的架构。|  
|table\_name|String|视图名称。|  
|check\_option|String|WITH CHECK OPTION 的类型。  如果原始视图使用 WITH CHECK OPTION 创建，则为 CASCADE。  否则，返回 NONE。|  
|is\_updatable|String|指定视图是否可以更新。  始终返回 NO。|  
  
## ViewColumns  
  
|列名|数据类型|描述|  
|--------|----------|--------|  
|view\_catalog|String|视图的编录。|  
|view\_schema|String|包含视图的架构。|  
|view\_name|String|视图名称。|  
|table\_catalog|String|与此视图关联的表的编录。|  
|table\_schema|String|包含与此视图关联的表的架构。|  
|table\_name|String|与此视图关联的表的名称。  基表。|  
|column\_name|String|列名称。|  
  
## UserDefinedTypes  
  
|列名|数据类型|描述|  
|--------|----------|--------|  
|assembly\_name|String|程序集文件的名称。|  
|UDT\_name|String|程序集的类名。|  
|version\_major|对象|主版本号。|  
|version\_minor|对象|次版本号。|  
|version\_build|对象|Build 号。|  
|version\_revision|对象|修订号。|  
|Culture\_info|对象|与此 UDT 关联的区域性信息。|  
|Public\_key|对象|此程序集使用的公钥。|  
|Is\_fixed\_length|Boolean|指定类型的长度是否始终与 max\_length 相同。|  
|max\_length|Int16|类型的最大长度（字节数）。|  
|permission\_set\_desc|String|程序集的权限集\/安全级别的友好名称。|  
|create\_date|DateTime|创建\/注册程序集的日期。|  
  
## 请参阅  
 [检索数据库架构信息](../../../../docs/framework/data/adonet/retrieving-database-schema-information.md)   
 [ADO.NET 托管提供程序和数据集开发人员中心](http://go.microsoft.com/fwlink/?LinkId=217917)