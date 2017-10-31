---
title: "如何：投影查询结果（WCF 数据服务） | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-oob"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "投影 [WCF 数据服务]"
  - "查询投影 [WCF 数据服务]"
  - "WCF 数据服务, 投影"
  - "WCF 数据服务, 查询"
ms.assetid: 474ac625-8770-43ba-8320-d3315ea9530f
caps.latest.revision: 3
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 3
---
# 如何：投影查询结果（WCF 数据服务）
投影提供减少查询返回的数据量的机制，方法是指定在响应中仅返回某个实体的某些属性。  可以通过在 LINQ 查询中使用 [!INCLUDE[ssAstoria](../../../../includes/ssastoria-md.md)] 查询选项或使用 `$select`select 子句（在 Visual Basic 中为 [Select](../Topic/select%20clause%20\(C%23%20Reference\).md)）对 [查询结果执行投影。](../Topic/Select%20Clause%20\(Visual%20Basic\).md) 有关更多信息，请参见[查询数据服务](../../../../docs/framework/data/wcf/querying-the-data-service-wcf-data-services.md)。  
  
 本主题中的示例使用罗斯文示例数据服务和自动生成的客户端数据服务类。  此服务和这些客户端数据类是在完成 [WCF 数据服务快速入门](../../../../docs/framework/data/wcf/quickstart-wcf-data-services.md)时创建的。  
  
## 示例  
 下面的示例演示一个 LINQ 查询，该查询将 Customers 实体投影到新的 CustomerAddress 类型，该类型仅包含特定地址属性以及标识属性。  此 `CustomerAddress` 类是在客户端上定义的并且具有客户端库可将它识别为实体类型的特性。  
  
 [!code-csharp[Astoria Northwind Client#SelectCustomerAddress](../../../../samples/snippets/csharp/VS_Snippets_Misc/astoria northwind client/cs/source.cs#selectcustomeraddress)]
 [!code-vb[Astoria Northwind Client#SelectCustomerAddress](../../../../samples/snippets/visualbasic/VS_Snippets_Misc/astoria northwind client/vb/source.vb#selectcustomeraddress)]  
  
## 示例  
 下面的示例演示一个 LINQ 查询，该查询将返回的 Customers 实体投影到新的 CustomerAddressNonEntity 类型，该类型仅包含特定地址属性，不包含标识属性。  此 `CustomerAddressNonEntity` 类是在客户端上定义的，但不具有作为实体类型的特性。  
  
 [!code-csharp[Astoria Northwind Client#SelectCustomerAddressNonEntity](../../../../samples/snippets/csharp/VS_Snippets_Misc/astoria northwind client/cs/source.cs#selectcustomeraddressnonentity)]
 [!code-vb[Astoria Northwind Client#SelectCustomerAddressNonEntity](../../../../samples/snippets/visualbasic/VS_Snippets_Misc/astoria northwind client/vb/source.vb#selectcustomeraddressnonentity)]  
  
## 示例  
 下面的示例演示在上述示例中使用的 `CustomerAddress` `CustomerAddressNonEntity` 类型的定义。  
  
 [!code-csharp[Astoria Northwind Client#CustomerAddressDefinition](../../../../samples/snippets/csharp/VS_Snippets_Misc/astoria northwind client/cs/customeraddress.cs#customeraddressdefinition)]
 [!code-vb[Astoria Northwind Client#CustomerAddressDefinition](../../../../samples/snippets/visualbasic/VS_Snippets_Misc/astoria northwind client/vb/customeraddress.vb#customeraddressdefinition)]