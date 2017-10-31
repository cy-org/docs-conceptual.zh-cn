---
title: "FolderBrowserDialog 组件概述（Windows 窗体） | Microsoft Docs"
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
  - "FolderBrowserDialog"
dev_langs: 
  - "jsharp"
helpviewer_keywords: 
  - "目录 [Windows 窗体], 在应用程序中支持浏览"
  - "FolderBrowserDialog 组件 [Windows 窗体], 关于 FolderBrowserDialog"
  - "文件夹 [Windows 窗体], 在应用程序中支持浏览"
ms.assetid: 796b622c-3ba9-4356-93bb-e217fc52f2c7
caps.latest.revision: 9
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 9
---
# FolderBrowserDialog 组件概述（Windows 窗体）
Windows 窗体 <xref:System.Windows.Forms.FolderBrowserDialog> 组件是用于浏览和选择文件夹的模式对话框。  也可以从 <xref:System.Windows.Forms.FolderBrowserDialog> 组件内创建新文件夹。  
  
> [!NOTE]
>  若要选择文件而不是文件夹，请使用 [OpenFileDialog](../../../../docs/framework/winforms/controls/openfiledialog-component-windows-forms.md) 组件。  
  
 使用 <xref:System.Windows.Forms.CommonDialog.ShowDialog%2A> 方法，可在运行时显示 <xref:System.Windows.Forms.FolderBrowserDialog> 组件。  设置 <xref:System.Windows.Forms.FolderBrowserDialog.RootFolder%2A> 属性可确定将出现在对话框的树状视图中的顶级文件夹和任何子文件夹。  在对话框显示后，就可以使用 <xref:System.Windows.Forms.FolderBrowserDialog.SelectedPath%2A> 属性获取所选文件夹的路径。  
  
 将 <xref:System.Windows.Forms.FolderBrowserDialog> 组件添加到窗体后，它就会出现在“Windows 窗体设计器”底部的栏中。  
  
## 请参阅  
 <xref:System.Windows.Forms.FolderBrowserDialog>   
 [如何：使用 Windows 窗体 FolderBrowserDialog 组件选择文件夹](../../../../docs/framework/winforms/controls/how-to-choose-folders-with-the-windows-forms-folderbrowserdialog-component.md)   
 [FolderBrowserDialog 组件](../../../../docs/framework/winforms/controls/folderbrowserdialog-component-windows-forms.md)