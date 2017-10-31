---
title: "自定义插入、更新和删除操作 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-ado"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 07eef055-8f6c-414d-850e-d323ff946cd0
caps.latest.revision: 3
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 3
---
# 自定义插入、更新和删除操作
默认情况下，[!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] 会生成动态 SQL 来实现插入、读取、更新和删除操作。  但实际上，您通常要自定义应用程序以满足您的业务需要。  
  
> [!NOTE]
>  如果正在使用 [!INCLUDE[vs_current_short](../../../../../../includes/vs-current-short-md.md)]，则可以使用 [!INCLUDE[vs_ordesigner_long](../../../../../../includes/vs-ordesigner-long-md.md)] 来自定义插入、更新和删除操作。  
  
 本节中的主题介绍了 [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] 提供的用于在应用程序中自定义插入、读取、更新和删除操作的技术。  
  
## 本节内容  
 [自定义操作：概述](../../../../../../docs/framework/data/adonet/sql/linq/customizing-operations-overview.md)  
 介绍 [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] 提供的用于自定义插入、读取、更新和删除操作的各种技术。  
  
 [插入、更新和删除操作](../../../../../../docs/framework/data/adonet/sql/linq/insert-update-and-delete-operations.md)  
 介绍用于操作数据库数据的 [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] 默认过程。  
  
 [开发人员在重写默认行为方面的责任](../../../../../../docs/framework/data/adonet/sql/linq/responsibilities-of-the-developer-in-overriding-default-behavior.md)  
 介绍开发人员在实现非 [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] 强制需求方面的责任。  
  
 [使用分部方法添加业务逻辑](../../../../../../docs/framework/data/adonet/sql/linq/adding-business-logic-by-using-partial-methods.md)  
 介绍如何使用分部方法重写自动生成的方法。