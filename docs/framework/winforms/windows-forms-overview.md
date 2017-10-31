---
title: "Windows 窗体概述 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-winforms"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "jsharp"
helpviewer_keywords: 
  - "智能客户端"
  - "Windows 窗体, 关于 Windows 窗体"
ms.assetid: 3a2b6284-c8d6-4e1c-8c69-0bed38f38cd4
caps.latest.revision: 34
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 34
---
# Windows 窗体概述
以下概述介绍了智能客户端应用程序的优点、Windows 窗体编程的主要功能以及可以如何使用 Windows 窗体来构建可满足当今企业和最终用户需求的智能客户端。  
  
## Windows 窗体和智能客户端应用程序  
 可以使用 Windows 窗体开发智能客户端。  *智能客户端*是包含丰富图形的应用程序，可轻松进行部署和更新，无论是否连接到 Internet 均可正常工作，并能以相较于基于 Windows 的传统应用程序更为安全的方式访问本地计算机上的资源。  
  
### 构建丰富的交互式用户界面  
 Windows 窗体是用于 [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)] 的智能客户端技术，是一组简化读取和写入文件系统等常见应用程序任务的托管库。  使用类似于 [!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)] 的开发环境时，可以创建 Windows 窗体智能客户端应用程序，该应用程序可显示信息、请求来自用户的输入以及通过网络和远程计算机通信。  
  
 在 Windows 窗体中，*窗体*是一种可视图面，可在其上对用户显示信息。  通常情况下，通过向窗体添加控件和开发对用户操作（如点击鼠标或按键）的响应来构建 Windows 窗体应用程序。  *控件*是分立的用户界面 \(UI\) 元素，用于显示数据或接受数据输入。  
  
 当用户对你的窗体或一个窗体控件执行了某个操作，该操作将生成一个事件。  你的应用程序通过使用代码对这些事件做出反应，并在事件发生时对其进行处理。  有关详细信息，请参阅[在 Windows 窗体中创建事件处理程序](../../../docs/framework/winforms/creating-event-handlers-in-windows-forms.md)。  
  
 Windows 窗体包含各种可以向窗体添加的控件：显示文本框、按钮、下拉框、单选按钮甚至网页的控件。  有关可在窗体上使用的所有控件的列表，请参阅[在 Windows 窗体上使用的控件](../../../docs/framework/winforms/controls/controls-to-use-on-windows-forms.md)。  如果某个现有控件不满足你的需要，Windows 窗体还支持使用 <xref:System.Windows.Forms.UserControl> 类创建自己的自定义控件。  
  
 Windows 窗体具有丰富的 UI 控件，这些控件可模拟 Microsoft Office 等高端应用程序中的功能。  使用 <xref:System.Windows.Forms.ToolStrip> 和 <xref:System.Windows.Forms.MenuStrip> 控件时，可以创建包含文本和图像的工具栏和菜单、显示子菜单和托管其他控件（如文本框和组合框）。  
  
 借助 [!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)] 拖放 Windows 窗体设计器，可以轻松创建 Windows 窗体应用程序。  只需用光标选中控件，然后将它们添加到窗体中所需的位置即可。  设计器提供诸如网格线和对齐线的工具，以便简化对齐控件的操作。  无论是使用 [!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)] 或在命令行进行编译，均可使用 <xref:System.Windows.Forms.FlowLayoutPanel>、<xref:System.Windows.Forms.TableLayoutPanel> 和 <xref:System.Windows.Forms.SplitContainer> 控件在更短的时间内创建高级窗体布局。  
  
 最后，如果必须创建自己的自定义用户界面元素，<xref:System.Drawing> 命名空间包含各种类，可用以直接在窗体上呈现线条、圆形和其他形状。  
  
> [!NOTE]
>  Windows 窗体控件并未被设计用于跨应用程序域进行封送处理。  因此，Microsoft 不支持跨 <xref:System.AppDomain> 边界传递 Windows 窗体控件，即使 <xref:System.MarshalByRefObject> 的 <xref:System.Windows.Controls.Control> 基类似乎指示这一操作可行。  只要不跨应用程序域边界传递 Windows 窗体控件，就将支持具有多个应用程序域的 Windows 窗体应用程序。  
  
#### 帮助创建窗体和控件  
 如需了解如何使用这些功能的步骤信息，请参阅以下“帮助”主题。  
  
|描述|帮助主题|  
|--------|----------|  
|在窗体上使用控件|[如何：向 Windows 窗体添加控件](../../../docs/framework/winforms/controls/how-to-add-controls-to-windows-forms.md)|  
|使用 <xref:System.Windows.Forms.ToolStrip> 控件|[如何：使用设计器创建含有标准项的基本 ToolStrip](../../../docs/framework/winforms/controls/create-a-basic-wf-toolstrip-with-standard-items-using-the-designer.md)|  
|创建带有 <xref:System.Drawing> 的图形|[图形编程入门](../../../docs/framework/winforms/advanced/getting-started-with-graphics-programming.md)|  
|创建自定义控件|[如何：从 UserControl 类继承](../../../docs/framework/winforms/controls/how-to-inherit-from-the-usercontrol-class.md)|  
  
### 显示和操作数据  
 许多应用程序必须显示数据库、XML 文件、XML Web 服务或其他数据源中的数据。  Windows 窗体提供了一个灵活的控件（名为 <xref:System.Windows.Forms.DataGridView> 控件），用于以传统的行和列格式显示此类表格数据，以便使每段数据块均占据其自己的单元格。  使用 <xref:System.Windows.Forms.DataGridView> 时，可以自定义各个单元格的外观，将任意行和列锁定在所需位置，在单元格内部显示复杂控件，此外还具有其他功能。  
  
 通过网络连接到数据源对于 Windows 窗体智能客户端而言是一个简单的任务。  <xref:System.Windows.Forms.BindingSource> 组件（对于 [!INCLUDE[vsprvslong](../../../includes/vsprvslong-md.md)] 和 [!INCLUDE[dnprdnlong](../../../includes/dnprdnlong-md.md)] 中的 Windows 窗体而言是全新内容）表示与数据源的连接，公开将数据绑定到控件的方法，导航到上一个和下一个记录，编辑记录并且将更改保存到原始源。  <xref:System.Windows.Forms.BindingNavigator> 控件通过 <xref:System.Windows.Forms.BindingSource> 组件提供一个简单界面，可供用户在记录间导航。  
  
 可以使用“数据源”窗口轻松创建数据绑定控件。  窗口显示数据源，如数据库、Web 服务和项目中的对象。  可以通过将此窗口中的项拖动到项目中的窗体上来创建数据绑定控件。  还可以通过将对象从“数据源”窗口拖动到现有控件上来将现有控件与数据进行数据绑定。  
  
 可在 Windows 窗体中管理的另一类数据绑定是*设置*。  大多数智能客户端应用程序均必须保留有关其运行时状态的某些信息（例如窗体的最后已知大小）并保留用户首选项数据（例如保存的文件的默认位置）。  “应用程序设置”功能通过提供一种在客户端计算机上存储两种类型的设置的简单方法来满足这些要求。  通过使用 [!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)] 或代码编辑器定义这些设置后，这些设置便作为 XML保留并自动在运行时读取回内存中。  
  
#### 帮助显示和操作数据  
 如需了解如何使用这些功能的步骤信息，请参阅以下“帮助”主题。  
  
|描述|帮助主题|  
|--------|----------|  
|使用 <xref:System.Windows.Forms.BindingSource> 组件|[如何：使用设计器将 Windows 窗体控件与 BindingSource 组件进行绑定](../../../docs/framework/winforms/controls/bind-wf-controls-with-the-bindingsource.md)|  
|使用 [!INCLUDE[vstecado](../../../includes/vstecado-md.md)] 数据源|[如何：使用 Windows 窗体 BindingSource 组件对 ADO.NET 数据进行排序和筛选](../../../docs/framework/winforms/controls/sort-and-filter-ado-net-data-with-wf-bindingsource-component.md)|  
|使用“数据源”窗口|[演练：在 Windows 窗体上显示数据](../Topic/Walkthrough:%20Displaying%20Data%20on%20a%20Windows%20Form.md)|  
|使用应用程序设置|[如何：创建应用程序设置](../../../docs/framework/winforms/advanced/how-to-create-application-settings.md)|  
  
### 将应用程序部署到客户端计算机  
 编写了应用程序后，必须将应用程序发送给用户，以便他们可以在自己的客户端计算机上安装和运行此应用程序。  使用 [!INCLUDE[ndptecclick](../../../includes/ndptecclick-md.md)] 技术时，只需进行几次点击便可以从 [!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)] 内部署应用程序，然后向用户提供指向 Web 上的应用程序的 URL。  [!INCLUDE[ndptecclick](../../../includes/ndptecclick-md.md)] 管理你的应用程序中的所有元素和依赖项，并确保应用程序正确安装到客户端计算机上。  
  
 [!INCLUDE[ndptecclick](../../../includes/ndptecclick-md.md)] 应用程序可以配置为仅在用户连接到网络时运行，或配置为联机和脱机时均可运行。  如果指定应用程序支持脱机操作，则 [!INCLUDE[ndptecclick](../../../includes/ndptecclick-md.md)] 将在用户的“开始”菜单中添加一个指向应用程序的链接。  然后用户便可以打开应用程序，而无需使用此 URL。  
  
 更新应用程序时，便向你的 Web 服务器发布了一个新的部署清单和应用程序的一个新副本。  [!INCLUDE[ndptecclick](../../../includes/ndptecclick-md.md)] 将检测到有可用更新并将升级用户的安装；更新旧程序集无需进行自定义编程。  
  
#### 帮助部署 ClickOnce 应用程序  
 有关 [!INCLUDE[ndptecclick](../../../includes/ndptecclick-md.md)] 的完整介绍，请参阅 [ClickOnce 安全和部署](../Topic/ClickOnce%20Security%20and%20Deployment.md)。  有关如何使用这些功能的步骤信息，请参阅以下“帮助”主题，  
  
|描述|帮助主题|  
|--------|----------|  
|使用 [!INCLUDE[ndptecclick](../../../includes/ndptecclick-md.md)] 部署应用程序|[如何：使用发布向导发布 ClickOnce 应用程序](../Topic/How%20to:%20Publish%20a%20ClickOnce%20Application%20using%20the%20Publish%20Wizard.md)<br /><br /> [演练：手动部署 ClickOnce 应用程序](../Topic/Walkthrough:%20Manually%20Deploying%20a%20ClickOnce%20Application.md)|  
|更新 [!INCLUDE[ndptecclick](../../../includes/ndptecclick-md.md)] 部署|[如何：管理 ClickOnce 应用程序的更新](../Topic/How%20to:%20Manage%20Updates%20for%20a%20ClickOnce%20Application.md)|  
|使用 [!INCLUDE[ndptecclick](../../../includes/ndptecclick-md.md)] 管理安全性|[如何：启用 ClickOnce 安全设置](../Topic/How%20to:%20Enable%20ClickOnce%20Security%20Settings.md)|  
  
### 其他控件和功能  
 Windows 窗体中有许多其他功能，可帮助快速轻松地实现常见任务，如对创建对话框、打印、添加帮助和文档以及将应用程序本地化为多种语言的支持。  此外，Windows 窗体依赖于 [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)] 的可靠的安全系统。  通过此系统，可以向客户发布更多安全应用程序。  
  
#### 帮助实现其他控件和功能  
 如需了解如何使用这些功能的步骤信息，请参阅以下“帮助”主题。  
  
|描述|帮助主题|  
|--------|----------|  
|打印窗体内容|[如何：在 Windows 窗体中打印图形](../../../docs/framework/winforms/advanced/how-to-print-graphics-in-windows-forms.md)<br /><br /> [如何：打印 Windows 窗体中的多页文本文件](../../../docs/framework/winforms/advanced/how-to-print-a-multi-page-text-file-in-windows-forms.md)|  
|了解有关 Windows 窗体安全的详细信息|[Windows 窗体中的安全性概述](../../../docs/framework/winforms/security-in-windows-forms-overview.md)|  
  
## 请参阅  
 [Windows 窗体入门](../../../docs/framework/winforms/getting-started-with-windows-forms.md)   
 [创建新的 Windows 窗体](../../../docs/framework/winforms/creating-a-new-windows-form.md)   
 [ToolStrip 控件概述](../../../docs/framework/winforms/controls/toolstrip-control-overview-windows-forms.md)   
 [DataGridView 控件概述](../../../docs/framework/winforms/controls/datagridview-control-overview-windows-forms.md)   
 [BindingSource 组件概述](../../../docs/framework/winforms/controls/bindingsource-component-overview.md)   
 [应用程序设置概述](../../../docs/framework/winforms/advanced/application-settings-overview.md)   
 [ClickOnce 安全和部署](../Topic/ClickOnce%20Security%20and%20Deployment.md)