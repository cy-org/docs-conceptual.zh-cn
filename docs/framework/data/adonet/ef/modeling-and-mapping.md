---
title: "建模和映射 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-ado"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "VB"
  - "CSharp"
  - "C++"
  - "ESQL"
  - "jsharp"
ms.assetid: ec8a9515-3708-4cde-a688-4d8e6975f150
caps.latest.revision: 7
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 7
---
# 建模和映射
在[!INCLUDE[adonet_ef](../../../../../includes/adonet-ef-md.md)]中，可以采用最适合您应用程序的方式定义概念模型、存储模型以及这两种模型之间的映射。  使用 [!INCLUDE[vsprvs](../../../../../includes/vsprvs-md.md)] 中的实体数据模型工具，可以从数据库或图形模型创建一个 .[edmx 文件](http://msdn.microsoft.com/zh-cn/f4c8e7ce-1db6-417e-9759-15f8b55155d4)，然后在数据库或模型发生更改时更新该文件。  
  
 实体框架4.1 开始，还可使用 Code First 开发以编程方式创建模型。  对于 Code First 开发，有两种不同的方案。  在两种情况下，开发人员通过对 .NET Framework 类定义进行编码来定义模型，然后可选择使用数据注释或 fluent API 指定其他映射或配置。  
  
 有关更多信息，请参见[创建和映射概念模型](http://go.microsoft.com/fwlink/?LinkId=235016)（可能为英文网页）。  
  
 您也可使用 EDM 生成器，它与 [!INCLUDE[dnprdnshort](../../../../../includes/dnprdnshort-md.md)] 一起提供。  EdmGen.exe 从现有数据源生成 .csdl、 .ssdl 和 .msl 文件。  也可以手动创建模型和映射内容。  有关详细信息，请参阅[EDM 生成器 \(EdmGen.exe\)](../../../../../docs/framework/data/adonet/ef/edm-generator-edmgen-exe.md)。