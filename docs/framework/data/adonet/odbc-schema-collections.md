---
title: "ODBC 架构集合 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-ado"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 1bb126a5-ceec-4649-a4bc-8aa19e801046
caps.latest.revision: 3
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 3
---
# ODBC 架构集合
本节讨论对适用于 Microsoft SQL Server、Oracle 和 Microsoft Jet 的 ODBC 驱动程序的架构集合支持。  
  
## Microsoft SQL Server ODBC 驱动程序  
 除了通用架构集合之外，Microsoft SQL Server ODBC 驱动程序还支持下列特定的架构集合：  
  
-   表  
  
-   索引  
  
-   Columns  
  
-   过程  
  
-   ProcedureColumns  
  
-   ProcedureParameters  
  
-   视图  
  
### Tables 和 Views  
  
|列名|数据类型|  
|--------|----------|  
|TABLE\_CAT|String|  
|TABLE\_SCHEM|String|  
|TABLE\_NAME|String|  
|TABLE\_TYPE|String|  
|REMARKS|String|  
  
### 索引  
  
|列名|数据类型|  
|--------|----------|  
|TABLE\_CAT|String|  
|TABLE\_SCHEM|String|  
|TABLE\_NAME|String|  
|NON\_UNIQUE|Int16|  
|INDEX\_QUALIFIER|String|  
|INDEX\_NAME|String|  
|TYPE|Int16|  
|ORDINAL\_POSITION|Int16|  
|COLUMN\_NAME|String|  
|ASC\_OR\_DESC|String|  
|CARDINATLITY|Int32|  
|PAGES|Int32|  
|FILTER\_CONDITION|String|  
|SS\_TYPE\_SCHEMA|String|  
|SS\_DATA\_TYPE|Byte|  
  
### Columns  
  
|列名|数据类型|  
|--------|----------|  
|TABLE\_CAT|String|  
|TABLE\_SCHEM|String|  
|TABLE\_NAME|String|  
|COLUMN\_NAME|String|  
|DATA\_TYPE|Int16|  
|TYPE\_NAME|String|  
|COLUMN\_SIZE|Int32|  
|BUFFER\_LENGTH|Int32|  
|DECIMAL\_DIGITS|Int16|  
|NUM\_PREC\_RADIX|Int16|  
|NULLABLE|Int16|  
|REMARKS|String|  
|COLUMN\_DEF|String|  
|SQL\_DATA\_TYPE|Int16|  
|SQL\_DATETIME\_SUB|Int16|  
|CHAR\_OCTET\_LENGTH|Int32|  
|ORDINAL\_POSITION|Int32|  
|IS\_NULLABLE|String|  
|SS\_TYPE\_CATALOG|String|  
|SS\_TYPE\_SCHEMA|String|  
|SS\_DATA\_TYPE|Byte|  
  
### 过程  
  
|列名|数据类型|  
|--------|----------|  
|PROCEDURE\_CAT|String|  
|PROCEDURE\_SCHEM|String|  
|PROCEDURE\_NAME|String|  
|NUM\_INPUT\_PARAMS|Int32|  
|NUM\_OUTPUT\_PARAMS|Int32|  
|NUM\_RESULT\_SETS|Int32|  
|REMARKS|String|  
|PROCEDURE\_TYPE|Int16|  
  
### ProcedureColumns  
  
|列名|数据类型|  
|--------|----------|  
|PROCEDURE\_CAT|String|  
|PROCEDURE\_SCHEM|String|  
|PROCEDURE\_NAME|String|  
|COLUMN\_NAME|String|  
|COLUMN\_TYPE|Int16|  
|DATA\_TYPE|Int16|  
|TYPE\_NAME|String|  
|COLUMN\_SIZE|Int32|  
|BUFFER\_LENGTH|Int32|  
|DECIMAL\_DIGITS|Int16|  
|NUM\_PREC\_RADIX|Int16|  
|NULLABLE|Int16|  
|REMARKS|String|  
|COLUMN\_DEF|String|  
|SQL\_DATA\_TYPE|Int16|  
|SQL\_DATETIME\_SUB|Int16|  
|CHAR\_OCTET\_LENGTH|Int32|  
|ORDINAL\_POSITION|Int32|  
|IS\_NULLABLE|String|  
|SS\_TYPE\_CATALOG|String|  
|SS\_TYPE\_SCHEMA|String|  
|SS\_DATA\_TYPE|Byte|  
  
### ProcedureParameters  
  
|列名|数据类型|  
|--------|----------|  
|PROCEDURE\_CAT|String|  
|PROCEDURE\_SCHEM|String|  
|PROCEDURE\_NAME|String|  
|COLUMN\_NAME|String|  
|COLUMN\_TYPE|Int16|  
|DATA\_TYPE|Int16|  
|TYPE\_NAME|String|  
|COLUMN\_SIZE|Int32|  
|BUFFER\_LENGTH|Int32|  
|DECIMAL\_DIGITS|Int16|  
|NUM\_PREC\_RADIX|Int16|  
|NULLABLE|Int16|  
|REMARKS|String|  
|COLUMN\_DEF|String|  
|SQL\_DATA\_TYPE|Int16|  
|SQL\_DATETIME\_SUB|Int16|  
|CHAR\_OCTET\_LENGTH|Int32|  
|ORDINAL\_POSITION|Int32|  
|IS\_NULLABLE|String|  
|SS\_TYPE\_CATALOG|String|  
|SS\_TYPE\_SCHEMA|String|  
|SS\_DATA\_TYPE|Byte|  
  
## Microsoft Oracle ODBC 驱动程序  
 除了通用架构集合之外，Microsoft SQL Server Oracle ODBC 驱动程序还支持下列特定的架构集合：  
  
-   表  
  
-   Columns  
  
-   过程  
  
-   ProcedureColumns  
  
-   ProcedureParameters  
  
-   视图  
  
-   索引  
  
### Tables 和 Views  
  
|列名|数据类型|  
|--------|----------|  
|TABLE\_QUALIFIER|String|  
|TABLE\_OWNER|String|  
|TABLE\_NAME|String|  
|TABLE\_TYPE|String|  
|REMARKS|String|  
  
### Columns  
  
|列名|数据类型|  
|--------|----------|  
|TABLE\_QUALIFIER|String|  
|TABLE\_OWNER|String|  
|TABLE\_NAME|String|  
|COLUMN\_NAME|String|  
|DATA\_TYPE|Int16|  
|TYPE\_NAME|String|  
|PRECISION|Int32|  
|LENGTH|Int32|  
|SCALE|Int16|  
|RADIX|Int16|  
|NULLABLE|Int16|  
|REMARKS|String|  
|ORDINAL\_POSITION|Int32|  
  
### 过程  
  
|列名|数据类型|  
|--------|----------|  
|PROCEDURE\_QUALIFIER|String|  
|PROCEDURE\_OWNER|String|  
|PROCEDURE\_NAME|String|  
|NUM\_INPUT\_PARAMS|Int16|  
|NUM\_OUTPUT\_PARAMS|Int16|  
|NUM\_RESULT\_SETS|Int16|  
|REMARKS|String|  
|PROCEDURE\_TYPE|Int16|  
  
### ProcedureColumns  
  
|列名|数据类型|  
|--------|----------|  
|PROCEDURE\_QUALIFIER|String|  
|PROCEDURE\_OWNER|String|  
|PROCEDURE\_NAME|String|  
|COLUMN\_NAME|String|  
|COLUMN\_TYPE|Int16|  
|DATA\_TYPE|Int16|  
|TYPE\_NAME|String|  
|PRECISION|Int32|  
|LENGTH|Int32|  
|SCALE|Int16|  
|RADIX|Int16|  
|NULLABLE|Int16|  
|REMARKS|String|  
|OVERLOAD|Int32|  
|ORDINAL\_POSITION|Int32|  
  
## Microsoft Jet ODBC 驱动程序  
 除了通用架构集合之外，Microsoft Jet ODBC 驱动程序还支持下列特定的架构集合：  
  
-   表  
  
-   索引  
  
-   Columns  
  
-   过程  
  
-   ProcedureColumns  
  
-   ProcedureParameters  
  
-   视图  
  
### Tables 和 Views  
  
|列名|数据类型|  
|--------|----------|  
|TABLE\_QUALIFIER|String|  
|TABLE\_OWNER|String|  
|TABLE\_NAME|String|  
|TABLE\_TYPE|String|  
|REMARKS|String|  
  
### Columns  
  
|列名|数据类型|  
|--------|----------|  
|TABLE\_QUALIFIER|String|  
|TABLE\_OWNER|String|  
|TABLE\_NAME|String|  
|COLUMN\_NAME|String|  
|DATA\_TYPE|Int16|  
|TYPE\_NAME|String|  
|PRECISION|Int32|  
|LENGTH|Int32|  
|SCALE|Int16|  
|RADIX|Int16|  
|NULLABLE|Int16|  
|REMARKS|String|  
|ORDINAL\_POSITION|Int32|  
  
### 过程  
  
|列名|数据类型|  
|--------|----------|  
|PROCEDURE\_QUALIFIER|String|  
|PROCEDURE\_OWNER|String|  
|PROCEDURE\_NAME|String|  
|NUM\_INPUT\_PARAMS|Int16|  
|NUM\_OUTPUT\_PARAMS|Int16|  
|NUM\_RESULT\_SETS|Int16|  
|REMARKS|String|  
|PROCEDURE\_TYPE|Int16|  
  
### ProcedureColumns  
  
|列名|数据类型|  
|--------|----------|  
|PROCEDURE\_QUALIFIER|String|  
|PROCEDURE\_OWNER|String|  
|PROCEDURE\_NAME|String|  
|COLUMN\_NAME|String|  
|COLUMN\_TYPE|Int16|  
|DATA\_TYPE|Int16|  
|TYPE\_NAME|String|  
|PRECISION|Int32|  
|LENGTH|Int32|  
|SCALE|Int16|  
|RADIX|Int16|  
|NULLABLE|Int16|  
|REMARKS|String|  
|OVERLOAD|Int32|  
|ORDINAL\_POSITION|Int32|  
  
### ProcedureParameters  
  
|列名|数据类型|  
|--------|----------|  
|PROCEDURE\_CAT|String|  
|PROCEDURE\_SCHEM|String|  
|PROCEDURE\_NAME|String|  
|COLUMN\_NAME|String|  
|COLUMN\_TYPE|Int16|  
|DATA\_TYPE|Int16|  
|TYPE\_NAME|String|  
|COLUMN\_SIZE|Int32|  
|BUFFER\_LENGTH|Int32|  
|DECIMAL\_DIGITS|Int16|  
|NUM\_PREC\_RADIX|Int16|  
|NULLABLE|Int16|  
|REMARKS|String|  
|COLUMN\_DEF|String|  
|SQL\_DATA\_TYPE|Int16|  
|SQL\_DATETIME\_SUB|Int16|  
|CHAR\_OCTET\_LENGTH|Int32|  
|ORDINAL\_POSITION|Int32|  
|IS\_NULLABLE|String|  
  
## 请参阅  
 [ADO.NET 托管提供程序和数据集开发人员中心](http://go.microsoft.com/fwlink/?LinkId=217917)