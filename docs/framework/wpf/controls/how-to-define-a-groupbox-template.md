---
title: "如何：定义 GroupBox 模板 | Microsoft Docs"
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
  - "控件, GroupBox"
  - "GroupBox 控件, 创建模板"
ms.assetid: 85a4d1a7-4753-4f4a-b26d-14fa10c1ddb5
caps.latest.revision: 9
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 9
---
# 如何：定义 GroupBox 模板
本示例演示如何为 <xref:System.Windows.Controls.GroupBox> 控件创建模板。  
  
## 示例  
 下面的示例通过为布局使用 <xref:System.Windows.Controls.Grid> 控件来定义 <xref:System.Windows.Controls.GroupBox> 控件模板。  该模板使用 <xref:System.Windows.Controls.BorderGapMaskConverter> 定义 <xref:System.Windows.Controls.GroupBox> 的边框，以使边框不会遮盖 <xref:System.Windows.Controls.HeaderedContentControl.Header%2A> 内容。  
  
 [!code-xml[GroupBoxSnippet#GroupBoxTemplate](../../../../samples/snippets/csharp/VS_Snippets_Wpf/GroupBoxSnippet/CS/Window1.xaml#groupboxtemplate)]  
  
## 请参阅  
 <xref:System.Windows.Controls.GroupBox>   
 [GroupBox How\-to Topics](http://msdn.microsoft.com/zh-cn/7692e155-a4c6-428c-b7e0-64b3740daca7)