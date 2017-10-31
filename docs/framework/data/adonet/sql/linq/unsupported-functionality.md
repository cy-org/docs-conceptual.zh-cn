---
title: "不支持的功能 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-ado"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: e480cfb5-697e-42c8-bed5-9264c945c4f9
caps.latest.revision: 2
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 2
---
# 不支持的功能
在 LINQ to SQL 中，无法通过转换现有的公共语言运行库 \(CLR\) 和 .NET Framework 构造公开以下 SQL 功能：  
  
-   `STDDEV`  
  
-   `LIKE`  
  
     尽管通过直接转换，不支持 `LIKE`，但是 <xref:System.Data.Linq.SqlClient.SqlMethods> 类中仍存在相似的功能。  有关详细信息，请参阅[M:System.Data.Linq.SqlClient.SqlMethods.Like\(System.String,System.String](assetId:///M:System.Data.Linq.SqlClient.SqlMethods.Like(System.String,System.String?qualifyHint=True&autoUpgrade=True)。  
  
-   `DATEDIFF`  
  
     LINQ to SQL 具有对 `DATEDIFF` 的有限支持。  [SqlMethods](assetId:///T:System.Data.Linq.SqlClient.SqlMethods?qualifyHint=False&autoUpgrade=True) 类中存在相似的功能。  
  
-   `ROUND`  
  
     LINQ to SQL 具有对 `ROUND` 的有限支持。  有关详细信息，请参阅[System.Math 方法](../Topic/System.Math%20Methods.md)。  
  
## 请参阅  
 [数据类型和函数](../Topic/Data%20Types%20and%20Functions.md)