---
title: "示例 OpenType 字体包 | Microsoft Docs"
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
  - "字体, OpenType 字体包"
  - "OpenType 字体包"
  - "版式, OpenType 字体包"
ms.assetid: 56b46fa1-a44e-419b-8f14-25ad51c715c3
caps.latest.revision: 23
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 22
---
# 示例 OpenType 字体包
本主题概述随 [!INCLUDE[TLA2#tla_wcsdk](../../../../includes/tla2sharptla-wcsdk-md.md)] 一起分发的示例 [!INCLUDE[TLA#tla_opentype](../../../../includes/tlasharptla-opentype-md.md)] 字体。  这些示例字体支持可供 [!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)] 应用程序使用的 [!INCLUDE[TLA#tla_opentype](../../../../includes/tlasharptla-opentype-md.md)] 扩展功能。  
  
   
  
<a name="overview"></a>   
## OpenType 字体包中的字体  
 [!INCLUDE[TLA2#tla_wcsdk](../../../../includes/tla2sharptla-wcsdk-md.md)] 提供一组可用来创建 [!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)] 应用程序的示例 [!INCLUDE[TLA#tla_opentype](../../../../includes/tlasharptla-opentype-md.md)] 字体。  这些示例字体在 Ascender Corporation 的许可下提供。  它们仅实现由 [!INCLUDE[TLA#tla_opentype](../../../../includes/tlasharptla-opentype-md.md)] 格式所定义的全部功能的一部分。  下表列出了示例 [!INCLUDE[TLA#tla_opentype](../../../../includes/tlasharptla-opentype-md.md)] 字体的名称。  
  
|**名称**|**文件**|  
|------------|------------|  
|Kootenay|Kooten.ttf|  
|Lindsey|Linds.ttf|  
|Miramonte|Miramo.ttf|  
|Miramonte Bold|Miramob.ttf|  
|Pericles|Peric.ttf|  
|Pericles Light|Pericl.ttf|  
|Pescadero|Pesca.ttf|  
|Pescadero Bold|Pescab.ttf|  
  
 示例 [!INCLUDE[TLA#tla_opentype](../../../../includes/tlasharptla-opentype-md.md)] 字体类似于下图所示。  
  
 ![示例字体包中的字体名称列表](../../../../docs/framework/wpf/advanced/media/samplefontpack01.png "samplefontpack01")  
OpenType 字体包中的字体  
  
 这些示例字体在 Ascender Corporation 的许可下提供。  Ascender 是一家高级字体产品提供商。  若要对示例字体的扩展版本或自定义版本进行授权，请参见 [Ascender Corporation's Web site](http://go.microsoft.com/fwlink/?LinkId=182627)（Ascender Corporation 的网站）。  
  
> [!NOTE]
>  作为开发人员，您有责任确保您具有在应用程序中嵌入的任何字体所必需的许可权限，否则请重新发布。  
  
<a name="installing_the_fonts"></a>   
## 安装字体  
 您可以选择将示例 [!INCLUDE[TLA#tla_opentype](../../../../includes/tlasharptla-opentype-md.md)] 字体安装到以下默认的 [!INCLUDE[TLA#tla_mswin](../../../../includes/tlasharptla-mswin-md.md)] 字体目录：**\\WINDOWS\\Fonts**。  使用“字体”控制面板可安装字体。  一旦这些字体安装到您的计算机上，引用默认的 [!INCLUDE[TLA#tla_mswin](../../../../includes/tlasharptla-mswin-md.md)] 字体的所有应用程序就都可以使用这些字体。您可以通过双击字体文件以多种字体大小来显示具有代表性的字符集。  下面的屏幕快照显示 Lindsey 字体文件 Linds.ttf。  
  
 ![Lindsey 字体 &#40;OpenType&#41;](../../../../docs/framework/wpf/advanced/media/typographyinwpf-04.png "TypographyInWPF\_04")  
显示 Lindsey 字体  
  
<a name="using_the_fonts"></a>   
## 使用字体  
 可以通过两种方法在应用程序中使用字体。  您可以将字体作为项目内容项添加到应用程序中，这些项目内容项不会作为资源嵌入到程序集中。  此外，您还可以将字体作为嵌入到应用程序的程序集文件中的项目资源项添加到应用程序中。  有关更多信息，请参见[将字体与应用程序一起打包](../../../../docs/framework/wpf/advanced/packaging-fonts-with-applications.md)。  
  
## 请参阅  
 <xref:System.Windows.Documents.Typography>   
 [OpenType 字体功能](../../../../docs/framework/wpf/advanced/opentype-font-features.md)   
 [将字体与应用程序一起打包](../../../../docs/framework/wpf/advanced/packaging-fonts-with-applications.md)