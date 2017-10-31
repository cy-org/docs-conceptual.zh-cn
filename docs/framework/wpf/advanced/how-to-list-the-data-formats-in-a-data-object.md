---
title: "如何：列出数据对象中的数据格式 | Microsoft Docs"
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
  - "数据格式 [WPF], 列出"
  - "DataFormats 类 [WPF]"
  - "拖放 [WPF], 列出数据格式"
ms.assetid: 18e7ba4b-ccef-4815-ae2d-3a32891010c0
caps.latest.revision: 5
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 5
---
# 如何：列出数据对象中的数据格式
下面的示例演示如何使用 <xref:System.Windows.DataObject.GetFormats%2A> 方法重载获取一个字符串数组，该数组表示某数据对象中可用的所有数据格式。  
  
## 示例  
  
### 说明  
 下面的代码示例使用 <xref:System.Windows.DataObject.GetFormats%2A> 重载获取一个字符串数组，该数组用于表示某数据对象中可用的所有数据格式（包括本机和可自动转换的格式）。  
  
### 代码  
 [!code-csharp[DragDrop_DragDropMiscCode#_DragDrop_GetAllDataFormats](../../../../samples/snippets/csharp/VS_Snippets_Wpf/DragDrop_DragDropMiscCode/CSharp/Window1.xaml.cs#_dragdrop_getalldataformats)]
 [!code-vb[DragDrop_DragDropMiscCode#_DragDrop_GetAllDataFormats](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/DragDrop_DragDropMiscCode/visualbasic/window1.xaml.vb#_dragdrop_getalldataformats)]  
  
## 示例  
  
### 说明  
 下面的代码示例使用 <xref:System.Windows.DataObject.GetFormats%2A> 重载获取一个字符串数组，该数组仅表示某数据对象中可用的数据格式（筛选出可自动转换的数据格式）。  
  
### 代码  
 [!code-csharp[DragDrop_DragDropMiscCode#_DragDrop_GetAllDataFormats_NativeOnly](../../../../samples/snippets/csharp/VS_Snippets_Wpf/DragDrop_DragDropMiscCode/CSharp/Window1.xaml.cs#_dragdrop_getalldataformats_nativeonly)]
 [!code-vb[DragDrop_DragDropMiscCode#_DragDrop_GetAllDataFormats_NativeOnly](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/DragDrop_DragDropMiscCode/visualbasic/window1.xaml.vb#_dragdrop_getalldataformats_nativeonly)]  
  
## 请参阅  
 <xref:System.Windows.IDataObject>   
 [拖放概述](../../../../docs/framework/wpf/advanced/drag-and-drop-overview.md)