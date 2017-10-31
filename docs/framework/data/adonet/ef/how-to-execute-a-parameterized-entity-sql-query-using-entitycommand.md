---
title: "如何：使用 EntityCommand 执行参数化 Entity SQL 查询 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-ado"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "VB"
  - "CSharp"
  - "C++"
  - "ESQL"
  - "jsharp"
ms.assetid: e93fea43-7e03-4d7d-9fee-2517b8b88cba
caps.latest.revision: 3
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 3
---
# 如何：使用 EntityCommand 执行参数化 Entity SQL 查询
本主题介绍如何使用 <xref:System.Data.EntityClient.EntityCommand> 对象执行具有参数的 [!INCLUDE[esql](../../../../../includes/esql-md.md)] 查询。  
  
### 运行本示例中的代码  
  
1.  将 [AdventureWorks Sales Model](http://msdn.microsoft.com/zh-cn/f16cd988-673f-4376-b034-129ca93c7832)添加到您的项目并将项目配置为使用[!INCLUDE[adonet_ef](../../../../../includes/adonet-ef-md.md)]。  有关详细信息，请参阅[How to: Use the Entity Data Model Wizard](http://msdn.microsoft.com/zh-cn/dadb058a-c5d9-4c5c-8b01-28044112231d)。  
  
2.  在应用程序的代码页中，添加以下 `using` 语句（在 Visual Basic 中为 `Imports`）：  
  
     [!code-csharp[DP EntityServices Concepts#Namespaces](../../../../../samples/snippets/csharp/VS_Snippets_Data/dp entityservices concepts/cs/source.cs#namespaces)]
     [!code-vb[DP EntityServices Concepts#Namespaces](../../../../../samples/snippets/visualbasic/VS_Snippets_Data/dp entityservices concepts/vb/source.vb#namespaces)]  
  
## 示例  
 以下示例显示如何使用两个参数构造一个查询字符串。  然后，它创建 <xref:System.Data.EntityClient.EntityCommand>，将两个参数添加到该 <xref:System.Data.EntityClient.EntityCommand> 的 <xref:System.Data.EntityClient.EntityParameter> 集合，并循环访问 `Contact` 项的集合。  
  
 [!code-csharp[DP EntityServices Concepts#ParameterizedQueryWithEntityCommand](../../../../../samples/snippets/csharp/VS_Snippets_Data/dp entityservices concepts/cs/source.cs#parameterizedquerywithentitycommand)]
 [!code-vb[DP EntityServices Concepts#ParameterizedQueryWithEntityCommand](../../../../../samples/snippets/visualbasic/VS_Snippets_Data/dp entityservices concepts/vb/source.vb#parameterizedquerywithentitycommand)]  
  
## 请参阅  
 [How to: Execute a Parameterized Query](http://msdn.microsoft.com/zh-cn/42048f03-c65c-4d98-b50a-3e7d537a63e8)   
 [Entity SQL 语言](../../../../../docs/framework/data/adonet/ef/language-reference/entity-sql-language.md)