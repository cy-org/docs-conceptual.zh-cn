---
title: "如何：使用 EdmGen.exe 生成对象层代码 | Microsoft Docs"
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
ms.assetid: c44d2ebe-f66f-42cb-9741-4a3f0c2dcffb
caps.latest.revision: 4
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 4
---
# 如何：使用 EdmGen.exe 生成对象层代码
本主题介绍如何使用 [EDM 生成器 \(EdmGen.exe\)](../../../../../docs/framework/data/adonet/ef/edm-generator-edmgen-exe.md) 工具生成基于 .csdl 文件的对象层代码。  
  
### 使用 EdmGen.exe 为 Visual Basic 项目的 School 模型生成对象层代码  
  
1.  创建 School 数据库。  有关详细信息，请参阅[Creating the School Sample Database](http://msdn.microsoft.com/zh-cn/c1bec483-a0ea-4660-aa0b-7b0a8b68fed0)。  
  
2.  生成 School 模型或获取 School.csdl 文件。  有关详细信息，请参阅[如何：使用 EdmGen.exe 生成模型和映射文件](../../../../../docs/framework/data/adonet/ef/how-to-use-edmgen-exe-to-generate-the-model-and-mapping-files.md)。  
  
3.  在命令提示符下执行以下命令（无换行符）：  
  
    ```  
    "%windir%\Microsoft.NET\Framework\v4.0.30319\edmgen.exe" /mode:EntityClassGeneration   
    /incsdl:.\School.csdl /outobjectlayer:.\School.Objects.vb /language:VB  
    ```  
  
### 使用 EdmGen.exe 为 C\# 项目的 School 模型生成对象层代码  
  
1.  创建 School 数据库。  有关详细信息，请参阅[Creating the School Sample Database](http://msdn.microsoft.com/zh-cn/c1bec483-a0ea-4660-aa0b-7b0a8b68fed0)。  
  
2.  生成 School 模型或获取 School.csdl 文件。  有关详细信息，请参阅[如何：使用 EdmGen.exe 生成模型和映射文件](../../../../../docs/framework/data/adonet/ef/how-to-use-edmgen-exe-to-generate-the-model-and-mapping-files.md)。  
  
3.  在命令提示符下执行以下命令（无换行符）：  
  
    ```  
    "%windir%\Microsoft.NET\Framework\v4.0.30319\edmgen.exe" /mode:EntityClassGeneration   
    /incsdl:.\School.csdl /outobjectlayer:.\School.Objects.cs /language:CSharp  
    ```  
  
## 请参阅  
 [建模和映射](../../../../../docs/framework/data/adonet/ef/modeling-and-mapping.md)   
 [How to: Manually Configure an Entity Framework Project](http://msdn.microsoft.com/zh-cn/73f6ae1d-b3b2-4577-aebd-ad5a75954e9e)   
 [ADO.NET Entity Data Model  Tools](http://msdn.microsoft.com/zh-cn/91076853-0881-421b-837a-f582f36be527)   
 [How to: Pre\-Generate Views to Improve Query Performance](http://msdn.microsoft.com/zh-cn/b18a9d16-e10b-4043-ba91-b632f85a2579)   
 [如何：使用 EdmGen.exe 生成模型和映射文件](../../../../../docs/framework/data/adonet/ef/how-to-use-edmgen-exe-to-generate-the-model-and-mapping-files.md)