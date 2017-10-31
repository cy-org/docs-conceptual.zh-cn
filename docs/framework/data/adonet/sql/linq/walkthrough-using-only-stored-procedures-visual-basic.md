---
title: "仅使用存储过程 (Visual Basic) | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-ado"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 5a736a30-ba66-4adb-b87c-57d19476e862
caps.latest.revision: 4
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 4
---
# 仅使用存储过程 (Visual Basic)
本演练提供了通过仅使用存储过程来访问数据的 [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] 基本端对端方案。  数据库管理员经常使用此方法来限制数据存储的访问方式。  
  
> [!NOTE]
>  您还可以在 [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] 应用程序中使用存储过程来重写默认行为，尤其是 `Create`、`Update` 和 `Delete` 进程的默认行为。  有关详细信息，请参阅[自定义插入、更新和删除操作](../../../../../../docs/framework/data/adonet/sql/linq/customizing-insert-update-and-delete-operations.md)。  
  
 出于本演练的需要，您将用到已映射到 Northwind 示例数据库中存储过程的两个方法：CustOrdersDetail 和 CustOrderHist。  这种映射发生在您运行 SqlMetal 命令行工具生成 [!INCLUDE[vbprvb](../../../../../../includes/vbprvb-md.md)] 文件时。  有关更多信息，请参见本演练后面的“先决条件”一节。  
  
 本演练不依赖于[!INCLUDE[vs_ordesigner_long](../../../../../../includes/vs-ordesigner-long-md.md)]。  使用 [!INCLUDE[vs_current_short](../../../../../../includes/vs-current-short-md.md)] 的开发人员还可以使用 [!INCLUDE[vs_ordesigner_short](../../../../../../includes/vs-ordesigner-short-md.md)] 来实现存储过程功能。  请参阅[LINQ to SQL 工具在 Visual Studio 中](../Topic/LINQ%20to%20SQL%20Tools%20in%20Visual%20Studio2.md)。  
  
 [!INCLUDE[note_settings_general](../../../../../../includes/note-settings-general-md.md)]  
  
 本演练是使用 Visual Basic 开发设置编写的。  
  
## 系统必备  
 本演练需要如下内容：  
  
-   本演练使用专用文件夹（“c:\\linqtest3”）来保存文件。  请在开始本演练前创建此文件夹。  
  
-   Northwind 示例数据库。  
  
     如果您的开发计算机上没有此数据库，您可以从 Microsoft 下载网站下载它。  有关说明，请参阅[下载示例数据库](../../../../../../docs/framework/data/adonet/sql/linq/downloading-sample-databases.md)。  下载此数据库后，请将 northwnd.mdf 文件复制到 c:\\linqtest3 文件夹。  
  
-   从 Northwind 数据库生成的 [!INCLUDE[vbprvb](../../../../../../includes/vbprvb-md.md)] 代码文件。  
  
     本演练是通过使用 SqlMetal 工具以及如下命令行编写的：  
  
     **sqlmetal \/code:"c:\\linqtest3\\northwind.vb" \/language:vb "c:\\linqtest3\\northwnd.mdf" \/sprocs \/functions \/pluralize**  
  
     有关详细信息，请参阅[SqlMetal.exe（代码生成工具）](../../../../../../docs/framework/tools/sqlmetal-exe-code-generation-tool.md)。  
  
## 概述  
 本演练由六项主要任务组成：  
  
-   在 [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] 中设置 [!INCLUDE[vs_current_short](../../../../../../includes/vs-current-short-md.md)] 解决方案。  
  
-   将 System.Data.Linq 程序集添加到项目中。  
  
-   向项目添加数据库代码文件。  
  
-   创建与数据库的连接。  
  
-   设置用户界面。  
  
-   运行和测试应用程序。  
  
## 创建 LINQ to SQL 解决方案  
 此任务为第一项任务，在此任务中，您要创建一个 [!INCLUDE[vs_current_short](../../../../../../includes/vs-current-short-md.md)] 解决方案，此解决方案包含生成和运行 [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] 项目所必需的引用。  
  
#### 创建 LINQ to SQL 解决方案  
  
1.  在 [!INCLUDE[vs_current_short](../../../../../../includes/vs-current-short-md.md)] 的 **“文件”**菜单上，单击**“新建项目”**。  
  
2.  在**“新建项目”**对话框中的**“项目类型”**窗格中，展开**“Visual Basic”**，然后单击**“Windows”**。  
  
3.  在**“模板”**窗格中，单击**“Windows 窗体应用程序”**。  
  
4.  在**“名称”**框中，键入 SprocOnlyApp。  
  
5.  单击“确定”。  
  
     Windows 窗体设计器即会打开。  
  
## 添加 LINQ to SQL 程序集引用  
 [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] 程序集未包含在标准的 Windows 窗体应用程序模板中。  您将需要按照以下步骤中的说明自行添加此程序集：  
  
#### 添加 System.Data.Linq.dll  
  
1.  在**解决方案资源管理器**中，单击**“显示所有文件”**。  
  
2.  在**解决方案资源管理器**中，右键单击**“引用”**，然后单击**“添加引用”**。  
  
3.  在**“添加引用”**对话框中，依次单击**“.NET”**、System.Data.Linq 程序集，再单击**“确定”**。  
  
     此程序集即被添加到项目中。  
  
## 将 Northwind 代码文件添加到项目  
 此步骤假定您已使用 SqlMetal 工具从 Northwind 示例数据库生成代码文件。  有关更多信息，请参见本演练前面部分的“先决条件”一节。  
  
#### 将 northwind 代码文件添加到项目  
  
1.  在**“项目”**菜单上单击**“添加现有项”**。  
  
2.  在**“添加现有项”**对话框中，移动到 c:\\linqtest3\\northwind.vb，然后单击**“添加”**。  
  
     northwind.vb 文件即被添加到项目中。  
  
## 创建数据库连接  
 在此步骤中，您要定义与 Northwind 示例数据库的连接。  本演练使用“c:\\linqtest3\\northwnd.mdf”作为路径。  
  
#### 创建数据库连接  
  
1.  在**解决方案资源管理器**中右键单击**“Form1.vb”**，然后单击**“查看代码”**。  
  
     `Class Form1` 将显示在代码编辑器中。  
  
2.  在 `Form1` 代码块中键入如下代码：  
  
     [!code-vb[DLinqWalk4VB#1](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqWalk4VB/vb/Form1.vb#1)]  
  
## 设置用户界面  
 在此任务中，您要创建用户界面，供用户执行存储过程以访问数据库中的数据之用。  在您按照本演练开发的应用程序中，用户可以只使用嵌入在此应用程序中的存储过程来访问数据库中的数据。  
  
#### 设置用户界面  
  
1.  返回 Windows 窗体设计器（**“Form1.vb\[Design\]”**）。  
  
2.  在**“视图”**菜单上单击**“工具箱”**。  
  
     工具箱即会打开。  
  
    > [!NOTE]
    >  单击**“自动隐藏”**图钉，以使工具箱在您执行本节中剩余步骤的过程中保持打开。  
  
3.  从工具箱中将两个按钮、两个文本框和两个标签拖到**“Form1”**上。  
  
     按照附图排列这些控件。  扩展**“Form1”**，让控件更便于显示。  
  
4.  右键单击**“Label1”**，然后单击**“属性”**。  
  
5.  将**“Text”**属性从**“Label1”**更改为**“Enter OrderID:”**。  
  
6.  对于**“Label2”**，请按相同的方式将**“Text”**属性从**“Label2”**更改为**“Enter CustomerID:”**。  
  
7.  按相同的方式，将**“Button1”**的**“Text”**属性更改为**“Order Details”**。  
  
8.  将**“Button2”**的**“Text”**属性更改为**“Order History”**。  
  
     将这些按钮控件加宽，以使所有文本均可见。  
  
#### 处理按钮单击  
  
1.  双击**“Form1”**上的**“Order Details”（订单明细）**以创建 `Button1` 事件处理程序并打开代码编辑器。  
  
2.  将如下代码键入到 `Button1` 处理程序中：  
  
     [!code-vb[DLinqWalk4VB#2](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqWalk4VB/vb/Form1.vb#2)]  
  
3.  现在，双击 Form1 上的**“Button2”**以创建 `Button2` 事件处理程序并打开代码编辑器。  
  
4.  将如下代码键入到 `Button2` 处理程序中：  
  
     [!code-vb[DLinqWalk4VB#3](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqWalk4VB/vb/Form1.vb#3)]  
  
## 测试应用程序  
 现在，可以开始测试您的应用程序了。  请注意，您可对数据存储施加的影响仅限于这两个存储过程能够执行的操作。  这些操作是要根据您输入的所有 orderID 返回相应订单包括的产品，或根据您输入的所有 CustomerID 返回相应客户的产品订购历史记录。  
  
#### 测试应用程序  
  
1.  按 F5 开始调试。  
  
     此时将显示 Form1。  
  
2.  在**“Enter OrderID”（输入 OrderID）**框中，键入 10249，然后单击**“Order Details”（订单明细）**。  
  
     随即会显示一个消息框，其中列出了 10249 号订单中所包括的产品。  
  
     单击**“确定”**关闭此消息框。  
  
3.  在**“Enter CustomerID”（输入 CustomerID）**框中，键入 `ALFKI`，然后单击**“Order History”（订单历史记录）**。  
  
     随即会显示一个消息框，其中列出了 ALFKI 客户的订单历史记录。  
  
     单击**“确定”**关闭此消息框。  
  
4.  在**“Enter OrderID”（输入 OrderID）**框中，键入 `123`，然后单击**“Order Details”（订单明细）**。  
  
     随即会显示一个消息框，其中显示“无结果”。  
  
     单击**“确定”**关闭此消息框。  
  
5.  在**“调试”**菜单上，单击**“停止调试”**。  
  
     调试会话即会关闭。  
  
6.  如果您已试验完毕，可以单击**“文件”**菜单上的**“关闭项目”**，并在看到相应提示时保存您的项目。  
  
## 后续步骤  
 您可以通过做一些更改来增强此项目的功能。  例如，您可以在列表框中列出可用的存储过程，供用户选择要执行哪些过程。  您还可以将报告的输出以流的方式传输到文本文件。  
  
## 请参阅  
 [通过演练学习](../../../../../../docs/framework/data/adonet/sql/linq/learning-by-walkthroughs.md)   
 [存储过程](../../../../../../docs/framework/data/adonet/sql/linq/stored-procedures.md)