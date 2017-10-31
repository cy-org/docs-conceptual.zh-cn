---
title: "SaveFileDialog 组件概述（Windows 窗体） | Microsoft Docs"
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
  - "SaveFileDialog"
dev_langs: 
  - "jsharp"
helpviewer_keywords: 
  - "保存文件对话框, 显示"
  - "SaveFileDialog 组件, 关于 SaveFileDialog"
ms.assetid: be7a625f-46fd-4d06-9985-b613dcbf9bd2
caps.latest.revision: 9
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 9
---
# SaveFileDialog 组件概述（Windows 窗体）
Windows 窗体 <xref:System.Windows.Forms.SaveFileDialog> 组件是一个预先配置的对话框。  它与 Windows 使用的标准**“保存文件”**对话框相同。  该组件继承自 <xref:System.Windows.Forms.CommonDialog> 类。  
  
## 使用 SaveFileDialog 组件  
 使用该控件作为一个简单的解决方案，使用户能够保存文件，而不用配置您自己的对话框。  利用标准的 Windows 对话框，创建基本功能可立即为用户所熟悉的应用程序。  但是应注意，使用 <xref:System.Windows.Forms.SaveFileDialog> 组件时，必须编写您自己的文件保存逻辑。  
  
 可使用 <xref:System.Windows.Forms.CommonDialog.ShowDialog%2A> 方法在运行时显示对话框。  使用 <xref:System.Windows.Forms.SaveFileDialog.OpenFile%2A> 方法可在读\/写模式下打开文件。  
  
 将 <xref:System.Windows.Forms.SaveFileDialog> 组件添加到窗体后，它出现在 Windows 窗体设计器底部的栏中。  
  
## 请参阅  
 <xref:System.Windows.Forms.SaveFileDialog>   
 [SaveFileDialog 组件](../../../../docs/framework/winforms/controls/savefiledialog-component-windows-forms.md)