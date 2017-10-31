---
title: "System.Object 方法 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-ado"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 5397fca0-689e-443e-802f-e1cbdc866427
caps.latest.revision: 2
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 2
---
# System.Object 方法
[!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] 支持以下 <xref:System.Object> 方法。  
  
|||  
|-|-|  
|<xref:System.Object.Equals%28System.Object%29?displayProperty=fullName>|<xref:System.Object.Equals%28System.Object%2CSystem.Object%29?displayProperty=fullName>|  
|<xref:System.Object.ToString?displayProperty=fullName>||  
  
 [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] 不支持以下 <xref:System.Object> 方法。  
  
|||  
|-|-|  
|<xref:System.Object.GetHashCode?displayProperty=fullName>|<xref:System.Object.ReferenceEquals%28System.Object%2CSystem.Object%29?displayProperty=fullName>|  
|<xref:System.Object.MemberwiseClone?displayProperty=fullName>|<xref:System.Object.GetType?displayProperty=fullName>|  
|用于二进制类型（如 `BINARY`、`VARBINARY`、`IMAGE` 和 `TIMESTAMP`）的 <xref:System.Object.ToString?displayProperty=fullName>。||  
  
## 与 .NET 的差异  
 用于双精度类型的 <xref:System.Object.ToString?displayProperty=fullName> 的输出对 SQL 使用 SQL `CONVERT`\(NVARCHAR\(30\), @x, 2\)。  在这种情况下 SQL 始终使用 16 位科学记数法（例如，用“0.000000000000000e\+000”表示 0）。  因此，<xref:System.Object.ToString?displayProperty=fullName> 转换与 .NET Framework 中的 <xref:System.Convert.ToString%2A?displayProperty=fullName> 产生的字符串不同。  
  
## 请参阅  
 [数据类型和函数](../../../../../../docs/framework/data/adonet/sql/linq/data-types-and-functions.md)