---
title: "关联集 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-ado"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: a65247b6-ce59-44ea-974c-14ae20a7995f
caps.latest.revision: 3
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 3
---
# 关联集
“关联集”是相同类型的[关联](../../../../docs/framework/data/adonet/association-type.md)实例的逻辑容器。  关联集不是一种数据建模构造，也就是说，它没有描述数据结构或关系。  相反，关联集提供了一种承载或存储环境构造（例如公共语言运行库或 SQL Server 数据库）来分组关联实例，以便可以将它们映射到某个数据存储区。  
  
 关联集在[实体容器](../../../../docs/framework/data/adonet/entity-container.md)中定义，后者是[实体集](../../../../docs/framework/data/adonet/entity-set.md)和关联集的逻辑分组。  
  
 关联集的定义包含以下信息：  
  
-   关联集名称。  （必需）  
  
-   要包含其实例的关联。  （必需）  
  
-   两个[关联集端](../../../../docs/framework/data/adonet/association-set-end.md)。  
  
## 示例  
 下图显示了一个具有两个关联的概念模型：`PublishedBy` 和 `WrittenBy`。  上图没有传达有关关联集的信息，但下图显示了一个基于此模型的关联集和实体集的示例。  
  
 ![示例模型](../../../../docs/framework/data/adonet/media/examplemodel.gif "ExampleModel")  
  
 下面的示例显示了基于上面所示的概念模型的一个关联集 \(`PublishedBy`\) 和两个实体集（`Books` 和 `Publishers`）。  `Books` 实体集中的 Bi 表示运行时的 `Book` 实体类型实例。  类似地，Pj 表示 `Publishers` 实体集中的 `Publisher` 实例。  BiPj 表示 `PublishedBy` 关联集中的 `PublishedBy` 关联实例。  
  
 ![设置示例](../../../../docs/framework/data/adonet/media/setsexample.gif "SetsExample")  
  
 [ADO.NET 实体框架](../../../../docs/framework/data/adonet/ef/index.md)使用一种称为概念架构定义语言 \([CSDL](../../../../docs/framework/data/adonet/ef/language-reference/csdl-specification.md)\) 的域特定语言 \(DSL\) 来定义概念模型。  下面的 CSDL 定义了一个实体容器，其中对于上图所示的每个关联都有一个关联集。  请注意，每个关联集的名称和关联都是使用 XML 特性定义的。  
  
 [!code-xml[EDM_Example_Model#EntityContainerExample](../../../../samples/snippets/xml/VS_Snippets_Data/edm_example_model/xml/books.edmx#entitycontainerexample)]  
  
 每个关联可以定义多个关联集，只要没有任何两个关联集共享一个[关联集端](../../../../docs/framework/data/adonet/association-set-end.md)即可。  下面的 CSDL 定义了一个实体容器，其中包含 `WrittenBy` 关联的两个关联集。  请注意，为 `Book` 和 `Author` 实体类型定义了多个实体集，并且没有关联集共享关联集端。  
  
 [!code-xml[EDM_Example_Model#MultipleAssociationSets](../../../../samples/snippets/xml/VS_Snippets_Data/edm_example_model/xml/books3.edmx#multipleassociationsets)]  
  
## 请参阅  
 [实体数据模型关键概念](../../../../docs/framework/data/adonet/entity-data-model-key-concepts.md)   
 [实体数据模型](../../../../docs/framework/data/adonet/entity-data-model.md)   
 [外键属性](../../../../docs/framework/data/adonet/foreign-key-property.md)