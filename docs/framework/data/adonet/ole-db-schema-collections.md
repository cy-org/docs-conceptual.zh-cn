---
title: "OLE DB 架构集合 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-ado"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 6380c36b-658e-4d67-91e8-7131ef4a7c2c
caps.latest.revision: 3
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 3
---
# OLE DB 架构集合
本节讨论对适用于 Microsoft SQL Server、Oracle 和 Microsoft Jet 的 OLE DB 提供程序的架构集合支持  
  
## Microsoft SQL Server OLE DB 提供程序  
 除了通用架构集合之外，Microsoft SQL Server OLE DB 驱动程序还支持下列特定的架构集合：  
  
-   表  
  
-   Columns  
  
-   过程  
  
-   ProcedureParameters  
  
-   Catalog  
  
-   索引  
  
### 表  
  
|列名|数据类型|  
|--------|----------|  
|TABLE\_CATALOG|String|  
|TABLE\_SCHEMA|String|  
|TABLE\_NAME|String|  
|TABLE\_TYPE|String|  
|TABLE\_GUID|Guid|  
|DESCRIPTION|String|  
|TABLE\_PROPID|Int64|  
|DATE\_CREATED|DateTime|  
|DATE\_MODIFIED|DateTime|  
  
### Columns  
  
|列名|数据类型|  
|--------|----------|  
|TABLE\_CATALOG|String|  
|TABLE\_SCHEMA|String|  
|TABLE\_NAME|String|  
|COLUMN\_NAME|String|  
|COLUMN\_GUID|Guid|  
|COLUMN\_PROPID|Int64|  
|ORDINAL\_POSITION|Int64|  
|COLUMN\_HASDEFAULT|Boolean|  
|COLUMN\_DEFAULT|String|  
|COLUMN\_FLAGS|Int64|  
|IS\_NULLABLE|Boolean|  
|DATA\_TYPE|Int32|  
|TYPE\_GUID|Guid|  
|CHARACTER\_MAXIMUM\_LENGTH|Int64|  
|CHARACTER\_OCTET\_LENGTH|Int64|  
|NUMERIC\_PRECISION|Int32|  
|NUMERIC\_SCALE|Int16|  
|DATETIME\_PRECISION|Int64|  
|CHARACTER\_SET\_CATALOG|String|  
|CHARACTER\_SET\_SCHEMA|String|  
|CHARACTER\_SET\_NAME|String|  
|COLLATION\_CATALOG|String|  
|COLLATION\_SCHEMA|String|  
|COLLATION\_NAME|String|  
|DOMAIN\_CATALOG|String|  
|DOMAIN\_SCHEMA|String|  
|DOMAIN\_NAME|String|  
|DESCRIPTION|String|  
|COLUMN\_LCID|Int32|  
|COLUMN\_COMPFLAGS|Int32|  
|COLUMN\_SORTID|Int32|  
|COLUMN\_TDSCOLLATION|Byte\[\]|  
|IS\_COMPUTED|Boolean|  
  
### 过程  
  
|列名|数据类型|  
|--------|----------|  
|PROCEDURE\_CATALOG|String|  
|PROCEDURE\_SCHEMA|String|  
|PROCEDURE\_NAME|String|  
|PROCEDURE\_TYPE|Int16|  
|PROCEDURE\_DEFINITION|String|  
|DESCRIPTION|String|  
|DATE\_CREATED|DateTime|  
|DATE\_MODIFIED|DateTime|  
  
### ProcedureParameters  
  
|列名|数据类型|  
|--------|----------|  
|PROCEDURE\_CATALOG|String|  
|PROCEDURE\_SCHEMA|String|  
|PROCEDURE\_NAME|String|  
|PARAMETER\_NAME|String|  
|ORDINAL\_POSITION|Int32|  
|PARAMETER\_TYPE|Int32|  
|PARAMETER\_HASDEFAULT|Boolean|  
|PARAMETER\_DEFAULT|String|  
|IS\_NULLABLE|Boolean|  
|DATA\_TYPE|Int32|  
|CHARACTER\_MAXIMUM\_LENGTH|Int64|  
|CHARACTER\_OCTET\_LENGTH|Int64|  
|NUMERIC\_PRECISION|Int32|  
|NUMERIC\_SCALE|Int16|  
|DESCRIPTION|String|  
|TYPE\_NAME|String|  
|LOCAL\_TYPE\_NAME|String|  
  
### Catalog  
  
|列名|数据类型|  
|--------|----------|  
|CATALOG\_NAME|String|  
|DESCRIPTION|String|  
  
### 索引  
  
|列名|数据类型|  
|--------|----------|  
|TABLE\_CATALOG|String|  
|TABLE\_SCHEMA|String|  
|TABLE\_NAME|String|  
|INDEX\_CATALOG|String|  
|INDEX\_SCHEMA|String|  
|INDEX\_NAME|String|  
|PRIMARY\_KEY|Boolean|  
|UNIQUE|Boolean|  
|CLUSTERED|Boolean|  
|TYPE|Int32|  
|FILL\_FACTOR|Int32|  
|INITIAL\_SIZE|Int32|  
|NULLS|Int32|  
|SORT\_BOOKMARKS|Boolean|  
|AUTO\_UPDATE|Boolean|  
|NULL\_COLLATION|Int32|  
|ORDINAL\_POSITION|Int64|  
|COLUMN\_NAME|String|  
|COLUMN\_GUID|Guid|  
|COLUMN\_PROPID|Int64|  
|COLLATION|Int16|  
|CARDINALITY|Decimal|  
|PAGES|Int32|  
|FILTER\_CONDITION|String|  
|INTEGRATED|Boolean|  
  
## Microsoft Oracle OLE DB 提供程序  
 除了通用架构集合之外，Microsoft Oracle OLE DB 驱动程序还支持下列特定的架构集合：  
  
-   表  
  
-   Columns  
  
-   过程  
  
-   ProcedureColumns  
  
-   ProcedureParameters  
  
-   视图  
  
-   索引  
  
### 表  
  
|列名|数据类型|  
|--------|----------|  
|TABLE\_CATALOG|String|  
|TABLE\_SCHEMA|String|  
|TABLE\_NAME|String|  
|TABLE\_TYPE|String|  
|TABLE\_GUID|Guid|  
|DESCRIPTION|String|  
|TABLE\_PROPID|Int64|  
|DATE\_CREATED|DateTime|  
|DATE\_MODIFIED|DateTime|  
  
### Columns  
  
|列名|数据类型|  
|--------|----------|  
|TABLE\_CATALOG|String|  
|TABLE\_SCHEMA|String|  
|TABLE\_NAME|String|  
|COLUMN\_NAME|String|  
|COLUMN\_GUID|Guid|  
|COLUMN\_PROPID|Int64|  
|ORDINAL\_POSITION|Int64|  
|COLUMN\_HASDEFAULT|Boolean|  
|COLUMN\_DEFAULT|String|  
|COLUMN\_FLAGS|Int64|  
|IS\_NULLABLE|Boolean|  
|DATA\_TYPE|Int32|  
|TYPE\_GUID|Guid|  
|CHARACTER\_MAXIMUM\_LENGTH|Int64|  
|CHARACTER\_OCTET\_LENGTH|Int64|  
|NUMERIC\_PRECISION|Int32|  
|NUMERIC\_SCALE|Int16|  
|DATETIME\_PRECISION|Int64|  
|CHARACTER\_SET\_CATALOG|String|  
|CHARACTER\_SET\_SCHEMA|String|  
|CHARACTER\_SET\_NAME|String|  
|COLLATION\_CATALOG|String|  
|COLLATION\_SCHEMA|String|  
|COLLATION\_NAME|String|  
|DOMAIN\_CATALOG|String|  
|DOMAIN\_SCHEMA|String|  
|DOMAIN\_NAME|String|  
|DESCRIPTION|String|  
  
### 过程  
  
|列名|数据类型|  
|--------|----------|  
|PROCEDURE\_CATALOG|String|  
|PROCEDURE\_SCHEMA|String|  
|PROCEDURE\_NAME|String|  
|PROCEDURE\_TYPE|Int16|  
|PROCEDURE\_DEFINITION|String|  
|DESCRIPTION|String|  
|DATE\_CREATED|DateTime|  
|DATE\_MODIFIED|DateTime|  
  
### ProcedureColumns  
  
|列名|数据类型|  
|--------|----------|  
|PROCEDURE\_CATALOG|String|  
|PROCEDURE\_SCHEMA|String|  
|PROCEDURE\_NAME|String|  
|COLUMN\_NAME|String|  
|COLUMN\_GUID|Guid|  
|COLUMN\_PROPID|Int64|  
|ROWSET\_NUMBER|Int64|  
|ORDINAL\_POSITION|Int64|  
|IS\_NULLABLE|Boolean|  
|DATA\_TYPE|Int32|  
|TYPE\_GUID|Guid|  
|CHARACTER\_MAXIMUM\_LENGTH|Int64|  
|CHARACTER\_OCTET\_LENGTH|Int64|  
|NUMERIC\_PRECISION|Int32|  
|NUMERIC\_SCALE|Int16|  
|DESCRIPTION|String|  
|OVERLOAD|Int16|  
  
### 视图  
  
|列名|数据类型|  
|--------|----------|  
|TABLE\_CATALOG|String|  
|TABLE\_SCHEMA|String|  
|TABLE\_NAME|String|  
|VIEW\_DEFINITION|String|  
|CHECK\_OPTION|Boolean|  
|IS\_UPDATABLE|Boolean|  
|DESCRIPTION|String|  
|DATE\_CREATED|DateTime|  
|DATE\_MODIFIED|DateTime|  
  
### 索引  
  
|列名|数据类型|  
|--------|----------|  
|TABLE\_CATALOG|String|  
|TABLE\_SCHEMA|String|  
|TABLE\_NAME|String|  
|INDEX\_CATALOG|String|  
|INDEX\_SCHEMA|String|  
|INDEX\_NAME|String|  
|PRIMARY\_KEY|Boolean|  
|UNIQUE|Boolean|  
|CLUSTERED|Boolean|  
|TYPE|Int32|  
|FILL\_FACTOR|Int32|  
|INITIAL\_SIZE|Int32|  
|NULLS|Int32|  
|SORT\_BOOKMARKS|Boolean|  
|AUTO\_UPDATE|Boolean|  
|NULL\_COLLATION|Int32|  
|ORDINAL\_POSITION|Int64|  
|COLUMN\_NAME|String|  
|COLUMN\_GUID|Guid|  
|COLUMN\_PROPID|Int64|  
|COLLATION|Int16|  
|CARDINALITY|Decimal|  
|PAGES|Int32|  
|FILTER\_CONDITION|String|  
|INTEGRATED|Boolean|  
  
## Microsoft Jet OLE DB  
 除了通用架构集合之外，Microsoft Jet OLE DB 驱动程序还支持下列特定的架构集合：  
  
-   表  
  
-   Columns  
  
-   过程  
  
-   视图  
  
-   索引  
  
### 表  
  
|列名|数据类型|  
|--------|----------|  
|TABLE\_CATALOG|String|  
|TABLE\_SCHEMA|String|  
|TABLE\_NAME|String|  
|TABLE\_TYPE|String|  
|TABLE\_GUID|Guid|  
|DESCRIPTION|String|  
|TABLE\_PROPID|Int64|  
|DATE\_CREATED|DateTime|  
|DATE\_MODIFIED|DateTime|  
  
### Columns  
  
|列名|数据类型|  
|--------|----------|  
|TABLE\_CATALOG|String|  
|TABLE\_SCHEMA|String|  
|TABLE\_NAME|String|  
|COLUMN\_NAME|String|  
|COLUMN\_GUID|Guid|  
|COLUMN\_PROPID|Int64|  
|ORDINAL\_POSITION|Int64|  
|COLUMN\_HASDEFAULT|Boolean|  
|COLUMN\_DEFAULT|String|  
|COLUMN\_FLAGS|Int64|  
|IS\_NULLABLE|Boolean|  
|DATA\_TYPE|Int32|  
|TYPE\_GUID|Guid|  
|CHARACTER\_MAXIMUM\_LENGTH|Int64|  
|CHARACTER\_OCTET\_LENGTH|Int64|  
|NUMERIC\_PRECISION|Int32|  
|NUMERIC\_SCALE|Int16|  
|DATETIME\_PRECISION|Int64|  
|CHARACTER\_SET\_CATALOG|String|  
|CHARACTER\_SET\_SCHEMA|String|  
|CHARACTER\_SET\_NAME|String|  
|COLLATION\_CATALOG|String|  
|COLLATION\_SCHEMA|String|  
|COLLATION\_NAME|String|  
|DOMAIN\_CATALOG|String|  
|DOMAIN\_SCHEMA|String|  
|DOMAIN\_NAME|String|  
|DESCRIPTION|String|  
  
### 过程  
  
|列名|数据类型|  
|--------|----------|  
|PROCEDURE\_CATALOG|String|  
|PROCEDURE\_SCHEMA|String|  
|PROCEDURE\_NAME|String|  
|PROCEDURE\_TYPE|Int16|  
|PROCEDURE\_DEFINITION|String|  
|DESCRIPTION|String|  
|DATE\_CREATED|DateTime|  
|DATE\_MODIFIED|DateTime|  
  
### 视图  
  
|列名|数据类型|  
|--------|----------|  
|TABLE\_CATALOG|String|  
|TABLE\_SCHEMA|String|  
|TABLE\_NAME|String|  
|VIEW\_DEFINITION|String|  
|CHECK\_OPTION|Boolean|  
|IS\_UPDATABLE|Boolean|  
|DESCRIPTION|String|  
|DATE\_CREATED|DateTime|  
|DATE\_MODIFIED|DateTime|  
  
### 索引  
  
|列名|数据类型|  
|--------|----------|  
|TABLE\_CATALOG|String|  
|TABLE\_SCHEMA|String|  
|TABLE\_NAME|String|  
|INDEX\_CATALOG|String|  
|INDEX\_SCHEMA|String|  
|INDEX\_NAME|String|  
|PRIMARY\_KEY|Boolean|  
|UNIQUE|Boolean|  
|CLUSTERED|Boolean|  
|TYPE|Int32|  
|FILL\_FACTOR|Int32|  
|INITIAL\_SIZE|Int32|  
|NULLS|Int32|  
|SORT\_BOOKMARKS|Boolean|  
|AUTO\_UPDATE|Boolean|  
|NULL\_COLLATION|Int32|  
|ORDINAL\_POSITION|Int64|  
|COLUMN\_NAME|String|  
|COLUMN\_GUID|Guid|  
|COLUMN\_PROPID|Int64|  
|COLLATION|Int16|  
|CARDINALITY|Decimal|  
|PAGES|Int32|  
|FILTER\_CONDITION|String|  
|INTEGRATED|Boolean|  
  
## 请参阅  
 [ADO.NET 托管提供程序和数据集开发人员中心](http://go.microsoft.com/fwlink/?LinkId=217917)