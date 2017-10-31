---
title: "继承支持 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-ado"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 19bb2794-b4e7-402e-8307-1d1517381a08
caps.latest.revision: 3
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 3
---
# 继承支持
[!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] 支持单表映射。  换言之，整个继承层次结构存储在单个数据库表中。  该表包含整个层次结构的所有可能数据列的平展联合。  （联合是将两个表组合成一个表的结果，组合后的表包含任一原始表中存在的行。） 每行中不适用于该行所表示的实例类型的列为 null。  
  
 单表映射策略是最简单的继承表示形式，为许多不同类别的查询提供了良好的性能特征。  
  
 若要在 [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] 中实现这种映射，必须在继承层次结构的根类中指定属性 \(Attribute\) 和属性 \(Attribute\) 的属性 \(Property\)。  有关详细信息，请参阅[如何：映射继承层次结构](../../../../../../docs/framework/data/adonet/sql/linq/how-to-map-inheritance-hierarchies.md)。  
  
 使用 [!INCLUDE[vs_current_short](../../../../../../includes/vs-current-short-md.md)] 的开发人员还可以使用 [!INCLUDE[vs_ordesigner_long](../../../../../../includes/vs-ordesigner-long-md.md)] 来映射继承层次结构。  
  
## 请参阅  
 [背景信息](../../../../../../docs/framework/data/adonet/sql/linq/background-information.md)