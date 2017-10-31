---
title: "如何：使用自动布局创建按钮 | Microsoft Docs"
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
  - "自动布局, 创建按钮"
  - "Button 控件, 使用自动布局进行创建"
  - "创建, 自动布局的按钮"
ms.assetid: 96c206d0-9e77-4784-9d2d-5045aed2021c
caps.latest.revision: 15
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 12
---
# 如何：使用自动布局创建按钮
此示例描述如何使用自动布局方法在可本地化的应用程序中创建按钮。  
  
 [!INCLUDE[TLA#tla_ui](../../../../includes/tlasharptla-ui-md.md)] 的本地化是一个很耗时的过程。  通常，本地化人员除了需要翻译文本之外，还需要调整元素的大小并重新定位元素。  过去，要针对任何一种语言改编 [!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)] 都需要进行调整。  现在，使用 [!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)] 的功能，您可以对元素进行设计以减少必需的调整工作。  这种编写可以更方便地调整大小和重新定位的应用程序的方法称为 `automatic layout`。  
  
 以下两个[!INCLUDE[TLA#tla_xaml](../../../../includes/tlasharptla-xaml-md.md)] 示例创建两个实例化按钮的应用程序；一个使用英文文本，另一个使用西班牙文本。  请注意，除文本之外代码是相同的；将调整按钮使其适合文本。  
  
## 示例  
 [!code-xml[LocalizationBtn_snip#1](../../../../samples/snippets/csharp/VS_Snippets_Wpf/LocalizationBtn_snip/CS/Pane1.xaml#1)]  
  
 [!code-xml[LocalizationBtn#1](../../../../samples/snippets/csharp/VS_Snippets_Wpf/LocalizationBtn/CS/Pane1.xaml#1)]  
  
 下图演示代码示例的输出。  
  
 ![具有不同语言的文本的同一按钮](../../../../docs/framework/wpf/advanced/media/globalizationbutton.png "GlobalizationButton")  
可自动调整大小的按钮  
  
## 请参阅  
 [使用自动布局概述](../../../../docs/framework/wpf/advanced/use-automatic-layout-overview.md)   
 [使用网格进行自动布局](../../../../docs/framework/wpf/advanced/how-to-use-a-grid-for-automatic-layout.md)