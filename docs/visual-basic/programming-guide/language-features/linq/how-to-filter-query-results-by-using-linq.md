---
title: "如何︰ 使用 LINQ (Visual Basic 中) 来筛选查询结果 |Microsoft 文档"
ms.custom: 
ms.date: 2015-07-20
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology:
- devlang-visual-basic
ms.topic: article
dev_langs:
- VB
helpviewer_keywords:
- filtering [Visual Basic]
- filtering data [LINQ in Visual Basic]
- filtering [LINQ in Visual Basic]
- queries [LINQ in Visual Basic], filtering results
- querying databases [LINQ]
- queries [LINQ in Visual Basic], how-to topics
- query samples [Visual Basic]
- filtering data [Visual Basic]
ms.assetid: ef103092-9bed-4134-97f4-2db696e83c12
caps.latest.revision: 6
author: dotnet-bot
ms.author: dotnetcontent
translation.priority.ht:
- cs-cz
- de-de
- es-es
- fr-fr
- it-it
- ja-jp
- ko-kr
- pl-pl
- pt-br
- ru-ru
- tr-tr
- zh-cn
- zh-tw
ms.translationtype: Machine Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: 5aee7c3b07bcb8e623fb9090218a2b4bc8426ee3
ms.contentlocale: zh-cn
ms.lasthandoff: 03/13/2017

---
# <a name="how-to-filter-query-results-by-using-linq-visual-basic"></a>如何：使用 LINQ 筛选查询结果 (Visual Basic)
语言集成查询 (LINQ) 更加方便地访问数据库信息和执行查询。  
  
 下面的示例演示如何创建的新应用程序对 SQL Server 数据库执行查询并使用按特定值筛选结果`Where`子句。 有关详细信息，请参阅[Where 子句](../../../../visual-basic/language-reference/queries/where-clause.md)。  
  
 本主题中的示例使用罗斯文示例数据库。 如果您的开发计算机上没有 Northwind 示例数据库，您可以下载它从[Microsoft Download Center](http://go.microsoft.com/fwlink/?LinkID=98088) Web 站点。 有关说明，请参阅[下载示例数据库](https://msdn.microsoft.com/library/bb399411)。  
  
[!INCLUDE[note_settings_general](~/includes/note-settings-general-md.md)]  
  
### <a name="to-create-a-connection-to-a-database"></a>若要创建与数据库的连接  
  
1.  在 Visual Studio 中，打开**服务器资源管理器**/**数据库资源管理器**通过单击**服务器资源管理器**/**数据库资源管理器**上**视图**菜单。  
  
2.  用鼠标右键单击**数据连接**中**服务器资源管理器**/**数据库资源管理器**，然后单击**添加连接**。  
  
3.  指定到 Northwind 示例数据库的有效连接。  
  
### <a name="to-add-a-project-that-contains-a-linq-to-sql-file"></a>若要添加的项目中包含一个 LINQ to SQL 文件  
  
1.  在 Visual Studio 中，在**文件**菜单上，指向**新建**，然后单击**项目**。 选择 Visual Basic **Windows 窗体应用程序**作为项目类型。  
  
2.  在 **“项目”** 菜单上，单击 **“添加新项”**。 选择**LINQ to SQL 类**项模板。  
  
3.  命名该文件`northwind.dbml`。 单击 **“添加”**。 此时，northwind.dbml 文件将打开对象关系设计器 （O/R 设计器）。  
  
### <a name="to-add-tables-to-query-to-the-or-designer"></a>若要添加到 O/R 设计器查询的表  
  
1.  在**服务器资源管理器**/**数据库资源管理器**，展开 Northwind 数据库的连接。 展开**表**文件夹。  
  
     如果已经关闭 O/R 设计器，您可以通过双击前面添加此时，northwind.dbml 文件将其重新打开。  
  
2.  单击客户表，将其拖到设计器的左窗格中。 单击订单表，将其拖到设计器的左窗格中。  
  
     设计器创建新`Customer`和`Order`为你的项目的对象。 请注意，设计器会自动检测表之间的关系并创建子相关对象的属性。 例如，IntelliSense 将显示该`Customer`对象具有`Orders`与该客户相关的所有订单的属性。  
  
3.  保存所做的更改并关闭设计器。  
  
4.  保存你的项目。  
  
### <a name="to-add-code-to-query-the-database-and-display-the-results"></a>添加代码以查询数据库并显示结果  
  
1.  从**工具箱**，拖动<xref:System.Windows.Forms.DataGridView>控件拖放到您的项目，form1 的默认设置 Windows 窗体。</xref:System.Windows.Forms.DataGridView>  
  
2.  双击 form1 若要将代码添加到`Load`形式的事件。  
  
3.  当表添加到 O/R 设计器时，设计器添加<xref:System.Data.Linq.DataContext>为你的项目的对象。</xref:System.Data.Linq.DataContext> 此对象包含必须具有访问这些表，以及各个对象和集合的每个表的代码。 <xref:System.Data.Linq.DataContext>对象名为您的项目根据.dbml 文件的名称。</xref:System.Data.Linq.DataContext> 对于此项目，<xref:System.Data.Linq.DataContext>对象被命名为`northwindDataContext`。</xref:System.Data.Linq.DataContext>  
  
     您可以创建的实例<xref:System.Data.Linq.DataContext>代码和查询中指定由 O/R 设计器的表。</xref:System.Data.Linq.DataContext>  
  
     添加以下代码到`Load`事件以查询公开为数据上下文的属性的表。 查询筛选结果，并且仅返回客户位于`London`。  
  
     [!code-vb[VbLINQToSQLHowTos #&11;](../../../../visual-basic/programming-guide/language-features/linq/codesnippet/VisualBasic/how-to-filter-query-results-by-using-linq_1.vb)]  
  
4.  按 F5 以运行您的项目并查看结果。  
  
5.  以下是您可以尝试的一些其他筛选器。  
  
     [!code-vb[VbLINQToSQLHowTos #&12;](../../../../visual-basic/programming-guide/language-features/linq/codesnippet/VisualBasic/how-to-filter-query-results-by-using-linq_2.vb)]  
  
## <a name="see-also"></a>另请参阅  
 [LINQ](../../../../visual-basic/programming-guide/language-features/linq/index.md)   
 [查询](../../../../visual-basic/language-reference/queries/queries.md)   
 [LINQ to SQL](https://msdn.microsoft.com/library/bb386976)   
 [DataContext 方法 （O/R 设计器）](https://docs.microsoft.com/visualstudio/data-tools/datacontext-methods-o-r-designer)

