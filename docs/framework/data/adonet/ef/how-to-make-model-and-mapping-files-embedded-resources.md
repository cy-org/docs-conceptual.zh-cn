---
title: "如何：创建模型及映射文件嵌入资源 | Microsoft Docs"
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
ms.assetid: 20dfae4d-e95a-4264-9540-f5ad23b462d3
caps.latest.revision: 3
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 3
---
# 如何：创建模型及映射文件嵌入资源
[!INCLUDE[adonet_ef](../../../../../includes/adonet-ef-md.md)]可用于将模型和映射文件部署为应用程序的嵌入资源。  包含嵌入模型和映射文件的程序集必须加载到实体连接所在的应用程序域中。  有关详细信息，请参阅[连接字符串](../../../../../docs/framework/data/adonet/ef/connection-strings.md)。  默认情况下，[!INCLUDE[adonet_edm](../../../../../includes/adonet-edm-md.md)]工具嵌入模型和映射文件。手动定义模型和映射文件时，请使用下面的过程以确保文件作为嵌入资源与[!INCLUDE[adonet_ef](../../../../../includes/adonet-ef-md.md)]应用程序一起部署。  
  
> [!NOTE]
>  若要维护嵌入资源，每次修改模型和映射文件时都必须重复此过程。  
  
### 嵌入模型和映射文件  
  
1.  在**“解决方案资源管理器”**中选择概念文件 \(.csdl\)。  
  
2.  在**“属性”**窗格中，将**“生成操作”**设置为**“嵌入的资源”**。  
  
3.  对存储文件 \(.ssdl\) 和映射文件 \(.msl\) 重复步骤 1 和步骤 2。  
  
4.  在**“解决方案资源管理器”**中，双击 App.config 文件，然后基于以下任一格式修改 `connectionString` 属性中的 `Metadata` 参数：  
  
    -   `Metadata=` `res://<assemblyFullName>/<resourceName>;`  
  
    -   `Metadata=` `res://*/<resourceName>;`  
  
    -   `Metadata=res://*;`  
  
     有关详细信息，请参阅[连接字符串](../../../../../docs/framework/data/adonet/ef/connection-strings.md)。  
  
## 示例  
 下面的连接字符串引用 [AdventureWorks 销售模型](http://msdn.microsoft.com/zh-cn/f16cd988-673f-4376-b034-129ca93c7832)的嵌入模型和映射文件。  该连接字符串存储在项目的 App.config 文件中。  
  
  
  
## 请参阅  
 [建模和映射](../../../../../docs/framework/data/adonet/ef/modeling-and-mapping.md)   
 [如何：定义连接字符串](../../../../../docs/framework/data/adonet/ef/how-to-define-the-connection-string.md)   
 [如何：生成 EntityConnection 连接字符串](../../../../../docs/framework/data/adonet/ef/how-to-build-an-entityconnection-connection-string.md)   
 [ADO.NET Entity Data Model  Tools](http://msdn.microsoft.com/zh-cn/91076853-0881-421b-837a-f582f36be527)