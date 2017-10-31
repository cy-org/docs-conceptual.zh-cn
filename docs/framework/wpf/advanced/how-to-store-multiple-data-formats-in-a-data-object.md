---
title: "如何：在数据对象中存储多种数据格式 | Microsoft Docs"
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
  - "DataFormats 类 [WPF], 存储多个格式"
  - "DataObject 类 [WPF], 存储多个格式"
  - "拖放 [WPF], 存储多个格式"
ms.assetid: 941ace29-29c4-4c26-b75b-ea7d06aa0d69
caps.latest.revision: 6
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 6
---
# 如何：在数据对象中存储多种数据格式
下面的示例演示如何使用 <xref:System.Windows.DataObject.SetData%28System.String%2CSystem.Object%29> 方法将数据以多种格式添加到数据对象中。  
  
## 示例  
  
### 说明  
  
### 代码  
 [!code-csharp[DragDrop_DragDropMiscCode#_DragDrop_StoreMultipleFormats](../../../../samples/snippets/csharp/VS_Snippets_Wpf/DragDrop_DragDropMiscCode/CSharp/Window1.xaml.cs#_dragdrop_storemultipleformats)]
 [!code-vb[DragDrop_DragDropMiscCode#_DragDrop_StoreMultipleFormats](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/DragDrop_DragDropMiscCode/visualbasic/window1.xaml.vb#_dragdrop_storemultipleformats)]  
  
## 请参阅  
 <xref:System.Windows.IDataObject>   
 [拖放概述](../../../../docs/framework/wpf/advanced/drag-and-drop-overview.md)