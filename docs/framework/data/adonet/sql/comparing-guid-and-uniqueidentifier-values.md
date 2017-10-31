---
title: "比较 GUID 和 uniqueidentifier 值 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-ado"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: aababd75-2335-43e3-ace8-4b7ae84191a8
caps.latest.revision: 4
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 4
---
# 比较 GUID 和 uniqueidentifier 值
SQL Server 中的全局唯一标识符 \(GUID\) 数据类型由 `uniqueidentifier` 数据类型表示，用于存储 16 字节的二进制值。  GUID 是一个二进制数字，其主要用途是作为标识符，该标识符在拥有位于许多地点的许多计算机的网络中必须是唯一的。  GUID 可以通过调用 Transact\-SQL NEWID 函数生成，保证在全局是唯一的。  有关更多信息，请参见“SQL Server 联机图书”中的“使用 uniqueidentifier 数据”。  
  
## 使用 SqlGuid 值  
 因为 GUID 值很长并且不明确，所以对用户没有意义。  如果键值使用随机生成的 GUID，并且您插入了许多行，将随机 I\/O 编入索引可能会对性能造成负面影响。  与其他数据类型相比，GUID 也相对较大。  通常，我们建议只对没有其他适用的数据类型的范围非常窄的方案使用 GUID。  
  
### 比较 GUID 值  
 `uniqueidentifier` 值可以使用比较运算符。  但是，没有通过比较两个值的位模式实现排序。  允许对 `uniqueidentifier` 值进行的唯一操作是比较（\=、\<\>、\<、\>、\<\=、\>\=）和 NULL 校验（IS NULL 和 IS NOT NULL）。  不允许使用任何其他算术运算符。  
  
 <xref:System.Guid> 和 <xref:System.Data.SqlTypes.SqlGuid> 都具有 `CompareTo` 方法，用于比较不同的 GUID 值。  但是，`System.Guid.CompareTo` 和 `SqlTypes.SqlGuid.CompareTo` 的实现方式有所不同。  <xref:System.Data.SqlTypes.SqlGuid> 使用 SQL Server 行为来实现 `CompareTo`，其中，值的最后 6 个字节是最高有效字节。  <xref:System.Guid> 计算全部 16 个字节。  以下示例演示这种行为的差异。  代码的第一部分显示未排序的 <xref:System.Guid> 值，代码的第二部分显示排序的 <xref:System.Guid> 值。  第三部分显示排序的 <xref:System.Data.SqlTypes.SqlGuid> 值。  输出显示在代码列表下。  
  
 [!code-csharp[DataWorks SqlTypes.Guid#1](../../../../../samples/snippets/csharp/VS_Snippets_ADO.NET/DataWorks SqlTypes.Guid/CS/source.cs#1)]
 [!code-vb[DataWorks SqlTypes.Guid#1](../../../../../samples/snippets/visualbasic/VS_Snippets_ADO.NET/DataWorks SqlTypes.Guid/VB/source.vb#1)]  
  
 此示例将生成下列结果。  
  
```  
Unsorted Guids:  
3aaaaaaa-bbbb-cccc-dddd-2eeeeeeeeeee  
2aaaaaaa-bbbb-cccc-dddd-1eeeeeeeeeee  
1aaaaaaa-bbbb-cccc-dddd-3eeeeeeeeeee  
  
Sorted Guids:  
1aaaaaaa-bbbb-cccc-dddd-3eeeeeeeeeee  
2aaaaaaa-bbbb-cccc-dddd-1eeeeeeeeeee  
3aaaaaaa-bbbb-cccc-dddd-2eeeeeeeeeee  
  
Sorted SqlGuids:  
2aaaaaaa-bbbb-cccc-dddd-1eeeeeeeeeee  
3aaaaaaa-bbbb-cccc-dddd-2eeeeeeeeeee  
1aaaaaaa-bbbb-cccc-dddd-3eeeeeeeeeee  
```  
  
## 请参阅  
 [SQL Server 数据类型和 ADO.NET](../../../../../docs/framework/data/adonet/sql/sql-server-data-types.md)   
 [ADO.NET 托管提供程序和数据集开发人员中心](http://go.microsoft.com/fwlink/?LinkId=217917)