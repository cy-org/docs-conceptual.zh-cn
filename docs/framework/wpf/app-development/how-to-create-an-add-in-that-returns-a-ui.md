---
title: "如何：创建返回 UI 的外接程序 | Microsoft Docs"
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
  - "外接程序 [WPF], 返回 UI"
  - "创建返回 UI 的外接程序 [WPF]"
  - "实现外接程序管线段 [WPF]"
ms.assetid: 57f274b7-4c66-4b72-92eb-81939a393776
caps.latest.revision: 9
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 5
---
# 如何：创建返回 UI 的外接程序
本示例演示如何创建将 [!INCLUDE[TLA#tla_wpf](../../../../includes/tlasharptla-wpf-md.md)] [!INCLUDE[TLA#tla_ui](../../../../includes/tlasharptla-ui-md.md)] 返回给宿主 [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] 独立应用程序的外接程序。  
  
 该外接程序返回一个 [!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)]，该 UI 为 [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] 用户控件。  该用户控件的内容为单个按钮，单击该按钮时将显示一个消息框。  [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] 独立应用程序承载该外接程序，并将用户控件（由该外接程序返回）显示为主应用程序窗口的内容。  
  
 **必备组件**  
  
 本示例重点演示对 [!INCLUDE[dnprdnshort](../../../../includes/dnprdnshort-md.md)] 外接程序模型进行的支持此方案的 [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] 扩展，并假设您具备以下条件：  
  
-   了解 [!INCLUDE[dnprdnshort](../../../../includes/dnprdnshort-md.md)] 外接程序模型的相关知识，包括管线、外接程序和宿主开发。  如果您对这些概念不熟悉，请参见[外接程序和扩展性](../../../../ml/index.xml)。  有关演示如何实现管线、外接程序和宿主应用程序的教程，请参见[演练：创建可扩展的应用程序](../Topic/Walkthrough:%20Creating%20an%20Extensible%20Application.md)。  
  
-   了解 [!INCLUDE[dnprdnshort](../../../../includes/dnprdnshort-md.md)] 外接程序模型的 [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] 扩展的相关知识，这些知识可在以下位置找到：[WPF 外接程序概述](../../../../docs/framework/wpf/app-development/wpf-add-ins-overview.md)。  
  
## 示例  
 要创建能够返回 [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] [!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)] 的外接程序，需要为每个管线段、外接程序和宿主应用程序编写特定代码。  
  
   
  
<a name="Contract"></a>   
## 实现协定管线段  
 协定必须定义用于返回 [!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)] 的方法，该方法的返回值必须为 <xref:System.AddIn.Contract.INativeHandleContract> 类型。  下面代码中的 `IWPFAddInContract` 协定的 `GetAddInUI` 方法对此进行了演示。  
  
 [!code-csharp[SimpleAddInReturnsAUISample#ContractCode](../../../../samples/snippets/csharp/VS_Snippets_Wpf/SimpleAddInReturnsAUISample/CSharp/Contracts/IWPFAddInContract.cs#contractcode)]
 [!code-vb[SimpleAddInReturnsAUISample#ContractCode](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/SimpleAddInReturnsAUISample/VisualBasic/Contracts/IWPFAddInContract.vb#contractcode)]  
  
<a name="AddInView"></a>   
## 实现外接程序视图管线段  
 由于外接程序实现的[!INCLUDE[TLA2#tla_ui#plural](../../../../includes/tla2sharptla-uisharpplural-md.md)] 是作为 <xref:System.Windows.FrameworkElement> 的子类提供的，因此与 `IWPFAddInView.GetAddInUI` 相关的外接程序视图的方法必须返回 <xref:System.Windows.FrameworkElement> 类型的值。  下面的代码演示实现为接口的协定外接程序视图。  
  
 [!code-csharp[SimpleAddInReturnsAUISample#AddInViewCode](../../../../samples/snippets/csharp/VS_Snippets_Wpf/SimpleAddInReturnsAUISample/CSharp/AddInViews/IWPFAddInView.cs#addinviewcode)]
 [!code-vb[SimpleAddInReturnsAUISample#AddInViewCode](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/SimpleAddInReturnsAUISample/VisualBasic/AddInViews/IWPFAddInView.vb#addinviewcode)]  
  
<a name="AddInSideAdapter"></a>   
## 实现外接程序端适配器管线段  
 协定方法返回 <xref:System.AddIn.Contract.INativeHandleContract>，而外接程序返回 <xref:System.Windows.FrameworkElement>（如外接程序视图指定的那样）。  因此，在越过隔离边界之前，必须将 <xref:System.Windows.FrameworkElement> 转换为 <xref:System.AddIn.Contract.INativeHandleContract>。  此任务由外接程序端适配器通过调用 <xref:System.AddIn.Pipeline.FrameworkElementAdapters.ViewToContractAdapter%2A> 完成，如下面的代码所示。  
  
 [!code-csharp[SimpleAddInReturnsAUISample#AddInSideAdapterCode](../../../../samples/snippets/csharp/VS_Snippets_Wpf/SimpleAddInReturnsAUISample/CSharp/AddInSideAdapters/WPFAddIn_ViewToContractAddInSideAdapter.cs#addinsideadaptercode)]
 [!code-vb[SimpleAddInReturnsAUISample#AddInSideAdapterCode](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/SimpleAddInReturnsAUISample/VisualBasic/AddInSideAdapters/WPFAddIn_ViewToContractAddInSideAdapter.vb#addinsideadaptercode)]  
  
<a name="HostView"></a>   
## 实现宿主视图管线段  
 由于宿主应用程序将显示 <xref:System.Windows.FrameworkElement>，因此与 `IWPFAddInHostView.GetAddInUI` 相关的宿主视图的方法必须返回 <xref:System.Windows.FrameworkElement> 类型的值。  下面的代码演示实现为接口的协定宿主视图。  
  
 [!code-csharp[SimpleAddInReturnsAUISample#HostViewCode](../../../../samples/snippets/csharp/VS_Snippets_Wpf/SimpleAddInReturnsAUISample/CSharp/HostViews/IWPFAddInHostView.cs#hostviewcode)]
 [!code-vb[SimpleAddInReturnsAUISample#HostViewCode](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/SimpleAddInReturnsAUISample/VisualBasic/HostViews/IWPFAddInHostView.vb#hostviewcode)]  
  
<a name="HostSideAdapter"></a>   
## 实现宿主端适配器管线段  
 协定方法返回 <xref:System.AddIn.Contract.INativeHandleContract>，而宿主应用程序需要 <xref:System.Windows.FrameworkElement>（如宿主视图指定的那样）。  因此，在越过隔离边界之后，必须将 <xref:System.AddIn.Contract.INativeHandleContract> 转换为 <xref:System.Windows.FrameworkElement>。  此任务由宿主端适配器通过调用 <xref:System.AddIn.Pipeline.FrameworkElementAdapters.ContractToViewAdapter%2A> 完成，如下面的代码所示。  
  
 [!code-csharp[SimpleAddInReturnsAUISample#HostSideAdapterCode](../../../../samples/snippets/csharp/VS_Snippets_Wpf/SimpleAddInReturnsAUISample/CSharp/HostSideAdapters/WPFAddIn_ContractToViewHostSideAdapter.cs#hostsideadaptercode)]
 [!code-vb[SimpleAddInReturnsAUISample#HostSideAdapterCode](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/SimpleAddInReturnsAUISample/VisualBasic/HostSideAdapters/WPFAddIn_ContractToViewHostSideAdapter.vb#hostsideadaptercode)]  
  
<a name="AddIn"></a>   
## 实现外接程序  
 创建外接程序端适配器和外接程序视图后，外接程序 \(`WPFAddIn1.AddIn`\) 必须实现 `IWPFAddInView.GetAddInUI` 方法以返回 <xref:System.Windows.FrameworkElement> 对象（在本示例中为 <xref:System.Windows.Controls.UserControl>）。  下面的代码演示 <xref:System.Windows.Controls.UserControl>、`AddInUI` 的实现。  
  
 [!code-xml[SimpleAddInReturnsAUISample#AddInUIMarkup](../../../../samples/snippets/csharp/VS_Snippets_Wpf/SimpleAddInReturnsAUISample/CSharp/WPFAddIn1/AddInUI.xaml#addinuimarkup)]  
  
 [!code-csharp[SimpleAddInReturnsAUISample#AddInUICodeBehind](../../../../samples/snippets/csharp/VS_Snippets_Wpf/SimpleAddInReturnsAUISample/CSharp/WPFAddIn1/AddInUI.xaml.cs#addinuicodebehind)]
 [!code-vb[SimpleAddInReturnsAUISample#AddInUICodeBehind](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/SimpleAddInReturnsAUISample/VisualBasic/WPFAddIn1/AddInUI.xaml.vb#addinuicodebehind)]  
  
 外接程序的 `IWPFAddInView.GetAddInUI` 实现只需要返回 `AddInUI` 的一个新实例，如下面的代码所示。  
  
 [!code-csharp[SimpleAddInReturnsAUISample#AddInCode](../../../../samples/snippets/csharp/VS_Snippets_Wpf/SimpleAddInReturnsAUISample/CSharp/WPFAddIn1/AddIn.cs#addincode)]
 [!code-vb[SimpleAddInReturnsAUISample#AddInCode](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/SimpleAddInReturnsAUISample/VisualBasic/WPFAddIn1/AddIn.vb#addincode)]  
  
<a name="App"></a>   
## 实现宿主应用程序  
 创建宿主端适配器和宿主视图后，宿主应用程序就可以使用 [!INCLUDE[dnprdnshort](../../../../includes/dnprdnshort-md.md)] 外接程序模型来打开管线，获得外接程序宿主视图，也可以调用 `IWPFAddInHostView.GetAddInUI` 方法。  下面的代码演示这些步骤。  
  
 [!code-csharp[SimpleAddInReturnsAUISample#GetUICode](../../../../samples/snippets/csharp/VS_Snippets_Wpf/SimpleAddInReturnsAUISample/CSharp/Host/MainWindow.xaml.cs#getuicode)]
 [!code-vb[SimpleAddInReturnsAUISample#GetUICode](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/SimpleAddInReturnsAUISample/VisualBasic/Host/MainWindow.xaml.vb#getuicode)]  
  
## 请参阅  
 [外接程序和扩展性](../../../../ml/index.xml)   
 [WPF 外接程序概述](../../../../docs/framework/wpf/app-development/wpf-add-ins-overview.md)