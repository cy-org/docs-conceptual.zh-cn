---
title: "安全性 (LINQ to DataSet) | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-ado"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 6116b2b8-75f4-4d8b-aea6-c13e55cda50b
caps.latest.revision: 2
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 2
---
# 安全性 (LINQ to DataSet)
本主题讨论 [!INCLUDE[linq_dataset](../../../../includes/linq-dataset-md.md)] 中的安全性问题。  
  
## 将查询传递到不受信任的组件  
 [!INCLUDE[linq_dataset](../../../../includes/linq-dataset-md.md)] 查询可在程序中的一点表述，而在另一点执行。  在表述查询的点，查询可引用在该点可见的任何元素，例如调用方法所属的类的私有成员，或者表示局部变量\/参数的符号。  在执行时，查询能有效访问那些查询在表述中引用的成员，即使其中调用代码没有可见性。  执行查询的代码没有任意添加的可见性，因为它无法选择访问内容。  它能严格访问查询所访问的内容，并且仅通过查询本身访问。  
  
 这意味着将查询的引用传递到其他代码段即表示信任接收该查询的组件，组件可访问查询引用的所有公共成员和私有成员。  通常情况下，不应将 [!INCLUDE[linq_dataset](../../../../includes/linq-dataset-md.md)] 查询传递到不受信任的组件，除非查询已经过仔细构造，使它不能公开应保留为私有的信息。  
  
## 外部输入  
 应用程序常常采用外部输入（来自用户或其他外部代理），并根据该输入执行操作。  在使用 [!INCLUDE[linq_dataset](../../../../includes/linq-dataset-md.md)] 的情况下，应用程序可能根据外部输入或使用查询中的外部输入以特定方式构造查询。[!INCLUDE[linq_dataset](../../../../includes/linq-dataset-md.md)] 查询在接受文本的任何位置都接受参数。  应用程序开发人员应使用参数化查询，而不是将来自外部代理的文本直接注入查询。  
  
 任何直接或间接从用户或外部代理派生的输入都可能包含利用目标语言的语法来执行未授权操作的内容。  这称为 SQL 注入式攻击，是以目标语言为 Transact\-SQL 的攻击模式命名的。  恶意用户利用这种直接注入到查询的用户输入删除数据库表、产生拒绝服务或者更改所执行操作的性质。  尽管在 [!INCLUDE[linq_dataset](../../../../includes/linq-dataset-md.md)] 可以撰写查询，但是要通过对象模型 API 执行。[!INCLUDE[linq_dataset](../../../../includes/linq-dataset-md.md)] 查询不像 Transact\-SQL 那样使用字符串操作或串联来撰写，所以从传统意义上讲不易受 SQL 注入式攻击影响。  
  
## 请参阅  
 [编程指南](../../../../docs/framework/data/adonet/programming-guide-linq-to-dataset.md)