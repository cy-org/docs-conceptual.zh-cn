---
title: "引用完整性约束 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-ado"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 3d3ba44b-4302-40d8-a7a9-62932e0395e5
caps.latest.revision: 3
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 3
---
# 引用完整性约束
实体数据模型 \(EDM\) 中的“引用完整性约束”与关系数据库中的引用完整性约束类似。  与数据库表中的一个（或多个）列可以引用另一个表的主键相同，[实体类型](../../../../docs/framework/data/adonet/entity-type.md)的一个（或多个）[属性](../../../../docs/framework/data/adonet/property.md)可以引用另一个实体类型的[实体键](../../../../docs/framework/data/adonet/entity-key.md)。  所引用的实体类型称为约束的主体端。  引用主体端的实体类型称为约束的依赖端。  
  
 引用完整性约束定义为两个实体类型间的[关联](../../../../docs/framework/data/adonet/association-type.md)的一部分。  引用完整性约束的定义指定了以下信息：  
  
-   约束的主体端。  （一个实体类型，其实体键由依赖端引用。）  
  
-   主体端的实体键。  
  
-   约束的依赖端。  （一个实体类型，它的一个或多个属性引用主体端的实体键。）  
  
-   依赖端的一个或多个引用属性。  
  
 EDM 中的引用完整性约束的用途是确保始终存在有效关联。  有关详细信息，请参阅[外键属性](../../../../docs/framework/data/adonet/foreign-key-property.md)。  
  
## 示例  
 下图显示了一个具有两个关联的概念模型：`WrittenBy` 和 `PublishedBy`。  `Book` 实体类型有一个属性 `PublisherId`，当您为 `PublishedBy` 关联定义一个引用完整性约束时，它将引用 `Publisher` 实体类型的实体键。  
  
 ![RefConstraintModel](../../../../docs/framework/data/adonet/media/refconstraintmodel.gif "RefConstraintModel")  
  
 [ADO.NET 实体框架](../../../../docs/framework/data/adonet/ef/index.md)使用一种称为概念架构定义语言 \([CSDL](../../../../docs/framework/data/adonet/ef/language-reference/csdl-specification.md)\) 的域特定语言 \(DSL\) 来定义概念模型。  下面的 CSDL 为上图所示的概念模型中的 `PublishedBy` 关联定义了一个引用完整性约束。  
  
 [!code-xml[EDM_Example_Model#RefConstraint](../../../../samples/snippets/xml/VS_Snippets_Data/edm_example_model/xml/books4.edmx#refconstraint)]  
  
## 请参阅  
 [实体数据模型关键概念](../../../../docs/framework/data/adonet/entity-data-model-key-concepts.md)   
 [实体数据模型](../../../../docs/framework/data/adonet/entity-data-model.md)