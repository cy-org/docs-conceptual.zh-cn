---
title: "如何：将装饰器绑定到元素 | Microsoft Docs"
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
  - "装饰器, 绑定到指定的 UIElements"
  - "UIElements, 将装饰器绑定到"
ms.assetid: b2101611-a0ee-4137-bdb8-9b3673d2e6b9
caps.latest.revision: 10
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 10
---
# 如何：将装饰器绑定到元素
此示例演示如何以编程方式将装饰器绑定到指定的 <xref:System.Windows.UIElement>。  
  
## 示例  
 若要将装饰器绑定到特定的 <xref:System.Windows.UIElement>，请按照以下步骤操作：  
  
1.  调用 `static` 方法 <xref:System.Windows.Documents.AdornerLayer.GetAdornerLayer%2A>，为要装饰的 <xref:System.Windows.UIElement> 获得 <xref:System.Windows.Documents.AdornerLayer> 对象。  <xref:System.Windows.Documents.AdornerLayer.GetAdornerLayer%2A> 从指定的 **UIElement** 开始沿着可视化树向上行进，返回它所发现的第一个装饰器层。  （如果未发现装饰器层，则该方法返回 Null。）  
  
2.  调用 <xref:System.Windows.Documents.AdornerLayer.Add%2A> 方法将装饰器绑定到目标 **UIElement**。  
  
 以下示例将 SimpleCircleAdorner（如上所示）绑定到名为 *myTextBox* 的 <xref:System.Windows.Controls.TextBox>。  
  
 [!code-csharp[Adorners_SimpleCircleAdorner#_AdornSingleElement](../../../../samples/snippets/csharp/VS_Snippets_Wpf/Adorners_SimpleCircleAdorner/CSharp/Window1.xaml.cs#_adornsingleelement)]
 [!code-vb[Adorners_SimpleCircleAdorner#_AdornSingleElement](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/Adorners_SimpleCircleAdorner/VisualBasic/Window1.xaml.vb#_adornsingleelement)]  
  
> [!NOTE]
>  目前不支持使用[!INCLUDE[TLA#tla_xaml](../../../../includes/tlasharptla-xaml-md.md)] 将装饰器绑定到另一个元素。  
  
## 请参阅  
 [装饰器概述](../../../../docs/framework/wpf/controls/adorners-overview.md)