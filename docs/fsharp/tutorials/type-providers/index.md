---
title: "类型提供程序"
description: "类型提供程序"
keywords: "visual f#, f#, 函数编程"
author: cartermp
ms.author: phcart
ms.date: 05/16/2016
ms.topic: language-reference
ms.prod: .net
ms.technology: devlang-fsharp
ms.devlang: fsharp
ms.assetid: 25697ef6-465e-4248-9de5-1d199d4a8b59
translationtype: Human Translation
ms.sourcegitcommit: 0a01ec92a90d99fafaacbd3f71f5177e5cf94a68
ms.openlocfilehash: e9e67e6531e0c1daad0c0d4a9f778670d5cb2263
ms.lasthandoff: 04/05/2017

---

# <a name="type-providers"></a>类型提供程序

> [!NOTE]
本指南根据 F# 3.0 编写，并将进行更新。  请参阅 [FSharp.Data](http://fsharp.github.io/FSharp.Data/) 了解最新的跨平台类型提供程序。

F# 类型提供程序是提供在程序中使用的类型、属性和方法的组件。 类型提供程序是面向富信息编程的 F# 3.0 支持的重要部分。 富信息编程的关键在于消除障碍以使用在 Internet 上和现代企业环境中找到的各种信息源。 将信息源包含在程序中时遇到的一项重大障碍是，需要将信息作为在编程语言环境中使用的类型、属性和方法呈现。 手动写入这些类型不仅相当耗时，而且难以维护。 常见的替代方法是使用代码生成器，它可将文件添加到项目中；但是，代码生成的常规类型无法很好地集成到 F# 所支持的编程的探索模式中，这是因为每次调整服务引用时都必须替换生成的代码。

F# 类型提供程序提供的类型通常基于外部信息源。 例如，适用于 SQL 的 F# 类型提供程序将提供直接使用你有权访问的任何 SQL 数据库的表所需的类型、属性和方法。 同样地，WSDL Web 服务的类型提供程序将提供直接使用任何 WSDL Web 服务所需的类型、属性和方法。

F# 类型提供程序提供的类型、属性和方法集可依赖程序代码中给定的参数。 例如，类型提供程序可提供依赖连接字符串或服务 URL 的不同类型。 这样一来，通过连接字符串或 URL 提供的信息空间便能直接集成到你的程序中。 类型提供程序还可确保仅按需展开类型组；也就是说，如果类型实际上是由你的程序引用的，则将其展开。 这允许以强类型的方式直接按需集成大型信息空间（如联机数据市场）。

F# 包含多个面向常用的 Internet 和企业数据服务的内置类型提供程序。 这些类型提供程序提供了对 SQL 关系数据库和基于网络的 OData 和 WSDL 服务的简单和常规访问，并且支持对这些数据源使用 F# LINQ 查询。

根据需要，你可以创建自己的自定义类型提供程序，也可以引用其他人创建的类型提供程序。 例如，假定你的组织具有一种数据服务，该服务提供了数量不断增长的命名数据集，每个数据集都有其自己的稳定数据架构。 你可选择创建一种类型提供程序，该程序不仅读取架构，还以强类型方式将最新的可用数据集提供给程序员。


## <a name="related-topics"></a>相关主题


|标题|描述|
|-----|-----------|
|[演练：使用类型提供程序访问 SQL 数据库](accessing-a-sql-database.md)|说明如何使用 SqlDataConnection 类型提供程序基于与数据库的直接连接的连接字符串来访问 SQL 数据库的表和存储过程。 此访问使用 LINQ to SQL 映射。|
|[演练：使用类型提供程序和实体访问 SQL 数据库](accessing-a-sql-database-entities.md)|说明如何使用 SqlEntityConnection 类型提供程序基于与数据库的直接连接的连接字符串来访问 SQL 数据库的表和存储过程。 此访问使用 LINQ to Entities 映射。 此方法使用任何数据库，而演示的示例为 SQL Server。|
|[演练：使用类型提供程序访问 OData 服务](accessing-an-odata-service.md)|说明如何使用 ODataService 类型提供程序基于服务 URL 以强类型方式访问 OData 服务。|
|[演练：使用类型提供程序访问 Web 服务](accessing-a-web-service.md)|说明如何使用 WsdlService 类型提供程序基于服务 URL 以强类型方式访问 WSDL Web 服务。|
|[演练：根据 DBML 文件生成 F# 类型 ](generating-fsharp-types-from-dbml.md)|说明如何使用 DbmlFile 类型提供程序基于提供 Linq to SQL 数据库架构规范的 DBML 文件来访问 SQL 数据库的表和存储过程。|
|[演练：根据 EDMX 架构文件生成 F# 类型](generating-fsharp-types-from-edmx.md)|说明如何使用 EdmxFile 类型提供程序基于提供实体框架架构规范的 EDMX 文件来访问 SQL 数据库的表和存储过程。|
|[教程：创建类型提供程序](creating-a-type-provider.md)|提供有关编写你自己的自定义类型提供程序的信息。|
|[类型提供程序安全性](type-provider-security.md)|提供有关开发类型提供程序时的安全注意事项的信息。|
|[类型提供程序疑难解答](troubleshooting-type-providers.md)|提供有关使用类型提供程序时会出现的常见问题的信息并包括解决方案的建议。|

## <a name="see-also"></a>另请参阅
[F# 语言参考](../../language-reference/index.md)

[Visual F#](../../index.md)
