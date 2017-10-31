---
title: "通过演练学习 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-ado"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: a8ae2965-6a49-4155-89b0-7fab2c488ab1
caps.latest.revision: 4
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 4
---
# 通过演练学习
[!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] 文档提供了一些演练。  本主题介绍一些一般性的演练问题（包括疑难解答），并提供指向用于了解 [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] 的一些入门级演练的链接。  
  
> [!NOTE]
>  此“入门”部分中的演练向您展示了支持 [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] 技术的基本代码。  在实际操作中，您通常会使用[!INCLUDE[vs_ordesigner_long](../../../../../../includes/vs-ordesigner-long-md.md)]和 Windows 窗体项目来实现您的 [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] 应用程序。  [!INCLUDE[vs_ordesigner_short](../../../../../../includes/vs-ordesigner-short-md.md)] 文档提供用于此目的的示例和演练。  
  
## 入门演练  
 本节中提供了若干演练。  这些演练基于 Northwind 示例数据库，以最不复杂的方式循序渐进地展示了 [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] 的功能。  
  
 应遵循的典型进展方案如下：  
  
|目标|Visual Basic|C\#|  
|--------|------------------|---------|  
|创建一个实体类并执行一个简单查询。|[演练：简单对象模型和查询 \(Visual Basic\)](../../../../../../docs/framework/data/adonet/sql/linq/walkthrough-simple-object-model-and-query-visual-basic.md)|[演练：简单对象模型和查询 \(C\#\)](../../../../../../docs/framework/data/adonet/sql/linq/walkthrough-simple-object-model-and-query-csharp.md)|  
|添加第二个类并执行一个更为复杂的查询。<br /><br /> （需要完成前一个演练。）|[演练：跨关系查询 \(Visual Basic\)](../../../../../../docs/framework/data/adonet/sql/linq/walkthrough-querying-across-relationships-visual-basic.md)|[演练：跨关系查询 \(C\#\)](../../../../../../docs/framework/data/adonet/sql/linq/walkthrough-querying-across-relationships-csharp.md)|  
|向数据库中添加项、更改并删除其中的项。|[演练：操作数据 \(Visual Basic\)](../../../../../../docs/framework/data/adonet/sql/linq/walkthrough-manipulating-data-visual-basic.md)|[演练：操作数据 \(C\#\)](../../../../../../docs/framework/data/adonet/sql/linq/walkthrough-manipulating-data-csharp.md)|  
|使用存储过程。|[仅使用存储过程 \(Visual Basic\)](../../../../../../docs/framework/data/adonet/sql/linq/walkthrough-using-only-stored-procedures-visual-basic.md)|[演练：仅使用存储过程 \(C\#\)](../../../../../../docs/framework/data/adonet/sql/linq/walkthrough-using-only-stored-procedures-csharp.md)|  
  
## 常规  
 以下信息大致介绍了这些演练：  
  
-   环境：每个 [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] 演练使用 [!INCLUDE[vs_current_short](../../../../../../includes/vs-current-short-md.md)] 作为其集成开发环境 \(IDE\)。  
  
-   SQL 引擎：所编写的这些演练需使用 SQL Server Express 来执行。  如果您没有 SQL Server Express，可以免费下载。  有关详细信息，请参阅[下载示例数据库](../../../../../../docs/framework/data/adonet/sql/linq/downloading-sample-databases.md)。  
  
    > [!NOTE]
    >  [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] 演练使用文件名作为连接字符串。  只需指定文件名即可，这是 [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] 为 SQL Server Express 用户提供的便捷之处。  始终要注意安全问题。  有关详细信息，请参阅 [LINQ to SQL 中的安全性](../../../../../../docs/framework/data/adonet/sql/linq/security-in-linq-to-sql.md)。  
  
-   [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] 演练通常需要 Northwind 示例数据库。  有关详细信息，请参阅[下载示例数据库](../../../../../../docs/framework/data/adonet/sql/linq/downloading-sample-databases.md)。  
  
-   您在演练中看到的对话框和菜单命令可能会与“帮助”中描述的有所不同，具体取决于您现用的设置或 [!INCLUDE[vs_current_short](../../../../../../includes/vs-current-short-md.md)] 版本。  若要更改设置，请单击**“工具”**菜单上的**“导入和导出设置”**。  有关详细信息，请参阅 [Customizing Development Settings in Visual Studio](http://msdn.microsoft.com/zh-cn/22c4debb-4e31-47a8-8f19-16f328d7dcd3)。  
  
-   对于介绍多层方案的演练，服务器必须位于与开发计算机不同的计算机上，并且您必须具有访问此服务器的相应权限。  
  
-   通常表示 Northwind 示例数据库中 Orders 表的类名为 `[Order]`。  这种转义是必需的，因为 `Order` 是 [!INCLUDE[vbprvb](../../../../../../includes/vbprvb-md.md)] 中的一个关键字。  
  
## 疑难解答  
 发生运行时错误的原因可能是您没有足够的权限来访问这些演练中使用的数据库。  请参见以下步骤以帮助解决最常见的此类问题。  
  
### 登录问题  
 您的应用程序可能尝试使用数据库不接受的数据库登录名来访问数据库。  
  
##### 验证或更改数据库登录名  
  
1.  在 Windows 的**“开始”**菜单上，依次指向**“所有程序”**、**“Microsoft SQL Server 2005”**、**“配置工具”**，然后单击**“SQL Server 配置管理器”**。  
  
2.  在**“SQL Server 配置管理器”**的左窗格中，单击**“SQL Server 2005 服务”**。  
  
3.  在右窗格中，右击**“SQL Server \(SQLEXPRESS\)”**，然后单击**“属性”**。  
  
4.  单击**“登录”**选项卡，验证您尝试登录到服务器的方式。  
  
     在大多数情况下，使用**“Local System”**即可登录。  
  
     如果您做了更改，请单击**“重新启动”**以重新启动此服务。  
  
### 协议  
 有时，您的应用程序用来访问数据库的协议可能未设置正确。  例如， **中的演练需要的[!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)]“Named Pipes”**协议默认是未启用的。  
  
##### 启用 Named Pipes 协议  
  
1.  在**“SQL Server 配置管理器”**的左窗格中，展开**“SQL Server 2005 网络配置”**，然后单击**“SQLEXPRESS 的协议”**。  
  
2.  在右窗格中，确保**“Named Pipes”**协议已启用。  如果它未启用，请右击**“Name Pipes”**，然后单击**“启用”**。  
  
     您将需要停止此服务，再重新启动它。  请按下一部分中的步骤操作。  
  
### 停止并重新启动服务  
 您必须先停止并重新启动服务，所做的更改才能生效。  
  
##### 停止并重新启动服务  
  
1.  在**“SQL Server 配置管理器”**的左窗格中，单击**“SQL Server 2005 服务”**。  
  
2.  在右窗格中，右击**“SQL Server \(SQLEXPRESS\)”**，然后单击**“停止”**。  
  
3.  右击**“SQL Server \(SQLEXPRESS\)”**，然后单击**“重新启动”**。  
  
## 请参阅  
 [入门](../../../../../../docs/framework/data/adonet/sql/linq/getting-started.md)