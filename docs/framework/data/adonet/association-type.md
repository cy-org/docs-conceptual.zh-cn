---
title: "关联类型 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-ado"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 26c409f6-06e8-4441-ac78-1b1076a3c005
caps.latest.revision: 3
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 3
---
# 关联类型
“关联类型”（也称为关联）是用来描述实体数据模型 \(EDM\) 中的关系的基本构造块。  在概念模型中，关联表示两个[实体类型](../../../../docs/framework/data/adonet/entity-type.md)（例如 `Customer` 和 `Order`）之间的关系。  在应用程序中，一个关联实例表示一个特定的关联（例如 `Customer` 实例与 `Order` 实例之间的关联）。  关联实例按逻辑分组在[关联集](../../../../docs/framework/data/adonet/association-set.md)中。  
  
 关联定义包含以下信息：  
  
-   唯一名称。  （必需）  
  
-   两个[关联端](../../../../docs/framework/data/adonet/association-end.md)，关系中的每个实体类型一个。  （必需）  
  
    > [!NOTE]
    >  关联不能表示两个以上的实体类型之间的关系。  但是，通过为每个关联端指定相同的实体类型，关联可以定义自身关系。  
  
-   一个[引用完整性约束](../../../../docs/framework/data/adonet/referential-integrity-constraint.md)。  （可选）  
  
 每个关联端必须指定一个[关联端重数](../../../../docs/framework/data/adonet/association-end-multiplicity.md)，它表明在关联的一端可以存在的实体类型实例的数量。  关联端重数的值可以为“一 \(1\)”、“零或一 \(0..1\)”或“多 \(\*\)”。  通过[导航属性](../../../../docs/framework/data/adonet/navigation-property.md)或外键（如果实体类型上有）可以访问关联某一端的实体类型实例。  有关更多信息，请参见[实体数据模型：外键](../../../../docs/framework/data/adonet/foreign-key-property.md)。  
  
## 示例  
 下图显示了一个具有两个关联的概念模型：`PublishedBy` 和 `WrittenBy`。  `PublishedBy` 关联的关联端是 `Book` 和 `Publisher` 实体类型。  `Publisher` 端的重数为“一 \(1\)”，`Book` 端的重数为“多 \(\*\)”，表明一个出版商可以出版很多书，而一本书只能由一个出版商出版。  
  
 ![示例模型](../../../../docs/framework/data/adonet/media/examplemodel.gif "ExampleModel")  
  
 [ADO.NET 实体框架](../../../../docs/framework/data/adonet/ef/index.md)使用一种称为概念架构定义语言 \([CSDL](../../../../docs/framework/data/adonet/ef/language-reference/csdl-specification.md)\) 的域特定语言 \(DSL\) 来定义概念模型。  下面的 CSDL 定义了上图中显示的 `PublishedBy` 关联：  
  
 [!code-xml[EDM_Example_Model#AssociationExample](../../../../samples/snippets/xml/VS_Snippets_Data/edm_example_model/xml/books.edmx#associationexample)]  
  
## 请参阅  
 [实体数据模型关键概念](../../../../docs/framework/data/adonet/entity-data-model-key-concepts.md)   
 [实体数据模型](../../../../docs/framework/data/adonet/entity-data-model.md)