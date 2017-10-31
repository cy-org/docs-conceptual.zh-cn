---
title: "如何：使用网格进行自动布局 | Microsoft Docs"
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
  - "自动布局, 网格使用"
  - "网格, 自动布局"
ms.assetid: ab9de407-e0c1-4047-bdf0-24951bf73879
caps.latest.revision: 13
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 10
---
# 如何：使用网格进行自动布局
本示例介绍如何在自动布局方法中使用网格来创建可本地化的应用程序。  
  
 [!INCLUDE[TLA#tla_ui](../../../../includes/tlasharptla-ui-md.md)] 的本地化是一个很耗时的过程。  通常，本地化人员除了需要翻译文本之外，还需要重新调整元素的大小并重新定位元素。  过去，要针对任何一种语言改编 [!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)] 都需要进行调整。  现在，使用 [!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)] 的功能，您可以对元素进行设计以减少必需的调整工作。  这种编写可以更方便地调整大小和重新定位的应用程序的方法称为 `auto layout`。  
  
 下面的[!INCLUDE[TLA#tla_xaml](../../../../includes/tlasharptla-xaml-md.md)] 示例演示如何使用网格来定位某些按钮和文本。  请注意，单元格的高度和宽度设置为 `Auto`；因此，包含带图像按钮的单元格会进行调整以适应此图像。  因为 <xref:System.Windows.Controls.Grid> 元素可以根据内容进行调整，所以在采用自动布局方法来设计可本地化的应用程序时，此元素非常有用。  
  
## 示例  
 下面的示例演示如何使用网格。  
  
 [!code-xml[LocalizationGrid#1](../../../../samples/snippets/csharp/VS_Snippets_Wpf/LocalizationGrid/CS/Pane1.xaml#1)]  
  
 下图显示了代码示例的输出。  
  
 ![网格示例](../../../../docs/framework/wpf/advanced/media/glob-grid.png "glob\_grid")  
网格  
  
## 请参阅  
 [使用自动布局概述](../../../../docs/framework/wpf/advanced/use-automatic-layout-overview.md)   
 [使用自动布局创建按钮](../../../../docs/framework/wpf/advanced/how-to-use-automatic-layout-to-create-a-button.md)