---
title: "演练：简单对象模型和查询 (Visual Basic) | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-ado"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: c878e457-f715-46e4-a136-ff14d6c86018
caps.latest.revision: 3
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 3
---
# 演练：简单对象模型和查询 (Visual Basic)
本演练提供了复杂性最小的基本端对端 [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] 方案。  您将创建一个可为示例 Northwind 数据库中的 Customers 表建模的实体类。  然后您将创建一个简单查询，用于列出位于伦敦的客户。  
  
 本演练在设计上是面向代码的，以帮助说明 [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] 概念。  一般来说，您会使用 [!INCLUDE[vs_ordesigner_long](../../../../../../includes/vs-ordesigner-long-md.md)] 来创建对象模型。  
  
 [!INCLUDE[note_settings_general](../../../../../../includes/note-settings-general-md.md)]  
  
 本演练是使用 Visual Basic 开发设置编写的。  
  
## 系统必备  
  
-   本演练使用专用文件夹（“c:\\linqtest”）来保存文件。  请在开始本演练前创建此文件夹。  
  
-   本演练需要 Northwind 示例数据库。  如果您的开发计算机上没有此数据库，您可以从 Microsoft 下载网站下载它。  有关说明，请参阅[下载示例数据库](../../../../../../docs/framework/data/adonet/sql/linq/downloading-sample-databases.md)。  下载此数据库后，请将文件复制到 c:\\linqtest 文件夹。  
  
## 概述  
 本演练由六项主要任务组成：  
  
-   在 [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] 中创建 [!INCLUDE[vs_current_short](../../../../../../includes/vs-current-short-md.md)] 解决方案。  
  
-   将类映射到数据库表。  
  
-   指定类中的属性表示数据库列。  
  
-   指定到 Northwind 数据库的连接。  
  
-   创建针对该数据库运行的简单查询。  
  
-   执行查询并观察结果。  
  
## 创建 LINQ to SQL 解决方案  
 此任务为第一项任务，在此任务中，您要创建一个 [!INCLUDE[vs_current_short](../../../../../../includes/vs-current-short-md.md)] 解决方案，此解决方案包含生成和运行 [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] 项目所必需的引用。  
  
#### 创建 LINQ to SQL 解决方案  
  
1.  在**“文件”**菜单上，单击**“新建项目”**。  
  
2.  在**“新建项目”**对话框的**“项目类型”**窗格中，单击**“Visual Basic”**。  
  
3.  在**“模板”**窗格中，单击**“控制台应用程序”**。  
  
4.  在**“名称”**框中，键入 LinqConsoleApp。  
  
5.  单击“确定”。  
  
## 添加 LINQ 引用和指令  
 本演练用到默认情况下您的项目中可能未安装的程序集。  如果在您的项目中未将 `System.Data.Linq` 作为引用列出（在**“解决方案资源管理器”**中单击**“显示所有文件”**并展开**“引用”**节点），请按照以下步骤中的说明添加它。  
  
#### 添加 System.Data.Linq  
  
1.  在**解决方案资源管理器**中，右键单击**“引用”**，然后单击**“添加引用”**。  
  
2.  在**“添加引用”**对话框中，依次单击**“.NET”**、System.Data.Linq 程序集，再单击**“确定”**。  
  
     此程序集即被添加到项目中。  
  
3.  同样在**“添加引用”**对话框中，单击**“.NET”**，滚动至 System.Windows.Forms 并单击它，然后单击**“确定”**。  
  
     此程序集（支持本演练中的消息框）即被添加到项目中。  
  
4.  在 `Module1` 上方添加以下指令：  
  
     [!code-vb[DLinqWalk1VB#1](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqWalk1VB/vb/Module1.vb#1)]  
  
## 将类映射到数据库表  
 在此步骤中，您将创建一个类，并将其映射到数据库表。  这样的类称为“实体类”。  请注意，只需添加 <xref:System.Data.Linq.Mapping.TableAttribute> 属性即可完成映射。  <xref:System.Data.Linq.Mapping.TableAttribute.Name%2A> 属性指定数据库中的表的名称。  
  
#### 创建一个实体类并将其映射到数据库表  
  
-   将下面的代码键入或粘贴到 `Sub Main` 上方紧靠它的 Module1.vb 中。  
  
     [!code-vb[DLinqWalk1VB#2](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqWalk1VB/vb/Module1.vb#2)]  
  
## 指定类中的属性表示数据库列  
 在此步骤中，您要完成几项任务。  
  
-   您要使用 <xref:System.Data.Linq.Mapping.ColumnAttribute> 属性 \(Attribute\) 指定实体类中的 `CustomerID` 和 `City` 属性 \(Property\) 表示数据库表中的列。  
  
-   您要指定 `CustomerID` 属性表示数据库中的主键列。  
  
-   您要指定 `_CustomerID` 和 `_City` 字段用作私有存储字段。  然后，[!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] 就可以直接存储和检索值，而不用使用可能包含业务逻辑的公共访问器。  
  
#### 表示两个数据库列的特性  
  
-   将下面的代码键入或粘贴到 `End Class` 前面紧靠它的 Module1.vb 中。  
  
     [!code-vb[DLinqWalk1VB#3](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqWalk1VB/vb/Module1.vb#3)]  
  
## 指定到 Northwind 数据库的连接  
 在此步骤中，要使用 <xref:System.Data.Linq.DataContext> 对象在您基于代码的数据结构和数据库本身之间建立连接。  <xref:System.Data.Linq.DataContext> 是您从数据库中检索对象和提交更改的主要通道。  
  
 您还需声明 `Table(Of Customer)`，用作您针对数据库中 Customers 表的查询的逻辑、类型化表。  您将在后续步骤中创建和执行这些查询。  
  
#### 指定数据库连接  
  
-   将下面的代码键入或粘贴到 `Sub Main` 方法中。  
  
     请注意，假定 `northwnd.mdf` 文件位于 linqtest 文件夹中。  有关更多信息，请参见本演练前面部分的“先决条件”一节。  
  
     [!code-vb[DLinqWalk1VB#4](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqWalk1VB/vb/Module1.vb#4)]  
  
## 创建简单查询  
 在此步骤中，您将创建一个查询，查找数据库中的 Customers 表内的哪些客户位于伦敦。  此步骤中的查询代码只描述查询。  它不执行查询。  这种方法称为“延迟执行”。  有关详细信息，请参阅 [Introduction to LINQ Queries \(C\#\)](../Topic/Introduction%20to%20LINQ%20Queries%20\(C%23\).md)。  
  
 您还将生成一个日志输出，显示 [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] 生成的 SQL 命令。  此日志记录功能（使用 <xref:System.Data.Linq.DataContext.Log%2A>）对调试有帮助，并有助于确定发送给数据库的命令是否准确地表示您的查询。  
  
#### 创建简单查询  
  
-   将下面的代码键入或粘贴到 `Sub Main` 声明之后的 `Table(Of Customer)` 方法中：  
  
     [!code-vb[DLinqWalk1AVB#5](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqWalk1AVB/vb/Module1.vb#5)]  
  
## 执行查询  
 在此步骤中，您将实际执行查询。  您在前面步骤中创建的查询表达式只有在需要结果时才会进行计算。  当您开始 `For Each` 迭代时，将对数据库执行 SQL 命令，并将对象具体化。  
  
#### 执行查询  
  
1.  将下面的代码键入或粘贴到 `Sub Main` 方法的结尾（在查询说明之后）：  
  
     [!code-vb[DLinqWalk1AVB#6](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqWalk1AVB/vb/Module1.vb#6)]  
  
2.  按 F5 调试该应用程序。  
  
    > [!NOTE]
    >  如果你的应用程序产生运行时错误，请参阅[通过演练学习](../../../../../../docs/framework/data/adonet/sql/linq/learning-by-walkthroughs.md) 中的“疑难解答”一节。  
  
     消息框会显示一个包含六个客户的列表。  控制台窗口会显示生成的 SQL 代码。  
  
3.  单击**“确定”**关闭该消息框。  
  
     应用程序即会关闭。  
  
4.  在**“文件”**菜单上，单击**“全部保存”**。  
  
     如果您要继续下一演练，您将需要此应用程序。  
  
## 后续步骤  
 [演练：跨关系查询 \(Visual Basic\)](../../../../../../docs/framework/data/adonet/sql/linq/walkthrough-querying-across-relationships-visual-basic.md) 主题在本演练结束的位置继续。  “跨关系进行查询”演练演示 [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] 如何跨表进行查询，这种查询与关系数据库中的联接类似。  
  
 如果您希望进行“跨关系进行查询”演练，请务必保存您刚完成的演练的解决方案，这是一项必备条件。  
  
## 请参阅  
 [通过演练学习](../../../../../../docs/framework/data/adonet/sql/linq/learning-by-walkthroughs.md)