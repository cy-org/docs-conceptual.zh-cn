---
title: "如何：使用 EntityCommand 执行参数化存储过程 | Microsoft Docs"
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
ms.assetid: 4f5639bf-bb7f-4982-bb1d-c7caa4348888
caps.latest.revision: 3
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 3
---
# 如何：使用 EntityCommand 执行参数化存储过程
本主题说明如何使用 <xref:System.Data.EntityClient.EntityCommand> 类执行参数化存储过程。  
  
### 运行本示例中的代码  
  
1.  将 [School Model](http://msdn.microsoft.com/zh-cn/859a9587-81ea-4a45-9bc0-f8d330e1adac)添加到您的项目并将项目配置为使用[!INCLUDE[adonet_ef](../../../../../includes/adonet-ef-md.md)]。  有关详细信息，请参阅[How to: Use the Entity Data Model Wizard](http://msdn.microsoft.com/zh-cn/dadb058a-c5d9-4c5c-8b01-28044112231d)。  
  
2.  在应用程序的代码页中，添加以下 `using` 语句（在 Visual Basic 中为 `Imports`）：  
  
     [!code-csharp[DP EntityServices Concepts#Namespaces](../../../../../samples/snippets/csharp/VS_Snippets_Data/dp entityservices concepts/cs/source.cs#namespaces)]
     [!code-vb[DP EntityServices Concepts#Namespaces](../../../../../samples/snippets/visualbasic/VS_Snippets_Data/dp entityservices concepts/vb/source.vb#namespaces)]  
  
3.  导入 `GetStudentGrades` 存储过程并将 `CourseGrade` 实体指定为返回类型。  有关如何导入存储过程的信息，请参见[How to: Import a Stored Procedure](http://msdn.microsoft.com/zh-cn/24e68bf4-bd6d-428d-bc35-92d7b8e3736d)。  
  
## 示例  
 下面的代码执行 `GetStudentGrades` 存储过程，其中，`StudentId` 为必需的参数。  然后由 <xref:System.Data.EntityClient.EntityDataReader> 读取结果。  
  
 [!code-csharp[DP EntityServices Concepts#StoredProcWithEntityCommand](../../../../../samples/snippets/csharp/VS_Snippets_Data/dp entityservices concepts/cs/source.cs#storedprocwithentitycommand)]
 [!code-vb[DP EntityServices Concepts#StoredProcWithEntityCommand](../../../../../samples/snippets/visualbasic/VS_Snippets_Data/dp entityservices concepts/vb/source.vb#storedprocwithentitycommand)]  
  
## 请参阅  
 [用于实体框架的 EntityClient 提供程序](../../../../../docs/framework/data/adonet/ef/entityclient-provider-for-the-entity-framework.md)