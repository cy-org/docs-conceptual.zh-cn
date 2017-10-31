---
title: "使用 LINQ to SQL 的典型步骤 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-ado"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 9a88bd51-bd74-48f7-a9b1-f650e8d55a3e
caps.latest.revision: 4
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 4
---
# 使用 LINQ to SQL 的典型步骤
若要实现 [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] 应用程序，请按照本主题后面部分说明的步骤操作。  请注意，很多步骤是可选的。  您可以以对象模型的默认状态使用它，这种可能性很高。  
  
 为了很快入手，请使用 [!INCLUDE[vs_ordesigner_long](../../../../../../includes/vs-ordesigner-long-md.md)] 来创建对象模型并开始编写查询代码。  
  
## 创建对象模型  
 第一步是用现有关系数据库的元数据创建对象模型。  对象模型按照开发人员所用的编程语言来表示数据库。  有关详细信息，请参阅 [LINQ to SQL 对象模型](../../../../../../docs/framework/data/adonet/sql/linq/the-linq-to-sql-object-model.md)。  
  
### 1.选择用于创建模型的工具。  
 有三种工具可用于创建模型。  
  
-   [!INCLUDE[vs_ordesigner_long](../../../../../../includes/vs-ordesigner-long-md.md)]  
  
     此设计器提供了用于从现有数据库创建对象模型的丰富用户界面。  此工具是 [!INCLUDE[vs_current_short](../../../../../../includes/vs-current-short-md.md)] IDE 的一部分，最适合小型或中型数据库。  
  
-   SQLMetal 代码生成工具  
  
     此命令行实用工具提供了与 [!INCLUDE[vs_ordesigner_short](../../../../../../includes/vs-ordesigner-short-md.md)]略微不同的一组选项。  最好使用此工具对大型数据库进行建模。  有关详细信息，请参阅[SqlMetal.exe（代码生成工具）](../../../../../../docs/framework/tools/sqlmetal-exe-code-generation-tool.md)。  
  
-   代码编辑器  
  
     您可以通过使用 [!INCLUDE[vs_current_short](../../../../../../includes/vs-current-short-md.md)]代码编辑器或其他编辑器编写自己的代码。  我们建议，在您具有现有数据库且可以使用 [!INCLUDE[vs_ordesigner_short](../../../../../../includes/vs-ordesigner-short-md.md)]或 SQLMetal 工具时不要使用这种方法，因为这种方法容易出错。  但是，代码编辑器在改进或修改您已通过使用其他工具生成的代码方面非常有用。  有关详细信息，请参阅[如何：使用代码编辑器自定义实体类](../../../../../../docs/framework/data/adonet/sql/linq/how-to-customize-entity-classes-by-using-the-code-editor.md)。  
  
### 2.选择您要生成的代码类型。  
  
-   用于基于属性的映射的 C\# 或 [!INCLUDE[vbprvb](../../../../../../includes/vbprvb-md.md)] 源代码文件。  
  
     然后将此代码文件加入您的 [!INCLUDE[vs_current_short](../../../../../../includes/vs-current-short-md.md)] 项目中。有关详细信息，请参阅[基于属性的映射](../../../../../../docs/framework/data/adonet/sql/linq/attribute-based-mapping.md)。  
  
-   用于外部映射的 XML 文件。  
  
     通过使用此方法，您可以将映射元数据放在应用程序代码外部。  有关详细信息，请参阅[外部映射](../../../../../../docs/framework/data/adonet/sql/linq/external-mapping.md)。  
  
    > [!NOTE]
    >  [!INCLUDE[vs_ordesigner_short](../../../../../../includes/vs-ordesigner-short-md.md)]不支持生成外部映射文件。  您必须使用 SQLMetal 工具来实现此功能。  
  
-   DBML 文件，您可以在生成最终代码文件之前修改此文件。  
  
     这是一项高级功能。  
  
### 3.改进代码文件以反映您的应用程序的需要。  
 为此，您可以使用 [!INCLUDE[vs_ordesigner_short](../../../../../../includes/vs-ordesigner-short-md.md)]或代码编辑器。  
  
## 使用对象模型  
 下图显示了在两层方案中开发人员与数据之间的关系。  有关其他方案，请参阅[使用 LINQ to SQL 的 N 层应用程序和远程应用程序](../../../../../../docs/framework/data/adonet/sql/linq/n-tier-and-remote-applications-with-linq-to-sql.md)。  
  
 ![DLinqObjectModel](../../../../../../docs/framework/data/adonet/sql/linq/media/dlinqobjectmodel.png "DLinqObjectModel")  
  
 既然您已经有了对象模型，您就可以在该模型中描述信息请求和操作数据。  您应从对象模型中的对象和属性的角度来考虑，而不是从数据库的行和列的角度来考虑。  您不是直接对数据库进行操作。  
  
 当您指示 [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] 执行您已描述的查询或对您已操作的数据调用 `SubmitChanges()` 时，[!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] 会用数据库的语言与数据库通信。  
  
 以下内容代表使用您已创建的对象模型的典型步骤。  
  
### 1.创建查询以从数据库中检索信息。  
 有关详细信息，请参阅[查询概念](../../../../../../docs/framework/data/adonet/sql/linq/query-concepts.md) 和 [查询示例](../../../../../../docs/framework/data/adonet/sql/linq/query-examples.md)。  
  
### 2.重写 Insert、Update 和 Delete 的默认行为。  
 这一步是可选的。  有关详细信息，请参阅[自定义插入、更新和删除操作](../../../../../../docs/framework/data/adonet/sql/linq/customizing-insert-update-and-delete-operations.md)。  
  
### 3.设置适当的选项以检测和报告并发冲突。  
 您可以保留模型用于处理并发冲突的默认值，也可以根据您的需要对其进行更改。  有关详细信息，请参阅[如何：指定测试哪些成员是否发生并发冲突](../../../../../../docs/framework/data/adonet/sql/linq/how-to-specify-which-members-are-tested-for-concurrency-conflicts.md) 和[如何：指定并发异常的引发时间](../../../../../../docs/framework/data/adonet/sql/linq/how-to-specify-when-concurrency-exceptions-are-thrown.md)。  
  
### 4.建立继承层次结构。  
 这一步是可选的。  有关详细信息，请参阅[继承支持](../../../../../../docs/framework/data/adonet/sql/linq/inheritance-support.md)。  
  
### 5.提供合适的用户界面。  
 这一步是可选的，取决于您的应用程序的使用方式。  
  
### 6.调试并测试应用程序。  
 有关详细信息，请参阅[调试支持](../../../../../../docs/framework/data/adonet/sql/linq/debugging-support.md)。  
  
## 请参阅  
 [入门](../../../../../../docs/framework/data/adonet/sql/linq/getting-started.md)   
 [创建对象模型](../../../../../../docs/framework/data/adonet/sql/linq/creating-the-object-model.md)   
 [存储过程](../../../../../../docs/framework/data/adonet/sql/linq/stored-procedures.md)