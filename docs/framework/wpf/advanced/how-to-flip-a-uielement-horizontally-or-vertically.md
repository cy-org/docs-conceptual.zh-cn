---
title: "如何：水平或垂直翻转 UIElement | Microsoft Docs"
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
  - "翻转 UIElements"
  - "UIElements, 翻转"
ms.assetid: 02c6730f-65c0-40d5-a553-4cb663721882
caps.latest.revision: 4
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 4
---
# 如何：水平或垂直翻转 UIElement
本示例演示如何使用 <xref:System.Windows.Media.ScaleTransform> 水平或垂直翻转 <xref:System.Windows.UIElement>。  在本示例中，通过向一个 <xref:System.Windows.UIElement> 类型的 <xref:System.Windows.Controls.Button> 控件的 <xref:System.Windows.UIElement.RenderTransform%2A> 属性应用 <xref:System.Windows.Media.ScaleTransform> 来翻转该控件。  
  
## 示例  
 下图显示要翻转的按钮。  
  
 ![无变换的按钮](../../../../docs/framework/wpf/advanced/media/graphicsmm-buttonflipbeforeflip.png "graphicsmm\_buttonflipbeforeflip")  
要翻转的 UIElement  
  
 下面显示创建该按钮的代码。  
  
 [!code-xml[Transforms_snip#GraphicsMMButtonWithoutFlip](../../../../samples/snippets/csharp/VS_Snippets_Wpf/Transforms_snip/CS/FlipExample.xaml#graphicsmmbuttonwithoutflip)]  
  
## 示例  
 若要水平翻转按钮，请创建一个 <xref:System.Windows.Media.ScaleTransform> 并将它的 <xref:System.Windows.Media.ScaleTransform.ScaleX%2A> 属性设置为 \-1。  将 <xref:System.Windows.Media.ScaleTransform> 应用于按钮的 <xref:System.Windows.UIElement.RenderTransform%2A> 属性。  
  
 [!code-xml[Transforms_snip#GraphicsMMFlipButtonExample1](../../../../samples/snippets/csharp/VS_Snippets_Wpf/Transforms_snip/CS/FlipExample.xaml#graphicsmmflipbuttonexample1)]  
  
 ![围绕 &#40;0,0&#41; 水平翻转的按钮](../../../../docs/framework/wpf/advanced/media/graphicsmm-buttonfliphorizontalflip-displaced.png "graphicsmm\_buttonfliphorizontalflip\_displaced")  
应用 ScaleTransform 之后的按钮  
  
## 示例  
 从上图可以看出，翻转了按钮，但是同时也移动了该按钮。  这是因为按钮是从左上角开始翻转的。  若要原地翻转按钮，需要将 <xref:System.Windows.Media.ScaleTransform> 应用于按钮的中心，而不是角。  将 <xref:System.Windows.Media.ScaleTransform> 应用于按钮中心的一个简便方法是将按钮的 <xref:System.Windows.UIElement.RenderTransformOrigin%2A> 属性设置为 0.5, 0.5。  
  
 [!code-xml[Transforms_snip#GraphicsMMFlipButtonExample2](../../../../samples/snippets/csharp/VS_Snippets_Wpf/Transforms_snip/CS/FlipExample.xaml#graphicsmmflipbuttonexample2)]  
  
 ![围绕中心水平翻转的按钮](../../../../docs/framework/wpf/advanced/media/graphicsmm-buttonfliphorizontalflip-inplace.png "graphicsmm\_buttonfliphorizontalflip\_inplace")  
RenderTransformOrigin 为 0.5, 0.5 的按钮  
  
## 示例  
 若要垂直翻转按钮，请设置 <xref:System.Windows.Media.ScaleTransform> 对象的 <xref:System.Windows.Media.ScaleTransform.ScaleY%2A> 属性，而不是 <xref:System.Windows.Media.ScaleTransform.ScaleX%2A> 属性。  
  
 [!code-xml[Transforms_snip#GraphicsMMVerticalFlipButtonExample2](../../../../samples/snippets/csharp/VS_Snippets_Wpf/Transforms_snip/CS/FlipExample.xaml#graphicsmmverticalflipbuttonexample2)]  
  
 ![围绕中心垂直翻转的按钮](../../../../docs/framework/wpf/advanced/media/graphicsmm-buttonflipverticalflip-inplace.png "graphicsmm\_buttonflipverticalflip\_inplace")  
垂直翻转的按钮  
  
## 请参阅  
 [变换概述](../../../../docs/framework/wpf/graphics-multimedia/transforms-overview.md)