---
title: "Oracle 架构集合 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-ado"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 89a75de8-dee8-45e2-a97f-254d7e62e7e1
caps.latest.revision: 3
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 3
---
# Oracle 架构集合
除了通用架构集合之外，Microsoft Oracle .NET Framework 数据提供程序还支持下列特定的架构集合：  
  
-   Columns  
  
-   索引  
  
-   IndexColumns  
  
-   过程  
  
-   序列  
  
-   Synonyms  
  
-   表  
  
-   Users  
  
-   视图  
  
-   函数  
  
-   包  
  
-   PackageBodies  
  
-   参数  
  
-   UniqueKeys  
  
-   PrimaryKeys  
  
-   ForeignKeys  
  
-   ForeignKeyColumns  
  
-   ProcedureParameters  
  
## Columns  
  
|列名|数据类型|描述|  
|--------|----------|--------|  
|OWNER|String|表、视图或群集的所有者。|  
|TABLE\_NAME|String|表、视图或群集的名称。|  
|COLUMN\_NAME|String|列名称。|  
|ID|Decimal|列在创建时的序列号。|  
|DATATYPE|String|列的数据类型。|  
|LENGTH|Decimal|列的长度（字节数）。|  
|PRECISION|Decimal|对于 NUMBER 数据类型为十进制精度；对于 FLOAT 数据类型为二进制精度；对于所有其他数据类型为 null。|  
|SCALE|Decimal|数字中小数点右侧的位数。|  
|NULLABLE|String|指定列是否允许 NULL。  如果列上存在 NOT NULL 约束，或列属于 PRIMARY KEY，值为 N。|  
  
## 索引  
  
|列名|数据类型|描述|  
|--------|----------|--------|  
|OWNER|String|索引的所有者。|  
|INDEX\_NAME|String|索引的名称。|  
|INDEX\_TYPE|String|索引的类型（NORMAL、BITMAP、FUNCTION\-BASED NORMAL、FUNCTION\-BASED BITMAP 或 DOMAIN）。|  
|TABLE\_OWNER|String|索引对象的所有者。|  
|TABLE\_NAME|String|索引对象的名称。|  
|TABLE\_TYPE|String|索引对象的类型（例如 TABLE、CLUSTER）。|  
|UNIQUENESS|String|索引是 UNIQUE 还是 NONUNIQUE。|  
|COMPRESSION|String|索引是 ENABLED 还是 DISABLED。|  
|PREFIX\_LENGTH|Decimal|压缩键的前缀中的列数。|  
|TABLESPACE\_NAME|String|包含索引的表空间的名称。|  
|INI\_TRANS|Decimal|初始事务数。|  
|MAX\_TRANS|Decimal|最大事务数。|  
|INITIAL\_EXTENT|Decimal|初始范围的大小。|  
|NEXT\_EXTENT|Decimal|辅助范围的大小。|  
|MIN\_EXTENTS|Decimal|段中允许的最小范围数。|  
|MAX\_EXTENTS|Decimal|段中允许的最大范围数。|  
|PCT\_INCREASE|Decimal|范围大小增加的百分比。|  
|PCT\_THRESHOLD|Decimal|每个索引条目允许的块空间的阈值百分比。|  
|INCLUDE\_COLUMN|Decimal|要加入通过索引组织的表的主键（非溢出）索引中的最后一列的列 ID。  此列映射到 \*\_TAB\_COLUMNS 数据字典视图的 COLUMN\_ID 列。|  
|FREELISTS|Decimal|为此段分配的进程空闲列表数。|  
|FREELIST\_GROUPS|Decimal|为此段分配的空闲列表组数。|  
|PCT\_FREE|Decimal|块中可用空间的最小百分比。|  
|LOGGING|String|日志信息。|  
|BLEVEL|Decimal|B\* 树级别：从根块到叶块的索引深度。  如果深度为 0，指示根块到叶块相同。|  
|LEAF\_BLOCKS|Decimal|索引中的叶块数。|  
|DISTINCT\_KEYS|Decimal|不同的索引值数。  对于强制使用 UNIQUE 和 PRIMARY KEY 约束的索引，此值与表中的行数相同 \(USER\_TABLES.NUM\_ROWS\)。|  
|AVG\_LEAF\_BLOCKS\_PER\_KEY|Decimal|平均叶块数，索引中的每个不同值舍入到最接近的整数。  对于强制使用 UNIQUE 和 PRIMARY KEY 约束的索引，此值始终为 1。|  
|AVG\_DATA\_BLOCKS\_PER\_KEY|Decimal|表中通过索引中舍入到最接近整数的不同值指向的平均数据块数。  此统计信息是包含的行中包含索引列的给定值的平均数据块数。|  
|CLUSTERING\_FACTOR|Decimal|根据索引值指示表中行的排序数量。|  
|STATUS|String|非分区索引是 VALID 还是 UNUSABLE。|  
|NUM\_ROWS|Decimal|索引中的行数。|  
|SAMPLE\_SIZE|Decimal|用于分析索引的示例的大小。|  
|LAST\_ANALYZED|DateTime|最近分析此索引的日期。|  
|DEGREE|String|每个实例用于扫描索引的线程数。|  
|INSTANCES|String|在其上扫描索引的实例数。|  
|PARTITIONED|String|此索引是否已分区 \(YES &#124; NO\)。|  
|TEMPORARY|String|索引是否在临时表上。|  
|GENERATED|String|索引名称是否由系统生成 \(Y&#124;N\)。|  
|SECONDARY|String|索引是否是由 Oracle9i Data Cartridge 的 ODCIIndexCreate 方法创建的辅助对象 \(Y&#124;N\)。|  
|BUFFER\_POOL|String|用于索引块的默认缓冲区池的名称。|  
|USER\_STATS|String|统计信息是否已由用户直接输入。|  
|DURATION|String|指示临时表的持续时间：1\)SYS$SESSION：在会话期间保留行，2\) SYS$TRANSACTION：在 COMMIT 之后删除行，3\) Null 表示永久表。|  
|PCT\_DIRECT\_ACCESS|Decimal|对于通过索引组织的表上的辅助索引，为具有 VALID 猜测的行的百分比。|  
|ITYP\_OWNER|String|对于域索引，为索引类型的所有者。|  
|ITYP\_NAME|String|对于域索引，为索引类型的名称。|  
|PARAMETERS|String|对于域索引，为参数字符串。|  
|GLOBAL\_STATS|String|对于分区索引，指示统计信息通过整体分析索引进行收集 \(YES\) 还是通过基础索引分区和子分区上的统计信息进行估计 \(NO\)。|  
|DOMIDX\_STATUS|String|反映域索引的状态。  NULL：指定的索引不是域索引。  VALID：索引是有效的域索引。  IDXTYP\_INVLD：此域索引的索引类型无效。|  
|DOMIDX\_OPSTATUS|String|反映在域索引上执行的操作的状态：NULL：指定的索引不是域索引。  VALID：执行操作而未发生错误。  FAILED：操作发生错误并失败。|  
|FUNCIDX\_STATUS|String|指示基于函数的索引的状态：NULL：这不是基于函数的索引，ENABLED：已启用基于函数的索引，DISABLED：已禁用基于函数的索引。|  
|JOIN\_INDEX|String|指示此索引是否是联接索引。|  
  
## IndexColumns  
  
|列名|数据类型|描述|  
|--------|----------|--------|  
|INDEX\_OWNER|String|索引的所有者。|  
|INDEX\_NAME|String|索引的名称。|  
|TABLE\_OWNER|String|表或群集的所有者。|  
|TABLE\_NAME|String|表或群集的名称。|  
|COLUMN\_NAME|String|对象类型列的列名或属性。|  
|COLUMN\_POSITION|Decimal|列或属性在索引中的位置。|  
|COLUMN\_LENGTH|Decimal|列的索引长度。|  
|CHAR\_LENGTH|Decimal|列的最大代码点长度。|  
|DESCEND|String|列是否按照降序进行排序。|  
  
## 过程  
  
|列名|数据类型|描述|  
|--------|----------|--------|  
|OWNER|String|对象的所有者。|  
|OBJECT\_NAME|String|对象的名称。|  
|SUBOBJECT\_NAME|String|子对象（例如分区）的名称。|  
|OBJECT\_ID|Decimal|对象的字典对象编号。|  
|DATA\_OBJECT\_ID|Decimal|包含对象的段的字典对象编号。|  
|LAST\_DDL\_TIME|DateTime|上次通过 DDL 命令修改对象（包括授予和吊销）的时间戳。|  
|TIMESTAMP|String|指定对象（字符数据）的时间戳。|  
|STATUS|String|对象的状态（VALID、INVALID 或 N\/A）。|  
|TEMPORARY|String|对象是否是临时对象（当前会话只能看到其放入此对象本身的数据）。|  
|GENERATED|String|此对象的名称是否由系统生成？  \(Y &#124; N\)。|  
|SECONDARY|String|此对象是否是由 Oracle9i Data Cartridge 的 ODCIIndexCreate 方法创建的辅助对象 \(Y &#124; N\)。|  
|CREATED|DateTime|创建对象的日期。|  
  
## 序列  
  
|列名|数据类型|描述|  
|--------|----------|--------|  
|SEQUENCE\_OWNER|String|序列所有者的名称。|  
|SEQUENCE\_NAME|String|序列名称。|  
|MIN\_VALUE|Decimal|序列的最小值。|  
|MAX\_VALUE|Decimal|序列的最大值。|  
|INCREMENT\_BY|Decimal|序列递增的值。|  
|CYCLE\_FLAG|String|在达到限制时序列是否环绕。|  
|ORDER\_FLAG|String|序列号是否按顺序生成。|  
|CACHE\_SIZE|Decimal|要缓存的序列号数。|  
|LAST\_NUMBER|Decimal|写入磁盘的上一个序列号。  如果序列使用缓存，写入磁盘的序列号是上一个放入序列缓存的序列号。  此序列号很可能大于上一个使用的序列号。|  
  
## Synonyms  
  
|列名|数据类型|描述|  
|--------|----------|--------|  
|OWNER|String|同义词的所有者。|  
|SYNONYM\_NAME|String|同义词的名称。|  
|TABLE\_OWNER|String|通过同义词引用的对象的所有者。|  
|TABLE\_NAME|String|通过同义词引用的对象的名称。|  
|DB\_LINK|String|所引用的数据库链接的名称（如果有）。|  
  
## 表  
  
|列名|数据类型|描述|  
|--------|----------|--------|  
|OWNER|String|表的所有者。|  
|TABLE\_NAME|String|表的名称。|  
|TYPE|String|表的类型。|  
  
## Users  
  
|列名|数据类型|描述|  
|--------|----------|--------|  
|NAME|String|用户的名称。|  
|ID|Decimal|用户的 ID 号。|  
|CREATEDATE|DateTime|用户的创建日期。|  
  
## 视图  
  
|列名|数据类型|描述|  
|--------|----------|--------|  
|OWNER|String|视图的所有者。|  
|VIEW\_NAME|String|视图的名称。|  
|TEXT\_LENGTH|Decimal|视图文本的长度。|  
|TEXT|String|视图文本。|  
|TYPE\_TEXT\_LENGTH|Decimal|类型化视图的类型子句的长度。|  
|TYPE\_TEXT|String|类型化视图的类型子句。|  
|OID\_TEXT\_LENGTH|Decimal|类型化视图的 WITH OID 子句的长度。|  
|OID\_TEXT|String|类型化视图的 WITH OID 子句。|  
|VIEW\_TYPE\_OWNER|String|视图类型的所有者（如果视图是类型化视图）。|  
|VIEW\_TYPE|String|视图类型（如果视图是类型化视图）。|  
|SUPERVIEW\_NAME|String|超级视图的名称。|  
  
## 函数  
  
|列名|数据类型|描述|  
|--------|----------|--------|  
|OWNER|String|对象的所有者。|  
|OBJECT\_NAME|String|对象的名称。|  
|SUBOBJECT\_NAME|String|子对象（例如分区）的名称。|  
|OBJECT\_ID|Decimal|对象的字典对象编号。|  
|DATA\_OBJECT\_ID|Decimal|包含对象的段的字典对象编号。|  
|OBJECT\_TYPE|String|对象的类型。|  
|CREATED|DateTime|创建对象的日期。|  
|LAST\_DDL\_TIME|DateTime|上次通过 DDL 命令修改对象（包括授予和吊销）的时间戳。|  
|TIMESTAMP|String|指定对象（字符数据）的时间戳。|  
|STATUS|String|对象的状态（VALID、INVALID 或 N\/A）。|  
|TEMPORARY|String|对象是否是临时对象（当前会话只能看到其放入此对象本身的数据）。|  
|GENERATED|String|此对象的名称是否由系统生成？  \(Y &#124; N\)。|  
|SECONDARY|String|此对象是否是由 Oracle9i Data Cartridge 的 ODCIIndexCreate 方法创建的辅助对象 \(Y &#124; N\)。|  
  
## 包  
  
|列名|数据类型|描述|  
|--------|----------|--------|  
|OWNER|String|对象的所有者。|  
|OBJECT\_NAME|String|对象的名称。|  
|SUBOBJECT\_NAME|String|子对象（例如分区）的名称。|  
|OBJECT\_ID|Decimal|对象的字典对象编号。|  
|DATA\_OBJECT\_ID|Decimal|包含对象的段的字典对象编号。|  
|LAST\_DDL\_TIME|DateTime|上次通过 DDL 命令修改对象（包括授予和吊销）的时间戳。|  
|TIMESTAMP|String|指定对象（字符数据）的时间戳。|  
|STATUS|String|对象的状态（VALID、INVALID 或 N\/A）。|  
|TEMPORARY|String|对象是否是临时对象（当前会话只能看到其放入此对象本身的数据）。|  
|GENERATED|String|此对象的名称是否由系统生成？  \(Y &#124; N\)。|  
|SECONDARY|String|此对象是否是由 Oracle9i Data Cartridge 的 ODCIIndexCreate 方法创建的辅助对象 \(Y &#124; N\)。|  
|CREATED|DateTime|创建对象的日期。|  
  
## PackageBodies  
  
|列名|数据类型|描述|  
|--------|----------|--------|  
|OWNER|String|对象的所有者。|  
|OBJECT\_NAME|String|对象的名称。|  
|SUBOBJECT\_NAME|String|子对象（例如分区）的名称。|  
|OBJECT\_ID|Decimal|对象的字典对象编号。|  
|DATA\_OBJECT\_ID|Decimal|包含对象的段的字典对象编号。|  
|LAST\_DDL\_TIME|DateTime|上次通过 DDL 命令修改对象（包括授予和吊销）的时间戳。|  
|TIMESTAMP|String|指定对象（字符数据）的时间戳。|  
|STATUS|String|对象的状态（VALID、INVALID 或 N\/A）。|  
|TEMPORARY|String|对象是否是临时对象（当前会话只能看到其放入此对象本身的数据）。|  
|GENERATED|String|此对象的名称是否由系统生成？  \(Y &#124; N\)。|  
|SECONDARY|String|此对象是否是由 Oracle9i Data Cartridge 的 ODCIIndexCreate 方法创建的辅助对象 \(Y &#124; N\)。|  
|CREATED|DateTime|创建对象的日期。|  
  
## 参数  
  
|列名|数据类型|描述|  
|--------|----------|--------|  
|OWNER|String|对象所有者的名称。|  
|PACKAGE\_NAME|String|包名称。|  
|OBJECT\_NAME|String|过程或函数的名称。|  
|ARGUMENT\_NAME|String|参数的名称。|  
|POSITION|Decimal|在参数列表中的位置，对于函数返回值为 NULL。|  
|SEQUENCE|Decimal|参数序列，包括所有嵌套级别。|  
|DEFAULT\_VALUE|String|参数的默认值。|  
|DEFAULT\_LENGTH|Decimal|参数的默认值的长度。|  
|IN\_OUT|String|参数方向（IN、OUT 或 IN\/OUT）。|  
|DATA\_LENGTH|Decimal|列的长度（字节数）。|  
|DATA\_PRECISION|Decimal|十进制位 \(NUMBER\) 或二进制位 \(FLOAT\) 的长度。|  
|DATA\_SCALE|Decimal|数字中小数点右侧的位数。|  
|DATA\_TYPE|String|参数的数据类型。|  
  
## UniqueKeys  
  
|列名|数据类型|描述|  
|--------|----------|--------|  
|OWNER|String|约束定义的所有者。|  
|CONSTRAINT\_NAME|String|约束定义的名称。|  
|TABLE\_NAME|String|与具有约束定义的表（或视图）关联的名称。|  
|SEARCH\_CONDITION|String|检查约束的搜索条件的文本。|  
|R\_OWNER|String|在引用约束中引用的表的所有者。|  
|R\_CONSTRAINT\_NAME|String|所引用表的唯一约束定义的名称。|  
|DELETE\_RULE|String|删除引用约束的规则（CASCADE 或 NO ACTION）。|  
|STATUS|String|约束的强制执行状态（ENABLED 或 DISABLED）。|  
|DEFERRABLE|String|约束是否可以推迟。|  
|VALIDATED|String|所有数据是否均遵循该约束（VALIDATED 或 NOT VALIDATED）。|  
|GENERATED|String|约束名称是由用户还是由系统生成。|  
|BAD|String|YES 值指示此约束以不明确的方式指定世纪。  为了避免因为这种不明确造成错误，使用 TO\_DATE 函数重写该约束，包含一个四位的年份。|  
|RELY|String|启用的约束强制执行还是非强制执行。|  
|LAST\_CHANGE|DateTime|上次启用或禁用约束的时间。|  
|INDEX\_OWNER|String|拥有索引的用户的名称。|  
|INDEX\_NAME|String|索引的名称。|  
  
## PrimaryKeys  
  
|列名|数据类型|描述|  
|--------|----------|--------|  
|OWNER|String|约束定义的所有者。|  
|CONSTRAINT\_NAME|String|约束定义的名称。|  
|TABLE\_NAME|String|与具有约束定义的表（或视图）关联的名称。|  
|SEARCH\_CONDITION|String|检查约束的搜索条件的文本。|  
|R\_OWNER|String|在引用约束中引用的表的所有者。|  
|R\_CONSTRAINT\_NAME|String|所引用表的唯一约束定义的名称。|  
|DELETE\_RULE|String|删除引用约束的规则（CASCADE 或 NO ACTION）。|  
|STATUS|String|约束的强制执行状态（ENABLED 或 DISABLED）。|  
|DEFERRABLE|String|约束是否可以推迟。|  
|VALIDATED|String|所有数据是否均遵循该约束（VALIDATED 或 NOT VALIDATED）。|  
|GENERATED|String|约束名称是由用户还是由系统生成。|  
|BAD|String|YES 值指示此约束以不明确的方式指定世纪。  为了避免因为这种不明确造成错误，使用 TO\_DATE 函数重写该约束，包含一个四位的年份。|  
|RELY|String|启用的约束强制执行还是非强制执行。|  
|LAST\_CHANGE|DateTime|上次启用或禁用约束的时间。|  
|INDEX\_OWNER|String|拥有索引的用户的名称。|  
|INDEX\_NAME|String|索引的名称。|  
  
## ForeignKeys  
  
|列名|数据类型|描述|  
|--------|----------|--------|  
|PRIMARY\_KEY\_CONSTRAINT\_NAME|String|约束定义的名称。|  
|PRIMARY\_KEY\_OWNER|String|约束定义的所有者。|  
|PRIMARY\_KEY\_TABLE\_NAME|String|与具有约束定义的表（或视图）关联的名称。|  
|FOREIGN\_KEY\_OWNER|String|约束定义的所有者。|  
|FOREIGN\_KEY\_CONSTRIANT\_NAME|String|约束定义的名称。|  
|FOREIGN\_KEY\_TABLE\_NAME|String|与具有约束定义的表（或视图）关联的名称。|  
|SEARCH\_CONDITION|String|检查约束的搜索条件的文本。|  
|R\_OWNER|String|在引用约束中引用的表的所有者。|  
|R\_CONSTRAINT\_NAME|String|所引用表的唯一约束定义的名称。|  
|DELETE\_RULE|String|删除引用约束的规则（CASCADE 或 NO ACTION）。|  
|STATUS|String|约束的强制执行状态（ENABLED 或 DISABLED）。|  
|VALIDATED|String|所有数据是否均遵循该约束（VALIDATED 或 NOT VALIDATED）。|  
|GENERATED|String|约束名称是由用户还是由系统生成。|  
|RELY|String|启用的约束强制执行还是非强制执行。|  
|LAST\_CHANGE|DateTime|上次启用或禁用约束的时间。|  
|INDEX\_OWNER|String|拥有索引的用户的名称。|  
|INDEX\_NAME|String|索引的名称。|  
  
## ForeignKeyColumns  
  
|列名|数据类型|描述|  
|--------|----------|--------|  
|OWNER|String|约束定义的所有者。|  
|CONSTRAINT\_NAME|String|约束定义的名称。|  
|TABLE\_NAME|String|具有约束定义的表的名称。|  
|COLUMN\_NAME|String|约束定义中指定的对象类型列的列或属性的名称。|  
|POSITION|Decimal|对象定义中列或属性的原始位置。|  
  
## ProcedureParameters  
  
|列名|数据类型|描述|  
|--------|----------|--------|  
|OWNER|String|对象的所有者。|  
|OBJECT\_NAME|String|过程或函数的名称。|  
|PACKAGE\_NAME|String|过程或函数的名称。|  
|OBJECT\_ID|Decimal|对象的对象编号。|  
|OVERLOAD|String|重载唯一标识符。|  
|ARGUMENT\_NAME|String|参数的名称。|  
|POSITION|Decimal|在参数列表中的位置，对于函数返回值为 null。|  
|SEQUENCE|Decimal|参数序列，包括所有嵌套级别。|  
|DATA\_LEVEL|Decimal|复合类型的参数的嵌套深度。|  
|DATA\_TYPE|String|参数的数据类型。|  
|DEFAULT\_VALUE|String|参数的默认值。|  
|DEFAULT\_LENGTH|Decimal|参数的默认值的长度。|  
|IN\_OUT|String|参数方向（IN、OUT 或 IN\/OUT）。|  
|DATA\_LENGTH|Decimal|列的长度（字节数）。|  
|DATA\_PRECISION|Decimal|十进制位 \(NUMBER\) 或二进制位 \(FLOAT\) 的长度。|  
|DATA\_SCALE|Decimal|数字中小数点右侧的位数。|  
|RADIX|Decimal|数字的参数基数。|  
|CHARACTER\_SET\_NAME|String|参数的字符集名称。|  
|TYPE\_OWNER|String|参数类型的所有者。|  
|TYPE\_NAME|String|参数类型的名称。  如果类型是包局部类型（即在包指定中声明），此列将显示包的名称。|  
|TYPE\_SUBNAME|String|只与包局部类型有关。  显示在 TYPE\_NAME 列中标识的包中声明的类型名称。|  
|TYPE\_LINK|String|只有 TYPE\_NAME 列中标识的包是远程包时，才与包局部类型有关。  此列显示用于引用远程包的数据库链接。|  
|PLS\_TYPE|String|对于数值参数，为参数的 PL\/SQL 类型的名称。  否则为 Null。|  
|CHAR\_LENGTH|Decimal|字符串数据类型的字符限制。|  
|CHAR\_USED|String|指示字节限制 \(B\) 或字符限制 \(C\) 是否正式用于字符串。|  
  
## 请参阅  
 [ADO.NET 托管提供程序和数据集开发人员中心](http://go.microsoft.com/fwlink/?LinkId=217917)