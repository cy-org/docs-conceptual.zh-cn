---
title: "如何：绑定到 Web 服务 | Microsoft Docs"
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
  - "绑定数据, Web 服务"
  - "数据绑定, Web 服务"
  - "Web 服务绑定"
ms.assetid: 77e2d373-69ba-4cbd-b6f5-2c83c38fc98b
caps.latest.revision: 6
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 6
---
# 如何：绑定到 Web 服务
此示例演示如何绑定到由 Web 服务方法调用返回的对象。  
  
## 示例  
 此示例使用 [MSDN\/TechNet Publishing System \(MTPS\) Content Service](http://go.microsoft.com/fwlink/?LinkId=95677)（MSDN\/TechNet 发布系统 \(MTPS\) 内容服务）检索指定文档支持的语言列表。  
  
 在调用 Web 服务之前，需要先创建对该服务的引用。  若要使用 [!INCLUDE[TLA#tla_visualstu](../../../../includes/tlasharptla-visualstu-md.md)] 创建对 MTPS 服务的 Web 引用，请按照以下步骤操作：  
  
1.  在 [!INCLUDE[TLA2#tla_visualstu](../../../../includes/tla2sharptla-visualstu-md.md)] 中打开项目。  
  
2.  从**“项目”**菜单上，单击**“添加 Web 引用”**。  
  
3.  在对话框中，将**“URL”**设置为 [http:\/\/services.msdn.microsoft.com\/contentservices\/contentservice.asmx?wsdl](http://services.msdn.microsoft.com/contentservices/contentservice.asmx?wsdl)。  
  
4.  按**“转到”**，然后按**“添加引用”**。  
  
 接下来，调用 Web 服务方法并将相应控件或窗口的 <xref:System.Windows.FrameworkElement.DataContext%2A> 设置为返回的对象。  MTPS 服务的 **GetContent** 方法采用对 **getContentRequest** 对象的引用。  因此，以下示例首先设置一个请求对象：  
  
 [!code-csharp[BindToWebService#Namespace](../../../../samples/snippets/csharp/VS_Snippets_Wpf/BindToWebService/CSharp/Window1.xaml.cs#namespace)]
 [!code-vb[BindToWebService#Namespace](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/BindToWebService/VisualBasic/Window1.xaml.vb#namespace)]  
[!code-csharp[BindToWebService#WebServiceCall](../../../../samples/snippets/csharp/VS_Snippets_Wpf/BindToWebService/CSharp/Window1.xaml.cs#webservicecall)]
[!code-vb[BindToWebService#WebServiceCall](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/BindToWebService/VisualBasic/Window1.xaml.vb#webservicecall)]  
  
 设置 <xref:System.Windows.FrameworkElement.DataContext%2A> 后，可以创建与 <xref:System.Windows.FrameworkElement.DataContext%2A> 所设置到的对象属性的绑定。  在此示例中，<xref:System.Windows.FrameworkElement.DataContext%2A> 设置为 **GetContent** 方法返回的 **getContentResponse** 对象。  在以下示例中，<xref:System.Windows.Controls.ItemsControl> 绑定到 **getContentResponse** 的 **availableVersionsAndLocales** 的 **locale** 值并显示该值。  
  
 [!code-xml[BindToWebService#Binding](../../../../samples/snippets/csharp/VS_Snippets_Wpf/BindToWebService/CSharp/Window1.xaml#binding)]  
  
 有关 **getContentResponse** 结构信息，请参见 [Content Service documentation](http://services.msdn.microsoft.com/ContentServices/ContentService.asmx)（内容服务文档）。  
  
## 请参阅  
 [数据绑定概述](../../../../docs/framework/wpf/data/data-binding-overview.md)   
 [绑定源概述](../../../../docs/framework/wpf/data/binding-sources-overview.md)   
 [使数据可用于 XAML 中的绑定](../../../../docs/framework/wpf/data/how-to-make-data-available-for-binding-in-xaml.md)