---
title: "手写识别 | Microsoft Docs"
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
  - "手写识别"
  - "手写识别"
ms.assetid: f4e8576d-e731-4bac-9818-22e2ae636636
caps.latest.revision: 11
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 9
---
# 手写识别
本节讨论了与 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 平台中数字墨迹有关的识别的基本知识。  
  
## 识别解决方案  
 下面的示例演示如何使用 <xref:System.Windows.Ink.InkAnalyzer> 识别墨迹。  
  
> [!NOTE]
>  此示例要求在系统上安装手写识别器。  
  
 在 Visual Studio 2005 中创建一个名为 InkRecognition 的新 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 应用程序项目。  用下列 XAML 代码替换 Window1.xaml 文件的内容。  此代码将呈现应用程序的用户界面。  
  
 [!code-xml[InkRecognition#1](../../../../samples/snippets/csharp/VS_Snippets_Wpf/InkRecognition/CSharp/Window1.xaml#1)]  
  
 添加对 WPF 墨迹分析程序集、IAWinFX.dll、IACore.dll 和 IALoader.dll 的引用，这些内容可以在 \\Program Files\\Reference Assemblies\\Microsoft\\Tablet PC\\v1.7 中找到。  用下列代码替换代码隐藏文件的内容。  
  
 [!code-csharp[InkRecognition#2](../../../../samples/snippets/csharp/VS_Snippets_Wpf/InkRecognition/CSharp/Window1.xaml.cs#2)]
 [!code-vb[InkRecognition#2](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/InkRecognition/VisualBasic/Window1.xaml.vb#2)]  
  
## 请参阅  
 <xref:System.Windows.Ink.InkAnalyzer>   
 <xref:System.Windows.Ink.AnalysisStatus>   
 <xref:System.Windows.Controls.InkCanvas>