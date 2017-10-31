---
title: "LINQ to ADO.NET（门户网站页）"
ms.custom: 
ms.date: 2015-07-20
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology:
- devlang-csharp
ms.topic: article
dev_langs:
- CSharp
ms.assetid: 6bd269b4-3509-4688-b672-836008704182
caps.latest.revision: 3
author: BillWagner
ms.author: wiwagn
translation.priority.mt:
- cs-cz
- pl-pl
- pt-br
- tr-tr
ms.translationtype: HT
ms.sourcegitcommit: 306c608dc7f97594ef6f72ae0f5aaba596c936e1
ms.openlocfilehash: d768d5796e5eb7ff4fed071d906c672b83b42d2b
ms.contentlocale: zh-cn
ms.lasthandoff: 07/28/2017

---
# <a name="linq-to-adonet-portal-page"></a>LINQ to ADO.NET（门户网站页）
通过 [!INCLUDE[linq_adonet](~/includes/linq-adonet-md.md)]，你可以使用 [!INCLUDE[vbteclinqext](~/includes/vbteclinqext-md.md)] 编程模型针对 [!INCLUDE[vstecado](~/includes/vstecado-md.md)] 中的任何可枚举对象进行查询。  
  
> [!NOTE]
>  [!INCLUDE[linq_adonet](~/includes/linq-adonet-md.md)] 文档位于 .NET Framework SDK 的 ADO.NET 部分：[LINQ 和 ADO.NET](http://msdn.microsoft.com/library/bf0c8f93-3ff7-49f3-8aed-f2b7ac938dec)。  
  
 有三种独立的 ADO.NET [!INCLUDE[vbteclinqext](~/includes/vbteclinqext-md.md)] 技术：[!INCLUDE[linq_dataset](~/includes/linq-dataset-md.md)]、[!INCLUDE[vbtecdlinq](~/includes/vbtecdlinq-md.md)] 和 [!INCLUDE[linq_entities](~/includes/linq-entities-md.md)]。 [!INCLUDE[linq_dataset](~/includes/linq-dataset-md.md)] 提供针对 <xref:System.Data.DataSet> 的形式多样的优化查询，[!INCLUDE[vbtecdlinq](~/includes/vbtecdlinq-md.md)] 使你可直接查询 [!INCLUDE[ssNoVersion](~/includes/ssnoversion-md.md)] 数据库架构，而 [!INCLUDE[linq_entities](~/includes/linq-entities-md.md)] 允许你查询 [!INCLUDE[adonet_edm](~/includes/adonet-edm-md.md)]。  
  
## <a name="linq-to-dataset"></a>LINQ to DataSet  
 <xref:System.Data.DataSet> 是 [!INCLUDE[vstecado](~/includes/vstecado-md.md)] 中使用最广泛的组件之一，也是断开连接的编程模型的关键元素，该模型是构建 [!INCLUDE[vstecado](~/includes/vstecado-md.md)] 的基础。 <xref:System.Data.DataSet> 虽然具有突出的优点，但其查询功能也存在限制。  
  
 [!INCLUDE[linq_dataset](~/includes/linq-dataset-md.md)] 让你可通过使用为其他多种数据源提供的相同查询功能，在 <xref:System.Data.DataSet> 中加入更丰富的查询功能。  
  
 有关详细信息，请参阅 [LINQ to DataSet](../../../../framework/data/adonet/linq-to-dataset.md)。  
  
## <a name="linq-to-sql"></a>LINQ to SQL  
 [!INCLUDE[vbtecdlinq](~/includes/vbtecdlinq-md.md)] 提供用于将关系数据作为对象进行管理的运行时基础结构。 在 [!INCLUDE[vbtecdlinq](~/includes/vbtecdlinq-md.md)] 中，关系数据库的数据模型映射到用开发人员所用的编程语言表示的对象模型。 执行应用程序时，[!INCLUDE[vbtecdlinq](~/includes/vbtecdlinq-md.md)] 会将对象模型中的语言集成查询转换为 SQL，然后将其发送到数据库进行执行。 数据库返回结果时，[!INCLUDE[vbtecdlinq](~/includes/vbtecdlinq-md.md)] 会将结果转换回可操作对象。  
  
 [!INCLUDE[vbtecdlinq](~/includes/vbtecdlinq-md.md)] 包括对数据库中的已存储过程和用户定义的函数和对象模型中的继承的支持。  
  
 有关详细信息，请参阅 [LINQ to SQL](https://msdn.microsoft.com/library/bb386976)。  
  
## <a name="linq-to-entities"></a>LINQ to Entities  
 通过 [!INCLUDE[adonet_edm](~/includes/adonet-edm-md.md)]，在 .NET 环境中将关系数据作为对象公开。 这使得对象层成为实现 [!INCLUDE[vbteclinq](~/includes/vbteclinq-md.md)] 支持的理想目标，开发人员可以采用生成业务逻辑所用的语言来构建数据库查询。 此功能称为 [!INCLUDE[linq_entities](~/includes/linq-entities-md.md)]。 有关详细信息，请参阅 [LINQ to Entities](../../../../framework/data/adonet/ef/language-reference/linq-to-entities.md)。  
  
## <a name="see-also"></a>请参阅  
 [LINQ 和 ADO.NET](http://msdn.microsoft.com/library/bf0c8f93-3ff7-49f3-8aed-f2b7ac938dec)   
 [语言集成查询 (LINQ) (C#)](../../../../csharp/programming-guide/concepts/linq/index.md)

