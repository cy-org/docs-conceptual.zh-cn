---
title: "如何：在 TextBox 控件中启用制表符 | Microsoft Docs"
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
  - "制表符, 启用"
  - "TextBox 控件, 启用制表符"
ms.assetid: 14b1b064-61f7-4958-be63-88d85b868d03
caps.latest.revision: 8
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 8
---
# 如何：在 TextBox 控件中启用制表符
本示例演示如何将制表符接受为 <xref:System.Windows.Controls.TextBox> 控件中的正常输入。  
  
## 示例  
 若要将制表符接受为 <xref:System.Windows.Controls.TextBox> 控件中的输入，请将 <xref:System.Windows.Controls.Primitives.TextBoxBase.AcceptsTab%2A> 特性设置为 **true**。  
  
 [!code-xml[TextBox_EnablingTab#_AcceptsTab](../../../../samples/snippets/csharp/VS_Snippets_Wpf/TextBox_EnablingTab/CS/Window1.xaml#_acceptstab)]  
  
## 请参阅  
 [TextBox 概述](../../../../docs/framework/wpf/controls/textbox-overview.md)   
 [RichTextBox 概述](../../../../docs/framework/wpf/controls/richtextbox-overview.md)