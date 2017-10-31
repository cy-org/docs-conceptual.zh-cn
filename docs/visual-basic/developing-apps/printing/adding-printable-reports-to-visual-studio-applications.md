---
title: "将可打印的报表添加到 Visual Studio 应用程序 | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "打印 [Visual Studio], 报告"
  - "报告, Visual Studio 中的打印"
ms.assetid: 93928405-ef41-495e-bce2-9d43d5a7080a
caps.latest.revision: 27
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 27
---
# 将可打印的报表添加到 Visual Studio 应用程序
[!INCLUDE[vs2017banner](../../../visual-basic/includes/vs2017banner.md)]

Visual Studio 支持各种报告解决方案，可以帮助您向 Visual Basic 应用程序中添加丰富的数据报告功能。  可以使用 ReportViewer 控件、Crystal Reports 或 SQL Server Reporting Services 来创建和添加报告。  
  
> [!NOTE]
>  SQL Server Reporting Services 是 SQL Server 2005 的一部分，而不是 Visual Studio 的一部分。  除非您已经安装了 SQL Server 2005，否则您的系统上不会安装有 Reporting Services。  
  
## Visual Basic 应用程序中 Microsoft 报告技术的概述  
 从以下方法中进行选择以在应用程序中使用 Microsoft 报告技术：  
  
-   向 Visual Basic Windows 应用程序中添加 ReportViewer 控件的一个或多个实例。  
  
-   通过调用 Report Server Web 服务，从而以编程方式集成 SQL Server Reporting Services。  
  
-   通过将 ReportViewer 控件作为报告查看器，将报告服务器作为报告处理器，从而将 ReportViewer 控件与 Microsoft SQL Server 2005 Reporting Services 一起使用。  （请注意，如果希望将报告服务器和 ReportViewer 控件一起使用，您必须使用 SQL Server 2005 版的 Reporting Services。）  
  
## 使用 ReportViewer 控件  
 将报告功能嵌入 Visual Basic Windows 应用程序的最简便方法就是向应用程序的窗体中添加 ReportViewer 控件。  该控件将直接向应用程序中添加报告处理功能，并提供一个集成报表设计器，因此可以使用来自任何 ADO.NET 数据对象的数据生成报告。  系统包含一个全功能 API，该 API 提供对该控件和报告的编程访问，以便配置运行时功能。  
  
 ReportViewer 在可任意发行的单个数据控件中提供了内置的报告处理和查看功能。  如果需要以下报告功能，请选择使用 ReportViewer 控件：  
  
-   客户端应用程序中的报告处理。  将在该控件提供的视图区域显示经过处理的报告。  
  
-   数据绑定到 ADO.NET 数据表。  可以创建使用为该控件提供的 <xref:System.Data.DataTable> 实例的报告。  还可以直接绑定到业务对象。  
  
-   可以包含在应用程序中的可再发行控件。  
  
-   页导航、打印、搜索和导出格式等运行时功能。  ReportViewer 工具栏提供对这些操作的支持。  
  
 若要使用 ReportViewer 控件，可以将其从 Visual Studio 工具箱的**“数据”**节拖动到 Visual Basic Windows 应用程序中的窗体上。  
  
### 在 Visual Studio 中创建供 ReportViewer 控件使用的报告  
 若要生成在 ReportViewer 中运行的报告，请向您的项目中添加一个**“报告”**模板。  Visual Studio 将创建一个客户端报告定义文件 \(.rdlc\)，并将该文件添加到项目中，然后在 Visual Studio 工作区中打开集成的报表设计器。  
  
 Visual Studio 报表设计器与**“数据源”**窗口相集成。  将某个字段从**“数据源”**窗口拖动到报告中时，报表设计器会将有关数据源的元数据复制到报告定义文件中。  ReportViewer 控件使用此元数据来自动生成数据绑定代码。  
  
 Visual Studio 报表设计器不包含报告预览功能。  若要预览报告，请运行应用程序，然后预览其中嵌入的报告。  
  
||  
|-|  
|向应用程序中添加基本报告功能|  
|1.  从**“工具箱”**的**“数据”**选项卡中将 ReportViewer 控件拖动到窗体上。<br />2.  在**“项目”**菜单上选择**“添加新项”**。  在**“添加新项”**对话框中选择**“报告”**图标，然后单击**“添加”**。<br />     将在开发环境中打开报表设计器，并将报告定义 \(.rdlc\) 文件添加到项目中。<br />3.  从**“工具箱”**中将报告项拖动到报告布局上，并根据需要排列报告项。<br />4.  将字段从**“数据源”**窗口中拖动到报告布局中的报告项。|  
  
## 在 Visual Basic 应用程序中使用 Reporting Services  
 Reporting Services 是一项基于服务器的报告技术，该技术包括在 SQL Server 中。  Reporting Services 包含 ReportViewer 控件中所没有的附加功能。  如果需要以下任何功能，请选择 Reporting Services：  
  
-   扩展部署和服务器端报告处理，可提高复杂报告或长时间运行的报告以及大量报告活动的性能。  
  
-   集成的数据和报告处理，并支持自定义报告控件和丰富的呈现输出格式。  
  
-   计划的报告处理，以便能够精确指定报告运行时间。  
  
-   通过电子邮件或向文件共享位置分发的基于订户的报告。  
  
-   临时报告，以便业务用户可以根据需要创建报告。  
  
-   数据驱动的订阅，以将自定义报告输出路由至动态的收件人列表。  
  
-   用于数据处理、报告传递、自定义身份验证以及报告呈现的自定义扩展。  
  
 报告服务器作为 Web 服务实现。  应用程序代码中必须包含对该 Web 服务的调用才能访问报告和其他元数据。  该 Web 服务提供对报告服务器实例的完全编程访问。  
  
 由于 Reporting Services 是一项基于 Web 的报告技术，因此默认查看器将显示以 HTML 格式呈现的报告。  如果不想使用 HTML 作为默认的报告呈现格式，则必须为应用程序编写一个自定义报告查看器。  
  
### 在 Visual Studio 中创建用于 Reporting Services 的报告  
 若要生成在报告服务器上运行的报告，请在 Visual Studio 中使用 Business Intelligence Development Studio 创建报告定义 \(.rdl\) 文件，Business Intelligence Development Studio 包含在 SQL Server 2005 中。  
  
> [!NOTE]
>  必须安装 SQL Server 2005 才能使用 SQL Server Reporting Services 和 Business Intelligence Development Studio。  
  
 Business Intelligence Development Studio 将添加特定于 SQL Server 组件的项目模板。  若要创建报告，可以选择**“报表服务器项目”**或**“报表服务器项目向导”**模板。  可以将数据源连接与查询指定为各种数据源类型，包括 SQL Server、Oracle、Analysis Services、XML 和 SQL Server Integration Services。  通过使用**“数据”**选项卡、**“布局”**选项卡和**“预览”**选项卡，可以在同一个工作区中定义数据、创建报告布局和预览报告。  
  
 为该控件或报表服务器生成的报告定义可以在这两项技术中的任意一项技术中重用。  
  
||  
|-|  
|创建在报表服务器上运行的报告|  
|1.  在**“文件”**菜单上选择**“新建”**。<br />     将打开**“新建项目”**对话框。<br />2.  在**“项目类型”**窗格中单击**“Business Intelligence 项目”**。<br />3.  在“模板”窗格中选择**“报表服务器项目”**或**“报表服务器项目向导”**。|  
  
## 将 ReportViewer 控件和 SQL Server Reporting Services 一起使用  
 可以在同一应用程序中将 ReportViewer 控件和 SQL Server 2005 报表服务一起使用。  
  
-   ReportViewer 控件提供一个查看器，可用来在应用程序中显示报表。  
  
-   报表服务提供报表，并在远程服务器上执行所有处理操作。  
  
 可将 ReportViewer 控件配置为显示在远程报表服务器上存储和处理的报表。  这种类型的配置称为“远程处理模式”。  在远程处理模式中，该控件将请求存储在远程报表服务器上的报表。  报表服务器会执行所有报表处理、数据处理及报表呈现工作。  将向控件返回一个处理完且已呈现的报表，并在视图区域中显示此报表。  
  
 在报表服务器上运行的报表支持其他导出格式，具有不同的报表参数化实现，使用该报表服务器所支持的数据源类型，并可在报表服务器上通过基于角色的授权模型进行访问。  
  
 若要使用远程处理模式，请在配置 ReportViewer 控件时指定服务器报表的 URL 和路径。