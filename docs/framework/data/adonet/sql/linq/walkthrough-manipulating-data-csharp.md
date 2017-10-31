---
title: "演练：操作数据 (C#) | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-ado"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 24adfbe0-0ad6-449f-997d-8808e0770d2e
caps.latest.revision: 2
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 2
---
# 演练：操作数据 (C#)
本演练提供了用于在数据库中添加、修改和删除数据的基本端对端 [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] 方案。  您将使用 Northwind 示例数据库的一个副本来添加一位客户，更改该客户的姓名，然后删除一个订单。  
  
 [!INCLUDE[note_settings_general](../../../../../../includes/note-settings-general-md.md)]  
  
 本演练是使用 Visual C\# 开发设置编写的。  
  
## 系统必备  
 本演练需要如下内容：  
  
-   本演练使用专用文件夹（“c:\\linqtest6”）来保存文件。  请在开始本演练前创建此文件夹。  
  
-   Northwind 示例数据库。  
  
     如果您的开发计算机上没有此数据库，您可以从 Microsoft 下载网站下载它。  有关说明，请参阅[下载示例数据库](../../../../../../docs/framework/data/adonet/sql/linq/downloading-sample-databases.md)。  下载此数据库后，请将 northwnd.mdf 文件复制到 c:\\linqtest6 文件夹。  
  
-   从 Northwind 数据库生成的 C\# 代码文件。  
  
     可以使用[!INCLUDE[vs_ordesigner_long](../../../../../../includes/vs-ordesigner-long-md.md)]或 SQLMetal 工具生成此文件。  本演练是通过使用 SQLMetal 工具以及如下命令行编写的：  
  
     **sqlmetal \/code:"c:\\linqtest6\\northwind.cs" \/language:csharp "C:\\linqtest6\\northwnd.mdf" \/pluralize**  
  
     有关详细信息，请参阅[SqlMetal.exe（代码生成工具）](../../../../../../docs/framework/tools/sqlmetal-exe-code-generation-tool.md)。  
  
## 概述  
 本演练由六项主要任务组成：  
  
-   在 [!INCLUDE[vs_current_short](../../../../../../includes/vs-current-short-md.md)] 中创建 [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] 解决方案。  
  
-   向项目添加数据库代码文件。  
  
-   创建新的客户对象。  
  
-   修改客户的联系人姓名。  
  
-   删除订单。  
  
-   将这些更改提交至 Northwind 数据库。  
  
## 创建 LINQ to SQL 解决方案  
 此任务为第一项任务，在此任务中，您要创建一个 [!INCLUDE[vs_current_short](../../../../../../includes/vs-current-short-md.md)] 解决方案，此解决方案包含生成和运行 [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] 项目所必需的引用。  
  
#### 创建 LINQ to SQL 解决方案  
  
1.  在 [!INCLUDE[vs_current_short](../../../../../../includes/vs-current-short-md.md)] 的**“文件”**菜单上指向**“新建”**，然后单击**“项目”**。  
  
2.  在**“新建项目”**对话框中的**“项目类型”**窗格中，单击**“Visual C\#”**。  
  
3.  在**“模板”**窗格中，单击**“控制台应用程序”**。  
  
4.  在**“名称”**框中，键入 LinqDataManipulationApp。  
  
5.  在**“位置”**框中，确认要用于存储项目文件的位置。  
  
6.  单击“确定”。  
  
## 添加 LINQ 引用和指令  
 本演练用到默认情况下您的项目中可能未安装的程序集。  如果在您的项目中未将 System.Data.Linq 作为引用列出，请按照以下步骤中的说明添加它。  
  
#### 添加 System.Data.Linq  
  
1.  在**解决方案资源管理器**中，右键单击**“引用”**，然后单击**“添加引用”**。  
  
2.  在**“添加引用”**对话框中，依次单击**“.NET”**、System.Data.Linq 程序集，再单击**“确定”**。  
  
     此程序集即被添加到项目中。  
  
3.  在 Program.cs 的顶部添加以下指令：  
  
     [!code-csharp[DLinqWalk3CS#1](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqWalk3CS/cs/Program.cs#1)]  
  
## 将 Northwind 代码文件添加到项目  
 以下这些步骤假定您已使用 SQLMetal 工具从 Northwind 示例数据库生成代码文件。  有关更多信息，请参见本演练前面部分的“先决条件”一节。  
  
#### 将 northwind 代码文件添加到项目  
  
1.  在**“项目”**菜单上单击**“添加现有项”**。  
  
2.  在**“添加现有项”**对话框中，导航到 c:\\linqtest6\\northwind.cs，然后单击**“添加”**。  
  
     northwind.cs 文件即被添加到项目中。  
  
## 设置数据库连接  
 首先，测试与数据库的连接。  特别要注意，数据库 Northwnd 不含 i 字符。  如果在后面的步骤中产生错误，请检查 northwind.cs 文件以确定 Northwind 分部类的拼法。  
  
#### 设置并测试数据库连接  
  
1.  将下面的代码键入或粘贴到 Program 类的 `Main` 方法中：  
  
     [!code-csharp[DLinqWalk3CS#2](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqWalk3CS/cs/Program.cs#2)]  
  
2.  按 F5 在此点测试应用程序。  
  
     **“控制台”**窗口即会打开。  
  
     您可以通过如下方法关闭应用程序：在**“控制台”**窗口中按 Enter，或在 [!INCLUDE[vs_current_short](../../../../../../includes/vs-current-short-md.md)] 的**“调试”**菜单上单击**“停止调试”**。  
  
## 创建新实体  
 创建新实体很简单。  可以使用 `new` 关键字创建对象（如 `Customer`）。  
  
 在本节及后续各节中，您将只对本地缓存进行更改。  如果您不调用 <xref:System.Data.Linq.DataContext.SubmitChanges%2A>，则不会向数据库发送任何更改，一直到本演练结束都是如此。  
  
#### 添加新的 Customer 实体对象  
  
1.  通过在 `Main` 方法中的 `Console.ReadLine();` 前添加如下代码，创建一个新的 `Customer`：  
  
     [!code-csharp[DLinqWalk3CS#3](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqWalk3CS/cs/Program.cs#3)]  
  
2.  按 F5 调试解决方案。  
  
3.  在**“控制台”**窗口中按 Enter 可停止调试并继续本演练。  
  
## 更新实体  
 在以下步骤中，您将检索一个 `Customer` 对象并修改其属性之一。  
  
#### 更改客户的姓名  
  
-   将下面的代码添加到 `Console.ReadLine();` 上方：  
  
     [!code-csharp[DLinqWalk3CS#4](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqWalk3CS/cs/Program.cs#4)]  
  
## 删除实体  
 使用同一客户对象，您可以删除第一个订单。  
  
 下面的代码演示如何切断行与行之间的关系，以及如何从数据库中删除行。  请将下面的代码添加到 `Console.ReadLine` 前面，以了解如何可以删除对象：  
  
#### 删除行  
  
-   将下面的代码添加到 `Console.ReadLine();` 上方紧靠它的位置：  
  
     [!code-csharp[DLinqWalk3CS#5](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqWalk3CS/cs/Program.cs#5)]  
  
## 将更改提交到数据库  
 创建、更新和删除对象所需执行的最后一步是将更改实际提交到数据库。  如不执行这一步，您所做的更改将仅限本地，不会出现在查询结果中。  
  
#### 将更改提交到数据库  
  
1.  将下面的代码插入到 `Console.ReadLine` 上方紧靠它的位置：  
  
     [!code-csharp[DLinqWalk3CS#6](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqWalk3CS/cs/Program.cs#6)]  
  
2.  将下面的代码插入到 `SubmitChanges` 后面，以显示提交更改前后的效果：  
  
     [!code-csharp[DLinqWalk3CS#7](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqWalk3CS/cs/Program.cs#7)]  
  
3.  按 F5 调试解决方案。  
  
4.  在**“控制台”**窗口中按 Enter，以关闭应用程序。  
  
> [!NOTE]
>  通过提交更改添加了新的客户后，您无法再次按原样执行此解决方案。  若要再次执行此解决方案，请更改要添加的客户姓名和客户 ID。  
  
## 请参阅  
 [通过演练学习](../../../../../../docs/framework/data/adonet/sql/linq/learning-by-walkthroughs.md)