---
title: "如何：定义连接字符串 | Microsoft Docs"
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
ms.assetid: 6027335d-4e26-420d-9151-6523289b1989
caps.latest.revision: 3
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 3
---
# 如何：定义连接字符串
本主题介绍如何定义在连接到概念模型时使用的连接字符串。  本主题基于 [AdventureWorks 销售](http://msdn.microsoft.com/zh-cn/f16cd988-673f-4376-b034-129ca93c7832)概念模型。  AdventureWorks 销售模型将在 [!INCLUDE[adonet_ef](../../../../../includes/adonet-ef-md.md)] 文档的与任务相关的所有主题中使用。  本主题假定您已配置[!INCLUDE[adonet_ef](../../../../../includes/adonet-ef-md.md)]且定义了 AdventureWorks 销售模型。  有关详细信息，请参阅[How to: Manually Define the Model and Mapping Files](http://msdn.microsoft.com/zh-cn/d4fd6864-f2a1-48f0-aa32-1e318775a99a)。  本主题中的过程还包括在[How to: Manually Configure an Entity Framework Project](http://msdn.microsoft.com/zh-cn/73f6ae1d-b3b2-4577-aebd-ad5a75954e9e)中。  
  
> [!NOTE]
>  如果在 [!INCLUDE[vsprvs](../../../../../includes/vsprvs-md.md)] 项目中使用[!INCLUDE[adonet_edm](../../../../../includes/adonet-edm-md.md)]向导，则该向导将自动生成 .edmx 文件并将该项目配置为使用[!INCLUDE[adonet_ef](../../../../../includes/adonet-ef-md.md)]。  有关详细信息，请参阅[How to: Use the Entity Data Model Wizard](http://msdn.microsoft.com/zh-cn/dadb058a-c5d9-4c5c-8b01-28044112231d)。  
  
### 定义实体框架连接字符串  
  
-   打开项目的应用程序配置文件 \(app.config\) 并添加以下连接字符串：  
  
  
  
     如果项目没有应用程序配置文件，可以通过从**“项目”**菜单中选择**“添加新项”**，选择**“常规”**类别，接着选择**“应用程序配置文件”**，然后单击**“添加”**，以添加应用程序配置文件。  
  
## 请参阅  
 [Quickstart](http://msdn.microsoft.com/zh-cn/0bc534be-789f-4819-b9f6-76e51d961675)   
 [How to: Create a New .edmx File](http://msdn.microsoft.com/zh-cn/beb8189e-e51c-4051-839c-9902c224abf2)   
 [ADO.NET Entity Data Model  Tools](http://msdn.microsoft.com/zh-cn/91076853-0881-421b-837a-f582f36be527)