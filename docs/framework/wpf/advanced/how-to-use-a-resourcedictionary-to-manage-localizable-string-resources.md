---
title: "如何：使用 ResourceDictionary 来管理可本地化的字符串资源 | Microsoft Docs"
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
  - "本地化 [WPF], 打包字符串资源"
  - "打包字符串资源"
  - "ResourceDictionary [WPF]"
  - "资源 [WPF], 打包字符串资源"
ms.assetid: 19e7d9a5-20df-4ad3-b157-fe6515902e5e
caps.latest.revision: 9
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 6
---
# 如何：使用 ResourceDictionary 来管理可本地化的字符串资源
本示例演示如何使用 <xref:System.Windows.ResourceDictionary> 来包装 [!INCLUDE[TLA#tla_wpf](../../../../includes/tlasharptla-wpf-md.md)] 应用程序的可本地化字符串资源。  
  
### 使用 ResourceDictionary 来管理可本地化的字符串资源  
  
1.  创建一个 <xref:System.Windows.ResourceDictionary>，其中包含要本地化的字符串。  下面的代码提供了一个示例。  
  
     [!code-xml[StringLocalizationSample#StringResourceDictionary](../../../../samples/snippets/csharp/VS_Snippets_Wpf/StringLocalizationSample/CSharp/StringResources.xaml#stringresourcedictionary)]  
  
     此代码从 mscorlib.dll 中的 <xref:System> 命名空间定义了一个类型为 <xref:System.String> 的字符串资源 `localizedMessage`。  
  
2.  使用下面的代码将 <xref:System.Windows.ResourceDictionary> 添加到应用程序中。  
  
     [!code-xml[StringLocalizationSample#ReferencingStringResourceDictionary](../../../../samples/snippets/csharp/VS_Snippets_Wpf/StringLocalizationSample/CSharp/App.xaml#referencingstringresourcedictionary)]  
  
3.  通过如下所示的[!INCLUDE[TLA#tla_xaml](../../../../includes/tlasharptla-xaml-md.md)] 来使用标记中的字符串资源。  
  
     [!code-xml[StringLocalizationSample#GetLocalizedResourceFromMarkup](../../../../samples/snippets/csharp/VS_Snippets_Wpf/StringLocalizationSample/CSharp/MainWindow.xaml#getlocalizedresourcefrommarkup)]  
  
4.  通过如下所示的代码来使用代码隐藏文件中的字符串资源。  
  
     [!code-csharp[StringLocalizationSample#GetLocalizedResourceFromCode](../../../../samples/snippets/csharp/VS_Snippets_Wpf/StringLocalizationSample/CSharp/MainWindow.xaml.cs#getlocalizedresourcefromcode)]
     [!code-vb[StringLocalizationSample#GetLocalizedResourceFromCode](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/StringLocalizationSample/VisualBasic/MainWindow.xaml.vb#getlocalizedresourcefromcode)]  
  
5.  将应用程序本地化  有关更多信息，请参见[对应用程序进行本地化](../../../../docs/framework/wpf/advanced/how-to-localize-an-application.md)。