---
title: "可以为 null 的结构化类型 (Entity SQL) | Microsoft Docs"
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
ms.assetid: ae006fa9-997e-45bb-8a04-a7f62026171e
caps.latest.revision: 2
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 2
---
# 可以为 null 的结构化类型 (Entity SQL)
结构化类型的 `null` 实例是不存在的实例。  这不同于其中所有属性都具有 `null` 值的现有实例。  
  
 本主题介绍可以为 Null 的结构化类型，包括哪些类型可以为 null 以及哪些代码模式会产生可以为 Null 的结构化类型的 `null` 实例。  
  
## 可以为 Null 的结构化类型的种类  
 有三种可以为 Null 的结构化类型：  
  
-   行类型。  
  
-   复杂类型。  
  
-   实体类型。  
  
## 能够产生结构化类型的 null 实例的代码模式  
 以下方案会产生 `null` 实例：  
  
-   将 `null` 说明为结构化类型：  
  
    ```  
    TREAT (NULL AS StructuredType)  
    ```  
  
-   将基类型向上转换为派生类型：  
  
    ```  
    TREAT (BaseType AS DerivedType)  
    ```  
  
-   对 false 条件进行外部联接：  
  
    ```  
    Collection1 LEFT OUTER JOIN Collection2  
    ON FalseCondition  
    ```  
  
     \-\-或  
  
    ```  
    Collection1 RIGHT OUTER JOIN Collection2  
    ON FalseCondition  
    ```  
  
     \-\-或  
  
    ```  
    Collection1 FULL OUTER JOIN Collection2  
    ON FalseCondition  
    ```  
  
-   取消 `null` 引用的引用：  
  
    ```  
    DEREF(NullRef)  
    ```  
  
-   从空集合获取 ANYELEMENT：  
  
    ```  
    ANYELEMENT(EmptyCollection)  
    ```  
  
-   检查结构化类型实例是否为 `null`：  
  
    ```csharp  
    ...  
    for (int i = 0; i < reader.FieldCount; i++)  
    {  
        if (reader.IsDBNull(i))  
        {  
            Console.WriteLine(“[NULL]”);  
        }  
        else  
        {  
            Console.WriteLine(reader.GetValue(i).ToString());  
        }  
    }  
    ```  
  
## 请参阅  
 [Entity SQL 概述](../../../../../../docs/framework/data/adonet/ef/language-reference/entity-sql-overview.md)