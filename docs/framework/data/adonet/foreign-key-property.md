---
title: "外键属性 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-ado"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 23cb6729-544d-4f67-9ee7-44e8a6545587
caps.latest.revision: 3
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 3
---
# 外键属性
实体数据模型 \(EDM\) 中的“外键属性”是某个[实体类型](../../../../docs/framework/data/adonet/entity-type.md)的一个或一组基元类型[属性](../../../../docs/framework/data/adonet/property.md)，其中包含另一个实体类型的[实体键](../../../../docs/framework/data/adonet/entity-key.md)。  
  
 外键属性相当于关系数据库中的外键列。  关系数据库中的外键列用来在表中的行之间建立关系，同样，概念模型中的外键属性用于在实体类型之间建立[关联](../../../../docs/framework/data/adonet/association-type.md)。  当两个实体类型中有一个类型具有外键属性时，将使用[引用完整性约束](../../../../docs/framework/data/adonet/referential-integrity-constraint.md)来定义这两个实体类型之间的关联。  
  
## 示例  
 下图显示了一个具有三个实体类型的概念模型：`Book`、`Publisher` 和 `Author`。  `Book` 实体类型有一个属性 `PublisherId`，当您为 `PublishedBy` 关联定义一个引用完整性约束时，它将引用 `Publisher` 实体类型的实体键。  
  
 ![RefConstraintModel](../../../../docs/framework/data/adonet/media/refconstraintmodel.gif "RefConstraintModel")  
  
 [ADO.NET 实体框架](../../../../docs/framework/data/adonet/ef/index.md)使用一种称为概念架构定义语言 \([CSDL](../../../../docs/framework/data/adonet/ef/language-reference/csdl-specification.md)\) 的域特定语言 \(DSL\) 来定义概念模型。  下面的 CSDL 使用外键属性 `PublisherId` 为上图所示的概念模型中的 `PublishedBy` 关联定义了一个引用完整性约束。  
  
 [!code-xml[EDM_Example_Model#RefConstraint](../../../../samples/snippets/xml/VS_Snippets_Data/edm_example_model/xml/books4.edmx#refconstraint)]  
  
## 请参阅  
 [实体数据模型关键概念](../../../../docs/framework/data/adonet/entity-data-model-key-concepts.md)   
 [实体数据模型](../../../../docs/framework/data/adonet/entity-data-model.md)