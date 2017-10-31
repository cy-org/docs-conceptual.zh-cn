---
title: "演练︰ 在 DataRepeater 控件 (Visual Studio) 中显示数据 |Microsoft 文档"
ms.date: 2015-07-20
ms.prod: .net
ms.suite: 
ms.technology:
- devlang-visual-basic
ms.topic: article
dev_langs:
- VB
helpviewer_keywords:
- DataRepeater, walkthrough
ms.assetid: 65dcdb95-6c3e-47cc-987d-190000f71653
caps.latest.revision: 12
author: dotnet-bot
ms.author: dotnetcontent
translation.priority.ht:
- de-de
- es-es
- fr-fr
- it-it
- ja-jp
- ko-kr
- ru-ru
- zh-cn
- zh-tw
translation.priority.mt:
- cs-cz
- pl-pl
- pt-br
- tr-tr
translationtype: Machine Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: 09f15c94c3d5a3387935c8d3f4758c0ecfd7cfcd
ms.lasthandoff: 03/13/2017

---
# <a name="walkthrough-displaying-data-in-a-datarepeater-control-visual-studio"></a>演练：在 DataRepeater 控件中显示数据 (Visual Studio)
本演练提供了基本的开始-完成方案中显示绑定的数据在<xref:Microsoft.VisualBasic.PowerPacks.DataRepeater>控件。</xref:Microsoft.VisualBasic.PowerPacks.DataRepeater>  
  
## <a name="prerequisite"></a>必备组件  
 本演练需要 Northwind 示例数据库。  
  
 如果你的开发计算机上没有此数据库，可以从 [Microsoft 下载中心](http://go.microsoft.com/fwlink/?LinkID=98088)进行下载。 有关说明，请参阅[下载示例数据库](https://msdn.microsoft.com/library/bb399411)。  
  
## <a name="overview"></a>概述  
 本演练的第一部分主要有以下四个任务：  
  
-   创建解决方案。  
  
-   添加<xref:Microsoft.VisualBasic.PowerPacks.DataRepeater>控件。</xref:Microsoft.VisualBasic.PowerPacks.DataRepeater>  
  
-   添加数据源。  
  
-   添加数据绑定控件。  
  
[!INCLUDE[note_settings_general](../../../csharp/language-reference/compiler-messages/includes/note_settings_general_md.md)]  
  
## <a name="creating-a-datarepeater-solution"></a>创建 DataRepeater 解决方案  
 在第一步中，创建项目和解决方案。  
  
#### <a name="to-create-a-datarepeater-solution"></a>创建 DataRepeater 解决方案的步骤  
  
1.  在 Visual Studio**文件**菜单上，单击**新项目**。  
  
2.  在 **“新建项目”** 对话框中的 **“项目类型”** 窗格中，展开 **“Visual Basic”**，然后单击 **“Windows”**。  
  
3.  在 **“模板”** 窗格中，单击 **“Windows 窗体应用程序”**。  
  
4.  在“名称”****框中键入 `DataRepeaterApp`。  
  
5.  单击 **“确定”**。  
  
     Windows 窗体设计器即会打开。  
  
6.  在“Windows 窗体设计器”中选择窗体。 在**属性**窗口中，设置**大小**属性设置为`800, 700`。  
  
## <a name="adding-a-datarepeater-control"></a>添加 DataRepeater 控件  
 在此步骤中，您将添加<xref:Microsoft.VisualBasic.PowerPacks.DataRepeater>到窗体的控件。</xref:Microsoft.VisualBasic.PowerPacks.DataRepeater>  
  
#### <a name="to-add-a-datarepeater-control"></a>添加 DataRepeater 控件的步骤  
  
1.  在 **“视图”** 菜单上单击 **“工具箱”**。  
  
     将打开 **“工具箱”** 。  
  
2.  选择**Visual Basic PowerPacks**选项卡。  
  
3.  拖动<xref:Microsoft.VisualBasic.PowerPacks.DataRepeater>控件拖动到**form1**。</xref:Microsoft.VisualBasic.PowerPacks.DataRepeater>  
  
4.  在属性窗口中设置**位置**属性设置为`0, 25`。  
  
5.  设置**大小**属性设置为`460, 600`。  
  
## <a name="adding-a-data-source"></a>添加数据源  
 在此步骤中，添加的数据源<xref:Microsoft.VisualBasic.PowerPacks.DataRepeater>控件。</xref:Microsoft.VisualBasic.PowerPacks.DataRepeater>  
  
#### <a name="to-add-a-data-source"></a>添加数据源  
  
1.  在 **“数据”** 菜单上，单击 **“显示数据源”**。  
  
2.  在 **“数据源”** 窗口中，单击 **“添加新数据源”**。  
  
3.  在 **“选择数据源类型”** 页上选择 **“数据库”** ，然后单击 **“下一步”**。  
  
4.  在 **“选择你的数据连接”** 页上执行下列步骤之一：  
  
    -   如果下拉列表中包含到 Northwind 示例数据库的数据连接，请单击该连接。  
  
         - 或 -  
  
    -   单击**新连接**以配置新的数据连接。 有关详细信息，请参阅[如何︰ 创建到 SQL Server 数据库的连接](http://msdn.microsoft.com/en-us/360c340d-e5a6-4a7e-a569-e95d500be43d)。  
  
5.  如果数据库需要密码，请选择该选项以包括敏感数据，然后单击 **“下一步”**。  
  
    > [!NOTE]
    >  如果出现一个对话框中，单击**是**将文件保存到您的项目。  
  
6.  单击**下一步**上**连接字符串保存到应用程序配置文件**页。  
  
7.  在 **“选择数据库对象”** 页面上展开 **“表”** 节点。  
  
8.  选中的复选框旁边**客户**和**订单**表，然后单击**完成**。  
  
     **NorthwindDataSet**添加到您的项目和**客户**和**订单**表将显示在**数据源**窗口。  
  
## <a name="adding-data-bound-controls"></a>添加数据绑定控件  
 在此步骤中，您可以将数据绑定控件添加到<xref:Microsoft.VisualBasic.PowerPacks.DataRepeater>。</xref:Microsoft.VisualBasic.PowerPacks.DataRepeater>  
  
#### <a name="to-add-data-bound-controls"></a>添加数据绑定控件  
  
1.  在**数据源**窗口中，选择的顶级节点**客户**表。  
  
2.  将表拖放类型更改**详细信息**通过单击**详细信息**表节点上的下拉列表中。  
  
3.  选择**客户**表节点，然后将其拖动到项模板区域 （上部区域） 的<xref:Microsoft.VisualBasic.PowerPacks.DataRepeater>控件。</xref:Microsoft.VisualBasic.PowerPacks.DataRepeater>  
  
     一个<xref:System.Windows.Forms.BindingNavigator>控件添加到窗体中，与**NorthwindDataSet**， **CustomersBindingSource**， **CustomersTableAdapter**， **TableAdapterManager**，和**CustomersBindingNavigator**组件添加到组件栏。</xref:System.Windows.Forms.BindingNavigator>  
  
4.  选择所有字段及其关联标签，并将它们置于项模板区域左边缘附近。  
  
5.  选择的最后五个字段 (**区域**， **Postal Code**，**国家/地区**，**电话**，和**传真**) 及其关联的标签并将它们移向上和向右的前六个字段。  
  
6.  选择项模板（控件的上半部分区域）。  
  
7.  在属性窗口中设置**大小**属性设置为`427, 170`。  
  
 此时，你就得到了一个有效的应用程序，该应用程序将显示客户的重复列表。 可以按 F5 运行该应用程序、更改数据以及添加或删除客户记录。  
  
 在下一个可选步骤中，您将学习如何自定义<xref:Microsoft.VisualBasic.PowerPacks.DataRepeater>控件。</xref:Microsoft.VisualBasic.PowerPacks.DataRepeater>  
  
## <a name="next-steps-optional"></a>后续步骤（可选）  
 演练的本部分有以下四个可选任务：  
  
-   更改外观的<xref:Microsoft.VisualBasic.PowerPacks.DataRepeater>控件。</xref:Microsoft.VisualBasic.PowerPacks.DataRepeater>  
  
-   防止用户添加或删除记录。  
  
-   添加搜索功能<xref:Microsoft.VisualBasic.PowerPacks.DataRepeater>控件。</xref:Microsoft.VisualBasic.PowerPacks.DataRepeater>  
  
-   添加到母版和详细信息表<xref:Microsoft.VisualBasic.PowerPacks.DataRepeater>控件。</xref:Microsoft.VisualBasic.PowerPacks.DataRepeater>  
  
## <a name="changing-the-appearance-of-the-datarepeater-control"></a>更改 DataRepeater 控件的外观  
 此可选步骤中，在您更改`BackColor`的<xref:Microsoft.VisualBasic.PowerPacks.DataRepeater>控件在设计时。</xref:Microsoft.VisualBasic.PowerPacks.DataRepeater> 你还将添加代码来以交替颜色显示行以及有条件地更改标签的 `ForeColor` 。  
  
#### <a name="to-change-the-appearance-of-the-control"></a>更改控件外观的步骤  
  
1.  在 Windows 窗体设计器中，选择的主 （下部） 区域<xref:Microsoft.VisualBasic.PowerPacks.DataRepeater>控件。</xref:Microsoft.VisualBasic.PowerPacks.DataRepeater>  
  
2.  在“属性”窗口中，将 `BackColor` 属性设置为白色。  
  
3.  双击<xref:Microsoft.VisualBasic.PowerPacks.DataRepeater>以打开代码编辑器。</xref:Microsoft.VisualBasic.PowerPacks.DataRepeater>  
  
4.  在代码编辑器中，事件中的下拉列表中，单击**DrawItem**。  
  
5.  在<xref:Microsoft.VisualBasic.PowerPacks.DataRepeater.DrawItem>事件处理程序中，将以下代码添加到备用`BackColor`:</xref:Microsoft.VisualBasic.PowerPacks.DataRepeater.DrawItem>  
  
     [!code-cs[VbPowerPacksDataRepeaterWalkthrough&#1;](../../../visual-basic/developing-apps/windows-forms/codesnippet/CSharp/walkthrough-displaying-data-in-a-datarepeater-control-visual-studio_1.cs) ] 
     [!code-vb [VbPowerPacksDataRepeaterWalkthrough&#1;](../../../visual-basic/developing-apps/windows-forms/codesnippet/VisualBasic/walkthrough-displaying-data-in-a-datarepeater-control-visual-studio_1.vb)]  
  
6.  在<xref:Microsoft.VisualBasic.PowerPacks.DataRepeater.DrawItem>事件处理程序中，添加以下代码，以更改`ForeColor`视情况标签的︰</xref:Microsoft.VisualBasic.PowerPacks.DataRepeater.DrawItem>  
  
     [!code-cs[VbPowerPacksDataRepeaterWalkthrough&#2;](../../../visual-basic/developing-apps/windows-forms/codesnippet/CSharp/walkthrough-displaying-data-in-a-datarepeater-control-visual-studio_2.cs) ] 
     [!code-vb [VbPowerPacksDataRepeaterWalkthrough&#2;](../../../visual-basic/developing-apps/windows-forms/codesnippet/VisualBasic/walkthrough-displaying-data-in-a-datarepeater-control-visual-studio_2.vb)]  
  
7.  按 F5 运行该应用程序并查看自定义项。  
  
## <a name="preventing-users-from-adding-or-deleting-records"></a>防止用户添加或删除记录  
 在此可选步骤中，添加代码来防止用户添加或删除中的记录<xref:Microsoft.VisualBasic.PowerPacks.DataRepeater>控件。</xref:Microsoft.VisualBasic.PowerPacks.DataRepeater>  
  
#### <a name="to-prevent-users-from-adding-and-deleting-records"></a>防止用户添加和删除记录的步骤  
  
1.  在 Windows 窗体设计器中，双击窗体打开代码编辑器。  
  
2.  将以下代码添加到 `Form_Load` 事件中：  
  
     [!code-cs[VbPowerPacksDataRepeaterWalkthrough&#3;](../../../visual-basic/developing-apps/windows-forms/codesnippet/CSharp/walkthrough-displaying-data-in-a-datarepeater-control-visual-studio_3.cs) ] 
     [!code-vb [VbPowerPacksDataRepeaterWalkthrough&#3;](../../../visual-basic/developing-apps/windows-forms/codesnippet/VisualBasic/walkthrough-displaying-data-in-a-datarepeater-control-visual-studio_3.vb)]  
  
3.  在类名称下拉列表中，单击**BindingNavigatorDeleteItem**。 在方法名称下拉列表中，单击**EnabledChanged**。  
  
4.  将以下代码添加到 `BindingNavigatorDeleteItem_EnabledChanged` 事件处理程序中：  
  
     [!code-cs[VbPowerPacksDataRepeaterWalkthrough&#4;](../../../visual-basic/developing-apps/windows-forms/codesnippet/CSharp/walkthrough-displaying-data-in-a-datarepeater-control-visual-studio_4.cs) ] 
     [!code-vb [VbPowerPacksDataRepeaterWalkthrough&#4;](../../../visual-basic/developing-apps/windows-forms/codesnippet/VisualBasic/walkthrough-displaying-data-in-a-datarepeater-control-visual-studio_4.vb)]  
  
    > [!NOTE]
    >  此步骤是必需因为<xref:System.Windows.Forms.BindingSource>将启用**DeleteItem**按钮当前记录发生更改的每次。</xref:System.Windows.Forms.BindingSource>  
  
5.  按 F5 运行该应用程序。 请注意， **DeleteItem**按钮被禁用，以及不能删除项目，通过按 DELETE 键。  
  
## <a name="adding-search-capability-to-the-datarepeater-control"></a>向 DataRepeater 控件添加搜索功能  
 在此步骤可选实现搜索中的值的功能<xref:Microsoft.VisualBasic.PowerPacks.DataRepeater>控件。</xref:Microsoft.VisualBasic.PowerPacks.DataRepeater> 如果找到了搜索字符串，该控件将选中包含该值的项并将该项滚动到视图中。  
  
#### <a name="to-add-search-capability"></a>添加搜索功能的步骤  
  
1.  拖动<xref:System.Windows.Forms.TextBox>控件从**工具箱**拖到窗体，其中包含<xref:Microsoft.VisualBasic.PowerPacks.DataRepeater>控件。</xref:Microsoft.VisualBasic.PowerPacks.DataRepeater> </xref:System.Windows.Forms.TextBox>  
  
     将在下其位置<xref:Microsoft.VisualBasic.PowerPacks.DataRepeater>控件。</xref:Microsoft.VisualBasic.PowerPacks.DataRepeater>  
  
2.  在属性窗口中，将更改**名称**属性设置为**搜索文本框**。  
  
3.  拖动<xref:System.Windows.Forms.Button>控件从**工具箱**拖到窗体，其中包含<xref:Microsoft.VisualBasic.PowerPacks.DataRepeater>控件。</xref:Microsoft.VisualBasic.PowerPacks.DataRepeater> </xref:System.Windows.Forms.Button> 将在下其位置<xref:Microsoft.VisualBasic.PowerPacks.DataRepeater>控件。</xref:Microsoft.VisualBasic.PowerPacks.DataRepeater>  
  
4.  在属性窗口中，将更改**名称**属性设置为**SearchButton**。 更改**文本**属性设置为**搜索**。  
  
5.  双击<xref:System.Windows.Forms.Button>控件以打开代码编辑器中，并将添加到下面的代码`SearchButton_Click`事件处理程序。</xref:System.Windows.Forms.Button>  
  
     [!code-cs[VbPowerPacksDataRepeaterWalkthrough&#5;](../../../visual-basic/developing-apps/windows-forms/codesnippet/CSharp/walkthrough-displaying-data-in-a-datarepeater-control-visual-studio_5.cs) ] 
     [!code-vb [VbPowerPacksDataRepeaterWalkthrough&#5;](../../../visual-basic/developing-apps/windows-forms/codesnippet/VisualBasic/walkthrough-displaying-data-in-a-datarepeater-control-visual-studio_5.vb)]  
  
6.  按 F5 运行该应用程序。 键入客户 ID 在**搜索文本框**，然后单击**搜索**按钮。  
  
## <a name="adding-a-master-and-detail-table-to-the-datarepeater"></a>向 DataRepeater 添加主表和详细信息表  
 在此可选步骤中，添加第二个<xref:Microsoft.VisualBasic.PowerPacks.DataRepeater>控件来显示每个客户的相关的订单。</xref:Microsoft.VisualBasic.PowerPacks.DataRepeater>  
  
#### <a name="to-add-a-master-and-detail-table"></a>添加主表和详细信息表的步骤  
  
1.  拖动第二个<xref:Microsoft.VisualBasic.PowerPacks.DataRepeater>控件从**Visual Basic PowerPacks**选项卡中**工具箱**拖到窗体。</xref:Microsoft.VisualBasic.PowerPacks.DataRepeater>  
  
2.  在属性窗口中设置**位置**属性设置为`465, 25`。  
  
3.  设置**大小**属性设置为`315, 600`。  
  
4.  在**数据源**窗口中，展开**客户**表节点，然后选择的详细信息节点**订单**表。  
  
5.  此拖放类型更改**订单**通过单击详细信息表**详细信息**表节点上的下拉列表中。  
  
6.  拖动此**订单**表节点拖动的项模板区域 （上部区域） 的第二个<xref:Microsoft.VisualBasic.PowerPacks.DataRepeater>控件。</xref:Microsoft.VisualBasic.PowerPacks.DataRepeater>  
  
     **Ordersbindingsource**组件和一个**OrdersTableAdapter**组件添加到组件栏。  
  
7.  按 F5 运行该应用程序。 当您在第一个选择每个客户<xref:Microsoft.VisualBasic.PowerPacks.DataRepeater>控制，订单为该客户将显示在第二个<xref:Microsoft.VisualBasic.PowerPacks.DataRepeater>控件。</xref:Microsoft.VisualBasic.PowerPacks.DataRepeater> </xref:Microsoft.VisualBasic.PowerPacks.DataRepeater>  
  
## <a name="see-also"></a>另请参阅  
 [DataRepeater 控件简介](../../../visual-basic/developing-apps/windows-forms/introduction-to-the-datarepeater-control-visual-studio.md)   
 [如何︰ 在 DataRepeater 控件中显示绑定的数据](../../../visual-basic/developing-apps/windows-forms/how-to-display-bound-data-in-a-datarepeater-control-visual-studio.md)   
 [如何︰ 在 DataRepeater 控件中的控件显示未绑定](../../../visual-basic/developing-apps/windows-forms/how-to-display-unbound-controls-in-a-datarepeater-control-visual-studio.md)   
 [如何︰ 更改 DataRepeater 控件的布局](../../../visual-basic/developing-apps/windows-forms/how-to-change-the-layout-of-a-datarepeater-control-visual-studio.md)   
 [如何︰ 在 DataRepeater 控件中显示项标题](../../../visual-basic/developing-apps/windows-forms/how-to-display-item-headers-in-a-datarepeater-control-visual-studio.md)   
 [如何︰ 在 DataRepeater 控件中搜索数据](../../../visual-basic/developing-apps/windows-forms/how-to-search-data-in-a-datarepeater-control-visual-studio.md)   
 [如何︰ 使用两个 DataRepeater 控件 (Visual Studio) 创建母版/详细信息窗体](../../../visual-basic/developing-apps/windows-forms/how-to-create-a-master-detail-form-by-using-two-datarepeater-controls.md)   
 [如何︰ 更改 DataRepeater 控件的外观](../../../visual-basic/developing-apps/windows-forms/how-to-change-the-appearance-of-a-datarepeater-control-visual-studio.md)   
 [如何︰ 禁止添加和删除 DataRepeater 项](../../../visual-basic/developing-apps/windows-forms/how-to-disable-adding-and-deleting-datarepeater-items-visual-studio.md)   
 [DataRepeater 控件疑难解答](../../../visual-basic/developing-apps/windows-forms/troubleshooting-the-datarepeater-control-visual-studio.md)
