---
title: "如何：执行返回复杂类型的查询 | Microsoft Docs"
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
ms.assetid: c2209fdb-70ef-4dea-8bb8-097fe96f5563
caps.latest.revision: 3
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 3
---
# 如何：执行返回复杂类型的查询
本主题演示如何执行返回包含复杂类型属性的实体类型对象的 [!INCLUDE[esql](../../../../../includes/esql-md.md)] 查询。  
  
### 运行本示例中的代码  
  
1.  将 [AdventureWorks Sales Model](http://msdn.microsoft.com/zh-cn/f16cd988-673f-4376-b034-129ca93c7832)添加到您的项目并将项目配置为使用[!INCLUDE[adonet_ef](../../../../../includes/adonet-ef-md.md)]。  有关详细信息，请参阅[How to: Use the Entity Data Model Wizard](http://msdn.microsoft.com/zh-cn/dadb058a-c5d9-4c5c-8b01-28044112231d)。  
  
2.  在应用程序的代码页中，添加以下 `using` 语句（在 Visual Basic 中为 `Imports`）：  
  
     [!code-csharp[DP EntityServices Concepts#Namespaces](../../../../../samples/snippets/csharp/VS_Snippets_Data/dp entityservices concepts/cs/source.cs#namespaces)]
     [!code-vb[DP EntityServices Concepts#Namespaces](../../../../../samples/snippets/visualbasic/VS_Snippets_Data/dp entityservices concepts/vb/source.vb#namespaces)]  
  
3.  双击 .edmx 文件可在实体设计器的[模型浏览器窗口](http://msdn.microsoft.com/zh-cn/94e836e8-a5ea-47ff-aa3e-599d8a02ebfd)中显示模型。  在实体设计器图面上，选择 `Contact` 实体类型的 `Email` 和 `Phone` 属性，然后右击并选择**“重构为新的复杂类型”**。  
  
4.  具有选定 `Email` 和 `Phone` 属性的新复杂类型将添加到**“模型浏览器”**。  该复杂类型具有一个默认名称：在**“属性”**窗口中将该类型重命名为 `EmailPhone`。  此外，新的 `ComplexProperty` 属性将添加到 `Contact` 实体类型。  将该属性重命名为 `EmailPhoneComplexType`。  
  
     有关使用“实体数据模型向导”创建和修改复杂类型的信息，请参见[How to: Refactor Existing Properties into a Complex Type Property](http://msdn.microsoft.com/zh-cn/5b2eb3b3-693d-42cb-b43a-405812d677eb)和[How to: Create and Modify Complex Types](http://msdn.microsoft.com/zh-cn/afb8e206-0ffe-4597-b6d4-6ab566897e1d)。  
  
## 示例  
 下面的示例执行一个查询，该查询返回 `Contact` 对象的集合并显示  对象的两个属性：`ContactID` 和 `EmailPhoneComplexType` 复杂类型的值。  
  
 [!code-csharp[DP EntityServices Concepts#ComplexTypeWithEntityCommand](../../../../../samples/snippets/csharp/VS_Snippets_Data/dp entityservices concepts/cs/source.cs#complextypewithentitycommand)]
 [!code-vb[DP EntityServices Concepts#ComplexTypeWithEntityCommand](../../../../../samples/snippets/visualbasic/VS_Snippets_Data/dp entityservices concepts/vb/source.vb#complextypewithentitycommand)]