---
title: "如何：枚举系统字体 | Microsoft Docs"
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
  - "枚举, 系统字体"
  - "字体, 枚举"
  - "系统字体, 枚举"
  - "版式, 枚举系统字体"
ms.assetid: 36e37791-55b9-4f01-a496-5cc10335e6a6
caps.latest.revision: 9
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 9
---
# 如何：枚举系统字体
## 示例  
 下面的示例演示如何枚举系统字体集合中的字体。  将 <xref:System.Windows.Media.Fonts.SystemFontFamilies%2A> 中的每一个 <xref:System.Windows.Media.FontFamily> 字体系列的名称作为一项添加到组合框中。  
  
 [!code-csharp[TextOverview#100](../../../../samples/snippets/csharp/VS_Snippets_Wpf/TextOverview/CSharp/Window1.xaml.cs#100)]
 [!code-vb[TextOverview#100](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/TextOverview/visualbasic/window1.xaml.vb#100)]  
  
 如果同一字体系列的多个版本位于同一目录，则 [!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)] 字体枚举返回字体的最新版本。  如果版本信息不提供解析，则返回具有最新时间戳的字体。  如果时间戳信息相等，则返回字母排序为第一的字体文件。