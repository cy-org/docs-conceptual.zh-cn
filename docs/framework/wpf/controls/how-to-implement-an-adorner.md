---
title: "如何：实现装饰器 | Microsoft Docs"
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
  - "装饰器, 实现"
ms.assetid: 56ae32b6-0599-455c-b52f-2ff97e6f1ec2
caps.latest.revision: 8
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 8
---
# 如何：实现装饰器
此示例演示最小装饰器的实现。  
  
## 实现者说明  
 注意：装饰器不包括任何继承呈现行为，确保装饰器呈现是装饰器实施者的责任。  实现呈现行为的常见方式是重写 <xref:System.Windows.UIElement.OnRender%2A> 方法，并使用一个或多个 <xref:System.Windows.Media.DrawingContext> 对象来按需呈现装饰器的视觉效果（如本示例所示）。  
  
## 示例  
  
### 说明  
 您可以通过实现一个从抽象 <xref:System.Windows.Documents.Adorner> 类继承的类来创建自定义装饰器。  本示例装饰器通过重写 <xref:System.Windows.UIElement.OnRender%2A> 方法，使用圆简单地装饰 <xref:System.Windows.UIElement> 的各个角。  
  
### 代码  
 [!code-csharp[Adorners_SimpleCircleAdorner#_SimpleCircleAdornerBody](../../../../samples/snippets/csharp/VS_Snippets_Wpf/Adorners_SimpleCircleAdorner/CSharp/Window1.xaml.cs#_simplecircleadornerbody)]
 [!code-vb[Adorners_SimpleCircleAdorner#_SimpleCircleAdornerBody](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/Adorners_SimpleCircleAdorner/VisualBasic/Window1.xaml.vb#_simplecircleadornerbody)]  
  
## 请参阅  
 [装饰器概述](../../../../docs/framework/wpf/controls/adorners-overview.md)