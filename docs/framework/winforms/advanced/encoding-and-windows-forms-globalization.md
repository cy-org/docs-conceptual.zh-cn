---
title: "编码和 Windows 窗体全球化 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-winforms"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "jsharp"
helpviewer_keywords: 
  - "DateTimePicker 控件 [Windows 窗体], 缺乏 Unicode 支持"
  - "全球化 [Windows 窗体], 字符集"
  - "ImageList 组件 [Windows 窗体], 缺乏 Unicode 支持"
  - "国际应用程序 [Windows 窗体], 字符显示"
  - "国际字符"
  - "ListView 控件 [Windows 窗体], 缺乏 Unicode 支持"
  - "本地化 [Windows 窗体], 字符集"
  - "MonthCalendar 控件 [Windows 窗体], 缺乏 Unicode 支持"
  - "ProgressBar 控件 [Windows 窗体], 启用 Unicode 的窗体"
  - "StatusBar 控件 [Windows 窗体], 缺乏 Unicode 支持"
  - "TabControl 控件 [Windows 窗体], 缺乏 Unicode 支持"
  - "ToolBar 控件 [Windows 窗体], 缺乏 Unicode 支持"
  - "TrackBar 控件 [Windows 窗体], 缺乏 Unicode 支持"
  - "TreeView 控件 [Windows 窗体], 缺乏 Unicode 支持"
  - "Unicode [Windows 窗体]"
  - "Windows 窗体, 编码"
ms.assetid: 22e8965d-a712-42b3-8167-3ee346bd70f9
caps.latest.revision: 9
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 9
---
# 编码和 Windows 窗体全球化
Windows 窗体应用程序完全支持 Unicode，这意味着每个字符都用唯一编号表示，无论何种平台、程序或语音都是如此。  有关 Unicode 的详细信息，请参阅 [Unicode 联盟网站](http://www.unicode.org)。  
  
## Unicode 的优点  
 启用 Unicode 的窗体的优点包括，能够处理仅限 Unicode（例如印地语）的脚本。  此外，还可以在单个窗体上使用多种语言。  以 Unicode 格式，所有字符都是两个字节长，所以不需要执行任何特殊操作来表示双字节字符。  还可以编写可在所有平台上工作的单个代码集。  这一点不同于 [!INCLUDE[vbprvb](../../../../includes/vbprvb-md.md)] 的以前版本，在以前版本中，你必须针对不同的平台（例如 Windows NT 和 [!INCLUDE[win98](../../../../includes/win98-md.md)]）编写不同的代码。  
  
 但是，某些控件不支持在 [!INCLUDE[win98](../../../../includes/win98-md.md)] 和 Windows Millennium Edition 中启用 Unicode。  全部继承自公共控件的这些控件将使用 Windows 代码页（例如 [!INCLUDE[vcpransi](../../../../includes/vcpransi-md.md)]）处理数据。  这些控件包括：<xref:System.Windows.Forms.TabControl>、￼<xref:System.Windows.Forms.TreeView>、￼<xref:System.Windows.Forms.DateTimePicker>、￼<xref:System.Windows.Forms.MonthCalendar>、￼<xref:System.Windows.Forms.TrackBar>、￼<xref:System.Windows.Forms.ProgressBar>、￼<xref:System.Windows.Forms.ImageList>、￼<xref:System.Windows.Forms.ToolBar>、<xref:System.Windows.Forms.ToolBar> 和 <xref:System.Windows.Forms.StatusBar>。  因此，不能在列出的平台上的这些控件中显示 Unicode 数据。  例如，不能在英语版 [!INCLUDE[win98](../../../../includes/win98-md.md)] 操作系统上显示日语字符。  
  
 对于 <xref:System.Windows.Forms.ToolBar> 和 <xref:System.Windows.Forms.StatusBar> 控件具有 Unicode 意识的替代项，可使用 <xref:System.Windows.Forms.ToolStrip> 和 <xref:System.Windows.Forms.StatusStrip> 控件替换这些旧控件。  要想维护应用程序中各可视化元素之间的外观和感觉，可使用用于呈现菜单的 <xref:System.Windows.Forms.MenuStrip> 控件代替 <xref:System.Windows.Forms.MainMenu>。  正如 <xref:System.Windows.Forms.ToolStrip> 和 <xref:System.Windows.Forms.StatusStrip> 一样，<xref:System.Windows.Forms.MenuStrip> 还可以处理和显示 Unicode 字符。  
  
## 请参阅  
 [全球化 Windows 窗体](../../../../docs/framework/winforms/advanced/globalizing-windows-forms.md)