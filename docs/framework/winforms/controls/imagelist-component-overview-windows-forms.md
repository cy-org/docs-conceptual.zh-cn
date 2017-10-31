---
title: "ImageList 组件概述（Windows 窗体） | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-winforms"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "ImageList"
dev_langs: 
  - "jsharp"
helpviewer_keywords: 
  - "集合控件, 图像"
  - "图标列表控件"
  - "ImageList 组件 [Windows 窗体], 关于 ImageList 组件"
ms.assetid: 7e25d89b-5633-40c1-afc3-82e0e301ffa2
caps.latest.revision: 8
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 8
---
# ImageList 组件概述（Windows 窗体）
Windows 窗体 <xref:System.Windows.Forms.ImageList> 组件用于存储图像，此图像之后可由控件显示。  借助图像列表，你可为图像的单个一致目录编写代码。  例如，只需更改按钮的 <xref:System.Windows.Forms.ButtonBase.ImageIndex%2A> 或 <xref:System.Windows.Forms.ButtonBase.ImageKey%2A> 属性，即可旋转 <xref:System.Windows.Forms.Button> 控件显示的图像。  还可将相同图像列表与多个控件关联。  例如，如果同时使用 <xref:System.Windows.Forms.ListView> 控件和 <xref:System.Windows.Forms.TreeView> 控件来显示相同的文件列表，更改文件在图像列表中的图标将导致新图标显示在这两个视图中。  
  
## 将 ImageList 与控件一起使用  
 可将图像列表与任何具有 `ImageList` 属性的控件一同使用，如果与 <xref:System.Windows.Forms.ListView> 控件一同使用，则此控件要具有 <xref:System.Windows.Forms.ListView.SmallImageList%2A> 和 <xref:System.Windows.Forms.ListView.LargeImageList%2A> 属性。  可与图像列表关联的控件包括：<xref:System.Windows.Forms.ListView>、<xref:System.Windows.Forms.TreeView>、<xref:System.Windows.Forms.ToolBar>、<xref:System.Windows.Forms.TabControl>、<xref:System.Windows.Forms.Button><xref:System.Windows.Forms.CheckBox>、<xref:System.Windows.Forms.RadioButton> 和 <xref:System.Windows.Forms.Label> 控件。  若要将图像列表与控件关联，请将控件的 `ImageList` 属性设置为 <xref:System.Windows.Forms.ImageList> 组件的名称。  
  
## 键属性  
 <xref:System.Windows.Forms.ImageList> 组件的键属性是 <xref:System.Windows.Forms.ImageList.Images%2A>，其中包含关联控件使用的图片。  可通过相应的索引值或键访问每张单独的图像。  <xref:System.Windows.Forms.ImageList.ColorDepth%2A> 属性确定图像呈现的颜色数。  由 <xref:System.Windows.Forms.ImageList.ImageSize%2A> 属性设置后，图像将以相同大小显示。  较大的图像将调整为合适大小。  
  
 如果正在使用 [!INCLUDE[vsprvslong](../../../../includes/vsprvslong-md.md)]，则有权访问可在应用程序中使用的大型标准图像库。  
  
## 请参阅  
 <xref:System.Windows.Forms.ImageList>   
 [如何：使用 Windows 窗体 ImageList 组件添加或移除图像](../../../../docs/framework/winforms/controls/how-to-add-or-remove-images-with-the-windows-forms-imagelist-component.md)