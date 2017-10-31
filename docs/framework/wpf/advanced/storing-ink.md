---
title: "存储墨迹 | Microsoft Docs"
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
  - "墨迹序列化格式 (ISF) "
  - "墨迹, 存储"
  - "ISF（墨迹序列化格式）"
  - "检索墨迹"
  - "存储墨迹"
ms.assetid: a3f6d16b-d682-4680-9965-907332b4d2b8
caps.latest.revision: 9
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 9
---
# 存储墨迹
<xref:System.Windows.Ink.StrokeCollection.Save%2A> 方法支持将墨迹存储为墨迹序列化格式 \(ISF\)。  <xref:System.Windows.Ink.StrokeCollection> 类的构造函数支持读取墨迹数据。  
  
## 墨迹存储和检索  
 本节讨论如何在 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 平台中存储和检索墨迹。  
  
 下面的示例实现按钮单击事件处理程序，该处理程序向用户呈现一个“保存文件”对话框，并将 <xref:System.Windows.Controls.InkCanvas> 中的墨迹保存为文件。  
  
 [!code-csharp[DigitalInkTopics#12](../../../../samples/snippets/csharp/VS_Snippets_Wpf/DigitalInkTopics/CSharp/Window1.xaml.cs#12)]
 [!code-vb[DigitalInkTopics#12](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/DigitalInkTopics/VisualBasic/Window1.xaml.vb#12)]  
  
 下面的示例实现按钮单击事件处理程序，该处理程序向用户呈现一个“打开文件”对话框，并将文件中的墨迹读取到 <xref:System.Windows.Controls.InkCanvas> 元素中。  
  
 [!code-csharp[DigitalInkTopics#13](../../../../samples/snippets/csharp/VS_Snippets_Wpf/DigitalInkTopics/CSharp/Window1.xaml.cs#13)]
 [!code-vb[DigitalInkTopics#13](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/DigitalInkTopics/VisualBasic/Window1.xaml.vb#13)]  
  
## 请参阅  
 <xref:System.Windows.Controls.InkCanvas>   
 [Windows Presentation Foundation](../../../../docs/framework/wpf/index.md)