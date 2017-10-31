---
title: "WPF 外接程序概述 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-wpf"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - ".NET Framework 外接程序模型 [WPF]"
  - "外接程序 [WPF], 体系结构"
  - "外接程序 [WPF], 优点"
  - "外接程序 [WPF], 限制"
  - "外接程序 [WPF], 性能"
  - "外接程序 [WPF], 用户界面"
  - "外接程序和用户界面 [WPF]"
  - "外接程序和 XAML 浏览器应用程序 [WPF]"
  - "外接程序概述 [WPF]"
ms.assetid: 00b4c776-29a8-4dba-b603-280a0cdc2ade
caps.latest.revision: 36
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 35
---
# WPF 外接程序概述
<a name="Introduction"></a> [!INCLUDE[dnprdnshort](../../../../includes/dnprdnshort-md.md)] 提供了一个外接程序模型，开发人员可以用它来创建支持外接程序扩展的应用程序。  使用此外接程序模型可以创建与应用程序功能集成并对应用程序功能进行扩展的外接程序。  在某些情况下，应用程序还需要显示外接程序所提供的 [!INCLUDE[TLA2#tla_ui#plural](../../../../includes/tla2sharptla-uisharpplural-md.md)]。  本主题演示 [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] 如何扩展 [!INCLUDE[dnprdnshort](../../../../includes/dnprdnshort-md.md)] 外接程序模型从而实现这些方案，演示 WPF 的体系结构、其优点及其局限。  
  
   
  
<a name="Requirements"></a>   
## 必备组件  
 必须熟悉 [!INCLUDE[dnprdnshort](../../../../includes/dnprdnshort-md.md)] 外接程序模型。  有关更多信息，请参见[外接程序和扩展性](../../../../ml/index.xml)。  
  
<a name="AddInsOverview"></a>   
## 外接程序概述  
 为了在应用程序中引入新功能，需要对其进行重新编译和重新部署。为避免这些复杂过程，应用程序实现了扩展机制，使开发人员（包括第一方和第三方）能够创建与应用程序集成的其他应用程序。  要支持这种扩展，最常用的方法是使用外接程序（也称为“加载项”和“插件”）。  通过外接程序公开扩展性的实际应用程序示例包括：  
  
-   Internet Explorer 加载项。  
  
-   Windows Media Player 插件。  
  
-   Visual Studio 外接程序。  
  
 例如，通过 Windows Media Player 外接程序模型，第三方开发人员可以实现“插件”，从而以各种方式对 Windows Media Player 进行扩展，包括为 Windows Media Player 本身不支持的媒体格式（例如 DVD、MP3）创建解码器和编码器，扩展音频效果和外观。  尽管有一些实体和行为是所有外接程序模型共有的，但生成的每个外接程序模型都是为了公开某个应用程序的特有功能。  
  
 典型外接程序扩展解决方案的三大要素是“协定”、“外接程序”和“宿主应用程序”。  协定定义了外接程序与宿主应用程序之间的两种集成方式：  
  
-   外接程序集成宿主应用程序所实现的功能。  
  
-   宿主应用程序公开供外接程序集成的功能。  
  
 要使外接程序能发挥作用，宿主应用程序需要在运行时找到并加载它们。  因此，支持外接程序的应用程序需要额外执行以下操作：  
  
-   **发现**：查找遵循宿主应用程序所支持的协定的外接程序。  
  
-   **激活**：加载、运行外接程序并与之建立通信。  
  
-   **隔离**：使用应用程序域或进程建立隔离边界，避免外接程序的潜在安全问题和执行问题对应用程序造成影响。  
  
-   **通信**：通过调用方法和传递数据，允许外接程序和宿主应用程序跨过隔离边界相互通信。  
  
-   **生存期管理**：以可预测的干净方式加载和卸载应用程序域和进程（请参见[应用程序域](../../../../docs/framework/app-domains/application-domains.md)）。  
  
-   **版本管理**：确保在创建宿主应用程序或外接程序的新版本后，它们仍可进行通信。  
  
 总之，开发一个可靠的外接程序模型不是一项简单的任务。  为此，[!INCLUDE[dnprdnshort](../../../../includes/dnprdnshort-md.md)] 提供了一种用于生成外接程序模型的基础结构。  
  
> [!NOTE]
>  有关外接程序的详尽信息，请参见[外接程序和扩展性](../../../../ml/index.xml)。  
  
<a name="NETFrameworkAddInModelOverview"></a>   
## .NET Framework 外接程序模型概述  
 [!INCLUDE[dnprdnshort](../../../../includes/dnprdnshort-md.md)] 外接程序模型在 <xref:System.AddIn> 命名空间中，它包含一组类型，旨在简化外接程序扩展的开发过程。  [!INCLUDE[dnprdnshort](../../../../includes/dnprdnshort-md.md)] 外接程序模型的基本单元是“协定”，它定义宿主应用程序与外接程序之间的通信方式。  协定向宿主应用程序公开特定于宿主应用程序的协定视图。  同样，向外接程序公开的是特定于外接程序的协定视图。  通过适配器，宿主应用程序和外接程序可以在它们各自的协定视图之间进行通信。  协定、视图和适配器称为管线段，一组相关的管线段组成一条“管线”。  在管线的基础上，[!INCLUDE[dnprdnshort](../../../../includes/dnprdnshort-md.md)] 外接程序模型才能支持发现、激活、安全隔离、执行隔离（同时使用应用程序域和进程）、通信、生存期管理和版本管理。  
  
 所有这些支持使得开发人员能够生成与宿主应用程序的功能相集成的外接程序。  但是，某些情况下，宿主应用程序需要显示外接程序所提供的 [!INCLUDE[TLA2#tla_ui#plural](../../../../includes/tla2sharptla-uisharpplural-md.md)]。  由于 [!INCLUDE[dnprdnshort](../../../../includes/dnprdnshort-md.md)] 中的每种显示方式都有自己的 [!INCLUDE[TLA2#tla_ui#plural](../../../../includes/tla2sharptla-uisharpplural-md.md)] 实现模型，因此 [!INCLUDE[dnprdnshort](../../../../includes/dnprdnshort-md.md)] 外接程序模型不支持任何特定的显示方式。  而是由 [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] 对 [!INCLUDE[dnprdnshort](../../../../includes/dnprdnshort-md.md)] 外接程序模型进行扩展，支持外接程序的 [!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)]。  
  
<a name="WPFAddInModel"></a>   
## WPF 外接程序  
 [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] 与 [!INCLUDE[dnprdnshort](../../../../includes/dnprdnshort-md.md)] 外接程序模型相结合，能够实现多种要求宿主应用程序显示外接程序 [!INCLUDE[TLA2#tla_ui#plural](../../../../includes/tla2sharptla-uisharpplural-md.md)] 的方案。  具体说来，这些方案由 [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] 使用以下两种编程模型实现：  
  
1.  **外接程序返回用户界面**。  外接程序按照协定的定义，通过方法调用将 [!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)] 返回给宿主应用程序。  此方案可用于以下情况：  
  
    -   外接程序返回的 [!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)] 的外观依赖于仅在运行时存在的数据或条件，例如动态生成的报告。  
  
    -   外接程序提供的服务 [!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)] 不同于可以使用此外接程序的宿主应用程序 [!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)]。  
  
    -   外接程序主要为宿主应用程序执行某项服务，并通过 [!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)] 向宿主应用程序报告状态。  
  
2.  **外接程序为用户界面**。  如协定所定义的那样，外接程序是一个 [!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)]。  此方案可用于以下情况：  
  
    -   凡外接程序提供的服务都需要显示，例如广告。  
  
    -   外接程序提供的服务 [!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)] 由可以使用该外接程序的所有宿主应用程序（如计算器或颜色选取器）共用。  
  
 这些方案要求 [!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)] 对象可以在宿主应用程序和外接应用程序域之间传递。  由于 [!INCLUDE[dnprdnshort](../../../../includes/dnprdnshort-md.md)] 外接程序模型依靠远程处理在应用程序域之间进行通信，所以在应用程序域之间传递的对象必须是可远程处理的。  
  
 可远程处理的对象是一个类的实例，执行下面的一个或多个任务：  
  
-   从 <xref:System.MarshalByRefObject> 类派生。  
  
-   实现 <xref:System.Runtime.Serialization.ISerializable> 接口。  
  
-   应用 <xref:System.SerializableAttribute> 特性。  
  
> [!NOTE]
>  有关创建可远程处理的 [!INCLUDE[dnprdnshort](../../../../includes/dnprdnshort-md.md)] 对象的更多信息，请参见[Making Objects Remotable](http://msdn.microsoft.com/zh-cn/01197253-3f13-43b7-894d-9683e431192a)。  
  
 [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] [!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)] 类型不可远程处理。  为解决此问题，[!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] 扩展了 [!INCLUDE[dnprdnshort](../../../../includes/dnprdnshort-md.md)] 外接程序模型，允许从宿主应用程序显示外接程序创建的 [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] [!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)]。  这种支持由 [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] 通过两种类型提供：<xref:System.AddIn.Contract.INativeHandleContract> 接口和由 <xref:System.AddIn.Pipeline.FrameworkElementAdapters> 类实现的两个静态方法：<xref:System.AddIn.Pipeline.FrameworkElementAdapters.ContractToViewAdapter%2A> 和 <xref:System.AddIn.Pipeline.FrameworkElementAdapters.ViewToContractAdapter%2A>。  在上层，这些类型和方法的用法如下：  
  
1.  [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] 要求由外接程序提供的 [!INCLUDE[TLA2#tla_ui#plural](../../../../includes/tla2sharptla-uisharpplural-md.md)] 是直接或间接从 <xref:System.Windows.FrameworkElement>（如形状、控件、用户控件、布局面板和页面）派生的类。  
  
2.  无论协定在何处声明在外接程序和宿主应用程序之间传递 UI，都必须将 UI 声明为 <xref:System.AddIn.Contract.INativeHandleContract>（而不是 <xref:System.Windows.FrameworkElement>）；<xref:System.AddIn.Contract.INativeHandleContract> 是可以越过隔离边界传递的外接程序 [!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)] 的可远程处理表示形式。  
  
3.  在从外接应用程序域传递之前，通过调用 <xref:System.AddIn.Pipeline.FrameworkElementAdapters.ViewToContractAdapter%2A> 将 <xref:System.Windows.FrameworkElement> 打包为 <xref:System.AddIn.Contract.INativeHandleContract>。  
  
4.  在传递到宿主应用程序的应用程序域之后，必须通过调用 <xref:System.AddIn.Pipeline.FrameworkElementAdapters.ContractToViewAdapter%2A> 将 <xref:System.AddIn.Contract.INativeHandleContract> 重新打包为 <xref:System.Windows.FrameworkElement>。  
  
 <xref:System.AddIn.Contract.INativeHandleContract>、<xref:System.AddIn.Pipeline.FrameworkElementAdapters.ContractToViewAdapter%2A> 和 <xref:System.AddIn.Pipeline.FrameworkElementAdapters.ViewToContractAdapter%2A> 的用法取决于具体情况。  下面几节介绍每个编程模型的详细信息。  
  
<a name="ReturnUIFromAddInContract"></a>   
## 外接程序返回用户界面  
 若要使外接程序向宿主应用程序返回 [!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)]，需要满足以下要求：  
  
1.  必须按照 [!INCLUDE[dnprdnshort](../../../../includes/dnprdnshort-md.md)] [外接程序和扩展性](../../../../ml/index.xml) 文档的描述，创建宿主应用程序、外接程序和管线。  
  
2.  协定必须实现 <xref:System.AddIn.Contract.IContract>，并且为了返回 [!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)]，协定必须使用 <xref:System.AddIn.Contract.INativeHandleContract> 类型的返回值声明方法。  
  
3.  在外接程序和宿主应用程序之间传递的 [!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)] 必须直接或间接从 <xref:System.Windows.FrameworkElement> 派生。  
  
4.  外接程序返回的 [!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)] 在越过隔离边界之前必须从 <xref:System.Windows.FrameworkElement> 转换为 <xref:System.AddIn.Contract.INativeHandleContract>。  
  
5.  返回的 [!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)] 在越过隔离边界之后必须从 <xref:System.AddIn.Contract.INativeHandleContract> 转换为 <xref:System.Windows.FrameworkElement>。  
  
6.  宿主应用程序显示返回的 <xref:System.Windows.FrameworkElement>。  
  
 有关演示如何实现返回 [!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)] 的外接程序的示例，请参见[创建返回 UI 的外接程序](../../../../docs/framework/wpf/app-development/how-to-create-an-add-in-that-returns-a-ui.md)。  
  
<a name="AddInIsAUI"></a>   
## 外接程序为用户界面  
 当外接程序为 [!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)] 时，必须满足以下要求：  
  
1.  必须按照 [!INCLUDE[dnprdnshort](../../../../includes/dnprdnshort-md.md)] [外接程序和扩展性](../../../../ml/index.xml) 文档的描述，创建宿主应用程序、外接程序和管线。  
  
2.  外接程序的协定接口必须实现 <xref:System.AddIn.Contract.INativeHandleContract>。  
  
3.  传递到宿主应用程序的外接程序必须直接或间接从 <xref:System.Windows.FrameworkElement> 派生。  
  
4.  在越过隔离边界之前，必须将外接程序从 <xref:System.Windows.FrameworkElement> 转换为 <xref:System.AddIn.Contract.INativeHandleContract>。  
  
5.  在越过隔离边界之后，必须将外接程序从 <xref:System.AddIn.Contract.INativeHandleContract> 转换为 <xref:System.Windows.FrameworkElement>。  
  
6.  宿主应用程序显示返回的 <xref:System.Windows.FrameworkElement>。  
  
 有关演示如何实现作为 [!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)] 的外接程序的示例，请参见[创建作为 UI 的外接程序](../../../../docs/framework/wpf/app-development/how-to-create-an-add-in-that-is-a-ui.md)。  
  
<a name="ReturningMultipleUIsFromAnAddIn"></a>   
## 从一个外接程序返回多个用户界面  
 外接程序通常提供多个 [!INCLUDE[TLA2#tla_ui#plural](../../../../includes/tla2sharptla-uisharpplural-md.md)] 供宿主应用程序进行显示。  例如，考虑一个作为 [!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)] 的外接程序，它同时还向宿主应用程序（也是一个 [!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)]）提供状态信息。  像这样的外接程序可以通过结合使用[外接程序返回用户界面](#ReturnUIFromAddInContract)和[外接程序为用户界面](#AddInIsAUI)两种模型中的技术来实现。  
  
<a name="AddInsAndXBAPs"></a>   
## 外接程序和 XAML 浏览器应用程序  
 到目前为止，在所使用的示例中，宿主应用程序都安装为独立应用程序。  实际上，如果满足以下附加的生成和实现要求，[!INCLUDE[TLA#tla_xbap#plural](../../../../includes/tlasharptla-xbapsharpplural-md.md)] 也可以承载外接程序：  
  
-   必须专门配置 [!INCLUDE[TLA2#tla_xbap](../../../../includes/tla2sharptla-xbap-md.md)] 应用程序清单，以便将管线（文件夹和程序集）和外接程序程序集下载到客户端计算机上的 [!INCLUDE[TLA#tla_clickonce](../../../../includes/tlasharptla-clickonce-md.md)] 应用程序缓存中 [!INCLUDE[TLA2#tla_xbap](../../../../includes/tla2sharptla-xbap-md.md)] 所在的文件夹中。  
  
-   用于发现和加载外接程序的 [!INCLUDE[TLA2#tla_xbap](../../../../includes/tla2sharptla-xbap-md.md)] 代码必须将用于 [!INCLUDE[TLA2#tla_xbap](../../../../includes/tla2sharptla-xbap-md.md)] 的 [!INCLUDE[TLA2#tla_clickonce](../../../../includes/tla2sharptla-clickonce-md.md)] 应用程序缓存用作管线和外接程序位置。  
  
-   如果外接程序引用位于源站点的松散文件，则 [!INCLUDE[TLA2#tla_xbap](../../../../includes/tla2sharptla-xbap-md.md)] 必须将外接程序加载到专门的安全性上下文中；在由 [!INCLUDE[TLA2#tla_xbap#plural](../../../../includes/tla2sharptla-xbapsharpplural-md.md)] 承载时，外接程序只能引用位于宿主应用程序的源站点的松散文件。  
  
 下面几个小节将详细介绍这些任务。  
  
### 配置用于 ClickOnce 部署的管线和外接程序  
 [!INCLUDE[TLA2#tla_xbap#plural](../../../../includes/tla2sharptla-xbapsharpplural-md.md)] 将下载到 [!INCLUDE[TLA2#tla_clickonce](../../../../includes/tla2sharptla-clickonce-md.md)] 部署缓存中的安全文件夹并从该文件夹中运行。  为使 [!INCLUDE[TLA2#tla_xbap](../../../../includes/tla2sharptla-xbap-md.md)] 能够承载外接程序，还必须将管道和外接程序程序集下载到安全文件夹。  若要实现此目的，需要配置应用程序清单，以包含要下载的管线和外接程序程序集。  这在 [!INCLUDE[TLA2#tla_visualstu](../../../../includes/tla2sharptla-visualstu-md.md)] 中最容易实现，但为使 [!INCLUDE[TLA2#tla_visualstu](../../../../includes/tla2sharptla-visualstu-md.md)] 检测到管道程序集，管道和外接程序程序集需要位于宿主 [!INCLUDE[TLA2#tla_xbap](../../../../includes/tla2sharptla-xbap-md.md)] 项目的根文件夹中。  
  
 因此，第一步是通过设置每个管道程序集和外接程序程序集项目的生成输出，向 [!INCLUDE[TLA2#tla_xbap](../../../../includes/tla2sharptla-xbap-md.md)] 项目的根文件夹生成管道和外接程序程序集。  下表显示管道程序集项目和外接程序程序集项目的生成输出路径，此路径位于与宿主 [!INCLUDE[TLA2#tla_xbap](../../../../includes/tla2sharptla-xbap-md.md)] 项目相同的解决方案和根文件夹中。  
  
 表 1：XBAP 承载的管线程序集的生成输出路径  
  
|管线程序集项目|生成输出路径|  
|-------------|------------|  
|协定|`..  \HostXBAP\Contracts\`|  
|外接程序视图|`..  \HostXBAP\AddInViews\`|  
|外接程序端适配器|`..  \HostXBAP\AddInSideAdapters\`|  
|宿主端适配器|`..  \HostXBAP\HostSideAdapters\`|  
|外接程序|`..  \HostXBAP\AddIns\WPFAddIn1`|  
  
 下一步是通过在 [!INCLUDE[TLA2#tla_visualstu](../../../../includes/tla2sharptla-visualstu-md.md)] 中执行以下操作，指定管道程序集和外接程序程序集作为 [!INCLUDE[TLA2#tla_xbap#plural](../../../../includes/tla2sharptla-xbapsharpplural-md.md)] 内容文件：  
  
1.  通过右击“解决方案资源管理器”中的每个管线文件夹，然后选择**“包括在项目中”**，将管线和外接程序程序集包含在项目中。  
  
2.  在**“属性”**窗口中将每个管线程序集和外接程序程序集的**“生成操作”**都设置为**“内容”**。  
  
 最后一步是配置应用程序清单，以包含要下载的管线程序集文件和外接程序程序集文件。  这些文件应位于 [!INCLUDE[TLA2#tla_xbap](../../../../includes/tla2sharptla-xbap-md.md)] 应用程序所占用的 [!INCLUDE[TLA2#tla_clickonce](../../../../includes/tla2sharptla-clickonce-md.md)] 缓存的根文件夹下的文件夹中。  通过执行以下操作，可以在 [!INCLUDE[TLA2#tla_visualstu](../../../../includes/tla2sharptla-visualstu-md.md)] 中实现该配置：  
  
1.  右击 [!INCLUDE[TLA2#tla_xbap](../../../../includes/tla2sharptla-xbap-md.md)] 项目，单击**“属性”**、**“发布”**，然后单击**“应用程序文件”**按钮。  
  
2.  在**“应用程序文件”**对话框中，将每个管线和外接程序 DLL 的**“发布状态”**都设置为**“包括\(自动\)”**，将每个管线和外接程序 DLL 的**“下载组”**都设置为**“\(必需\)”**。  
  
### 从应用程序基使用管线和外接程序  
 在为 [!INCLUDE[TLA2#tla_clickonce](../../../../includes/tla2sharptla-clickonce-md.md)] 部署配置管道和外接程序时，将它们下载到 [!INCLUDE[TLA2#tla_xbap](../../../../includes/tla2sharptla-xbap-md.md)] 所在的 [!INCLUDE[TLA2#tla_clickonce](../../../../includes/tla2sharptla-clickonce-md.md)] 缓存文件夹中。  若要从 [!INCLUDE[TLA2#tla_xbap](../../../../includes/tla2sharptla-xbap-md.md)] 中使用管道和外接程序，[!INCLUDE[TLA2#tla_xbap](../../../../includes/tla2sharptla-xbap-md.md)] 代码必须从应用程序基获取管道和外接程序。  用于处理管线和外接程序的 [!INCLUDE[dnprdnshort](../../../../includes/dnprdnshort-md.md)] 外接程序模型的各种类型和成员为这种情况提供特殊支持。  首先，路径由 <xref:System.AddIn.Hosting.PipelineStoreLocation> 枚举值标识。  此值用在使用管线的相关外接程序成员的重载中，这些成员包括：  
  
-   <xref:System.AddIn.Hosting.AddInStore.FindAddIns%28System.Type%2CSystem.AddIn.Hosting.PipelineStoreLocation%29?displayProperty=fullName>  
  
-   [AddInStore.FindAddIns\(Type, PipelineStoreLocation, String\<xref:System.AddIn.Hosting.AddInStore.FindAddIns%28System.Type%2CSystem.AddIn.Hosting.PipelineStoreLocation%2CSystem.String%5B%5D%29?displayProperty=fullName>  
  
-   <xref:System.AddIn.Hosting.AddInStore.Rebuild%28System.AddIn.Hosting.PipelineStoreLocation%29?displayProperty=fullName>  
  
-   <xref:System.AddIn.Hosting.AddInStore.Update%28System.AddIn.Hosting.PipelineStoreLocation%29?displayProperty=fullName>  
  
### 访问宿主的源站点  
 为确保外接程序可以引用源站点的文件，必须使用等效于宿主应用程序的安全隔离来加载外接程序。  此安全级别由 <xref:System.AddIn.Hosting.AddInSecurityLevel?displayProperty=fullName> 枚举值标识，并在外接程序激活时传递到 <xref:System.AddIn.Hosting.AddInToken.Activate%2A> 方法。  
  
<a name="WPFAddInModelArchitecture"></a>   
## WPF 外接程序体系结构  
 在最上层，如我们所见，[!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] 使用 <xref:System.AddIn.Contract.INativeHandleContract>、<xref:System.AddIn.Pipeline.FrameworkElementAdapters.ViewToContractAdapter%2A> 和 <xref:System.AddIn.Pipeline.FrameworkElementAdapters.ContractToViewAdapter%2A> 使 [!INCLUDE[dnprdnshort](../../../../includes/dnprdnshort-md.md)] 外接程序实现了 [!INCLUDE[TLA2#tla_ui#plural](../../../../includes/tla2sharptla-uisharpplural-md.md)]（直接或间接从 <xref:System.Windows.FrameworkElement> 派生而来）。  结果是向宿主应用程序返回从宿主应用程序 [!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)] 显示的 <xref:System.Windows.FrameworkElement>。  
  
 对于简单的 [!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)] 外接程序方案，这些内容已足够详细，可以满足开发人员的需要。  对于更复杂的方案，特别是那些尝试使用附加 [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] 服务（如布局、资源和数据绑定）的方案，需要更为深入地掌握 [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] 如何扩展支持 [!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)] 的 [!INCLUDE[dnprdnshort](../../../../includes/dnprdnshort-md.md)] 外接程序模型的知识，才能理解它的优点和限制。  
  
 基本上，[!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] 不会将 [!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)] 从外接程序传递到宿主应用程序；而 [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] 通过使用 [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] 互操作性传递 [!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)] 的 Win32 窗口句柄。  因此，当 [!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)] 从外接程序传递到宿主应用程序时，会发生以下情况：  
  
-   在外接程序端，[!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] 获得一个将由宿主应用程序显示的 [!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)] 的窗口句柄。  此窗口句柄由内部 [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] 类封装，该类从 <xref:System.Windows.Interop.HwndSource> 派生并实现 <xref:System.AddIn.Contract.INativeHandleContract>。  此类的实例由 <xref:System.AddIn.Pipeline.FrameworkElementAdapters.ViewToContractAdapter%2A> 返回，并从外接程序的应用程序域封送到宿主应用程序的应用程序域。  
  
-   在宿主应用程序端，[!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] 将 <xref:System.Windows.Interop.HwndSource> 重新打包为从 <xref:System.Windows.Interop.HwndHost> 派生并使用 <xref:System.AddIn.Contract.INativeHandleContract> 的内部 [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] 类。  <xref:System.AddIn.Pipeline.FrameworkElementAdapters.ContractToViewAdapter%2A> 将此类的实例返回到宿主应用程序。  
  
 存在 <xref:System.Windows.Interop.HwndHost>，用于显示来自 [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] [!INCLUDE[TLA2#tla_ui#plural](../../../../includes/tla2sharptla-uisharpplural-md.md)] 的由窗口句柄标识的 [!INCLUDE[TLA2#tla_ui#plural](../../../../includes/tla2sharptla-uisharpplural-md.md)]。  有关更多信息，请参见 [WPF 和 Win32 互操作](../../../../docs/framework/wpf/advanced/wpf-and-win32-interoperation.md)。  
  
 总之，<xref:System.AddIn.Contract.INativeHandleContract>、<xref:System.AddIn.Pipeline.FrameworkElementAdapters.ViewToContractAdapter%2A> 和 <xref:System.AddIn.Pipeline.FrameworkElementAdapters.ContractToViewAdapter%2A> 的存在，使 [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] [!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)] 的窗口句柄能够从外接程序传递到宿主应用程序，并在宿主应用程序中由 <xref:System.Windows.Interop.HwndHost> 封装并由宿主应用程序的 [!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)] 显示。  
  
> [!NOTE]
>  由于宿主应用程序获取 <xref:System.Windows.Interop.HwndHost>，因此宿主应用程序无法将 <xref:System.AddIn.Pipeline.FrameworkElementAdapters.ContractToViewAdapter%2A> 返回的对象转换为由外接程序实现的类型（如 <xref:System.Windows.Controls.UserControl>）。  
  
 从本质上，<xref:System.Windows.Interop.HwndHost> 具有某些限制，这些限制会影响宿主应用程序使用它们的方式。  不过，[!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] 针对外接程序方案的几项功能，对 <xref:System.Windows.Interop.HwndHost> 进行了扩展。  下面介绍这些优点和限制。  
  
<a name="WPFAddInModelBenefits"></a>   
## WPF 外接程序的优点  
 由于使用从 <xref:System.Windows.Interop.HwndHost> 派生的内部类从宿主应用程序显示 [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] 外接程序 [!INCLUDE[TLA2#tla_ui#plural](../../../../includes/tla2sharptla-uisharpplural-md.md)]，因此，在 [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] [!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)] 服务（如布局、呈现、数据绑定、样式、模板和资源）方面，这些 [!INCLUDE[TLA2#tla_ui#plural](../../../../includes/tla2sharptla-uisharpplural-md.md)] 受到 <xref:System.Windows.Interop.HwndHost> 功能的限制。  但是，[!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] 扩展了其内部 <xref:System.Windows.Interop.HwndHost> 子类的附加功能，包括：  
  
-   在宿主应用程序的 [!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)] 和外接程序的 [!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)] 之间的 Tab 键切换功能。  请注意，不论外接程序是完全受信任还是部分受信任，“外接程序为 [!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)]”编程模型都要求使用外接程序端适配器来重写 <xref:System.AddIn.Pipeline.ContractBase.QueryContract%2A> 以实现 Tab 键切换功能。  
  
-   满足从宿主应用程序 [!INCLUDE[TLA2#tla_ui#plural](../../../../includes/tla2sharptla-uisharpplural-md.md)] 显示的外接程序 [!INCLUDE[TLA2#tla_ui#plural](../../../../includes/tla2sharptla-uisharpplural-md.md)] 的可访问性要求。  
  
-   使 [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] 应用程序可在多个应用程序域方案中安全运行。  
  
-   在外接程序使用安全隔离（即部分信任安全沙盒）运行时，防止非法访问外接程序 [!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)] 窗口句柄。  调用 <xref:System.AddIn.Pipeline.FrameworkElementAdapters.ViewToContractAdapter%2A> 以确保安全性：  
  
    -   对于“外接程序返回 [!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)]”编程模型，越过隔离边界传递外接程序 [!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)] 窗口句柄的唯一方法是调用 <xref:System.AddIn.Pipeline.FrameworkElementAdapters.ViewToContractAdapter%2A>。  
  
    -   对于“外接程序为 [!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)]”编程模型，要求对外接程序端适配器重写 <xref:System.AddIn.Pipeline.ContractBase.QueryContract%2A> 并调用 <xref:System.AddIn.Pipeline.FrameworkElementAdapters.ViewToContractAdapter%2A>（如前面几个示例所示），就像从宿主端适配器调用外接程序端适配器的 `QueryContract` 实现一样。  
  
-   提供多个应用程序域执行保护。  由于应用程序域的限制，即使存在隔离边界，外接程序应用程序域中引发的未经处理的异常也会导致整个应用程序崩溃。  但是 [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] 和 [!INCLUDE[dnprdnshort](../../../../includes/dnprdnshort-md.md)] 外接程序模型提供了一种简单方法，可以避免此问题，提高应用程序的稳定性。  如果宿主应用程序为 [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] 应用程序，则显示 [!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)] 的 [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] 外接程序为应用程序域的运行线程创建一个 <xref:System.Windows.Threading.Dispatcher>。  通过处理 [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] 外接程序的 <xref:System.Windows.Threading.Dispatcher> 的 <xref:System.Windows.Threading.Dispatcher.UnhandledException> 事件，可以检测应用程序域中引发的所有未经处理的异常。  从 <xref:System.Windows.Threading.Dispatcher.CurrentDispatcher%2A> 属性中可以获取 <xref:System.Windows.Threading.Dispatcher>。  
  
<a name="WPFAddInModelLimitations"></a>   
## WPF 外接程序限制  
 对于从宿主应用程序显示的外接程序 [!INCLUDE[TLA2#tla_ui#plural](../../../../includes/tla2sharptla-uisharpplural-md.md)]，除了 [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] 向 <xref:System.Windows.Interop.HwndSource>、<xref:System.Windows.Interop.HwndHost> 和窗口句柄所提供的默认行为增加的优点之外，也存在一些限制：  
  
-   从宿主应用程序显示的外接程序 [!INCLUDE[TLA2#tla_ui#plural](../../../../includes/tla2sharptla-uisharpplural-md.md)] 不遵从宿主应用程序的剪辑行为。  
  
-   互操作性方案中的“空域”概念也适用于外接程序（请参见 [技术区概述](../../../../docs/framework/wpf/advanced/technology-regions-overview.md)）。  
  
-   宿主应用程序的 [!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)] 服务（如资源继承、数据绑定和命令设置）不会自动提供给外接程序 [!INCLUDE[TLA2#tla_ui#plural](../../../../includes/tla2sharptla-uisharpplural-md.md)]。  若要向外接程序提供这些服务，需要更新管线。  
  
-   外接程序 [!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)] 不能旋转、缩放、扭曲，也不受变换的影响（请参见[变换概述](../../../../docs/framework/wpf/graphics-multimedia/transforms-overview.md)）。  
  
-   通过 <xref:System.Drawing> 命名空间的绘图操作呈现的外接程序 [!INCLUDE[TLA2#tla_ui#plural](../../../../includes/tla2sharptla-uisharpplural-md.md)] 中的内容可以包含 Alpha 混合。  但是，包含它的外接程序 [!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)] 和宿主应用程序 [!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)] 都必须是 100% 不透明；换言之，二者的 `Opacity` 属性都必须设置为 1。  
  
-   如果包含外接程序 [!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)] 的宿主应用程序的窗口的 <xref:System.Windows.Window.AllowsTransparency%2A> 属性设置为 `true`，则外接程序不可见。  即使外接程序 [!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)] 为 100% 不透明（即 `Opacity` 属性的值为 1）也是如此。  
  
-   外接程序 [!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)] 必须出现在同一顶级窗口中其他 [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] 元素之上。  
  
-   外接程序 [!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)] 的任何部分都不能使用 <xref:System.Windows.Media.VisualBrush> 呈现。  外接程序可以获取生成的 [!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)] 的快照，从而创建一个位图，通过协定所定义的方法可将该位图传递到宿主应用程序。  
  
-   外接程序 [!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)] 的 <xref:System.Windows.Controls.MediaElement> 不能播放媒体文件。  
  
-   宿主应用程序既不会接收，也不会引发为外接程序 [!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)] 生成的鼠标事件，宿主应用程序 [!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)] 的 `IsMouseOver` 属性值为 `false`。  
  
-   当焦点在外接程序 [!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)] 的控件之间转移时，宿主应用程序既不会接收，也不会引发 `GotFocus` 和 `LostFocus` 事件。  
  
-   在打印时，包含外接程序 [!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)] 的宿主应用程序部分将显示为空白。  
  
-   在所有者外接程序卸载之前，如果宿主应用程序继续执行，则必须手动关闭由外接程序 [!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)] 创建的所有调度程序（请参见 <xref:System.Windows.Threading.Dispatcher>）。  协定可以实现一些方法，宿主应用程序使用这些方法，可以在外接程序卸载之前通知外接程序，从而允许外接程序 [!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)] 关闭自己的调度程序。  
  
-   如果外接程序 [!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)] 是 <xref:System.Windows.Controls.InkCanvas> 或包含 <xref:System.Windows.Controls.InkCanvas>，则不能卸载该外接程序。  
  
<a name="PerformanceOptimization"></a>   
## 性能优化  
 默认情况下，如果使用多个应用程序域，则每个应用程序所需的所有 [!INCLUDE[dnprdnshort](../../../../includes/dnprdnshort-md.md)] 程序集都会加载到该应用程序的域中。  因此，创建新应用程序域和在应用程序域中启动应用程序所需的时间可能会影响性能。  [!INCLUDE[dnprdnshort](../../../../includes/dnprdnshort-md.md)] 提供了一种减少启动时间的方法，即指示应用程序共享各应用程序域的程序集（如果已经加载）。  为此，可以使用 <xref:System.LoaderOptimizationAttribute> 特性，该特性必须应用于入口点方法 \(`Main`\)。  这种情况下，只能使用代码来实现应用程序定义（请参见[应用程序管理概述](../../../../docs/framework/wpf/app-development/application-management-overview.md)）。  
  
## 请参阅  
 <xref:System.LoaderOptimizationAttribute>   
 [外接程序和扩展性](../../../../ml/index.xml)   
 [应用程序域](../../../../docs/framework/app-domains/application-domains.md)   
 [.NET Framework Remoting Overview](http://msdn.microsoft.com/zh-cn/eccb1d31-0a22-417a-97fd-f4f1f3aa4462)   
 [Making Objects Remotable](http://msdn.microsoft.com/zh-cn/01197253-3f13-43b7-894d-9683e431192a)   
 [帮助主题](../../../../docs/framework/wpf/app-development/how-to-topics.md)