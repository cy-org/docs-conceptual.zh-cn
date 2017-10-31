---
title: "实体集 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-ado"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 59ec6ab0-88e5-4d25-b112-7a4eccbe61f0
caps.latest.revision: 3
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 3
---
# 实体集
“实体集”是某个[实体类型](../../../../docs/framework/data/adonet/entity-type.md)的实例和派生自该实例类型的任何类型的实例的逻辑容器。  （有关派生类型的信息，请参见[实体数据模型：继承](../../../../docs/framework/data/adonet/entity-data-model-inheritance.md)。）实体类型与实体集之间的关系类似于关系数据库中行与表之间的关系：与行类似，实体类型描述了数据结构，而与表类似，实体集包含了给定结构的实例。  实体集不是一种数据建模构造，它没有描述数据结构。  相反，实体集提供了一种承载或存储环境构造（例如公共语言运行库或 SQL Server 数据库）来分组实体类型实例，以便可以将它们映射到某个数据存储区。  
  
 实体集在[实体容器](../../../../docs/framework/data/adonet/entity-container.md)中定义，后者是实体集和[关联集](../../../../docs/framework/data/adonet/association-set.md)的逻辑分组。  
  
 对于实体集中存在的实体类型实例，必须满足以下条件：  
  
-   实例的类型或者与实体集所基于的实体类型相同，或者是该实体类型的一个子类型。  
  
-   实例的[实体键](../../../../docs/framework/data/adonet/entity-key.md)在该实体集中是唯一的。  
  
-   实例不存在于任何其他实体集中。  
  
    > [!NOTE]
    >  可以使用相同的实体类型定义多个实体集，但某个给定实体类型的一个实例只能存在于一个实体集中。  
  
 不必为概念模型中的每个实体类型都定义实体集。  
  
## 示例  
 下图显示了一个具有三个实体类型的概念模型：`Book`、`Publisher` 和 `Author`。  
  
 ![示例模型](../../../../docs/framework/data/adonet/media/examplemodel.gif "ExampleModel")  
  
 下图显示了基于上面所示的概念模型的两个实体集（`Books` 和 `Publishers`）和一个关联集 \(`PublishedBy`\)。  `Books` 实体集中的 Bi 表示运行时的 `Book` 实体类型实例。  类似地，Pj 表示 `Publishers` 实体集中的 `Publisher` 实例。  BiPj 表示 `PublishedBy` 关联集中的 `PublishedBy` 关联实例。  
  
 ![设置示例](../../../../docs/framework/data/adonet/media/setsexample.gif "SetsExample")  
  
 [ADO.NET 实体框架](../../../../docs/framework/data/adonet/ef/index.md)使用一种称为概念架构定义语言 \([CSDL](../../../../docs/framework/data/adonet/ef/language-reference/csdl-specification.md)\) 的域特定语言 \(DSL\) 来定义概念模型。  下面的 CSDL 定义了一个实体容器，其中对于上图所示的概念模型中的每个实体类型都有一个实体集。  请注意，每个实体集的名称和实体类型都是使用 XML 特性定义的。  
  
 [!code-xml[EDM_Example_Model#EntityContainerExample](../../../../samples/snippets/xml/VS_Snippets_Data/edm_example_model/xml/books.edmx#entitycontainerexample)]  
  
 每个类型可以定义多个实体集 \(MEST\)。  下面的 CSDL 定义了一个实体容器，其中包含 `Book` 实体类型的两个实体集：  
  
 [!code-xml[EDM_Example_Model#MESTExample](../../../../samples/snippets/xml/VS_Snippets_Data/edm_example_model/xml/books2.edmx#mestexample)]  
  
## 请参阅  
 [实体数据模型关键概念](../../../../docs/framework/data/adonet/entity-data-model-key-concepts.md)   
 [实体数据模型](../../../../docs/framework/data/adonet/entity-data-model.md)