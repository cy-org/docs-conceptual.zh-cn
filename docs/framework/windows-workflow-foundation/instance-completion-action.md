---
title: "实例完成操作 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 90cc99d2-9fef-42fd-bcbf-a56917993721
caps.latest.revision: 8
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 8
---
# 实例完成操作
SQL 工作流实例存储的**实例完成操作**属性，允许您指定在工作流实例完成之后是否从持久性数据库中删除该实例的数据和元数据。此属性的允许值为 **DeleteAll** 和 **DeleteNothing**。以下列表对这两个选项进行了说明：  
  
-   **DeleteAll（默认值）。**如果该属性的值设置为 DeleteAll，则在工作流实例完成之后会将从持久性数据库中删除该实例的数据和元数据。  
  
-   **DeleteNothing。**如果该属性的值设置为 DeleteNothing，则即使在工作流实例完成之后也会将该实例的数据和元数据保留在持久性数据库中。  
  
    > [!CAUTION]
    >  实例完成之后继续保留实例状态信息会导致持久性数据库增大。随着数据库的增大，持久性子系统执行数据库操作所花费的时间会越来越长，因此需要定期从持久性数据库中清除实例状态信息，以使服务在满足您的性能需求的级别执行。