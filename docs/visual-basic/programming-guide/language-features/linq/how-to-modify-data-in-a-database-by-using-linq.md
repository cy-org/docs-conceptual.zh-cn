---
title: "如何︰ 通过使用 LINQ (Visual Basic 中) 来修改数据库中的数据 |Microsoft 文档"
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
- inserting rows [LINQ to SQL]
- deleting rows [LINQ to SQL]
- updating rows [LINQ to SQL]
- inserting data [Visual Basic]
- deleting data
- data [Visual Basic], updating
- updating data [LINQ]
- queries [LINQ in Visual Basic], data changes in database
- queries [LINQ in Visual Basic], how-to topics
ms.assetid: cf52635f-0c1b-46c3-aff1-bdf181cf19b1
caps.latest.revision: 15
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
translationtype: Machine Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: 44ca3e44d8411a6329d176eb778677bfab2b365c
ms.lasthandoff: 03/13/2017

---
# <a name="how-to-modify-data-in-a-database-by-using-linq-visual-basic"></a>如何：使用 LINQ 修改数据库中的数据 (Visual Basic)
语言集成查询 (LINQ) 查询更加易于访问数据库信息和修改数据库中的值。  
  
 下面的示例演示如何创建新的应用程序，以检索和更新信息在 SQL Server 数据库中。  
  
 本主题中的示例使用罗斯文示例数据库。 如果您的开发计算机上没有 Northwind 示例数据库，您可以下载它从[Microsoft Download Center](http://go.microsoft.com/fwlink/?LinkID=98088) Web 站点。 有关说明，请参阅[下载示例数据库](https://msdn.microsoft.com/library/bb399411)。  
  
### <a name="to-create-a-connection-to-a-database"></a>若要创建与数据库的连接  
  
1.  在 Visual Studio 中，打开**服务器资源管理器**/**数据库资源管理器**通过单击**视图**菜单，然后再选择**服务器资源管理器**/**数据库资源管理器**。  
  
2.  用鼠标右键单击**数据连接**中**服务器资源管理器**/**数据库资源管理器**，然后单击**添加连接**。  
  
3.  指定到 Northwind 示例数据库的有效连接。  
  
### <a name="to-add-a-project-with-a-linq-to-sql-file"></a>若要将使用 LINQ 项目添加到 SQL 文件  
  
1.  在 Visual Studio 中，在**文件**菜单上，指向**新建**，然后单击**项目**。 选择 Visual Basic **Windows 窗体应用程序**作为项目类型。  
  
2.  在 **“项目”** 菜单上，单击 **“添加新项”**。 选择**LINQ to SQL 类**项模板。  
  
3.  命名该文件`northwind.dbml`。 单击 **“添加”**。 对象关系设计器 （O/R 设计器） 打开以进行`northwind.dbml`文件。  
  
### <a name="to-add-tables-to-query-and-modify-to-the-designer"></a>若要添加表以查询和修改到设计器  
  
1.  在**服务器资源管理器**/**数据库资源管理器**，展开 Northwind 数据库的连接。 展开**表**文件夹。  
  
     如果已经关闭 O/R 设计器，您可以重新打开它通过双击`northwind.dbml`前面添加的文件。  
  
2.  单击客户表，将其拖到设计器的左窗格中。  
  
     设计器创建新的 Customer 对象为你的项目。  
  
3.  保存所做的更改并关闭设计器。  
  
4.  保存你的项目。  
  
### <a name="to-add-code-to-modify-the-database-and-display-the-results"></a>添加代码以修改数据库并显示结果  
  
1.  从**工具箱**，拖动<xref:System.Windows.Forms.DataGridView>控件拖放到您的项目，form1 的默认设置 Windows 窗体。</xref:System.Windows.Forms.DataGridView>  
  
2.  当表添加到 O/R 设计器时，设计器添加<xref:System.Data.Linq.DataContext>对象传递给您的项目。</xref:System.Data.Linq.DataContext> 此对象包含可用于访问客户表的代码。 它还包含用于定义本地的客户对象和一个客户集合，以便对表的代码。 <xref:System.Data.Linq.DataContext>对象名为您的项目根据.dbml 文件的名称。</xref:System.Data.Linq.DataContext> 对于此项目，<xref:System.Data.Linq.DataContext>对象被命名为`northwindDataContext`。</xref:System.Data.Linq.DataContext>  
  
     您可以创建的实例<xref:System.Data.Linq.DataContext>对象在您的代码和查询和修改由 O/R 设计器指定的客户集合。</xref:System.Data.Linq.DataContext> 之前通过调用将提交对 Customers 集合所做的更改不会反映在数据库中<xref:System.Data.Linq.DataContext.SubmitChanges%2A>方法<xref:System.Data.Linq.DataContext>对象。</xref:System.Data.Linq.DataContext> </xref:System.Data.Linq.DataContext.SubmitChanges%2A>  
  
     双击 Windows 窗体，form1，以将代码添加到<xref:System.Windows.Forms.Form.Load>事件，以查询作为您<xref:System.Data.Linq.DataContext>。</xref:System.Data.Linq.DataContext>属性公开的客户表</xref:System.Windows.Forms.Form.Load> 添加以下代码：  
  
    ```vb  
    Private db As northwindDataContext  
  
    Private Sub Form1_Load(ByVal sender As System.Object,   
                           ByVal e As System.EventArgs  
                          ) Handles MyBase.Load  
      db = New northwindDataContext()  
  
      RefreshData()  
    End Sub  
  
    Private Sub RefreshData()  
      Dim customers = From cust In db.Customers   
                      Where cust.City(0) = "W"   
                      Select cust  
  
      DataGridView1.DataSource = customers  
    End Sub  
    ```  
  
3.  从**工具箱**，将三个<xref:System.Windows.Forms.Button>拖到窗体的控件。</xref:System.Windows.Forms.Button> 选择第一个`Button`控件。 在**属性**窗口中，设置`Name`的`Button`控制转移到`AddButton`和`Text`到`Add`。 选择第二个按钮并设置`Name`属性设置为`UpdateButton`和`Text`属性设置为`Update`。 选择第三个按钮并设置`Name`属性设置为`DeleteButton`和`Text`属性设置为`Delete`。  
  
4.  双击**添加**按钮以将代码添加到其`Click`事件。 添加以下代码：  
  
    ```vb  
    Private Sub AddButton_Click(ByVal sender As System.Object,   
                                ByVal e As System.EventArgs  
                               ) Handles AddButton.Click  
      Dim cust As New Customer With {   
        .City = "Wellington",   
        .CompanyName = "Blue Yonder Airlines",   
        .ContactName = "Jill Frank",   
        .Country = "New Zealand",   
        .CustomerID = "JILLF"}  
  
      db.Customers.InsertOnSubmit(cust)  
  
      Try  
        db.SubmitChanges()  
      Catch  
        ' Handle exception.  
      End Try  
  
      RefreshData()  
    End Sub  
    ```  
  
5.  双击**更新**按钮以将代码添加到其`Click`事件。 添加以下代码：  
  
    ```vb  
    Private Sub UpdateButton_Click(ByVal sender As System.Object, _  
                                   ByVal e As System.EventArgs  
                                  ) Handles UpdateButton.Click  
      Dim updateCust = (From cust In db.Customers   
                        Where cust.CustomerID = "JILLF").ToList()(0)  
  
      updateCust.ContactName = "Jill Shrader"  
  
      Try  
        db.SubmitChanges()  
      Catch  
        ' Handle exception.  
      End Try  
  
      RefreshData()  
    End Sub  
    ```  
  
6.  双击**删除**按钮以将代码添加到其`Click`事件。 添加以下代码：  
  
    ```vb  
    Private Sub DeleteButton_Click(ByVal sender As System.Object, _  
                                   ByVal e As System.EventArgs  
                                  ) Handles DeleteButton.Click  
      Dim deleteCust = (From cust In db.Customers   
                        Where cust.CustomerID = "JILLF").ToList()(0)  
  
      db.Customers.DeleteOnSubmit(deleteCust)  
  
      Try  
        db.SubmitChanges()  
      Catch  
        ' Handle exception.  
      End Try  
  
      RefreshData()  
    End Sub  
    ```  
  
7.  按 F5 运行项目。 单击**添加**添加一条新记录。 单击**更新**修改新记录。 单击**删除**来删除新的记录。  
  
## <a name="see-also"></a>另请参阅  
 [LINQ](../../../../visual-basic/programming-guide/language-features/linq/index.md)   
 [查询](../../../../visual-basic/language-reference/queries/queries.md)   
 [LINQ to SQL](https://msdn.microsoft.com/library/bb386976)   
 [DataContext 方法 （O/R 设计器）](https://docs.microsoft.com/visualstudio/data-tools/datacontext-methods-o-r-designer)   
 [如何︰ 分配存储的过程以便执行更新、 插入和删除操作 （O/R 设计器）](http://msdn.microsoft.com/library/e88224ab-ff61-4a3a-b6b8-6f3694546cac)
