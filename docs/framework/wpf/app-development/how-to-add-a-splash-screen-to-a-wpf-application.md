---
title: "如何：将初始屏幕添加到 WPF 应用程序 | Microsoft Docs"
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
  - "初始屏幕 [WPF]"
  - "SplashScreen 类 [WPF]"
  - "启动窗口 [WPF]"
  - "WPF, 初始屏幕"
ms.assetid: d70a25c4-5fb9-4c27-b01d-b1b8ef39b3fd
caps.latest.revision: 14
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 14
---
# 如何：将初始屏幕添加到 WPF 应用程序
本主题介绍如何将启动窗口（也称为“初始屏幕”）添加到 Windows Presentation Foundation \(WPF\) 应用程序。  
  
### 添加现有图像作为初始屏幕  
  
1.  创建或查找要用于初始屏幕的图像。  可以使用 Windows 图像处理组件 \(WIC\) 支持的任何图像格式。  例如，可以使用 BMP、GIF、JPEG、PNG 或 TIFF 格式。  
  
2.  将图像文件添加到 WPF 应用程序项目。  有关更多信息，请参见[NIB:How to: Add Existing Items to a Project](http://msdn.microsoft.com/zh-cn/15f4cfb7-78ab-457f-9f14-099a25a6a2d3)。  
  
3.  在解决方案资源管理器中选择该图像。  
  
4.  在“属性”窗口中，单击**“生成操作”**属性的下拉箭头。  
  
5.  从下拉列表中选择**“SplashScreen”**。  
  
    > [!NOTE]
    >  如果没有看到**“SplashScreen”**选项，请务必检查您使用的是否为 [!INCLUDE[vs_orcas_long](../../../../includes/vs-orcas-long-md.md)] SP1 或更高版本。  
  
6.  按 F5 生成并运行该应用程序。  
  
     初始屏幕图像显示在屏幕中间，当主应用程序窗口显示时，该图像将淡出。  
  
### 将初始屏幕从应用程序中移除  
  
1.  在解决方案资源管理器中选择初始屏幕图像。  
  
2.  在“属性”窗口中，将**“生成操作”**设置为**“无”**。  
  
### 将初始屏幕从应用程序中移除  
  
-   在解决方案资源管理器中删除初始屏幕图像。  
  
-   从项目中排除初始屏幕图像。  
  
## 请参阅  
 <xref:System.Windows.SplashScreen>   
 [NIB:How to: Add Existing Items to a Project](http://msdn.microsoft.com/zh-cn/15f4cfb7-78ab-457f-9f14-099a25a6a2d3)