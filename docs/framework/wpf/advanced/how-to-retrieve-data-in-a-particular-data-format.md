---
title: "如何：以特定数据格式检索数据 | Microsoft Docs"
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
  - "DataFormats 类 [WPF], 检索数据"
  - "DataObject 类 [WPF], 检索数据"
  - "拖放 [WPF], 检索数据"
ms.assetid: a625acf3-1144-44cd-add7-456aefc3859f
caps.latest.revision: 6
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 6
---
# 如何：以特定数据格式检索数据
下面的示例演示如何以指定的格式从数据对象中检索数据。  
  
## 示例  
  
### 说明  
 下面的代码示例使用 <xref:System.Windows.DataObject.GetDataPresent%28System.String%29> 重载先检查指定的数据格式是否可用（本机方式或通过自动转换）；如果指定的格式可用，则该示例使用 <xref:System.Windows.DataObject.GetData%28System.String%29> 方法检索数据。  
  
### 代码  
 [!code-csharp[DragDrop_DragDropMiscCode#_DragDrop_GetSpecificDataFormat](../../../../samples/snippets/csharp/VS_Snippets_Wpf/DragDrop_DragDropMiscCode/CSharp/Window1.xaml.cs#_dragdrop_getspecificdataformat)]
 [!code-vb[DragDrop_DragDropMiscCode#_DragDrop_GetSpecificDataFormat](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/DragDrop_DragDropMiscCode/visualbasic/window1.xaml.vb#_dragdrop_getspecificdataformat)]  
  
## 示例  
  
### 说明  
 下面的代码示例使用 <xref:System.Windows.DataObject.GetDataPresent%28System.String%2CSystem.Boolean%29> 重载先检查指定的数据格式是否本机可用（筛选掉可自动转换的数据格式）；如果指定的格式可用，则该示例使用 <xref:System.Windows.DataObject.GetData%28System.String%29> 方法检索数据。  
  
### 代码  
 [!code-csharp[DragDrop_DragDropMiscCode#_DragDrop_GetSpecificDataFormat_Native](../../../../samples/snippets/csharp/VS_Snippets_Wpf/DragDrop_DragDropMiscCode/CSharp/Window1.xaml.cs#_dragdrop_getspecificdataformat_native)]
 [!code-vb[DragDrop_DragDropMiscCode#_DragDrop_GetSpecificDataFormat_Native](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/DragDrop_DragDropMiscCode/visualbasic/window1.xaml.vb#_dragdrop_getspecificdataformat_native)]  
  
## 请参阅  
 <xref:System.Windows.IDataObject>   
 [拖放概述](../../../../docs/framework/wpf/advanced/drag-and-drop-overview.md)