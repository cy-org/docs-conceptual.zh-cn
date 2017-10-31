---
title: "如何︰ 使用 LINQ (Visual Basic 中) 调用存储的过程 |Microsoft 文档"
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
- queries [LINQ in Visual Basic], stored procedure calls
- stored procedures sample [Visual Basic]
- stored procedures [LINQ to SQL]
- queries [LINQ in Visual Basic], how-to topics
ms.assetid: 6436d384-d1e0-40aa-8afd-451007477260
caps.latest.revision: 12
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
ms.openlocfilehash: abc3970fc5ab6f4a2f4b67b5efa2b19afb07337b
ms.contentlocale: zh-cn
ms.lasthandoff: 03/13/2017

---
# <a name="how-to-call-a-stored-procedure-by-using-linq-visual-basic"></a>如何：使用 LINQ 调用存储过程 (Visual Basic)
语言集成查询 (LINQ) 就可以轻松地访问数据库的信息，包括数据库对象，如存储过程。  
  
 下面的示例演示如何创建 SQL Server 数据库中调用存储的过程的应用程序。 此示例演示如何在数据库中调用两个不同的存储的过程。 每个过程返回查询的结果。 一个过程采用输入的参数，以及另一个过程不带参数。  
  
 本主题中的示例使用罗斯文示例数据库。 如果您的开发计算机上没有 Northwind 示例数据库，您可以下载它从[Microsoft Download Center](http://go.microsoft.com/fwlink/?LinkID=98088) Web 站点。 有关说明，请参阅[下载示例数据库](https://msdn.microsoft.com/library/bb399411)。  
  
[!INCLUDE[note_settings_general](~/includes/note-settings-general-md.md)]  
  
### <a name="to-create-a-connection-to-a-database"></a>若要创建与数据库的连接  
  
1.  在 Visual Studio 中，打开**服务器资源管理器**/**数据库资源管理器**通过单击**服务器资源管理器**/**数据库资源管理器**上**视图**菜单。  
  
2.  用鼠标右键单击**数据连接**中**服务器资源管理器**/**数据库资源管理器**，然后单击**添加连接**。  
  
3.  指定到 Northwind 示例数据库的有效连接。  
  
### <a name="to-add-a-project-that-contains-a-linq-to-sql-file"></a>若要添加的项目中包含一个 LINQ to SQL 文件  
  
1.  在 Visual Studio 中，在**文件**菜单上，指向**新建**，然后单击**项目**。 选择 Visual Basic **Windows 窗体应用程序**作为项目类型。  
  
2.  在 **“项目”** 菜单上，单击 **“添加新项”**。 选择**LINQ to SQL 类**项模板。  
  
3.  命名该文件`northwind.dbml`。 单击 **“添加”**。 此时，northwind.dbml 文件打开对象关系设计器 （O/R 设计器）。  
  
### <a name="to-add-stored-procedures-to-the-or-designer"></a>若要将存储的过程添加到 O/R 设计器  
  
1.  在**服务器资源管理器**/**数据库资源管理器**，展开 Northwind 数据库的连接。 展开**存储过程**文件夹。  
  
     如果已经关闭 O/R 设计器，您可以通过双击前面添加此时，northwind.dbml 文件将其重新打开。  
  
2.  单击**年份的销售额**存储过程并将其拖到设计器的右窗格中。 单击**Ten Most Expensive Products**存储的过程将将其拖到设计器的右窗格中。  
  
3.  保存所做的更改并关闭设计器。  
  
4.  保存你的项目。  
  
### <a name="to-add-code-to-display-the-results-of-the-stored-procedures"></a>添加代码以显示存储过程的结果  
  
1.  从**工具箱**，拖动<xref:System.Windows.Forms.DataGridView>控件拖放到您的项目，form1 的默认设置 Windows 窗体。</xref:System.Windows.Forms.DataGridView>  
  
2.  双击 form1 若要将代码添加到其`Load`事件。  
  
3.  当存储的过程添加到 O/R 设计器时，设计器添加<xref:System.Data.Linq.DataContext>为你的项目的对象。</xref:System.Data.Linq.DataContext> 此对象包含必须具有访问这些过程的代码。 <xref:System.Data.Linq.DataContext>对象项目命名为根据.dbml 文件的名称。</xref:System.Data.Linq.DataContext> 对于此项目，<xref:System.Data.Linq.DataContext>对象被命名为`northwindDataContext`。</xref:System.Data.Linq.DataContext>  
  
     您可以创建的实例<xref:System.Data.Linq.DataContext>在您的代码和调用存储的过程方法由指定的 O/R 设计器。</xref:System.Data.Linq.DataContext> 若要将绑定到<xref:System.Windows.Forms.DataGridView>对象时，你可能需要强制执行查询立即执行，通过调用<xref:System.Linq.Enumerable.ToList%2A>方法存储过程的结果。</xref:System.Linq.Enumerable.ToList%2A> </xref:System.Windows.Forms.DataGridView>  
  
     添加以下代码到`Load`事件，以调用存储过程公开为数据上下文的方法之一。  
  
     [!code-vb[VbLINQtoSQLHowTos #&1;](../../../../visual-basic/programming-guide/language-features/linq/codesnippet/VisualBasic/how-to-call-a-stored-procedure-by-using-linq_1.vb)]  
    [!code-vb[VbLINQtoSQLHowTos #&2;](../../../../visual-basic/programming-guide/language-features/linq/codesnippet/VisualBasic/how-to-call-a-stored-procedure-by-using-linq_2.vb)]  
  
4.  按 F5 以运行您的项目并查看结果。  
  
## <a name="see-also"></a>另请参阅  
 [LINQ](../../../../visual-basic/programming-guide/language-features/linq/index.md)   
 [查询](../../../../visual-basic/language-reference/queries/queries.md)   
 [LINQ to SQL](https://msdn.microsoft.com/library/bb386976)   
 [DataContext 方法 （O/R 设计器）](https://docs.microsoft.com/visualstudio/data-tools/datacontext-methods-o-r-designer)   
 [如何︰ 分配存储的过程以便执行更新、 插入和删除操作 （O/R 设计器）](http://msdn.microsoft.com/library/e88224ab-ff61-4a3a-b6b8-6f3694546cac)

