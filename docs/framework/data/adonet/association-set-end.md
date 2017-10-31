---
title: "关联集端 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-ado"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: fe4bf1d3-047a-4a37-98c5-a66e70811346
caps.latest.revision: 4
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 4
---
# 关联集端
“关联集端”标识位于某个[关联集](../../../../docs/framework/data/adonet/association-set.md)一端的[实体类型](../../../../docs/framework/data/adonet/entity-type.md)和[实体集](../../../../docs/framework/data/adonet/entity-set.md)。  关联集端定义为关联集的一部分；一个关联集必须有且只有两个关联集端。  
  
 关联集端定义包含以下信息：  
  
-   关联集中涉及的实体类型之一。  （必需）  
  
-   关联集中涉及的实体类型的实体集。  （必需）  
  
## 示例  
 下图显示了一个具有两个关联的概念模型：`WrittenBy` 和 `PublishedBy`。  
  
 ![示例模型](../../../../docs/framework/data/adonet/media/examplemodel.gif "ExampleModel")  
  
 下图显示了基于上面所示的概念模型的一个关联集 \(`PublishedBy`\) 和两个实体集（`Books` 和 `Publishers`）。  关联集端是 `Books` 和 `Publishers` 实体集。  `Books` 实体集中的 Bi 表示运行时的 `Book` 实体类型实例。  类似地，Pj 表示 `Publishers` 实体集中的 `Publisher` 实例。  BiPj 表示 `PublishedBy` 关联集中的 `PublishedBy` 关联实例。  
  
 ![设置示例](../../../../docs/framework/data/adonet/media/setsexample.gif "SetsExample")  
  
 [ADO.NET 实体框架](../../../../docs/framework/data/adonet/ef/index.md)使用一种称为概念架构定义语言 \([CSDL](../../../../docs/framework/data/adonet/ef/language-reference/csdl-specification.md)\) 的 DSL 来定义概念模型。  下面的 CSDL 定义了一个实体容器，其中对于上图所示的每个关联都有一个关联集。  请注意，关联集端定义为每个关联集定义的一部分。  
  
 [!code-xml[EDM_Example_Model#EntityContainerExample](../../../../samples/snippets/xml/VS_Snippets_Data/edm_example_model/xml/books.edmx#entitycontainerexample)]  
  
## 请参阅  
 [实体数据模型关键概念](../../../../docs/framework/data/adonet/entity-data-model-key-concepts.md)   
 [实体数据模型](../../../../docs/framework/data/adonet/entity-data-model.md)