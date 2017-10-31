---
title: "结构化导航概述 | Microsoft Docs"
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
  - "结构化导航 [WPF]"
ms.assetid: 025d30ef-fec5-436d-ad7a-5d5483331c26
caps.latest.revision: 43
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 36
---
# 结构化导航概述
可以由 [!INCLUDE[TLA#tla_xbap](../../../../includes/tlasharptla-xbap-md.md)]、<xref:System.Windows.Controls.Frame> 或 <xref:System.Windows.Navigation.NavigationWindow> 承载的内容由多个页面组成，这些页面可以通过 pack [!INCLUDE[TLA#tla_uri#plural](../../../../includes/tlasharptla-urisharpplural-md.md)] 来标识，并且可以通过超链接来导航。  页面的结构以及导航页面的方式（通过超链接来定义）称为导航拓扑。  这样的拓扑适合于各种应用程序类型，尤其适合于在文档之间导航的应用程序类型。  对于此类应用程序，用户可以从一个页面导航到另一个页面，并且任何页面都不需要知道对方的任何信息。  
  
 但是，对于其他类型的应用程序，当在其页面之间导航时，您确实需要知道这些页面信息。  以一个人力资源应用程序为例，它具有一个列出组织中的所有员工的页面，即“List Employees”（列出员工）页。  该页还允许用户通过单击超链接来添加新员工。  当单击此超链接时，页面将导航到“Add an Employee”（添加员工）页，以收集新员工的详细信息，并将其返回到“List Employees”（列出员工）页，以创建新员工并更新列表。  这种样式的导航与调用方法来执行某些处理并返回值（称为结构化编程）类似。  同样，这种样式的导航称为“结构化导航”。  
  
 <xref:System.Windows.Controls.Page> 类未实现对结构化导航的支持。  <xref:System.Windows.Navigation.PageFunction%601> 类派生自 <xref:System.Windows.Controls.Page>，并使用结构化导航所需的基本构造来对它进行扩展。  本主题演示如何使用 <xref:System.Windows.Navigation.PageFunction%601> 建立结构化导航。  
  
   
  
<a name="Structured_Navigation"></a>   
## 结构化导航  
 当一个页面调用结构化导航中的另一页面时，需要下面的部分或全部行为：  
  
-   调用页导航到被调用页，并且可以选择传递被调用页所需的参数。  
  
-   当用户已使用完调用页时，被调用页将明确返回到调用页，并且可以：  
  
    -   返回描述调用页是如何完成（例如，用户按的是 OK（确定）按钮还是 Cancel（取消）按钮）的状态信息。  
  
    -   返回从用户那里收集的数据（例如，新员工的详细信息）。  
  
-   当调用页返回到被调用页时，被调用页会从导航历史记录中移除，以便将被调用页的一个实例与另一个实例分开。  
  
 下图说明了这些行为。  
  
 ![调用页与被调用页之间的流](../../../../docs/framework/wpf/app-development/media/structurednavigationoverviewfigure1.png "StructuredNavigationOverviewFigure1")  
  
 您可以通过将 <xref:System.Windows.Navigation.PageFunction%601> 用作被调用页来实现这些行为。  
  
<a name="Structured_Navigation_with_PageFunction"></a>   
## 使用 PageFunction 进行结构化导航  
 本主题演示如何实现涉及一个 <xref:System.Windows.Navigation.PageFunction%601> 的结构化导航的基本机制。  在本示例中，<xref:System.Windows.Controls.Page> 调用 <xref:System.Windows.Navigation.PageFunction%601>，以便从用户那里获取 <xref:System.String> 值并返回该值。  
  
### 创建调用页  
 调用 <xref:System.Windows.Navigation.PageFunction%601> 的页可以是 <xref:System.Windows.Controls.Page>，也可以是 <xref:System.Windows.Navigation.PageFunction%601>。  在本示例中，它是 <xref:System.Windows.Controls.Page>，如下面的代码所示。  
  
 [!code-xml[StructuredNavigationSample#CallingPageDefaultMARKUP1](../../../../samples/snippets/csharp/VS_Snippets_Wpf/StructuredNavigationSample/CSharp/CallingPage.xaml#callingpagedefaultmarkup1)]  
[!code-xml[StructuredNavigationSample#CallingPageDefaultMARKUP2](../../../../samples/snippets/csharp/VS_Snippets_Wpf/StructuredNavigationSample/CSharp/CallingPage.xaml#callingpagedefaultmarkup2)]  
  
 [!code-csharp[StructuredNavigationSample#CallingPageDefaultCODEBEHIND1](../../../../samples/snippets/csharp/VS_Snippets_Wpf/StructuredNavigationSample/CSharp/CallingPage.xaml.cs#callingpagedefaultcodebehind1)]
 [!code-vb[StructuredNavigationSample#CallingPageDefaultCODEBEHIND1](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/StructuredNavigationSample/VisualBasic/CallingPage.xaml.vb#callingpagedefaultcodebehind1)]  
[!code-csharp[StructuredNavigationSample#CallingPageDefaultCODEBEHIND2](../../../../samples/snippets/csharp/VS_Snippets_Wpf/StructuredNavigationSample/CSharp/CallingPage.xaml.cs#callingpagedefaultcodebehind2)]
[!code-vb[StructuredNavigationSample#CallingPageDefaultCODEBEHIND2](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/StructuredNavigationSample/VisualBasic/CallingPage.xaml.vb#callingpagedefaultcodebehind2)]  
[!code-csharp[StructuredNavigationSample#CallingPageDefaultCODEBEHIND3](../../../../samples/snippets/csharp/VS_Snippets_Wpf/StructuredNavigationSample/CSharp/CallingPage.xaml.cs#callingpagedefaultcodebehind3)]
[!code-vb[StructuredNavigationSample#CallingPageDefaultCODEBEHIND3](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/StructuredNavigationSample/VisualBasic/CallingPage.xaml.vb#callingpagedefaultcodebehind3)]  
  
### 创建要调用的页面函数  
 因为调用页可以使用被调用页来从用户那里收集数据并返回数据，所以 <xref:System.Windows.Navigation.PageFunction%601> 实现为一个泛型类，它的类型参数指定被调用页将返回的值的类型。  下面的代码示例显示被调用页的初始实现，它使用 <xref:System.Windows.Navigation.PageFunction%601>，后者返回 <xref:System.String>。  
  
 [!code-xml[StructuredNavigationSample#CalledPageFunctionMARKUP](../../../../samples/snippets/csharp/VS_Snippets_Wpf/StructuredNavigationSample/CSharp/CalledPageFunction.xaml#calledpagefunctionmarkup)]  
  
 [!code-csharp[StructuredNavigationSample#CalledPageFunctionCODEBEHIND1](../../../../samples/snippets/csharp/VS_Snippets_Wpf/StructuredNavigationSample/CSharp/CalledPageFunction.xaml.cs#calledpagefunctioncodebehind1)]
 [!code-vb[StructuredNavigationSample#CalledPageFunctionCODEBEHIND1](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/StructuredNavigationSample/VisualBasic/CalledPageFunction.xaml.vb#calledpagefunctioncodebehind1)]  
[!code-csharp[StructuredNavigationSample#CalledPageFunctionCODEBEHIND2](../../../../samples/snippets/csharp/VS_Snippets_Wpf/StructuredNavigationSample/CSharp/CalledPageFunction.xaml.cs#calledpagefunctioncodebehind2)]
[!code-vb[StructuredNavigationSample#CalledPageFunctionCODEBEHIND2](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/StructuredNavigationSample/VisualBasic/CalledPageFunction.xaml.vb#calledpagefunctioncodebehind2)]  
  
 <xref:System.Windows.Navigation.PageFunction%601> 的声明与 <xref:System.Windows.Controls.Page> 的声明类似，但增加了类型参数。  从代码示例中可以看出，在 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] 标记和代码隐藏中均指定了类型参数，前者使用 `x:TypeArguments` 特性，后者使用标准的泛型参数语法。  
  
 不必仅使用 [!INCLUDE[dnprdnshort](../../../../includes/dnprdnshort-md.md)] 类作为类型参数。  可以调用 <xref:System.Windows.Navigation.PageFunction%601> 来收集特定于域的数据，这些数据抽象化为自定义类型。  下面的代码演示如何将自定义类型用作 <xref:System.Windows.Navigation.PageFunction%601> 的类型参数。  
  
 [!code-csharp[CustomTypePageFunctionSnippets#CustomTypeCODE1](../../../../samples/snippets/csharp/VS_Snippets_Wpf/CustomTypePageFunctionSnippets/CSharp/CustomType.cs#customtypecode1)]
 [!code-vb[CustomTypePageFunctionSnippets#CustomTypeCODE1](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/CustomTypePageFunctionSnippets/VisualBasic/CustomType.vb#customtypecode1)]  
[!code-csharp[CustomTypePageFunctionSnippets#CustomTypeCODE2](../../../../samples/snippets/csharp/VS_Snippets_Wpf/CustomTypePageFunctionSnippets/CSharp/CustomType.cs#customtypecode2)]
[!code-vb[CustomTypePageFunctionSnippets#CustomTypeCODE2](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/CustomTypePageFunctionSnippets/VisualBasic/CustomType.vb#customtypecode2)]  
  
 [!code-xml[CustomTypePageFunctionSnippets#CustomTypePageFunctionMARKUP1](../../../../samples/snippets/csharp/VS_Snippets_Wpf/CustomTypePageFunctionSnippets/CSharp/CustomTypePageFunction.xaml#customtypepagefunctionmarkup1)]  
[!code-xml[CustomTypePageFunctionSnippets#CustomTypePageFunctionMARKUP2](../../../../samples/snippets/csharp/VS_Snippets_Wpf/CustomTypePageFunctionSnippets/CSharp/CustomTypePageFunction.xaml#customtypepagefunctionmarkup2)]  
  
 [!code-csharp[CustomTypePageFunctionSnippets#CustomTypePageFunctionCODEBEHIND1](../../../../samples/snippets/csharp/VS_Snippets_Wpf/CustomTypePageFunctionSnippets/CSharp/CustomTypePageFunction.xaml.cs#customtypepagefunctioncodebehind1)]
 [!code-vb[CustomTypePageFunctionSnippets#CustomTypePageFunctionCODEBEHIND1](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/CustomTypePageFunctionSnippets/VisualBasic/CustomTypePageFunction.xaml.vb#customtypepagefunctioncodebehind1)]  
  
  
 <xref:System.Windows.Navigation.PageFunction%601> 的类型参数提供了调用页与被调用页之间的通信的基础，此通信将在后面几节介绍。  
  
 您将看到，使用 <xref:System.Windows.Navigation.PageFunction%601> 的声明标识的类型在从 <xref:System.Windows.Navigation.PageFunction%601> 向调用页返回数据方面扮演了重要的角色。  
  
### 调用 PageFunction 和传递参数  
 若要调用页面，调用页必须实例化被调用页，并使用 <xref:System.Windows.Navigation.NavigationService.Navigate%2A> 方法导航到它。  这使得调用页可以将初始数据传递给被调用页，例如，被调用页收集的数据的默认值。  
  
 下面的代码显示使用非默认构造函数从调用页接受参数的被调用页。  
  
 [!code-csharp[StructuredNavigationSample#AcceptsInitialDataCODEBEHIND1](../../../../samples/snippets/csharp/VS_Snippets_Wpf/StructuredNavigationSample/CSharp/CalledPageFunction.xaml.cs#acceptsinitialdatacodebehind1)]
 [!code-vb[StructuredNavigationSample#AcceptsInitialDataCODEBEHIND1](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/StructuredNavigationSample/VisualBasic/CalledPageFunction.xaml.vb#acceptsinitialdatacodebehind1)]  
[!code-csharp[StructuredNavigationSample#AcceptsInitialDataCODEBEHIND2](../../../../samples/snippets/csharp/VS_Snippets_Wpf/StructuredNavigationSample/CSharp/CalledPageFunction.xaml.cs#acceptsinitialdatacodebehind2)]
[!code-vb[StructuredNavigationSample#AcceptsInitialDataCODEBEHIND2](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/StructuredNavigationSample/VisualBasic/CalledPageFunction.xaml.vb#acceptsinitialdatacodebehind2)]  
[!code-csharp[StructuredNavigationSample#AcceptsInitialDataCODEBEHIND3](../../../../samples/snippets/csharp/VS_Snippets_Wpf/StructuredNavigationSample/CSharp/CalledPageFunction.xaml.cs#acceptsinitialdatacodebehind3)]
[!code-vb[StructuredNavigationSample#AcceptsInitialDataCODEBEHIND3](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/StructuredNavigationSample/VisualBasic/CalledPageFunction.xaml.vb#acceptsinitialdatacodebehind3)]  
[!code-csharp[StructuredNavigationSample#AcceptsInitialDataCODEBEHIND4](../../../../samples/snippets/csharp/VS_Snippets_Wpf/StructuredNavigationSample/CSharp/CalledPageFunction.xaml.cs#acceptsinitialdatacodebehind4)]
[!code-vb[StructuredNavigationSample#AcceptsInitialDataCODEBEHIND4](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/StructuredNavigationSample/VisualBasic/CalledPageFunction.xaml.vb#acceptsinitialdatacodebehind4)]  
  
 下面的代码显示调用页，它处理 <xref:System.Windows.Documents.Hyperlink> 的 <xref:System.Windows.Documents.Hyperlink.Click> 事件，以使被调用页实例化并向其传递初始字符串值。  
  
 [!code-xml[StructuredNavigationSample#PassingDataMARKUP2](../../../../samples/snippets/csharp/VS_Snippets_Wpf/StructuredNavigationSample/CSharp/CallingPage.xaml#passingdatamarkup2)]  
[!code-csharp[StructuredNavigationSample#PassingDataCODEBEHIND1](../../../../samples/snippets/csharp/VS_Snippets_Wpf/StructuredNavigationSample/CSharp/CallingPage.xaml.cs#passingdatacodebehind1)]
[!code-vb[StructuredNavigationSample#PassingDataCODEBEHIND1](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/StructuredNavigationSample/VisualBasic/CallingPage.xaml.vb#passingdatacodebehind1)]  
[!code-csharp[StructuredNavigationSample#PassingDataCODEBEHIND2](../../../../samples/snippets/csharp/VS_Snippets_Wpf/StructuredNavigationSample/CSharp/CallingPage.xaml.cs#passingdatacodebehind2)]
[!code-vb[StructuredNavigationSample#PassingDataCODEBEHIND2](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/StructuredNavigationSample/VisualBasic/CallingPage.xaml.vb#passingdatacodebehind2)]  
[!code-csharp[StructuredNavigationSample#PassingDataCODEBEHIND3](../../../../samples/snippets/csharp/VS_Snippets_Wpf/StructuredNavigationSample/CSharp/CallingPage.xaml.cs#passingdatacodebehind3)]
[!code-vb[StructuredNavigationSample#PassingDataCODEBEHIND3](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/StructuredNavigationSample/VisualBasic/CallingPage.xaml.vb#passingdatacodebehind3)]  
  
 不必向被调用页传递参数。  可以执行以下操作：  
  
-   从调用页：  
  
    1.  使用默认构造函数实例化被调用的 <xref:System.Windows.Navigation.PageFunction%601>。  
  
    2.  将参数存储在 <xref:System.Windows.Application.Properties%2A> 中。  
  
    3.  导航到被调用的 <xref:System.Windows.Navigation.PageFunction%601>。  
  
-   从被调用的 <xref:System.Windows.Navigation.PageFunction%601>：  
  
    -   检索并使用存储在 <xref:System.Windows.Application.Properties%2A> 中的参数。  
  
 但是，您不久就会看到，您仍然需要使用代码来实例化并导航到被调用页以收集被调用页返回的数据。  为此，<xref:System.Windows.Navigation.PageFunction%601> 需要保持活动状态；否则，当您下一次导航到 <xref:System.Windows.Navigation.PageFunction%601> 时，[!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] 将使用默认构造函数来实例化 <xref:System.Windows.Navigation.PageFunction%601>。  
  
 但是，在被调用页返回之前，需要返回可以由调用页检索的数据。  
  
### 将任务的任务结果和任务数据返回到调用页  
 在用户使用完被调用页后（在本示例中通过按 OK（确定）或 Cancel（取消）按钮来表示），被调用页需要返回。  因为调用页已使用被调用页来从用户那里收集数据，所以调用页需要两种类型的信息：  
  
1.  用户是否取消了被调用页（在本示例中通过按 OK（确定）或 Cancel（取消）按钮）。  这使得调用页可以确定是否处理被调用页从用户那里收集的数据。  
  
2.  用户提供的数据。  
  
 为了返回信息，<xref:System.Windows.Navigation.PageFunction%601> 实现 <xref:System.Windows.Navigation.PageFunction%601.OnReturn%2A> 方法。  下面的代码演示如何调用它。  
  
 [!code-csharp[StructuredNavigationSample#ReturnCODEBEHIND1](../../../../samples/snippets/csharp/VS_Snippets_Wpf/StructuredNavigationSample/CSharp/CalledPageFunction.xaml.cs#returncodebehind1)]
 [!code-vb[StructuredNavigationSample#ReturnCODEBEHIND1](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/StructuredNavigationSample/VisualBasic/CalledPageFunction.xaml.vb#returncodebehind1)]  
[!code-csharp[StructuredNavigationSample#ReturnCODEBEHIND2](../../../../samples/snippets/csharp/VS_Snippets_Wpf/StructuredNavigationSample/CSharp/CalledPageFunction.xaml.cs#returncodebehind2)]
[!code-vb[StructuredNavigationSample#ReturnCODEBEHIND2](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/StructuredNavigationSample/VisualBasic/CalledPageFunction.xaml.vb#returncodebehind2)]  
  
 在本示例中，如果用户按 Cancel（取消）按钮，则会向调用页返回 `null` 值。  如果改为按“确定”按钮，则返回用户提供的字符串值。  <xref:System.Windows.Navigation.PageFunction%601.OnReturn%2A> 是一个 `protected` `virtual` 方法，通过调用该方法可向调用页返回数据。  数据需要打包在泛型 <xref:System.Windows.Navigation.ReturnEventArgs%601> 类型的实例中，其类型参数指定 <xref:System.Windows.Navigation.ReturnEventArgs%601.Result%2A> 返回的值的类型。  这样，当您使用特定的类型参数声明 <xref:System.Windows.Navigation.PageFunction%601> 时，即指明 <xref:System.Windows.Navigation.PageFunction%601> 将返回由类型参数指定的类型的实例。  在本示例中，类型参数以及由此而得到的返回值属于 <xref:System.String> 类型。  
  
 当调用 <xref:System.Windows.Navigation.PageFunction%601.OnReturn%2A> 时，调用页需要某种方法来接收 <xref:System.Windows.Navigation.PageFunction%601> 的返回值。  为此，<xref:System.Windows.Navigation.PageFunction%601> 实现由调用页处理的 <xref:System.Windows.Navigation.PageFunction%601.Return> 事件。  当调用 <xref:System.Windows.Navigation.PageFunction%601.OnReturn%2A> 时，会引发 <xref:System.Windows.Navigation.PageFunction%601.Return>，因此调用页可以向 <xref:System.Windows.Navigation.PageFunction%601.Return> 注册来接收通知。  
  
 [!code-csharp[StructuredNavigationSample#ProcessResultCODEBEHIND1](../../../../samples/snippets/csharp/VS_Snippets_Wpf/StructuredNavigationSample/CSharp/CallingPage.xaml.cs#processresultcodebehind1)]
 [!code-vb[StructuredNavigationSample#ProcessResultCODEBEHIND1](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/StructuredNavigationSample/VisualBasic/CallingPage.xaml.vb#processresultcodebehind1)]  
[!code-csharp[StructuredNavigationSample#ProcessResultCODEBEHIND2](../../../../samples/snippets/csharp/VS_Snippets_Wpf/StructuredNavigationSample/CSharp/CallingPage.xaml.cs#processresultcodebehind2)]
[!code-vb[StructuredNavigationSample#ProcessResultCODEBEHIND2](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/StructuredNavigationSample/VisualBasic/CallingPage.xaml.vb#processresultcodebehind2)]  
  
### 当任务完成时移除任务页  
 当被调用页返回，并且用户未取消被调用页时，调用页将处理由用户提供并且从被调用页返回的数据。  这种方式的数据获取通常是一个独立的活动；当被调用页返回时，调用页需要创建并导航到新的调用页来捕获更多数据。  
  
 但是，除非从[日记](GTMT)中移除了被调用页，否则，用户将能够重新导航到调用页的上一个实例。  是否在[日记](GTMT)中保留 <xref:System.Windows.Navigation.PageFunction%601> 由 <xref:System.Windows.Navigation.PageFunctionBase.RemoveFromJournal%2A> 属性决定。  默认情况下，调用 <xref:System.Windows.Navigation.PageFunction%601.OnReturn%2A> 时会自动移除页面函数，因为 <xref:System.Windows.Navigation.PageFunctionBase.RemoveFromJournal%2A> 设置为 `true`。  若要在调用 <xref:System.Windows.Navigation.PageFunction%601.OnReturn%2A> 后在导航历史记录中保留页面函数，请将 <xref:System.Windows.Navigation.PageFunctionBase.RemoveFromJournal%2A> 设置为 `false`。  
  
<a name="Other_Types_of_Structured_Navigation"></a>   
## 其他类型的结构化导航  
 本主题举例说明了 <xref:System.Windows.Navigation.PageFunction%601> 的最基本使用，以支持调用\/返回结构化导航。  这一基础使您能够创建更复杂的结构化导航类型。  
  
 例如，有时调用页需要多个页面来从用户那里收集足够的数据或者执行任务。  多个页面的使用称为“向导”。  
  
 在其他情况下，应用程序可能具有依赖于结构化导航来有效操作的复杂导航拓扑。  有关更多信息，请参见[导航拓扑概述](../../../../docs/framework/wpf/app-development/navigation-topologies-overview.md)。  
  
## 请参阅  
 <xref:System.Windows.Navigation.PageFunction%601>   
 <xref:System.Windows.Navigation.NavigationService>   
 [导航拓扑概述](../../../../docs/framework/wpf/app-development/navigation-topologies-overview.md)