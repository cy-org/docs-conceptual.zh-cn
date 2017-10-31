---
title: "如何：装饰面板的子级 | Microsoft Docs"
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
  - "装饰器, 绑定到面板的子级"
  - "Panel 控件, 将装饰器绑定到子级"
ms.assetid: 4cc9b972-b472-4e5c-bdf3-3702d7fbb1f5
caps.latest.revision: 9
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 9
---
# 如何：装饰面板的子级
此示例演示如何以编程方式将装饰器绑定到指定的 <xref:System.Windows.Controls.Panel> 的子级。  
  
## 示例  
 若要将装饰器绑定到 <xref:System.Windows.Controls.Panel> 的子级，请按照下列步骤操作：  
  
1.  声明一个新的 <xref:System.Windows.Documents.AdornerLayer> 对象并调用 `static` <xref:System.Windows.Documents.AdornerLayer.GetAdornerLayer%2A> 方法来查找要对其子级进行装饰的元素的装饰器层。  
  
2.  依次枚举父元素的子级并调用 <xref:System.Windows.Documents.AdornerLayer.Add%2A> 方法将装饰器绑定到每个子级元素。  
  
 以下示例将 SimpleCircleAdorner（如上所示）绑定到名为 *myStackPanel* 的 <xref:System.Windows.Controls.StackPanel> 的子级。  
  
 [!code-csharp[Adorners_SimpleCircleAdorner#_AdornChildren](../../../../samples/snippets/csharp/VS_Snippets_Wpf/Adorners_SimpleCircleAdorner/CSharp/Window1.xaml.cs#_adornchildren)]
 [!code-vb[Adorners_SimpleCircleAdorner#_AdornChildren](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/Adorners_SimpleCircleAdorner/VisualBasic/Window1.xaml.vb#_adornchildren)]  
  
> [!NOTE]
>  目前不支持使用[!INCLUDE[TLA#tla_xaml](../../../../includes/tlasharptla-xaml-md.md)] 将装饰器绑定到另一个元素。  
  
## 请参阅  
 [装饰器概述](../../../../docs/framework/wpf/controls/adorners-overview.md)