---
title: "OpenFileDialog 组件概述（Windows 窗体） | Microsoft Docs"
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
  - "OpenFileDialog"
dev_langs: 
  - "jsharp"
helpviewer_keywords: 
  - "“打开文件”对话框, 在 Windows 窗体中显示"
  - "OpenFileDialog 组件, 关于 OpenFileDialog"
ms.assetid: cd717300-46b6-4f82-8207-b218fa7fa407
caps.latest.revision: 10
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 10
---
# OpenFileDialog 组件概述（Windows 窗体）
Windows 窗体 <xref:System.Windows.Forms.OpenFileDialog> 组件是一个预先配置的对话框。  它与 Windows 操作系统所公开的**“打开文件”**对话框相同。  该组件继承自 <xref:System.Windows.Forms.CommonDialog> 类。  
  
## 使用此组件  
 在基于 Windows 的应用程序中可将该组件用作简单的文件选择解决方案，而不用配置您自己的对话框。  利用标准的 Windows 对话框，您可以创建其基本功能可立即为用户所熟悉的应用程序。  但是应注意，使用 <xref:System.Windows.Forms.OpenFileDialog> 组件时，必须编写您自己的文件打开逻辑。  
  
 可使用 <xref:System.Windows.Forms.CommonDialog.ShowDialog%2A> 方法在运行时显示对话框。  使用 <xref:System.Windows.Forms.OpenFileDialog.Multiselect%2A> 属性可使用户选择多个要打开的文件。  另外，可使用 <xref:System.Windows.Forms.OpenFileDialog.ShowReadOnly%2A> 属性确定在对话框中是否出现只读复选框。  <xref:System.Windows.Forms.OpenFileDialog.ReadOnlyChecked%2A> 属性指示是否选中只读复选框。  最后，<xref:System.Windows.Forms.FileDialog.Filter%2A> 属性设置当前文件名筛选字符串，该字符串确定出现在对话框的“文件类型”框中的选项。  
  
 将 <xref:System.Windows.Forms.OpenFileDialog> 组件添加到窗体后，它出现在 Windows 窗体设计器底部的栏中。  
  
## 请参阅  
 <xref:System.Windows.Forms.OpenFileDialog>   
 [OpenFileDialog 组件](../../../../docs/framework/winforms/controls/openfiledialog-component-windows-forms.md)