---
title: "Windows 窗体应用程序基础知识 (Visual Basic 中) |Microsoft 文档"
ms.date: 2015-07-20
ms.prod: .net
ms.suite: 
ms.technology:
- devlang-visual-basic
ms.topic: article
dev_langs:
- VB
helpviewer_keywords:
- Windows applications
- Windows Forms, Visual Basic
ms.assetid: 0b919d30-7fd6-42db-85c8-543d15312441
caps.latest.revision: 20
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
ms.openlocfilehash: 8275d3c06ebd89254a07127b4850d32ef0580830
ms.lasthandoff: 03/13/2017

---
# <a name="windows-forms-application-basics-visual-basic"></a>Windows 窗体应用程序基础知识 (Visual Basic)
一个重要部分[!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)]是能够创建在用户的计算机本地运行的 Windows 窗体应用程序。 Visual Studio 可用于创建使用 Windows 窗体的应用程序和用户界面。 Windows 窗体应用程序基于从类<xref:System.Windows.Forms>命名空间。</xref:System.Windows.Forms>  
  
## <a name="designing-windows-forms-applications"></a>设计 Windows 窗体应用程序  
 您可以创建 Windows 窗体和 Windows 服务应用程序与[!INCLUDE[vsprvs](../../../csharp/includes/vsprvs_md.md)]。 有关详细信息，请参阅下列主题：  
  
-   [Windows 窗体入门](https://msdn.microsoft.com/library/ms229601.aspx)。 提供有关如何创建和编写 Windows 窗体信息。  
   
-   [Windows 窗体控件](https://msdn.microsoft.com/library/ettb6e2a.aspx)。 主题详细介绍使用 Windows 窗体控件的集合。  
  
-   [Windows 服务应用程序](https://msdn.microsoft.com/library/y817hyb6.aspx)。 列出了这些主题介绍如何创建 Windows 服务。  
  
## <a name="building-rich-interactive-user-interfaces"></a>构建丰富的交互式用户界面  
 Windows 窗体是智能客户端的组件[!INCLUDE[dnprdnshort](../../../csharp/getting-started/includes/dnprdnshort_md.md)]，一组托管库，可用来读取和写入文件系统等常见应用程序任务。 使用类似的开发环境[!INCLUDE[vsprvs](../../../csharp/includes/vsprvs_md.md)]，您可以通过网络与远程计算机创建 Windows 窗体应用程序显示信息、 请求来自用户的输入以及进行通信。  
  
 Windows 窗体在窗体是向用户的信息显示在其一个可视化图面。 您通常通过窗体上放置控件并开发对用户操作，如鼠标单击或按键响应来构建 Windows 窗体应用程序。 一个*控件*是用于显示数据或接受数据输入的分立的用户界面 (UI) 元素。  
  
### <a name="events"></a>事件  
 当用户对你的窗体或它的某个控件，则会生成一个事件。 你的应用程序通过使用代码对这些事件做出反应，并在事件发生时对其进行处理。 有关详细信息，请参阅[Windows 窗体中创建事件处理程序](https://msdn.microsoft.com/library/dacysss4.aspx)。  
  
### <a name="controls"></a>控件  
 Windows 窗体包含各种可以放置在窗体的控件︰ 显示文本框、 按钮、 下拉列表框、 单选按钮和甚至网页的控件。 可以在窗体使用的所有控件的列表，请参阅[Windows 窗体上使用的控件](https://msdn.microsoft.com/library/3xdhey7w.aspx)。 如果现有控件不满足您的需要，Windows 窗体还支持创建自定义控件使用<xref:System.Windows.Forms.UserControl>类。</xref:System.Windows.Forms.UserControl>  
  
 Windows 窗体具有丰富的 UI 控件，这些控件可模拟 Microsoft Office 等高端应用程序中的功能。 使用<xref:System.Windows.Forms.ToolStrip>和<xref:System.Windows.Forms.MenuStrip>控件，可以创建工具栏和菜单包含文本和图像、 显示子菜单和托管其他控件如文本框和组合框。</xref:System.Windows.Forms.MenuStrip> </xref:System.Windows.Forms.ToolStrip>  
  
 与[!INCLUDE[vsprvs](../../../csharp/includes/vsprvs_md.md)]拖放窗体设计器中，可以轻松创建 Windows 窗体应用程序︰ 只需用光标选中控件，并将它们放置在要在窗体上。 设计器提供诸如网格线和"捕捉线"工具，以便简化对齐控件。 无论是使用[!INCLUDE[vsprvs](../../../csharp/includes/vsprvs_md.md)]或编译在命令行中，您可以使用<xref:System.Windows.Forms.FlowLayoutPanel>，<xref:System.Windows.Forms.TableLayoutPanel>和<xref:System.Windows.Forms.SplitContainer>控件来创建高级窗体布局的最小时间和精力。</xref:System.Windows.Forms.SplitContainer> </xref:System.Windows.Forms.TableLayoutPanel> </xref:System.Windows.Forms.FlowLayoutPanel>  
  
### <a name="custom-ui-elements"></a>自定义用户界面元素  
 最后，如果必须创建自己的自定义用户界面元素，<xref:System.Drawing>命名空间包含的所有类需要呈现线条、 圆形和其他形状直接在窗体上的。</xref:System.Drawing>  
  
 有关使用这些功能的分步信息，请参阅以下帮助主题。  
  
|到|请参阅|  
|--------|---------|  
|创建与新的 Windows 窗体应用程序[!INCLUDE[vsprvs](../../../csharp/includes/vsprvs_md.md)]|[演练︰ 创建简单的 Windows 窗体](http://msdn.microsoft.com/en-us/2d9daec0-0543-41d0-acb1-964f685bddbb)|  
|使用窗体上控件|[如何︰ 向 Windows 窗体添加控件](https://msdn.microsoft.com/library/0h5y8567.aspx)|   
|创建带有图形<xref:System.Drawing></xref:System.Drawing>|[图形编程入门](https://msdn.microsoft.com/library/da0f23z7.aspx)|  
|创建自定义控件|[如何︰ 从 UserControl 类继承](https://msdn.microsoft.com/library/00ctb4z0.aspx)|  
  
## <a name="displaying-and-manipulating-data"></a>显示和操作数据  
 许多应用程序必须显示数据库、XML 文件、XML Web 服务或其他数据源中的数据。 Windows 窗体提供了一个灵活的控件，调用<xref:System.Windows.Forms.DataGridView>用于呈现在传统的行和列的格式，此类表格数据，以便使每个数据块均占据其自己的单元格的控件。</xref:System.Windows.Forms.DataGridView> 使用<xref:System.Windows.Forms.DataGridView>可以自定义各个单元格的外观、 锁定任意行和列中的位置，并显示在单元格，此外还具有其他功能内的复杂控件。</xref:System.Windows.Forms.DataGridView>  
  
 通过网络连接到数据源对于 Windows 窗体智能客户端而言是一个简单的任务。 <xref:System.Windows.Forms.BindingSource>组件，在 Windows Forms 的新增[!INCLUDE[vsprvslong](../../../csharp/misc/includes/vsprvslong_md.md)]和[!INCLUDE[dnprdnlong](../../../csharp/programming-guide/events/includes/dnprdnlong_md.md)]、 表示到数据源的连接和公开数据绑定到控件，导航到上一页和下一页记录，编辑记录并且将更改保存回原始数据源的方法。</xref:System.Windows.Forms.BindingSource> <xref:System.Windows.Forms.BindingNavigator>控件提供了一个简单的界面，通过<xref:System.Windows.Forms.BindingSource>组件可以对用户在记录间导航。</xref:System.Windows.Forms.BindingSource> </xref:System.Windows.Forms.BindingNavigator>  
  
### <a name="data-bound-controls"></a>数据绑定控件  
 您可以创建数据绑定控件轻松地使用数据源窗口，其中显示您项目中的数据源，例如数据库、 Web 服务和对象。 可以通过将此窗口中的项拖动到项目中的窗体上来创建数据绑定控件。 还可以通过将对象从“数据源”窗口拖动到现有控件上来将现有控件与数据进行数据绑定。  
  
### <a name="settings"></a>设置  
 您可以管理在 Windows 窗体数据绑定的另一种是设置。 大多数智能客户端应用程序必须保留有关其运行时状态，如窗体的最后已知大小的一些信息，并保留用户首选项数据，例如保存的文件的默认位置。 应用程序设置功能通过提供一种简单的方法来将这两种类型的设置存储在客户端计算机上满足这些要求。 一旦定义使用[!INCLUDE[vsprvs](../../../csharp/includes/vsprvs_md.md)]或代码编辑器中，这些设置便作为 XML 保留并自动在运行时读取回内存。  
  
 有关使用这些功能的分步信息，请参阅以下帮助主题。  
  
|到|请参阅|  
|--------|---------|  
|使用<xref:System.Windows.Forms.BindingSource>组件</xref:System.Windows.Forms.BindingSource>|[如何︰ 将 Windows 窗体控件与 BindingSource 组件使用设计器绑定](https://msdn.microsoft.com/library/801dxw2t.aspx)|  
|使用[!INCLUDE[vstecado](../../../csharp/programming-guide/concepts/linq/includes/vstecado_md.md)]数据源|[如何︰ 进行排序和筛选 ADO.NET 数据使用 Windows 窗体 BindingSource 组件](https://msdn.microsoft.com/library/ya3sah92.aspx)|  
|使用数据源窗口|[演练：在 Windows 窗体上显示数据](https://docs.microsoft.com/visualstudio/data-tools/accessing-data-in-visual-studio)|  
  
## <a name="deploying-applications-to-client-computers"></a>将应用程序部署到客户端计算机  
 一旦您已经编写您的应用程序，以便他们可以安装并在他们自己的客户端计算机上运行该必须将它发送给您的用户。 使用[!INCLUDE[ndptecclick](../../../visual-basic/developing-apps/printing/includes/ndptecclick_md.md)]技术，您可以部署应用程序内的[!INCLUDE[vsprvs](../../../csharp/includes/vsprvs_md.md)]，只需进行几次点击并向用户提供指向 Web 上的应用程序的 URL。 [!INCLUDE[ndptecclick](../../../visual-basic/developing-apps/printing/includes/ndptecclick_md.md)]管理的所有元素和您的应用程序中的依赖关系并确保客户端计算机上正确安装应用程序。  
  
 [!INCLUDE[ndptecclick](../../../visual-basic/developing-apps/printing/includes/ndptecclick_md.md)] 应用程序可以配置为仅在用户连接到网络时运行，或配置为联机和脱机时均可运行。 如果指定应用程序应支持脱机操作，[!INCLUDE[ndptecclick](../../../visual-basic/developing-apps/printing/includes/ndptecclick_md.md)]将链接添加到您的应用程序在用户的**启动**菜单上，以便用户可以打开它而使用的 URL。  
  
 更新应用程序时，便向你的 Web 服务器发布了一个新的部署清单和应用程序的一个新副本。 [!INCLUDE[ndptecclick](../../../visual-basic/developing-apps/printing/includes/ndptecclick_md.md)]检测到那里可用更新，并将升级用户的安装;无需任何自定义编程需要更新旧程序集。  
  
 有关的完整介绍[!INCLUDE[ndptecclick](../../../visual-basic/developing-apps/printing/includes/ndptecclick_md.md)]，请参阅[ClickOnce 安全和部署](https://docs.microsoft.com/visualstudio/deployment/clickonce-security-and-deployment)。 有关使用这些功能的分步信息，请参阅以下帮助主题︰  
  
|到|请参阅|  
|--------|---------|  
|部署的应用程序[!INCLUDE[ndptecclick](../../../visual-basic/developing-apps/printing/includes/ndptecclick_md.md)]|[如何：使用发布向导发布 ClickOnce 应用程序](https://docs.microsoft.com/visualstudio/deployment/how-to-publish-a-clickonce-application-using-the-publish-wizard)<br /><br /> [演练：手动部署 ClickOnce 应用程序](https://docs.microsoft.com/visualstudio/deployment/walkthrough-manually-deploying-a-clickonce-application)|  
|更新[!INCLUDE[ndptecclick](../../../visual-basic/developing-apps/printing/includes/ndptecclick_md.md)]部署|[如何：管理 ClickOnce 应用程序的更新](https://docs.microsoft.com/visualstudio/deployment/how-to-manage-updates-for-a-clickonce-application)|  
|管理与安全[!INCLUDE[ndptecclick](../../../visual-basic/developing-apps/printing/includes/ndptecclick_md.md)]|[如何：启用 ClickOnce 安全设置](https://docs.microsoft.com/visualstudio/deployment/how-to-enable-clickonce-security-settings)|  
  
## <a name="other-controls-and-features"></a>其他控件和功能  
 Windows 窗体中有许多其他功能，可帮助快速轻松地实现常见任务，如对创建对话框、打印、添加帮助和文档以及将应用程序本地化为多种语言的支持。 此外，Windows 窗体依赖的可靠安全系统[!INCLUDE[dnprdnshort](../../../csharp/getting-started/includes/dnprdnshort_md.md)]，使您能够发布到您的客户更安全的应用程序。  
  
 有关使用这些功能的分步信息，请参阅以下帮助主题︰  
  
|到|请参阅|  
|--------|---------|  
|打印窗体的内容|[如何︰ 在 Windows 窗体中打印图形](https://msdn.microsoft.com/library/741a0ktc.aspx)<br /><br /> [如何︰ 打印 Windows 窗体中的多页文本文件](https://msdn.microsoft.com/library/cwbe712d.aspx)|   
|了解有关 Windows 窗体安全的详细信息|[Windows 窗体概述中的安全性](https://msdn.microsoft.com/library/90k49ccb.aspx)|  
  
## <a name="see-also"></a>另请参阅  
 <xref:Microsoft.VisualBasic.ApplicationServices.WindowsFormsApplicationBase></xref:Microsoft.VisualBasic.ApplicationServices.WindowsFormsApplicationBase>   
 [Windows 窗体概述](https://msdn.microsoft.com/library/8bxxy49h.aspx)   
 [My.Forms 对象](../../../visual-basic/language-reference/objects/my-forms-object.md)
