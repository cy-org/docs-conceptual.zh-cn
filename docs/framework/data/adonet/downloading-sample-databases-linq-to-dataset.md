---
title: "下载示例数据库 (LINQ to DataSet) | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-ado"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: eb42a7af-d410-4b7f-b4a8-13c72ce6fd09
caps.latest.revision: 2
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 2
---
# 下载示例数据库 (LINQ to DataSet)
[!INCLUDE[linq_dataset](../../../../includes/linq-dataset-md.md)] 文档中的示例和演练使用 AdventureWorks 示例数据库。  您可以从 Microsoft 下载站点免费下载此产品。[!INCLUDE[linq_dataset](../../../../includes/linq-dataset-md.md)] 文档中的示例和演练使用 SQL Server 作为数据存储区。  免费提供的 SQL Server Express Edition 也可代替 SQL Server 用作数据存储区。  
  
## 下载并安装 AdventureWorks 数据库  
  
#### 下载和安装适用于 SQL Server 的 AdventureWorks 示例数据库  
  
1.  打开 Internet Explorer。  
  
2.  转到 [SQL Server 2005 示例和示例数据库](http://go.microsoft.com/fwlink/?linkid=31046)（可能为英文网页）网站。  
  
3.  按照说明下载适用于您的处理器类型的 AdventureWorks 示例数据库（如 AdventureWorksDB.msi）并将该 .MSI 文件保存到您的本地计算机。  
  
4.  如果您通过下载或在 SQL Server 安装过程中安装了先前版本的 AdventureWorks，则在运行 AdventureWorks.msi 之前必须删除该版本。  
  
#### 删除先前下载的 AdventureWorks 示例数据库  
  
1.  删除 AdventureWorks 或 AdventureWorksDW 数据库。  
  
2.  从**“添加或删除程序”**中选择**“AdventureWorksDB”**或**“AdventureWorksBI”**，然后单击**“删除”**。  
  
#### 删除先前使用安装程序安装的 AdventureWorks 示例数据库  
  
1.  删除 AdventureWorks 或 AdventureWorksDW 数据库。  
  
2.  从**“添加或删除程序”**中选择**“Microsoft SQL Server 2005”**，然后单击**“更改”**。  
  
3.  从**“选择组件”**中选择**“工作站组件”**，然后单击**“下一步”**。  
  
4.  从**“欢迎使用 SQL Server 安装向导”**中单击**“下一步”**。  
  
5.  从**“系统配置检查”**中单击**“下一步”**。  
  
6.  从**“更改或删除实例”**中单击**“更改已安装的组件”**。  
  
7.  从**“功能选择”**中展开**“文档、示例和示例数据库”**节点。  
  
8.  选择**“示例代码和应用程序”**。  展开**“示例数据库”**，选择要删除的示例数据库，然后选择**“整个功能将不可用”**。  单击**“下一步”**。  
  
9. 单击**“安装”**，完成安装向导。  
  
#### 将 AdventureWorks 示例数据库文件附加到 SQL Server 的实例  
  
1.  下载了文件示例数据库安装程序文件后，双击**“AdventureWorksDB.msi”**文件（或您下载的文件）以安装该数据库。  默认情况下，该数据库安装在 c:\\Program Files\\Microsoft SQL Server\\MSSQL.1\\MSSQL\\Data 位置。  
  
2.  通过执行下面的脚本 SQLCMD 或 SQL Server Management Studio，将 AdventureWorks 数据库文件附加到 SQL Server 的实例：  
  
    ```  
    exec sp_attach_db @dbname=N'AdventureWorks', @filename1=N'C:\Program Files\Microsoft SQL Server\MSSQL.1\MSSQL\Data\AdventureWorks_Data.mdf', @filename2=N'C:\Program Files\Microsoft SQL Server\MSSQL.1\MSSQL\Data\AdventureWorks_log.ldf'  
    ```  
  
     如果您已将这些文件安装到其他驱动器或目录，则必须在执行 `sp_attach_db` 存储过程之前适当修改路径。  
  
## 下载 SQL Server Express Edition  
 [!INCLUDE[linq_dataset](../../../../includes/linq-dataset-md.md)] 一节中的示例和演练使用 SQL Server 2005 作为数据存储区，但也可以修改为使用 SQL Server Express Edition。  SQL Server Express Edition 免费提供，您可以利用应用程序重新发布它。  如果您要使用 [!INCLUDE[vsprvs](../../../../includes/vsprvs-md.md)]，则 Pro 和更高的版本将会包括 SQL Server Express Edition。  
  
#### 下载并安装 SQL Server Express Edition  
  
1.  启动 Internet Explorer。  
  
2.  转到 [Microsoft SQL Server 2005 Express Edition](http://go.microsoft.com/fwlink/?LinkID=31070) 下载页。  
  
3.  按照网站上的安装说明操作。  
  
## 请参阅  
 [入门](../../../../docs/framework/data/adonet/getting-started-linq-to-dataset.md)