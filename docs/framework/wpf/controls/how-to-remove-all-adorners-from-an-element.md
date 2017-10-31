---
title: "如何：从元素移除所有装饰器 | Microsoft Docs"
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
  - "装饰器, 移除"
ms.assetid: fe5303a3-b76e-4643-aafb-51419032b47b
caps.latest.revision: 10
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 10
---
# 如何：从元素移除所有装饰器
此示例演示如何以编程方式从指定的 <xref:System.Windows.UIElement> 中移除所有的装饰器。  
  
## 示例  
 此详细的代码示例移除由 <xref:System.Windows.Documents.AdornerLayer.GetAdorners%2A> 返回的装饰器数组中的所有装饰器。  此示例恰好从名为 *myTextBox* 的 <xref:System.Windows.UIElement> 中检索装饰器。  如果在对 <xref:System.Windows.Documents.AdornerLayer.GetAdorners%2A> 的调用中指定的元素没有装饰器，则返回 `null`。  此代码显式检查 null 数组，最适用于其中 null 数组相对来说应比较常见的应用程序。  
  
 [!code-csharp[AdornersMiscCode#_RemoveAllAdornersLong](../../../../samples/snippets/csharp/VS_Snippets_Wpf/AdornersMiscCode/CSharp/Window1.xaml.cs#_removealladornerslong)]
 [!code-vb[AdornersMiscCode#_RemoveAllAdornersLong](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/AdornersMiscCode/visualbasic/window1.xaml.vb#_removealladornerslong)]  
  
## 示例  
 此简化的代码示例在功能上等效于上述详细示例。  此代码不显式检查 null 数组，因此可能会引发一个 <xref:System.NullReferenceException> 异常。  此代码最适用于其中应很少出现 null 数组的应用程序。  
  
 [!code-csharp[AdornersMiscCode#_RemoveAllAdornersShort](../../../../samples/snippets/csharp/VS_Snippets_Wpf/AdornersMiscCode/CSharp/Window1.xaml.cs#_removealladornersshort)]
 [!code-vb[AdornersMiscCode#_RemoveAllAdornersShort](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/AdornersMiscCode/visualbasic/window1.xaml.vb#_removealladornersshort)]  
  
## 请参阅  
 [装饰器概述](../../../../docs/framework/wpf/controls/adorners-overview.md)