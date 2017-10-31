---
title: "模型声明函数 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-ado"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: aba87f13-5685-4f6b-ad14-918e8a7d5c2a
caps.latest.revision: 3
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 3
---
# 模型声明函数
“模型声明函数”是在概念模型中声明的函数，但不是在概念模型中定义的。  该函数可能是在承载或存储环境中定义的。  例如，模型声明函数可能映射至在数据库中定义的函数，从而在概念模型中提供服务器端的功能。  
  
 模型声明函数的声明包含以下信息：  
  
-   函数名。  （必需）  
  
-   返回值的类型。  （可选）  
  
    > [!NOTE]
    >  如果未指定返回值，则返回类型为 void。  
  
-   参数信息，包括参数名和类型。  （可选）  
  
## 示例  
 [ADO.NET 实体框架](../../../../docs/framework/data/adonet/ef/index.md)使用一种称为概念架构定义语言 \([CSDL](../../../../docs/framework/data/adonet/ef/language-reference/csdl-specification.md)\) 的域特定语言 \(DSL\) 来定义概念模型。  在 CSDL 中，模型声明函数的一种实现方式是[函数导入](http://msdn.microsoft.com/zh-cn/125704ae-56c7-4233-80b7-389a10f3a65d)。  下面的 CSDL 定义了一个实体容器，其中包含一个函数导入定义。  请注意，由于未指定返回类型，因而该函数的返回类型为 void。  
  
 [!code-xml[EDM_Example_Model#FunctionImport](../../../../samples/snippets/xml/VS_Snippets_Data/edm_example_model/xml/books4.edmx#functionimport)]  
  
## 请参阅  
 [实体数据模型关键概念](../../../../docs/framework/data/adonet/entity-data-model-key-concepts.md)   
 [实体数据模型](../../../../docs/framework/data/adonet/entity-data-model.md)