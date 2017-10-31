---
title: "如何：使用应用程序资源 | Microsoft Docs"
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
  - "应用程序资源"
  - "资源, 应用程序资源"
ms.assetid: 507ea937-5191-406b-8797-0a3d9f94156d
caps.latest.revision: 16
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 13
---
# 如何：使用应用程序资源
本示例演示如何使用应用程序资源。  
  
## 示例  
 下面的示例演示应用程序定义文件。  应用程序定义文件定义资源部分（<xref:System.Windows.Application.Resources%2A> 属性的值）。  构成应用程序的所有其他页可以访问在应用程序级别定义的资源。  这种情况下，资源是声明样式。  因为包含控件模板的完整样式可能很长，本示例删除了在样式的 <xref:System.Windows.Controls.ContentControl.ContentTemplate%2A> 属性 setter 中定义的控件模板。  
  
 [!code-xml[ResourcesApplication#PreTemplateResource](../../../../samples/snippets/csharp/VS_Snippets_Wpf/ResourcesApplication/CS/app.xaml#pretemplateresource)]  
[!code-xml[ResourcesApplication#PostTemplateResource](../../../../samples/snippets/csharp/VS_Snippets_Wpf/ResourcesApplication/CS/app.xaml#posttemplateresource)]  
  
 下面的示例演示了引用上例中定义的应用程序级资源的 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] 页。  通过使用 [StaticResource 标记扩展](../../../../docs/framework/wpf/advanced/staticresource-markup-extension.md)（用于指定请求的资源的唯一资源键）引用该资源。  在当前页中没有找到具有“GelButton”键的资源，所以请求资源的资源查找范围超出当前页，进入已定义的应用程序级资源。  
  
 [!code-xml[ResourcesApplication#ConsumingPage](../../../../samples/snippets/csharp/VS_Snippets_Wpf/ResourcesApplication/CS/page1.xaml#consumingpage)]  
  
## 请参阅  
 [XAML 资源](../../../../docs/framework/wpf/advanced/xaml-resources.md)   
 [应用程序管理概述](../../../../docs/framework/wpf/app-development/application-management-overview.md)   
 [帮助主题](../../../../docs/framework/wpf/advanced/resources-how-to-topics.md)