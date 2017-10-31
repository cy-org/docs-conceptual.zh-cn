---
title: "如何：使用应用程序范围的资源字典 | Microsoft Docs"
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
  - "应用程序范围资源字典"
  - "字典, Resource — 资源"
  - "资源字典, 应用程序范围"
ms.assetid: 53857682-bd2c-4f2c-8f25-1307d0b451a2
caps.latest.revision: 11
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 8
---
# 如何：使用应用程序范围的资源字典
此示例演示如何定义和使用应用程序范围的自定义资源字典。  
  
## 示例  
 <xref:System.Windows.Application> 为共享的资源 <xref:System.Windows.Application.Resources%2A> 公开应用程序范围的存储区。  默认情况下，使用 <xref:System.Windows.ResourceDictionary> 类型的实例初始化 <xref:System.Windows.Application.Resources%2A> 属性。  当您使用 <xref:System.Windows.Application.Resources%2A> 获取并设置应用程序范围的属性时，可以使用此实例。  （有关更多信息，请参见[How to: Get and Set an Application\-Scope Resource](http://msdn.microsoft.com/zh-cn/39e0420c-c9fc-47dc-8956-fdd95b214095)。）  
  
 如果您有多个使用 <xref:System.Windows.Application.Resources%2A> 设置的资源，您可以使用自定义资源字典存储这些资源，并使用它设置 <xref:System.Windows.Application.Resources%2A>。  下面演示如何使用 XAML 声明自定义资源字典。  
  
 [!code-xml[HOWTOResourceDictionaries#1](../../../../samples/snippets/csharp/VS_Snippets_Wpf/HowToResourceDictionaries/CSharp/MyResourceDictionary.xaml#1)]  
  
 使用 <xref:System.Windows.Application.Resources%2A> 交换整个资源字典使您可以支持应用程序范围的主题，每个主题都通过一个资源字典来封装。  下面的示例演示如何设置 <xref:System.Windows.ResourceDictionary>。  
  
 [!code-xml[HOWTOResourceDictionaries#2](../../../../samples/snippets/csharp/VS_Snippets_Wpf/HowToResourceDictionaries/CSharp/App.xaml#2)]  
  
 下面演示如何使用 XAML 从 <xref:System.Windows.Application.Resources%2A> 公开的资源字典获取应用程序范围的资源。  
  
 [!code-xml[HOWTOResourceDictionaries#4](../../../../samples/snippets/csharp/VS_Snippets_Wpf/HowToResourceDictionaries/CSharp/MainWindow.xaml#4)]  
  
 此外还演示如何获取代码中的资源。  
  
 [!code-csharp[HOWTOResourceDictionaries#3](../../../../samples/snippets/csharp/VS_Snippets_Wpf/HowToResourceDictionaries/CSharp/MainWindow.xaml.cs#3)]
 [!code-vb[HOWTOResourceDictionaries#3](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/HowToResourceDictionaries/VB/MainWindow.xaml.vb#3)]  
  
 使用 <xref:System.Windows.Application.Resources%2A> 时有两个注意事项。  首先，字典的*键* 是一个对象，因此设置和获取属性值时必须使用完全相同的对象实例。  （请注意：使用字符串时该键区分大小写。）其次，字典的*值* 是一个对象，因此获取属性值时需要将该值转换成需要的类型。  
  
## 请参阅  
 <xref:System.Windows.ResourceDictionary>   
 <xref:System.Windows.Application.Resources%2A>   
 [XAML 资源](../../../../docs/framework/wpf/advanced/xaml-resources.md)   
 [合并资源字典](../../../../docs/framework/wpf/advanced/merged-resource-dictionaries.md)