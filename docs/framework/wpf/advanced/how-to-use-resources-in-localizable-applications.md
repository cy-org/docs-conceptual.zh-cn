---
title: "如何：使用可本地化的应用程序中的资源 | Microsoft Docs"
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
  - "应用程序, 可本地化的"
  - "可本地化的应用程序"
ms.assetid: 08539ad6-7fca-4f34-b82b-ff439e11dfa7
caps.latest.revision: 14
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 11
---
# 如何：使用可本地化的应用程序中的资源
本地化意味着根据不同的区域性对 [!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)] 进行改编。  为此，必须翻译诸如标题、说明、列表框项等文本。  为简化翻译过程，要翻译的项将收集到资源文件中。  有关如何创建要进行本地化的资源文件的信息，请参见[对应用程序进行本地化](../../../../docs/framework/wpf/advanced/how-to-localize-an-application.md)。  若要使 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 应用程序可本地化，开发人员需要将所有可本地化的资源生成为一个资源程序集。  该资源程序集本地化为不同语言，代码隐藏功能使用资源管理 [!INCLUDE[TLA#tla_api](../../../../includes/tlasharptla-api-md.md)] 来进行加载。  [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 应用程序所需的文件之一是项目文件 \(.proj\)。  您在应用程序中使用的所有资源都应包括在项目文件中。  下面的代码示例演示这一情况。  
  
## 示例  
 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)]  
  
 `<Resource Include="data\picture1.jpg"/>`  
  
 `<EmbeddedResource Include="data\stringtable.en-US.restext"/>`  
  
 若要在应用程序中使用资源，需要实例化 <xref:System.Resources.ResourceManager>，然后加载要使用的资源。  下面的示例演示如何执行此操作。  
  
 [!code-csharp[LocalizationResources#2](../../../../samples/snippets/csharp/VS_Snippets_Wpf/LocalizationResources/CSharp/page1.xaml.cs#2)]