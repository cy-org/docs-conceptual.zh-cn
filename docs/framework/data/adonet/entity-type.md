---
title: "实体类型 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-ado"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: a6dee9ab-9e4a-48f2-a169-3f79cc15821c
caps.latest.revision: 3
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 3
---
# 实体类型
“实体类型”是用于描述实体数据模型 \(EDM\) 中的数据结构的基本构造块。  在概念模型中，实体类型表示顶级概念（例如客户或订单）的结构。  实体类型是实体类型实例的模板。  每个模板都包含以下信息：  
  
-   唯一名称。  （必选。）  
  
-   由一个或多个属性定义的[实体键](../../../../docs/framework/data/adonet/entity-key.md)。  （必选。）  
  
-   采用[属性](../../../../docs/framework/data/adonet/property.md)形式的数据。  （可选）。  
  
-   [导航属性](../../../../docs/framework/data/adonet/navigation-property.md)，用于从[关联](../../../../docs/framework/data/adonet/association-type.md)的一[端](../../../../docs/framework/data/adonet/association-end.md)导航至其他端。  （可选）  
  
 在应用程序中，实体类型的实例表示一个特定对象（例如特定客户或订单）。  实体类型的每个实例在某个[实体集](../../../../docs/framework/data/adonet/entity-set.md)中都必须具有一个唯一的[实体键](../../../../docs/framework/data/adonet/entity-key.md)。  
  
 只有两个实体类型实例的类型相同且其实体键的值也相同时，才认为它们是相等的。  
  
## 示例  
 下图显示了一个具有三个实体类型的概念模型：`Book`、`Publisher` 和 `Author`：  
  
 ![示例模型](../../../../docs/framework/data/adonet/media/examplemodel.gif "ExampleModel")  
  
 请注意，构成其实体键的每个实体类型的属性均用“\(Key\)”标示出来。  
  
 [ADO.NET 实体框架](../../../../docs/framework/data/adonet/ef/index.md)使用一种称为概念架构定义语言 \([CSDL](../../../../docs/framework/data/adonet/ef/language-reference/csdl-specification.md)\) 的域特定语言 \(DSL\) 来定义概念模型。  下面的 CSDL 定义了上图中显示的 `Book` 实体类型。  
  
 [!code-xml[EDM_Example_Model#EntityExample](../../../../samples/snippets/xml/VS_Snippets_Data/edm_example_model/xml/books.edmx#entityexample)]  
  
## 请参阅  
 [实体数据模型关键概念](../../../../docs/framework/data/adonet/entity-data-model-key-concepts.md)   
 [实体数据模型](../../../../docs/framework/data/adonet/entity-data-model.md)   
 [方面](../../../../docs/framework/data/adonet/facet.md)