---
title: "将可移植类库与模型-视图-视图模型配合使用 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-standard"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "VB"
  - "CSharp"
  - "C++"
  - "jsharp"
helpviewer_keywords: 
  - "可移植类库 [.NET Framework], 和 MVVM"
  - "MVVM, 和可移植类库"
ms.assetid: 41a0b9f8-15a2-431a-bc35-e310b2953b03
caps.latest.revision: 17
author: "mairaw"
ms.author: "mairaw"
manager: "wpickett"
caps.handback.revision: 17
---
# 将可移植类库与模型-视图-视图模型配合使用
可以使用 [可移植类库](../../../docs/standard/cross-platform/cross-platform-development-with-the-portable-class-library.md) .NET Framework 实现视图模型视图模型模式 \(MVVM\) 和共享多个平台进行的程序集。  
  
 MVVM 是隔离基础业务逻辑的用户界面的应用程序的模式。  您可以在[!INCLUDE[vs_dev11_long](../../../includes/vs-dev11-long-md.md)]中的[!INCLUDE[net_portable](../../../includes/net-portable-md.md)]项目中实现模型和视图模型类，然后针对不同的平台创建自定义视图。  如下图所示，此方法一次只允许编写数据模型和业务逻辑，和使用 .NET framework、Silverlight、windows phone 和 Windows  [!INCLUDE[win8_appname_long](../../../includes/win8-appname-long-md.md)] 应用程序的代码。  
  
 ![可移植的 MVVM 关系图](../../../docs/standard/cross-platform/media/portablemvvmdiagram.png "PortableMVVMdiagram")  
  
 本主题不提供有关 MVVM 模式的常规信息。  它仅提供有关如何使用 [!INCLUDE[net_portable](../../../includes/net-portable-md.md)] 实现 MVVM 的信息。  有关MVVM的更多信息，请参见MSDN Library[MVVM Quickstart](http://go.microsoft.com/fwlink/?LinkId=234934)。  
  
## 支持 MVVM 的类  
 当您面向 [!INCLUDE[net_v45](../../../includes/net-v45-md.md)] 时，[!INCLUDE[net_win8_profile](../../../includes/net-win8-profile-md.md)]、Silverlight 以及 [!INCLUDE[net_portable](../../../includes/net-portable-md.md)] 项目的 Windows Phone 7.5 时，以下类可用于实现 MVVM 模式：  
  
-   <xref:System.Collections.ObjectModel.ObservableCollection%601?displayProperty=fullName> 类  
  
-   <xref:System.Collections.ObjectModel.ReadOnlyObservableCollection%601?displayProperty=fullName> 类  
  
-   <xref:System.Collections.Specialized.INotifyCollectionChanged?displayProperty=fullName> 类  
  
-   <xref:System.Collections.Specialized.NotifyCollectionChangedAction?displayProperty=fullName> 类  
  
-   <xref:System.Collections.Specialized.NotifyCollectionChangedEventArgs?displayProperty=fullName> 类  
  
-   <xref:System.Collections.Specialized.NotifyCollectionChangedEventHandler?displayProperty=fullName> 类  
  
-   <xref:System.ComponentModel.DataErrorsChangedEventArgs?displayProperty=fullName> 类  
  
-   <xref:System.ComponentModel.INotifyDataErrorInfo?displayProperty=fullName> 类  
  
-   <xref:System.ComponentModel.INotifyPropertyChanged?displayProperty=fullName> 类  
  
-   <xref:System.Windows.Input.ICommand?displayProperty=fullName> 类  
  
-   <xref:System.ComponentModel.DataAnnotations?displayProperty=fullName> 命名空间中的所有类。  
  
## 实现 MVVM  
 若要实现 MVVM，通常在 [!INCLUDE[net_portable](../../../includes/net-portable-md.md)] 项目中创建模型和视图模型，因为 [!INCLUDE[net_portable](../../../includes/net-portable-md.md)] 项目无法引用不可移植的项目。  模型和视图模型可以在同一项目或在单独的项目中。  如果使用分离项目，请从视图模型项目向模型项目添加引用。  
  
 在编译模型和视图模型项目后，在包含视图的应用程序中引用这些程序集。  如果视图仅与视图模型进行交互，则您只需引用包含该视图模型的程序集。  
  
### 模型  
 下面的示例演示可能位于 [!INCLUDE[net_portable](../../../includes/net-portable-md.md)] 项目中的简化模型类。  
  
 [!code-csharp[PortableClassLibraryMVVM#1](../../../samples/snippets/csharp/VS_Snippets_CLR/portableclasslibrarymvvm/cs/customer.cs#1)]
 [!code-vb[PortableClassLibraryMVVM#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR/portableclasslibrarymvvm/vb/customer.vb#1)]  
  
 下面的示例演示一种简单的方法填充、检索和更新 [!INCLUDE[net_portable](../../../includes/net-portable-md.md)] 项目中的数据。  在实际应用程序中，您将检索源数据，如 Windows Communication Foundation \(WCF\) 服务。  
  
 [!code-csharp[PortableClassLibraryMVVM#2](../../../samples/snippets/csharp/VS_Snippets_CLR/portableclasslibrarymvvm/cs/customerrepository.cs#2)]
 [!code-vb[PortableClassLibraryMVVM#2](../../../samples/snippets/visualbasic/VS_Snippets_CLR/portableclasslibrarymvvm/vb/customerrepository.vb#2)]  
  
### 视图模型  
 视图模型的基类通常在实现 MVVM 模式时添加。  下面的示例演示基类。  
  
 [!code-csharp[PortableClassLibraryMVVM#3](../../../samples/snippets/csharp/VS_Snippets_CLR/portableclasslibrarymvvm/cs/viewmodelbase.cs#3)]
 [!code-vb[PortableClassLibraryMVVM#3](../../../samples/snippets/visualbasic/VS_Snippets_CLR/portableclasslibrarymvvm/vb/viewmodelbase.vb#3)]  
  
 <xref:System.Windows.Input.ICommand> 接口的实现经常与 MVVM 模式一起使用。  下面的示例演示 <xref:System.Windows.Input.ICommand> 接口的实现。  
  
 [!code-csharp[PortableClassLibraryMVVM#4](../../../samples/snippets/csharp/VS_Snippets_CLR/portableclasslibrarymvvm/cs/relaycommand.cs#4)]
 [!code-vb[PortableClassLibraryMVVM#4](../../../samples/snippets/visualbasic/VS_Snippets_CLR/portableclasslibrarymvvm/vb/relaycommand.vb#4)]  
  
 下面的示例演示简化视图模型。  
  
 [!code-csharp[PortableClassLibraryMVVM#5](../../../samples/snippets/csharp/VS_Snippets_CLR/portableclasslibrarymvvm/cs/mainpageviewmodel.cs#5)]
 [!code-vb[PortableClassLibraryMVVM#5](../../../samples/snippets/visualbasic/VS_Snippets_CLR/portableclasslibrarymvvm/vb/customerviewmodel.vb#5)]  
  
### 视图  
 从 [!INCLUDE[net_v45](../../../includes/net-v45-md.md)] 应用程序、[!INCLUDE[win8_appname_long](../../../includes/win8-appname-long-md.md)] 应用程序、基于 Silverlight 的应用程序或 windows 7.5 应用程序，您可以引用包含模型和视图模型项目的程序集。然后创建与视图模型进行交互的视图。  下面的示例演示从视图模型的数据检索和更新的简单的 Windows Presentation Foundation \(WPF\) 应用程序。  可以在 Silverlight、Windows Phone 或 [!INCLUDE[win8_appname_long](../../../includes/win8-appname-long-md.md)] 应用程序中创建类似的视图。  
  
 [!code-xml[PortableClassLibraryMVVM#6](../../../samples/snippets/csharp/VS_Snippets_CLR/portableclasslibrarymvvm/cs/mainwindow.xaml#6)]  
  
## 请参阅  
 [可移植类库](../../../docs/standard/cross-platform/cross-platform-development-with-the-portable-class-library.md)