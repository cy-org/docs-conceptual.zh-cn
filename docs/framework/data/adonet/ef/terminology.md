---
title: "实体框架术语 | Microsoft Docs"
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
ms.assetid: fa2a1bd1-6118-487b-8673-eebc66b92945
caps.latest.revision: 4
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 4
---
# 实体框架术语
本主题定义[!INCLUDE[adonet_ef](../../../../../includes/adonet-ef-md.md)]文档中经常引用的术语。  如果有其他可用信息，则会提供指向相关主题的链接。  
  
|术语|定义|  
|--------|--------|  
|Association — 关联|实体类型之间的关系的定义。<br /><br /> 有关详细信息，请参阅[Association Element \(CSDL\)](http://msdn.microsoft.com/zh-cn/c305169a-8af7-432f-9ba7-800a163aed41)和[关联类型](../../../../../docs/framework/data/adonet/association-type.md)。|  
|Association Set — 关联集|包含同一类型关联实例的逻辑容器。<br /><br /> 有关详细信息，请参阅[AssociationSet Element \(CSDL\)](http://msdn.microsoft.com/zh-cn/512cbb75-cebe-4f3f-970d-3419deeff684)和[关联集](../../../../../docs/framework/data/adonet/association-set.md)。|  
|Code First|从 实体框架4.1 开始，可使用 Code First 开发以编程方式创建模型。  对于 Code First 开发，有两种不同的方案。  在两种情况下，开发人员通过对 .NET Framework 类定义进行编码来定义模型，然后可选择使用数据注释或 fluent API 指定其他映射或配置。<br /><br /> 请注意，Code First 开发是[实体框架 5.0](http://go.microsoft.com/fwlink/?LinkId=234900)（可能为英文网页）的一部分。  Entity Framework 5.0 不是 .NET Framework 的一部分，但基于 .NET Framework 4.5 构建。  实体框架 5.0 以[“实体框架”](http://go.microsoft.com/fwlink/?LinkID=215714)（可能为英文网页）[NuGet](http://go.microsoft.com/fwlink/?LinkId=232488) 包的形式提供。  有关更多信息，请参见[实体框架发行和版本管理](http://go.microsoft.com/fwlink/?LinkId=234899)（可能为英文网页）。|  
|Command Tree — 命令目录树|所有[!INCLUDE[adonet_ef](../../../../../includes/adonet-ef-md.md)]查询（由一个或多个表达式组成）的常用编程表示形式。<br /><br /> 有关详细信息，请参阅[实体框架概述](../../../../../docs/framework/data/adonet/ef/overview.md)。|  
|Complex Type — 复杂类型|一个 [!INCLUDE[dnprdnshort](../../../../../includes/dnprdnshort-md.md)] 类，该类表示在概念模型中定义的复杂属性。  通过复杂类型，可以在实体中组织标量属性。  复杂对象是复杂类型的实例。  有关详细信息，请参阅[ComplexType Element \(CSDL\)](http://msdn.microsoft.com/zh-cn/f1c2f311-9889-4b87-abd8-a94f322052e3)和[复杂类型](../../../../../docs/framework/data/adonet/complex-type.md)。|  
|ComplexType|数据类型的规范，表示没有键属性的实体类型的非标量属性。<br /><br /> 有关详细信息，请参阅[ComplexType Element \(CSDL\)](http://msdn.microsoft.com/zh-cn/f1c2f311-9889-4b87-abd8-a94f322052e3)和[复杂类型](../../../../../docs/framework/data/adonet/complex-type.md)。|  
|Conceptual Model — 概念模型|[!INCLUDE[adonet_ef](../../../../../includes/adonet-ef-md.md)]的应用程序域中实体类型、复杂类型、关联、实体容器、实体集和关联集的抽象规范。  概念模型在 .csdl 文件中采用 CSDL 定义。<br /><br /> 有关详细信息，请参阅[建模和映射](../../../../../docs/framework/data/adonet/ef/modeling-and-mapping.md)。|  
|.csdl 文件|一种 XML 文件，该文件包含以 CSDL 表示的概念模型。|  
|概念性架构定义语言 \(CSDL\)|一种基于 XML 的语言，可用于定义概念模型的实体类型、关联、实体容器、实体集和关联集。<br /><br /> 有关详细信息，请参阅[CSDL 规范](../../../../../docs/framework/data/adonet/ef/language-reference/csdl-specification.md)。|  
|Container — 容器|实体集和关联集的逻辑分组。<br /><br /> 有关详细信息，请参阅[EntityContainer Element \(CSDL\)](http://msdn.microsoft.com/zh-cn/06d03ecb-3b7a-4e7f-95d5-b95307d47a27)和[实体容器](../../../../../docs/framework/data/adonet/entity-container.md)。|  
|并发|允许多个用户同时访问和更改共享数据的进程。  默认情况下，[!INCLUDE[adonet_ef](../../../../../includes/adonet-ef-md.md)]实现开放式并发模型。|  
|方向|指某些关联的非对称性。  方向是通过架构中的 `NavigationProperty` 或 `ReferentialConstraint` 元素的 `FromRole` 和 `ToRole` 属性指定的。<br /><br /> 有关详细信息，请参阅[NavigationProperty Element \(CSDL\)](http://msdn.microsoft.com/zh-cn/5829a238-a50e-4c81-901d-7b54fc00f27e)和[导航属性](../../../../../docs/framework/data/adonet/navigation-property.md)。|  
|Eager Loading — 预先加载|加载特定相关对象集以及在查询中显式请求的对象的过程。|  
|.edmx 文件|一种 XML 文件，该文件包含概念模型（以 CSDL 表示）、存储模型（以 SSDL 表示）以及这两个模型之间的映射（以 MSL 表示）。  .edmx 文件通过[!INCLUDE[adonet_edm](../../../../../includes/adonet-edm-md.md)]工具创建。有关更多信息，请参见 [.edmx File Overview](http://msdn.microsoft.com/zh-cn/f4c8e7ce-1db6-417e-9759-15f8b55155d4)。|  
|end|参与关联的实体。<br /><br /> 有关详细信息，请参阅[End Element \(CSDL\)](http://msdn.microsoft.com/zh-cn/04f3c141-95bc-424b-989b-1c071b449e7c)和[关联端](../../../../../docs/framework/data/adonet/association-end.md)。|  
|Entity — 实体|应用程序域中的概念，数据类型是根据实体定义的。<br /><br /> 有关详细信息，请参阅[EntityType Element \(CSDL\)](http://msdn.microsoft.com/zh-cn/19562e9f-fd70-4b59-bc15-3e289cbb6054)和[实体类型](../../../../../docs/framework/data/adonet/entity-type.md)。|  
|EntityClient|一个与存储无关的 [!INCLUDE[vstecado](../../../../../includes/vstecado-md.md)] 数据提供程序，该提供程序包含诸如 `EntityConnection`、`EntityCommand` 和 `EntityDataReader` 等类。  它与 [!INCLUDE[esql](../../../../../includes/esql-md.md)] 一起使用，并连接到特定于存储的 [!INCLUDE[vstecado](../../../../../includes/vstecado-md.md)] 数据提供程序（例如 `SqlClient`）。<br /><br /> 有关详细信息，请参阅[用于实体框架的 EntityClient 提供程序](../../../../../docs/framework/data/adonet/ef/entityclient-provider-for-the-entity-framework.md)。|  
|Entity Container — 实体容器|用于指定将在指定的命名空间中实现的实体集和关联集。<br /><br /> 有关详细信息，请参阅[EntityContainer Element \(CSDL\)](http://msdn.microsoft.com/zh-cn/06d03ecb-3b7a-4e7f-95d5-b95307d47a27)和[实体容器](../../../../../docs/framework/data/adonet/entity-container.md)。|  
|实体数据模型 \(EDM\)|以实体和关系来描述数据结构（不考虑其存储形式）的一组概念。<br /><br /> 有关详细信息，请参阅[实体数据模型](../../../../../docs/framework/data/adonet/entity-data-model.md)。|  
|Entity Framework|一套支持开发面向数据的软件应用程序的技术，这些技术使开发人员能够处理映射到数据源中的逻辑架构的概念模型。<br /><br /> 有关详细信息，请参阅[实体框架概述](../../../../../docs/framework/data/adonet/ef/overview.md)。|  
|实体集|一种逻辑容器，包含给定类型及其子类型的实体。  实体集映射到数据库中的表。<br /><br /> 有关详细信息，请参阅[EntitySet Element \(CSDL\)](http://msdn.microsoft.com/zh-cn/ec56db77-718d-4c0e-adc9-f1d33c896287)和[实体集](../../../../../docs/framework/data/adonet/entity-set.md)。|  
|Entity SQL|一种与存储无关的 SQL 方言，它可直接处理概念实体架构，并支持概念模型概念（如继承和关系）。<br /><br /> 有关详细信息，请参阅[Entity SQL 语言](../../../../../docs/framework/data/adonet/ef/language-reference/entity-sql-language.md)。|  
|Entity Type — 实体类型|一个 [!INCLUDE[dnprdnshort](../../../../../includes/dnprdnshort-md.md)] 类，该类表示在概念模型中定义的实体。  实体类型可以具有标量属性、复杂属性和导航属性。  对象是实体类型的实例。  有关详细信息，请参阅[使用对象](../../../../../docs/framework/data/adonet/ef/working-with-objects.md)。|  
|EntityType|数据类型的规范，它包含一个键和一个命名属性集，表示概念模型或存储模型中的顶级项。<br /><br /> 有关详细信息，请参阅[EntityType Element \(CSDL\)](http://msdn.microsoft.com/zh-cn/19562e9f-fd70-4b59-bc15-3e289cbb6054)和[实体类型](../../../../../docs/framework/data/adonet/entity-type.md)。|  
|Explicit Loading — 显式加载|当查询返回对象时，不会同时加载相关对象。  默认情况下，只有对导航属性使用 `Load` 方法显式请求时才会加载相关对象。|  
|外键关联|实体之间的关联，通过外键属性进行管理。|  
|标识关系|一种关系，其中主体实体的主键是依赖实体的主键的一部分。  在这种关系中，没有主体实体，依赖实体就不能存在。|  
|独立关联|实体之间的关联，由独立对象表示和跟踪。|  
|密钥|实体类型的属性 \(Attribute\)，用于指定使用哪个属性 \(Property\) 或属性 \(Property\) 集标识实体类型的唯一实例。  在对象层中由 <xref:System.Data.EntityKey> 类表示。<br /><br /> 有关详细信息，请参阅[Key Element \(CSDL\)](http://msdn.microsoft.com/zh-cn/0cdb1402-dbc7-4a04-a11e-5729cdf7431b)和[实体键](../../../../../docs/framework/data/adonet/entity-key.md)。|  
|延迟加载|当查询返回对象时，不会同时加载相关对象。  但在访问导航属性时，会自动加载相关对象。|  
|[!INCLUDE[linq_entities](../../../../../includes/linq-entities-md.md)]|用于定义一组查询运算符的查询语法，通过这些运算符，可以在 [!INCLUDE[csprcs](../../../../../includes/csprcs-md.md)] 和 [!INCLUDE[vbprvb](../../../../../includes/vbprvb-md.md)] 中以直接的声明性方式表示遍历、筛选和投影操作。<br /><br /> 有关详细信息，请参阅[LINQ to Entities](../../../../../docs/framework/data/adonet/ef/language-reference/linq-to-entities.md)。|  
|映射|概念模型与存储模型中的项之间的对应规范。<br /><br /> 有关详细信息，请参阅[MSL 规范](../../../../../docs/framework/data/adonet/ef/language-reference/msl-specification.md)。|  
|.msl 文件|一种 XML 文件，该文件以 MSL 表示，包含概念模型与存储模型之间的映射。|  
|映射规范语言 \(MSL\)|一种基于 XML 的语言，可用于将概念模型中定义的项映射到存储模型中的项。<br /><br /> 有关详细信息，请参阅[MSL 规范](../../../../../docs/framework/data/adonet/ef/language-reference/msl-specification.md)。|  
|Modification Functions — 修改函数|用于插入、更新和删除数据源中的数据的存储过程。  这类函数可用来替代[!INCLUDE[adonet_ef](../../../../../includes/adonet-ef-md.md)]生成的命令。  修改函数是由存储模型中的 `Function` 元素定义的。  [ModificationFunctionMapping](http://msdn.microsoft.com/zh-cn/b44b5b13-9937-448b-ba36-7a0cfefea782) 元素将这类修改函数映射到对概念模型中定义的实体执行的插入、更新和删除操作。|  
|重数|关系每一方可以存在的实体数量，由关联进行定义。  也称为基数。<br /><br /> 有关详细信息，请参阅[End Element \(CSDL\)](http://msdn.microsoft.com/zh-cn/04f3c141-95bc-424b-989b-1c071b449e7c)和[关联端](../../../../../docs/framework/data/adonet/association-end.md)。|  
|Multiple Entity Sets Per Type — 每种类型多个实体集|在多个实体集中定义一个实体类型的功能。<br /><br /> 有关详细信息，请参阅[EntitySet Element \(CSDL\)](http://msdn.microsoft.com/zh-cn/ec56db77-718d-4c0e-adc9-f1d33c896287)和[How to: Define a Model with Multiple Entity Sets per Type](http://msdn.microsoft.com/zh-cn/61aa4fca-5ac0-4f47-9bc8-46e8c2965ef7)。|  
|Navigation Property — 导航属性|实体类型的属性，表示与其他实体类型的关系，由关联定义。  导航属性用于根据关联另一端的重数返回相关对象，如 <xref:System.Data.Objects.DataClasses.EntityCollection%601> 或 <xref:System.Data.Objects.DataClasses.EntityReference%601>。<br /><br /> 有关详细信息，请参阅[NavigationProperty Element \(CSDL\)](http://msdn.microsoft.com/zh-cn/5829a238-a50e-4c81-901d-7b54fc00f27e)和[导航属性](../../../../../docs/framework/data/adonet/navigation-property.md)。|  
|Query Path — 查询路径|路径的字符串表示形式，用于指定执行对象查询时要返回的相关对象。  查询路径是通过调用 <xref:System.Data.Objects.ObjectQuery%601> 的 <xref:System.Data.Objects.ObjectQuery%601.Include%2A> 方法定义的。<br /><br /> 有关详细信息，请参阅[Loading Related Objects](http://msdn.microsoft.com/zh-cn/452347d2-7b3b-44cd-9001-231299a28cb1)。|  
|对象上下文|表示概念模型中定义的实体容器。  它包含与基础数据源的连接，并提供更改跟踪和标识解析等服务。  对象上下文由 <xref:System.Data.Objects.ObjectContext> 或 `DbContext` 类的实例表示。<br /><br /> `DbContext` 开发是[实体框架 5.0](http://go.microsoft.com/fwlink/?LinkId=234900)（可能为英文网页）的一部分。  Entity Framework 5.0 不是 .NET Framework 的一部分，但基于 .NET Framework 4.5 构建。  实体框架 5.0 以[“实体框架”](http://go.microsoft.com/fwlink/?LinkID=215714)（可能为英文网页）[NuGet](http://go.microsoft.com/fwlink/?LinkId=232488) 包的形式提供。  有关更多信息，请参见[实体框架发行和版本管理](http://go.microsoft.com/fwlink/?LinkId=234899)（可能为英文网页）。|  
|对象层|实体框架所使用的实体类型和对象上下文定义。|  
|Object Query — 对象查询|在对象上下文中对数据模型执行的查询，该查询以对象形式返回数据。<br /><br /> 有关详细信息，请参阅[Object Queries](http://msdn.microsoft.com/zh-cn/0768033c-876f-471d-85d5-264884349276)。|  
|Object\-relational Mapping — 对象关系映射|一种技术，用于将关系数据库中的数据转换为可在面向对象的软件应用程序中使用的数据类型。<br /><br /> [!INCLUDE[adonet_ef](../../../../../includes/adonet-ef-md.md)]通过将存储模型中定义的关系数据映射到概念模型中定义的数据类型来提供对象关系映射服务。<br /><br /> 有关详细信息，请参阅[建模和映射](../../../../../docs/framework/data/adonet/ef/modeling-and-mapping.md)。|  
|Object Services — 对象服务|[!INCLUDE[adonet_ef](../../../../../includes/adonet-ef-md.md)]提供的服务，通过这种服务，应用程序代码可以对 [!INCLUDE[dnprdnshort](../../../../../includes/dnprdnshort-md.md)] 对象这样的实体进行操作。|  
|持久性未知对象|一种不包含与数据存储有关的任何逻辑的对象。  也称为 POCO 实体。|  
|POCO|纯旧式 CLR 对象。  一种不从另一个类继承也不实现接口的对象。|  
|POCO 实体|[!INCLUDE[adonet_ef](../../../../../includes/adonet-ef-md.md)]中的一种实体，该实体不从 <xref:System.Data.Objects.DataClasses.EntityObject> 或 <xref:System.Data.Objects.DataClasses.ComplexObject> 继承，也不实现[!INCLUDE[adonet_ef](../../../../../includes/adonet-ef-md.md)]接口。  通常，POCO 实体是在[!INCLUDE[adonet_ef](../../../../../includes/adonet-ef-md.md)]应用程序中使用的现有域对象。  这些实体支持持久性未知。  有关详细信息，请参阅[Working with POCO Entities](http://msdn.microsoft.com/zh-cn/5e0fb82a-b6d1-41a1-b37b-c12db61629d3)。|  
|代理对象|一种从 POCO 类派生的对象，该对象由[!INCLUDE[adonet_ef](../../../../../includes/adonet-ef-md.md)]生成，以支持更改跟踪和延迟加载。  有关详细信息，请参阅[Requirements for Creating POCO Proxies](http://msdn.microsoft.com/zh-cn/dcdbf982-9b9d-4582-806a-64de4a1c03c8)。|  
|Referential Constraint — 引用约束|在概念模型中定义的约束，该约束指示一个实体与另一个实体之间存在依赖关系。  此约束意味着，如果没有对应的主体实体实例，就不会存在依赖性实体的实例。<br /><br /> 有关详细信息，请参阅[ReferentialConstraint Element \(CSDL\)](http://msdn.microsoft.com/zh-cn/24f96a80-85b5-4f2e-a14c-0e3eb6796fa0)和[引用完整性约束](../../../../../docs/framework/data/adonet/referential-integrity-constraint.md)。|  
|Relationship — 关系|实体之间的逻辑连接。|  
|Role — 角色|为关联的每个 `End` 提供的名称，用于明确关系的语义。<br /><br /> 有关详细信息，请参阅[End Element \(CSDL\)](http://msdn.microsoft.com/zh-cn/04f3c141-95bc-424b-989b-1c071b449e7c)和[关联端](../../../../../docs/framework/data/adonet/association-end.md)。|  
|标量属性|实体的属性，它映射到存储模型中的单个字段。|  
|自跟踪实体|从文本模板转换工具包 \(T4\) 中生成的一种实体，该实体可以将更改记录到标量属性、复杂属性以及导航属性中。|  
|Simple Type — 简单类型|一种基元类型，用于定义概念模型中的属性。<br /><br /> 有关详细信息，请参阅[Conceptual Model Types \(CSDL\)](http://msdn.microsoft.com/zh-cn/987b995f-e429-4569-9559-b4146744def4)和[实体数据模型：基元数据类型](../../../../../docs/framework/data/adonet/entity-data-model-primitive-data-types.md)。|  
|Split Type — 拆分实体|一种实体类型，它映射到存储模型中的两个不同类型。<br /><br /> 有关详细信息，请参阅[How to: Define a Model with a Single Entity Mapped to Two Tables](http://msdn.microsoft.com/zh-cn/01762517-e4ab-439d-99e6-564ab7d6f3ed)。|  
|存储模型|受支持的数据源（例如关系数据库）的数据逻辑模型定义。  存储模型在 .ssdl 文件中采用 SSDL 定义。<br /><br /> 有关详细信息，请参阅[建模和映射](../../../../../docs/framework/data/adonet/ef/modeling-and-mapping.md)和[SSDL 规范](../../../../../docs/framework/data/adonet/ef/language-reference/ssdl-specification.md)。|  
|.ssdl 文件|一种 XML 文件，该文件包含以 SSDL 表示的存储模型。|  
|存储架构定义语言 \(SSDL\)|一种基于 XML 的语言，用于定义存储模型（常常对应于数据库架构）的实体类型、关联、实体容器、实体集和关联集。<br /><br /> 有关详细信息，请参阅[SSDL 规范](../../../../../docs/framework/data/adonet/ef/language-reference/ssdl-specification.md)。|  
|每个层次结构一个表|在数据库中对类型层次结构建模的方法，此方法将层次结构中的所有类型的特性包含在一个表中。|  
|每个类型一个表|在数据库中对类型层次结构建模的方法，此方法使用具有一对一关系的多个表来对各种类型建模。|  
  
## 请参阅  
 [ADO.NET 实体框架](../../../../../docs/framework/data/adonet/ef/index.md)   
 [实体框架概述](../../../../../docs/framework/data/adonet/ef/overview.md)   
 [入门](../../../../../docs/framework/data/adonet/ef/getting-started.md)   
 [实体框架资源](../../../../../docs/framework/data/adonet/ef/resources.md)